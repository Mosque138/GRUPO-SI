# GRUPO-SI
# Sistema de Gestión de Pedidos a Domicilio

## 1. Contexto Administrativo

El sistema de gestión de pedidos a domicilio fue diseñado con una estructura centralizada, ya que la información y los procesos son controlados por un administrador principal. De esta forma se puede llevar un mejor control de los pedidos, los clientes y los repartidores.

Se eligió este tipo de estructura porque permite organizar mejor la información y facilita el seguimiento de cada pedido desde que se registra hasta que es entregado al cliente.

---

## 2. Modelado de Roles

| Rol           | Función                                          | Permisos                                                                       |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------ |
| Administrador | Administra el sistema.                           | Crear, modificar y eliminar usuarios, productos y pedidos. Consultar reportes. |
| Operador      | Atiende los pedidos realizados por los clientes. | Registrar pedidos y actualizar su estado.                                      |
| Repartidor    | Entrega los pedidos a los clientes.              | Consultar pedidos asignados y marcar entregas realizadas.                      |
| Cliente       | Realiza pedidos.                                 | Ver productos, hacer pedidos y consultar el estado de sus compras.             |
| Auditor       | Revisa la información del sistema.               | Consultar registros y verificar los procesos realizados.                       |

---

## 3. Matriz RACI

| Actividad           | Administrador | Operador | Repartidor | Auditor |
| ------------------- | ------------- | -------- | ---------- | ------- |
| Registrar usuarios  | R/A           | I        | I          | C       |
| Registrar productos | R/A           | C        | I          | I       |
| Registrar pedidos   | A             | R        | I          | I       |
| Asignar pedidos     | A             | R        | I          | C       |
| Entregar pedidos    | I             | C        | R          | A       |
| Revisar reportes    | R             | I        | I          | A       |

**R:** Responsable de realizar la actividad.

**A:** Aprueba o responde por el resultado.

**C:** Es consultado.

**I:** Es informado.

---

# 4. Diccionario de Datos

## Tabla Clientes

| Campo      | Tipo de dato | Validación               | Calidad priorizada |
| ---------- | ------------ | ------------------------ | ------------------ |
| id_cliente | INT          | Valor único              | Integridad         |
| nombre     | VARCHAR(100) | No puede estar vacío     | Precisión          |
| telefono   | VARCHAR(15)  | Solo números             | Exactitud          |
| direccion  | VARCHAR(200) | Campo obligatorio        | Completitud        |
| correo     | VARCHAR(100) | Formato de correo válido | Exactitud          |

---

## Tabla Usuarios

| Campo          | Tipo de dato | Validación                 | Calidad priorizada |
| -------------- | ------------ | -------------------------- | ------------------ |
| id_usuario     | INT          | Valor único                | Integridad         |
| nombre_usuario | VARCHAR(50)  | Obligatorio                | Precisión          |
| contraseña     | VARCHAR(255) | Mínimo 8 caracteres        | Seguridad          |
| rol            | VARCHAR(30)  | Debe existir un rol válido | Consistencia       |
| estado         | VARCHAR(20)  | Activo o Inactivo          | Consistencia       |

---

## Tabla Roles

| Campo       | Tipo de dato | Validación  | Calidad priorizada |
| ----------- | ------------ | ----------- | ------------------ |
| id_rol      | INT          | Valor único | Integridad         |
| nombre_rol  | VARCHAR(30)  | Obligatorio | Precisión          |
| descripcion | VARCHAR(150) | Opcional    | Completitud        |

---

## Tabla Productos

| Campo           | Tipo de dato  | Validación            | Calidad priorizada |
| --------------- | ------------- | --------------------- | ------------------ |
| id_producto     | INT           | Valor único           | Integridad         |
| nombre_producto | VARCHAR(100)  | Obligatorio           | Precisión          |
| precio          | DECIMAL(10,2) | Mayor que cero        | Exactitud          |
| stock           | INT           | No puede ser negativo | Consistencia       |
| descripcion     | VARCHAR(255)  | Opcional              | Completitud        |

---

## Tabla Pedidos

| Campo        | Tipo de dato  | Validación               | Calidad priorizada |
| ------------ | ------------- | ------------------------ | ------------------ |
| id_pedido    | INT           | Valor único              | Integridad         |
| id_cliente   | INT           | Debe existir en Clientes | Consistencia       |
| fecha_pedido | DATETIME      | Fecha válida             | Integridad         |
| estado       | VARCHAR(30)   | Estado permitido         | Consistencia       |
| total        | DECIMAL(10,2) | No negativo              | Exactitud          |

---

## Tabla Detalle_Pedido

| Campo       | Tipo de dato  | Validación                | Calidad priorizada |
| ----------- | ------------- | ------------------------- | ------------------ |
| id_detalle  | INT           | Valor único               | Integridad         |
| id_pedido   | INT           | Debe existir en Pedidos   | Consistencia       |
| id_producto | INT           | Debe existir en Productos | Consistencia       |
| cantidad    | INT           | Mayor que cero            | Exactitud          |
| subtotal    | DECIMAL(10,2) | Calculado automáticamente | Precisión          |

---

## Tabla Repartidores

| Campo          | Tipo de dato | Validación                 | Calidad priorizada |
| -------------- | ------------ | -------------------------- | ------------------ |
| id_repartidor  | INT          | Valor único                | Integridad         |
| nombre         | VARCHAR(100) | Obligatorio                | Precisión          |
| telefono       | VARCHAR(15)  | Solo números               | Exactitud          |
| vehiculo       | VARCHAR(50)  | Obligatorio                | Completitud        |
| disponibilidad | VARCHAR(20)  | Disponible o No Disponible | Consistencia       |

---

## Tabla Entregas

| Campo          | Tipo de dato | Validación                   | Calidad priorizada |
| -------------- | ------------ | ---------------------------- | ------------------ |
| id_entrega     | INT          | Valor único                  | Integridad         |
| id_pedido      | INT          | Debe existir en Pedidos      | Consistencia       |
| id_repartidor  | INT          | Debe existir en Repartidores | Consistencia       |
| fecha_entrega  | DATETIME     | Fecha válida                 | Integridad         |
| estado_entrega | VARCHAR(30)  | Entregado o Pendiente        | Consistencia       |


## 5. Reglas de validacion

Para evitar que se almacene información incorrecta en el sistema, se tendrán en cuenta las siguientes validaciones:

* No permitir campos vacíos en la información principal.
* Verificar que los correos electrónicos tengan un formato válido.
* No permitir cantidades o precios negativos.
* Comprobar que el cliente exista antes de registrar un pedido.
* Utilizar estados definidos para los pedidos.
* Limitar el acceso a ciertas funciones según el rol de cada usuario.

Estas medidas ayudan a que la información registrada sea más confiable y útil para el funcionamiento del sistema.
