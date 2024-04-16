
# Aplicación CRUD de PHP

Este repositorio contiene una aplicación PHP CRUD (Create, Read, Update, Delete) simple. Es una demostración básica de cómo integrar PHP con una base de datos MySQL para gestionar datos de usuarios. La aplicación permite a los usuarios agregar, ver, editar y eliminar información de usuario.

## Tecnologías Utilizadas

- **PHP:** Lenguaje de script del lado del servidor utilizado para el desarrollo web.
- **MySQL:** Sistema de gestión de base de datos utilizado para almacenar datos de usuario.
- **HTML & CSS:** Utilizados para estructurar y dar estilo a las páginas web.
- **Tailwind CSS:** Un framework de CSS utilitario para el desarrollo rápido de interfaces de usuario.

## Páginas y Funcionalidades

### 1. Página de Inicio (`display.php`)

![Página de Inicio](images/display.png)

- **Funcionalidad:** Muestra todos los usuarios de la base de datos en un formato de tabla.
- **Características:** 
  - Ver todos los usuarios.
  - Enlaces de navegación para agregar, editar o eliminar información de usuario.

### 2. Agregar Usuario (`user.php`)

![Agregar Usuario](images/add.png)

- **Funcionalidad:** Permite agregar un nuevo usuario a la base de datos.
- **Características:** 
  - Formulario para ingresar detalles del usuario (nombre, correo electrónico, teléfono móvil, contraseña).
  - Validación de datos y envío a la base de datos.

### 3. Editar Usuario (`edit.php`)

![Editar Usuario](images/edit.png)

- **Funcionalidad:** Permite editar detalles de usuarios existentes.
- **Características:** 
  - Formulario prellenado con la información actual del usuario.
  - Actualización de detalles del usuario en la base de datos.

### 4. Eliminar Usuario (`delete.php`)

- **Funcionalidad:** Facilita la eliminación de un usuario de la base de datos.
- **Características:** 
  - Eliminación de información de usuario basada en el ID de usuario.

## Conexión a la Base de Datos (`connect.php`)

- **Propósito:** Establece una conexión con la base de datos MySQL.
- **Credenciales:** Utiliza nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.

## Cómo Ejecutar

1. Clona el repositorio en tu máquina local.
2. Configura un entorno PHP y MySQL (como XAMPP).
3. Crea la base de datos usando phpmyadmin.
4. Ejecuta la aplicación en un servidor local.

## Nota de Seguridad

Esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Es recomendable utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos para prevenir ataques de inyección SQL.

---

Siéntete libre de contribuir a este proyecto o sugerir mejoras. Para cualquier consulta o problema, por favor abre un issue en este repositorio.

 # **2.6 INVESTIGACION:  Formularios para la elaboracion de un CRUD**

CRUD se refiere a las cuatro operaciones básicas utilizadas en la manipulación de datos en la mayoría de las bases de datos relacionales. Cada letra representa una operación específica:

<p align="center">
  <img width="460" height="200" src="https://github.com/PFLC/624-crus-basicos-Avantria/assets/93795004/b9dc6283-49eb-473d-a60c-41f7c846405a">
</p>

**1. Crear un nuevo usuario:**
- Este código PHP se encarga de insertar un nuevo usuario en una base de datos MySQL.
- Se conecta a la base de datos y recibe los datos del nuevo usuario a través de una solicitud POST.
- Luego ejecuta una consulta SQL para insertar los datos del nuevo usuario en la tabla de usuarios.
- Finalmente, devuelve un mensaje indicando si la operación fue exitosa o si ocurrió algún error.

**Ejemplo**
```
<?php
$servername = "localhost";
$username = "tu_usuario_mysql";
$password = "tu_contraseña_mysql";
$dbname = "tu_base_de_datos";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}

$nombre = $_POST['nombre'];
$correo = $_POST['correo'];

$sql = "INSERT INTO usuarios (nombre, correo) VALUES ('$nombre', '$correo')";

if ($conn->query($sql) === TRUE) {
    echo "Usuario creado exitosamente";
} else {
    echo "Error al crear usuario: " . $conn->error;
}


$conn->close();
?>
```
**2. Leer usuarios:**

- Este código PHP consulta la base de datos para recuperar todos los usuarios almacenados en la tabla de usuarios.
- Se conecta a la base de datos y ejecuta una consulta SQL para seleccionar todos los registros de la tabla de usuarios.
- Itera sobre los resultados y muestra la información de cada usuario (ID, nombre, correo) en el navegador.
- Si no hay resultados, muestra un mensaje indicando que no se encontraron usuarios.

**Ejemplo**

```
<?php
$servername = "localhost";
$username = "tu_usuario_mysql";
$password = "tu_contraseña_mysql";
$dbname = "tu_base_de_datos";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}

$sql = "SELECT id, nombre, correo FROM usuarios";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - Nombre: " . $row["nombre"]. " - Correo: " . $row["correo"]. "<br>";
    }
} else {
    echo "0 resultados";
}

$conn->close();
?>

```
**3. Actualizar usuario:**

- Este código PHP actualiza la información de un usuario existente en la base de datos.
- Se conecta a la base de datos y recibe los nuevos datos del usuario a través de una solicitud POST, incluido el ID del usuario que se actualizará.
- Luego ejecuta una consulta SQL para actualizar los datos del usuario en la tabla de usuarios.
- Devuelve un mensaje indicando si la operación fue exitosa o si ocurrió algún error.

**Ejemplo**

```
<?php
$servername = "localhost";
$username = "tu_usuario_mysql";
$password = "tu_contraseña_mysql";
$dbname = "tu_base_de_datos";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}

$id = $_POST['id'];
$nombre = $_POST['nombre'];
$correo = $_POST['correo'];

$sql = "UPDATE usuarios SET nombre='$nombre', correo='$correo' WHERE id=$id";

if ($conn->query($sql) === TRUE) {
    echo "Usuario actualizado exitosamente";
} else {
    echo "Error al actualizar usuario: " . $conn->error;
}

$conn->close();
?>
```
**4. Eliminar usuario:**

- Este código PHP elimina un usuario existente de la base de datos.
- Se conecta a la base de datos y recibe el ID del usuario que se eliminará a través de una solicitud POST.
- Luego ejecuta una consulta SQL para eliminar el usuario correspondiente de la tabla de usuarios.
- Devuelve un mensaje indicando si la operación fue exitosa o si ocurrió algún error.

**Ejemplo**
```
<?php
$servername = "localhost";
$username = "tu_usuario_mysql";
$password = "tu_contraseña_mysql";
$dbname = "tu_base_de_datos";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}

$id = $_POST['id'];

$sql = "DELETE FROM usuarios WHERE id=$id";

if ($conn->query($sql) === TRUE) {
    echo "Usuario eliminado exitosamente";
} else {
    echo "Error al eliminar usuario: " . $conn->error;
}

$conn->close();
?>
```
**Captura de el servidor que tiene el LAMP de TeddySun implementado en el**
<p align="center">
  <img width="460" height="200" src="https://github.com/PFLC/624-crus-basicos-Avantria/assets/93795004/fee43005-f2e4-4e57-b90c-adc98f04896d">
</p>
