<?php
include("conexion.php");

// Obtener proyectos
$sql = "SELECT id, nombre FROM proyectos";
$result = $conn->query($sql);

$proyectos = [];
if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        $proyectos[] = $row;
    }
} else {
    $proyectos[] = ['id' => 0, 'nombre' => 'Ninguno'];
}

// Verificar si se ha enviado el formulario
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    // Obtener datos del formulario
    $nombreProducto = $_POST['nombre'];
    $descripcionProducto = $_POST['descripcion'];
    $precioProducto = $_POST['precio'];
    
    // Crear producto
    $sql = "INSERT INTO productos (nombre, descripcion, precio) VALUES ('$nombreProducto', '$descripcionProducto', $precioProducto)";
    
    if ($conn->query($sql) === TRUE) {
        $productoId = $conn->insert_id;
        echo "Producto creado exitosamente con ID: " . $productoId . "<br>";
        
        // Asignar proyectos al producto
        foreach ($proyectos as $proyecto) {
            $proyectoId = $proyecto['id'];
            $sql = "INSERT INTO productos_proyectos (producto_id, proyecto_id) VALUES ($productoId, $proyectoId)";
            if ($conn->query($sql) !== TRUE) {
                echo "Error al asignar proyecto ID $proyectoId al producto: " . $conn->error . "<br>";
            }
        }
        
        echo "Proyectos asignados al producto.";
    } else {
        echo "Error al crear el producto: " . $conn->error;
    }
}
?>

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crear Producto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            width: 400px;
        }

        h2 {
            text-align: center;
            color: #333;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 8px;
            color: #555;
        }

        input[type="text"],
        input[type="number"],
        select,
        textarea {
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
            width: 100%;
            box-sizing: border-box;
        }

        textarea {
            resize: vertical;
            height: 100px;
        }

        input[type="submit"] {
            background-color: #B43B37
;
            color: #fff;
            border: none;
            padding: 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        input[type="submit"]:hover {
            background-color: #731C1A
;
        }

        .volver {
            text-decoration: none;
            padding: 10px 20px;
            border-radius: 4px;
            background-color: #B43B37
;
            color: #fff;
            display: inline-block;
            margin-top: 20px;
        }

        .volver:hover{
            background-color: #731C1A
;
        }
    </style>
</head>

<body>
    <div class="container">
        <h2>Crear Producto</h2>
        <form action="crear_productos.php" method="post">
            <label for="nombre">Nombre del Producto:</label>
            <input type="text" id="nombre" name="nombre" required>

            <label for="descripcion">Descripción:</label>
            <textarea id="descripcion" name="descripcion" required></textarea>

            <label for="precio">Precio:</label>
            <input type="number" id="precio" name="precio" step="0.01" required>

            <label for="proyecto">Proyecto:</label>
            <select id="proyecto" name="proyecto">
                <?php
                // Obtener proyectos para el formulario
                foreach ($proyectos as $proyecto) {
                    echo "<option value='" . $proyecto['id'] . "'>" . $proyecto['nombre'] . "</option>";
                }
                ?>
            </select>
            <input type="submit" value="Crear Producto">
            <center><a href="index.php" class="volver">Volver</a></center>
        </form>
    </div>
</body>

</html>

<?php
// Cerrar conexión
$conn->close();
?>
