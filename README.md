# gitacttest
# xampp/htdocs/miniproject/index.php
# Me llamo Ronier y este es mi segunda linea #
# Este codigo random de bienvenida en php #
<?php
session_start();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST["username"];
    $password = $_POST["password"];

    // Lee el archivo de usuarios
    $users = file("users.txt", FILE_IGNORE_NEW_LINES);

    foreach ($users as $user) {
        list($storedUsername, $storedPassword) = explode(":", $user);
        
        if ($username == $storedUsername && $password == $storedPassword) {
            $_SESSION["authenticated"] = true;
            header("Location: index.php");
            exit;
        }
    }

    // Si no se encuentra un usuario válido, muestra un mensaje de error
    $error_message = "Usuario o contraseña incorrectos.";
}
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Iniciar Sesión</title>
</head>
<body>
    <h2>Iniciar Sesión</h2>
    <?php if (isset($error_message)) : ?>
        <p style="color: red;"><?php echo $error_message; ?></p>
    <?php endif; ?>
    <form method="post" action="">
        <label for="username">Usuario:</label>
        <input type="text" name="username" required><br>
        
        <label for="password">Contraseña:</label>
        <input type="password" name="password" required><br>
        
        <input type="submit" value="Iniciar Sesión">
    </form>
</body>
</html>
