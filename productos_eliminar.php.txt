<?php
include("conexion.php");

if (isset($_GET['id']) && filter_var($_GET['id'], FILTER_VALIDATE_INT)) {
    $id = $_GET['id'];

    // Iniciar una transacción
    $conn->begin_transaction();

    try {
        // Eliminar referencias en la tabla productos_proyectos
        $query = $conn->prepare("DELETE FROM productos_proyectos WHERE producto_id = ?");
        $query->bind_param('i', $id);
        $query->execute();
        $query->close();

        // Ahora eliminar el producto
        $query = $conn->prepare("DELETE FROM productos WHERE id = ?");
        $query->bind_param('i', $id);
        $query->execute();
        $query->close();

        // Confirmar la transacción
        $conn->commit();

        echo "<script>alert('Producto eliminado exitosamente');</script>";
    } catch (Exception $e) {
        // Revertir la transacción en caso de error
        $conn->rollback();
        echo "<script>alert('Error al eliminar el producto: " . $e->getMessage() . "');</script>";
    }

    // Redirigir de vuelta a index.php después de la operación
    echo "<script>window.location.href = 'index.php';</script>";
} else {
    echo "<script>alert('ID de producto no válido');</script>";
    echo "<script>window.location.href = 'index.php';</script>";
}

// Cerrar la conexión
$conn->close();
?>
