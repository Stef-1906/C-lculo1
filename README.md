<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Calculadora de Ecuaciones e Inecuaciones</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    input, button {
      padding: 10px;
      margin: 5px;
    }
    #resultado {
      margin-top: 20px;
      font-weight: bold;
      white-space: pre-wrap;
    }
  </style>
</head>
<body>
  <h2>Calculadora de Ecuaciones e Inecuaciones Lineales</h2>

  <p>Ejemplo: <code>2x + 3 = 7</code> ó <code>3x - 5 < 10</code></p>

  <input type="text" id="input" placeholder="Escribe tu ecuación o inecuación">
  <button onclick="resolver()">Resolver paso a paso</button>

  <div id="resultado"></div>

  <script>
    function resolver() {
      const entrada = document.getElementById("input").value.replace(/\s+/g, "");
      const resultadoDiv = document.getElementById("resultado");
      const operadores = ["=", "<", ">", "<=", ">="];
      let operador = null;

      for (const op of operadores) {
        if (entrada.includes(op)) {
          operador = op;
          break;
        }
      }

      if (!operador) {
        resultadoDiv.innerText = "Por favor, ingresa una ecuación o inecuación válida.";
        return;
      }

      const [izq, der] = entrada.split(operador);

      // Se espera formato ax + b = c
      const regex = /([-+]?\d*)x([+-]?\d+)?/;
      const match = izq.match(regex);

      if (!match) {
        resultadoDiv.innerText = "Formato no reconocido. Asegúrate de usar ecuaciones lineales con 'x'.";
        return;
      }

      const a = match[1] === "" || match[1] === "+" ? 1 : match[1] === "-" ? -1 : parseFloat(match[1]);
      const b = match[2] ? parseFloat(match[2]) : 0;
      const c = parseFloat(der);

      let pasos = `Ecuación original: ${entrada}\n`;
      pasos += `Paso 1: Identificamos términos -> a = ${a}, b = ${b}, c = ${c}\n`;

      pasos += `Paso 2: Restamos ${b} de ambos lados:\n`;
      const paso2 = c - b;
      pasos += `\t${a}x ${operador} ${paso2}\n`;

      pasos += `Paso 3: Dividimos ambos lados para despejar x:\n`;
      const resultado = paso2 / a;
      pasos += `\tx ${operador} ${resultado}\n`;

      resultadoDiv.innerText = pasos;
    }
  </script>
</body>
</html>
