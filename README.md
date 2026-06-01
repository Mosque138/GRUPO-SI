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

## 4. Diccionario de Datos

### Tabla Clientes

| Campo      | Tipo de dato | Validación                               | Calidad priorizada |
| ---------- | ------------ | ---------------------------------------- | ------------------ |
| id_cliente | INT          | Valor único                              | Integridad         |
| nombre     | VARCHAR(100) | No puede estar vacío                     | Precisión          |
| telefono   | VARCHAR(15)  | Solo números                             | Exactitud          |
| direccion  | VARCHAR(200) | Campo obligatorio                        | Completitud        |
| correo     | VARCHAR(100) | Debe tener formato de correo electrónico | Exactitud          |

### Tabla Pedidos

| Campo        | Tipo de dato  | Validación                        | Calidad priorizada |
| ------------ | ------------- | --------------------------------- | ------------------ |
| id_pedido    | INT           | Valor único                       | Integridad         |
| id_cliente   | INT           | Debe existir en la tabla Clientes | Consistencia       |
| fecha_pedido | DATETIME      | Fecha válida                      | Integridad         |
| estado       | VARCHAR(30)   | Pendiente, En camino o Entregado  | Consistencia       |
| total        | DECIMAL(10,2) | No puede ser negativo             | Exactitud          |

### Tabla Productos

| Campo           | Tipo de dato  | Validación              | Calidad priorizada |
| --------------- | ------------- | ----------------------- | ------------------ |
| id_producto     | INT           | Valor único             | Integridad         |
| nombre_producto | VARCHAR(100)  | Campo obligatorio       | Precisión          |
| precio          | DECIMAL(10,2) | Debe ser mayor que cero | Exactitud          |
| stock           | INT           | No puede ser negativo   | Consistencia       |

---

## 5. Reglas para evitar errores en los datos (GIGO)

Para evitar que se almacene información incorrecta en el sistema, se tendrán en cuenta las siguientes validaciones:

* No permitir campos vacíos en la información principal.
* Verificar que los correos electrónicos tengan un formato válido.
* No permitir cantidades o precios negativos.
* Comprobar que el cliente exista antes de registrar un pedido.
* Utilizar estados definidos para los pedidos.
* Limitar el acceso a ciertas funciones según el rol de cada usuario.

Estas medidas ayudan a que la información registrada sea más confiable y útil para el funcionamiento del sistema.
