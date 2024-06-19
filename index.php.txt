<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Registro</title>
    <!DOCTYPE html>
<html lang="es">

<a name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Productos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        th,
        td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background-color: #f2f2f2;
        }

        .eliminar {
            text-decoration: none;
            padding: 5px 10px;
            border-radius: 4px;
            background-color: #D50202;
            color: #fff;
        }

        .ver{
            text-decoration: none;
            padding: 5px 10px;
            border-radius: 4px;
            background-color: #E39709;
            color: #fff;
        }

        .editar{
            text-decoration: none;
            padding: 5px 10px;
            border-radius: 4px;
            background-color: #B80062;
            color: #fff; 
        }

        .eliminar:hover {
            background-color: #8C0105;
        }

        .ver:hover{
           background-color: #AD7401
;
        }
        
        .editar:hover{
            background-color: #8F046B
;   
        }

        .NuevoP {
            text-decoration: none;
            padding: 10px 20px;
            border-radius: 4px;
            background-color: #AD0128;
            color: #fff;
            display: inline-block;
            margin-top: 20px;
        }

        .NuevoP {
            background-color:#6C061D;
        }
    </style>
</head>
<body>
    <h2>Registro</h2>
    <form action="login.php" method="post">
        <label for="username">Nombre de usuario:</label>
        <input type="text" name="username" required><br>
        <label for="password">Contraseña:</label>
        <input type="password" name="password" required><br>
        <input type="submit" value="Registrarse">
    </form>
</body>
</html>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    include 'con_reg.php';

    $username = $_POST['username'];
    $password = password_hash($_POST['password'], PASSWORD_DEFAULT);

    $sql = "INSERT INTO users (username, password) VALUES ('$username', '$password')";

    if ($conn->query($sql) === TRUE) {
        echo "Registro exitoso. <a href='inicio.php'>Iniciar sesión</a>";
    } else {
        echo "Error: " . $sql . "<br>" . $conn->error;
    }

    $conn->close();
}
?>