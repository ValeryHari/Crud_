<?php
include("conexion.php");
include("productos_tabla.php");
$id = $_GET['id'];

$querybuscar = mysqli_query($conn, "SELECT pro.id, pro.nombre, pro.descripcion, pro.precio, cat.nombre as categoria 
                                    FROM productos pro 
                                    INNER JOIN categoria_productos cat ON pro.categoria_id = cat.id 
                                    WHERE pro.id = '$id'");

$mostrar = mysqli_fetch_array($querybuscar);

$proid = $mostrar['id'];
$pronom = $mostrar['nombre'];
$prodes = $mostrar['descripcion'];
$propre = $mostrar['precio'];
$procat = $mostrar['categoria'];
?>

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ver Producto</title>
    <link rel="stylesheet" href="estilos.css">
</head>

<body>
    <div class="container">
        <h2>Ver Producto</h2>
        <table class="tabla-productos">
            <tr>
                <td><b>ID:</b></td>
                <td><?php echo $proid; ?></td>
            </tr>
            <tr>
                <td><b>Nombre:</b></td>
                <td><?php echo $pronom; ?></td>
            </tr>
            <tr>
                <td><b>Descripción:</b></td>
                <td><?php echo $prodes; ?></td>
            </tr>
            <tr>
                <td><b>Precio:</b></td>
                <td><?php echo $propre; ?></td>
            </tr>
            <tr>
                <td><b>Categoría:</b></td>
                <td><?php echo $procat; ?></td>
            </tr>
        </table>
        <div class="link">
            <a href="productos_tabla.php?pag=<?php echo $pagina; ?>">Regresar</a>
        </div>
    </div>
</body>

</html>