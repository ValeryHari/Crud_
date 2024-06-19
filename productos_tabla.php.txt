<?php
include("conexion.php");
?>

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Productos</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h2>Lista de Productos</h2>
        <table class="tabla-productos">
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Descripción</th>
                <th>Precio</th>
                <th>Categoría</th>
                <th>Acciones</th>
            </tr>
            <?php
            if (isset($_GET['accion']) && $_GET['accion'] == 'eliminar' && isset($_GET['id'])) {
                $id = $_GET['id'];
                mysqli_query($conn, "DELETE FROM productos WHERE id='$id'");
                $pagina = $_GET['pag'];
                header("Location: productos_tabla.php?pag=$pagina");
                exit();
            }

            $sql = "SELECT pro.id, pro.nombre, pro.descripcion, pro.precio, cat.nombre AS categoria 
                    FROM productos pro
                    INNER JOIN categoria_productos cat ON pro.categoria_id = cat.id";
            $result = mysqli_query($conn, $sql);

            if (!$result) {
                echo "Error en la consulta: " . mysqli_error($conn);
            } else {

                while ($row = mysqli_fetch_array($result)) {
                    echo "<tr>";
                    echo "<td>{$fila['id']}</td>";
                    echo "<td>{$fila['nombre']}</td>";
                    echo "<td>{$fila['descripcion']}</td>";
                    echo "<td>{$fila['precio']}</td>";
                    echo "<td>{$fila['categoria']}</td>";
                    echo "<td>";
                    echo "<a href='ver_producto.php?id={$fila['id']}&pag=$pagina'>Ver</a> | ";
                    echo "<a href='modificar_producto.php?id={$fila['id']}&pag=$pagina'>Modificar</a> | ";
                    echo "<a href='productos_tabla.php?accion=eliminar&id={$fila['id']}&pag=$pagina' onClick=\"javascript: return confirm('¿Deseas eliminar este producto?');\">Eliminar</a>";
                    echo "</td>";
                    echo "</tr>";
                }
            }
            ?>
        </table>
        <div class="link">
            <a href="crear_productos.php">Crear Nuevo Producto</a>
        </div>
    </div>
</body>

</html>

<?php
// Cerrar conexión
$conn->close();
?>