<?php
include("conexion.php"); // Incluir archivo de conexión
include("barra_lateral.php");
?>

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
    <div class="container">
        <h2>Lista de Productos</h2>
        <table>
        <a href="crear_productos.php" class="NuevoP">Nuevo Producto</a>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Descripción</th>
                <th>Precio</th>
                <th>Acciones</th>
            </tr>
            <?php
            $query = "SELECT * FROM productos";
            $result = mysqli_query($conn, $query);

            if (!$result) {
                die("Error al obtener productos: " . mysqli_error($conn));
            }

            while ($row = mysqli_fetch_assoc($result)) {
                echo "<tr>";
                echo "<td>" . $row['id'] . "</td>";
                echo "<td>" . $row['nombre'] . "</td>";
                echo "<td>" . $row['descripcion'] . "</td>";
                echo "<td>" . $row['precio'] . "</td>";
                echo "<td>
                        <a href='productos_ver.php?id=" . $row['id'] . "' class='ver'>Ver</a>
                        <a href='productos_modificar.php?id=" . $row['id'] . "' class='editar'>Modificar</a>
                        <a href='productos_eliminar.php?id=" . $row['id'] . "' class='eliminar' onclick='return confirm(\"¿Estás seguro de querer eliminar este producto?\")'>Eliminar</a>
                      </td>";
                echo "</tr>";
            }

            mysqli_close($conn);
            ?>
        </table>
    </div>
</body>

</html>