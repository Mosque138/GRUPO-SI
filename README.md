# GRUPO-SI
# Sistema de Gestión de Pedidos a Domicilio

## 1. - Contexto Administrativo

El sistema de gestión de pedidos a domicilio fue diseñado con una estructura centralizada, ya que la información y los procesos son controlados por un administrador principal. De esta forma se puede llevar un mejor control de los pedidos, los clientes y los repartidores.

Se eligió este tipo de estructura porque permite organizar mejor la información y facilita el seguimiento de cada pedido desde que se registra hasta que es entregado al cliente.

---

## - Modelado de Roles

| Rol           | Función                                          | Permisos                                                                       |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------ |
| Administrador | Administra el sistema.                           | Crear, modificar y eliminar usuarios, productos y pedidos. Consultar reportes. |
| Operador      | Atiende los pedidos realizados por los clientes. | Registrar pedidos y actualizar su estado.                                      |
| Repartidor    | Entrega los pedidos a los clientes.              | Consultar pedidos asignados y marcar entregas realizadas.                      |
| Cliente       | Realiza pedidos.                                 | Ver productos, hacer pedidos y consultar el estado de sus compras.             |
| Auditor       | Revisa la información del sistema.               | Consultar registros y verificar los procesos realizados.                       |

---

## - Matriz RACI

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

# - Diccionario de Datos

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


## - Reglas de validacion

Para evitar que se almacene información incorrecta en el sistema, se tendrán en cuenta las siguientes validaciones:

* No permitir campos vacíos en la información principal.
* Verificar que los correos electrónicos tengan un formato válido.
* No permitir cantidades o precios negativos.
* Comprobar que el cliente exista antes de registrar un pedido.
* Utilizar estados definidos para los pedidos.
* Limitar el acceso a ciertas funciones según el rol de cada usuario.

Estas medidas ayudan a que la información registrada sea más confiable y útil para el funcionamiento del sistema.

## Dimensiones de Calidad de los Datos

En el desarrollo del sistema se tuvieron en cuenta diferentes aspectos para garantizar que la información almacenada sea confiable y útil.

* **Precisión:** Los datos deben representar correctamente la información real. Por ejemplo, que el nombre de un cliente esté escrito correctamente.

* **Exactitud:** Los valores registrados deben ser correctos. Por ejemplo, que el precio de un producto corresponda al valor real.

* **Consistencia:** La información debe mantenerse igual en todas las partes del sistema. Por ejemplo, que un cliente registrado tenga el mismo identificador en todos sus pedidos.

* **Integridad:** Los datos deben estar completos y relacionados correctamente entre las tablas de la base de datos.

* **Completitud:** Los campos obligatorios deben contener información antes de guardar un registro.

# 2. El Prototipo Funcional (Lógica del Sistema)

## - Validación de Entrada

El sistema de gestión de pedidos a domicilio cuenta con validaciones que permiten evitar el ingreso de datos incorrectos o incompletos. Estas validaciones ayudan a evitar errores en la información almacenada y garantizan una mejor calidad de los datos,
Algunas de las validaciones implementadas son:

* No permitir campos obligatorios vacíos.
* Verificar que el número de teléfono contenga únicamente números.
* Validar que el correo electrónico tenga un formato correcto.
* Evitar registrar cantidades negativas en los productos.
* No permitir precios iguales o menores a cero.
* Verificar que exista un cliente antes de registrar un pedido.
* Comprobar que los estados de los pedidos correspondan a las opciones definidas por el sistema.

## - Arquitectura

El sistema maneja la información siguiendo una estructura organizada que va desde la captura de datos hasta la generación de información útil para la empresa.

El proceso funciona de la siguiente manera:

1. Se registran los datos de clientes, productos y repartidores.
2. El cliente realiza un pedido.
3. El sistema almacena la información del pedido y sus productos.
4. El pedido es asignado a un repartidor.
5. El repartidor actualiza el estado de la entrega.
6. Toda la información queda almacenada en la base de datos.
7. Finalmente, el sistema genera reportes sobre pedidos, entregas y ventas realizadas.

## - Tipo de Sistema de Información

El proyecto se clasifica como un sistema TPS (Transaction Processing System o Sistema de Procesamiento de Transacciones).
Esto se debe a que su función principal es registrar y procesar operaciones diarias como:

* Registro de clientes.
* Registro de productos.
* Creación de pedidos.
* Asignación de repartidores.
* Registro de entregas.
* Actualización de estados de pedidos.

Este tipo de sistema es utilizado principalmente por el nivel operativo de la empresa, ya que son los empleados encargados de realizar las actividades diarias y registrar la información necesaria para el funcionamiento del servicio de domicilios.
Además, los reportes generados por el sistema pueden ser consultados por supervisores o administradores para realizar seguimiento a las operaciones y al desempeño del negocio.
