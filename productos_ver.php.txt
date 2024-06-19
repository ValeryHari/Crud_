<?php
include("conexion.php");

$id = isset($_GET['id']) ? intval($_GET['id']) : 0;

$query = "SELECT * FROM productos WHERE id='$id'";
$result = mysqli_query($conn, $query);
$producto = mysqli_fetch_assoc($result);

mysqli_close($conn);
?>

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ver Producto</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h2>Ver Producto</h2>
        <?php if ($producto): ?>
        <table>
            <tr>
                <th>ID</th>
                <td><?php echo htmlspecialchars($producto['id']); ?></td>
            </tr>
            <tr>
                <th>Nombre</th>
                <td><?php echo htmlspecialchars($producto['nombre']); ?></td>
            </tr>
            <tr>
                <th>Descripción</th>
                <td><?php echo htmlspecialchars($producto['descripcion']); ?></td>
            </tr>
            <tr>
                <th>Precio</th>
                <td><?php echo htmlspecialchars($producto['precio']); ?></td>
            </tr>
        </table>
        <?php else: ?>
        <p>Producto no encontrado.</p>
        <?php endif; ?>
        <a href="index.php" class="volver">Volver</a>
    </div>
</body>

</html>
