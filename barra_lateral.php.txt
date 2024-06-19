<?php
session_start();
include('conexion.php');
?>

<html>

<head>
    <title>CRUD 4AMP</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <style>
        .BarraLateral {
        position: fixed;
        top: 0;
        left: 0;
        width: 200px;
        height: 100%;
        background-color: #9B0A0A;
        box-sizing: border-box;
        text-align:center;
        }
        .BarraLateral ul {
        list-style: none;
        padding: 0;
        margin-top:10%; 
        font-size:18px;			
        }

        .BarraLateral li 
        {
        text-align:left;
        padding: 12px 10px;
        background-color: rgba(0, 0, 0, .5);
        color:#d9dbe0;
        }

        .BarraLateral a 
        {
        color: white;
        text-decoration: none;
        }
                
        .ContenedorPrincipal 
        {
        margin-left: 200px;
        padding: 20px;
        box-sizing: border-box;
        text-align:center;
        }
                
        @media (max-width: 768px) 
            {
        .BarraLateral 
        {
        width: 100%;
        height: auto;
        position: relative;
        }

        .ContenedorPrincipal 
        {
        margin-left: 0;
        }			
            }

    </style>

</head>

<body>
    <div class="BarraLateral">
        <form>
        <ul>
            <hr>
            <li><a href="crear_productos.php">Crear productos</a></li>
        </ul>
</form>
    </div>
</body>

</html>