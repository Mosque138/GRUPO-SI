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

<img width="842" height="123" alt="clientes" src="https://github.com/user-attachments/assets/d44081cb-b32e-4899-ab56-36e49740a7e6" />


---

## Tabla Usuarios

<img width="841" height="120" alt="usuarios" src="https://github.com/user-attachments/assets/be35b4cc-3eef-4aa3-a851-0234c148080e" />

---

## Tabla Roles

<img width="839" height="78" alt="roles" src="https://github.com/user-attachments/assets/249a469a-4476-4a9f-ba35-d746990ac073" />

---

## Tabla Productos

<img width="839" height="124" alt="productos" src="https://github.com/user-attachments/assets/899af365-bc97-482d-8272-f7827e404966" />

---

## Tabla Pedidos

<img width="842" height="121" alt="pedidos" src="https://github.com/user-attachments/assets/61d9a337-6559-49ef-a21c-baaf36b8f109" />

---

## Tabla Detalle_Pedido

<img width="842" height="120" alt="detalle pedido" src="https://github.com/user-attachments/assets/f48f9c87-8c7f-45f9-9064-7e3c0b0b6f94" />

---

## Tabla Repartidores

<img width="839" height="121" alt="repartidores" src="https://github.com/user-attachments/assets/f3ccf176-eac8-4a0a-a013-1183bcdd4535" />

---

## Tabla Entregas

<img width="842" height="121" alt="entregas" src="https://github.com/user-attachments/assets/ec727c03-34c3-4259-9c1c-cf5aba478be1" />



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
