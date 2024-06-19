<?php
include("conexion.php");

$id = $_GET['id'];

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $nombre = $_POST['nombre'];
    $descripcion = $_POST['descripcion'];
    $precio = $_POST['precio'];

    $query = "UPDATE productos SET nombre='$nombre', descripcion='$descripcion', precio='$precio' WHERE id='$id'";
    $result = mysqli_query($conn, $query);

    if ($result) {
        echo "<script>alert('Producto modificado exitosamente');</script>";
    } else {
        echo "<script>alert('Error al modificar el producto');</script>";
    }

    echo "<script>window.location.href = 'index.php';</script>";
} else {
    $query = "SELECT * FROM productos WHERE id='$id'";
    $result = mysqli_query($conn, $query);
    $producto = mysqli_fetch_assoc($result);
}

mysqli_close($conn);
?>

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modificar Producto</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h2>Modificar Producto</h2>
        <form method="POST">
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" value="<?php echo $producto['nombre']; ?>" required>

            <label for="descripcion">Descripción:</label>
            <input type="text" id="descripcion" name="descripcion" value="<?php echo $producto['descripcion']; ?>" required>

            <label for="precio">Precio:</label>
            <input type="number" step="0.01" id="precio" name="precio" value="<?php echo $producto['precio']; ?>" required>

            <input type="submit" value="Modificar Producto">
            <center><a href="index.php" class="volver">Volver</a></center>
        </form>
    </div>
</body>

</html>