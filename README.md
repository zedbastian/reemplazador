<!DOCTYPE html>
<html>
<head>
    <title>Reemplazar Texto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f2f2f2;
        }

        .container {
            display: flex;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
            margin: 20px;
        }

        .box {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
            margin: 10px;
            flex: 1;
            border-radius: 10px; /* Añadido: bordes redondeados */
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Añadido: sombra */
            background-color: #fff; /* Añadido: fondo blanco */
        }

        #facturas {
            width: 100%;
            height: 150px;
            resize: none;
        }

        #resultados {
            width: 100%;
            text-align: left;
            margin-top: 10px;
            padding: 10px; /* Añadido: espacio interno */
            border-radius: 10px; /* Añadido: bordes redondeados */
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Añadido: sombra */
            background-color: #f9f9f9; /* Añadido: fondo gris claro */
        }

        #textoInicio, #textoFinal {
            width: calc(100% - 22px); /* Añadido: ajuste para compensar el padding */
            padding: 5px;
            font-size: 14px;
            border: none; /* Añadido: eliminar borde */
            outline: none; /* Añadido: eliminar contorno al seleccionar */
        }

        button {
            background-color: #0074d9;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            border-radius: 5px; /* Añadido: bordes redondeados */
            transition: background-color 0.3s; /* Añadido: transición de color */
        }

        button:hover {
            background-color: #0056b3; /* Añadido: color de fondo al pasar el ratón */
        }

        p {
            margin: 5px 0; /* Añadido: espacio entre párrafos */
        }

        .flyout {
            position: relative;
            display: inline-block;
        }

        .flyout-content {
            display: none;
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            padding: 12px 16px;
            z-index: 1;
            border-radius: 5px;
        }

        .flyout:hover .flyout-content {
            display: block;
            font-size: 12px; /* Ajustado: reducir tamaño del globo */
        }
    </style>
</head>
<body>

<div class="container">
    <div class="flyout">
        <div class="box" id="boxIzquierda">
            <input type="text" id="textoInicio" placeholder="Texto delante">
            <div class="flyout-content">
                <p>Aquí puedes ingresar el texto inicial.</p>
            </div>
        </div>
    </div>
    <div class="box" id="boxCentro">
        <textarea id="facturas" placeholder="Ingrese las facturas aquí"></textarea>
        <div class="flyout-content">
            <p>Este es el área donde puedes ingresar las facturas, una por línea.</p>
        </div>
    </div>
    <div class="flyout">
        <div class="box" id="boxDerecha">
            <input type="text" id="textoFinal" placeholder="Texto final">
            <div class="flyout-content">
                <p>Aquí puedes ingresar el texto final.</p>
            </div>
        </div>
    </div>
</div>

<div class="container">
    <button onclick="reemplazarTexto()">Reemplazar y Copiar</button>
</div>

<div class="container">
    <div class="box" id="resultados"></div>
</div>

<script>
function reemplazarTexto() {
    var textoInicio = document.getElementById("textoInicio").value.trim();
    var textoFinal = document.getElementById("textoFinal").value.trim();
    var facturasInput = document.getElementById("facturas").value;
    
    // Separar las facturas ingresadas por saltos de línea
    var facturas = facturasInput.split('\n').filter(Boolean);

    var resultados = [];

    for (var i = 0; i < facturas.length; i++) {
        var factura = (textoInicio + facturas[i] + textoFinal).trim();
        
        // Eliminar las dos últimas letras del texto final solo en la última fila
        if (i === facturas.length - 1) {
            factura = factura.slice(0, -2);
        }
        
        // Eliminar todas las comillas dobles
        factura = factura.replace(/"/g, '');

        resultados.push(factura);
    }

    var resultadosDiv = document.getElementById("resultados");
    resultadosDiv.innerHTML = resultados.join('<br>'); // Agregado: agregar saltos de línea
    
    // Copiar el contenido al portapapeles
    var elementoTemporizador = document.createElement("textarea");
    elementoTemporizador.value = resultados.join('\n'); // Agregado: copiar con saltos de línea
    document.body.appendChild(elementoTemporizador);
    elementoTemporizador.select();
    document.execCommand("copy");
    document.body.removeChild(elementoTemporizador);
}
</script>

</body>
</html>
