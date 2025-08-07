<!DOCTYPE html>
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Calculadora de Ecuaciones e Inecuaciones</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; max-width: 600px; }
    input, select, button { font-size: 1.2em; padding: 5px; margin: 5px 0; }
    #resultado { margin-top: 20px; background: #f0f0f0; padding: 15px; border-radius: 5px; white-space: pre-wrap; }
    .paso { margin-bottom: 10px; }
    button.download-btn { background-color: #4CAF50; color: white; border: none; cursor: pointer; }
    button.download-btn:hover { background-color: #45a049; }
  </style>
</head>
<body>
  <h1>Calculadora de Ecuaciones e Inecuaciones Lineales</h1>
  <p>Resuelve ecuaciones o inecuaciones del tipo: <strong>ax + b [operador] 0</strong></p>

  <label for="a">a (coeficiente de x): </label><br/>
  <input type="number" id="a" step="any" /><br/>

  <label for="b">b (término independiente): </label><br/>
  <input type="number" id="b" step="any" /><br/>

  <label for="operador">Operador: </label><br/>
  <select id="operador">
    <option value="=">=</option>
    <option value="<">&lt;</option>
    <option value=">">&gt;</option>
    <option value="<=">&le;</option>
    <option value=">=">&ge;</option>
  </select><br/>

  <button onclick="resolver()">Resolver</button>
  <button class="download-btn" onclick="descargarHTML()">Descargar código HTML</button>

  <div id="resultado"></div>

  <script>
    function resolver() {
      const a = parseFloat(document.getElementById('a').value);
      const b = parseFloat(document.getElementById('b').value);
      const op = document.getElementById('operador').value;
      const resultadoDiv = document.getElementById('resultado');
      resultadoDiv.innerHTML = '';

      if (isNaN(a) || isNaN(b)) {
        resultadoDiv.innerHTML = 'Por favor ingresa valores válidos para a y b.';
        return;
      }

      resultadoDiv.innerHTML += `Ecuación/Inecuación dada: ${a}x ${b >= 0 ? '+ ' + b : '- ' + (-b)} ${op} 0\n\n`;

      if (a === 0) {
        if (op === '=') {
          if (b === 0) {
            resultadoDiv.innerHTML += 'Como a=0 y b=0, la ecuación es "0 = 0". Cualquier valor de x es solución.';
          } else {
            resultadoDiv.innerHTML += `Como a=0 y b=${b}, la ecuación es "${b} = 0", que no es verdadera. No hay solución.`;
          }
        } else {
          let desigualdadValida;
          switch(op) {
            case '<': desigualdadValida = (b < 0); break;
            case '>': desigualdadValida = (b > 0); break;
            case '<=': desigualdadValida = (b <= 0); break;
            case '>=': desigualdadValida = (b >= 0); break;
          }
          if (desigualdadValida) {
            resultadoDiv.innerHTML += `Como a=0, la inecuación es "${b} ${op} 0", que es verdadera. Cualquier valor de x es solución.`;
          } else {
            resultadoDiv.innerHTML += `Como a=0, la inecuación es "${b} ${op} 0", que es falsa. No hay solución.`;
          }
        }
        return;
      }

      resultadoDiv.innerHTML += `Paso 1: Restar ${b} en ambos lados:\n`;
      resultadoDiv.innerHTML += `${a}x ${op} ${-b}\n\n`;

      resultadoDiv.innerHTML += `Paso 2: Dividir ambos lados entre ${a} (${a > 0 ? "positivo" : "negativo"}, esto puede cambiar la dirección de la desigualdad):\n`;

      let opFinal = op;
      if (a < 0 && op !== '=') {
        if (op === '<') opFinal = '>';
        else if (op === '>') opFinal = '<';
        else if (op === '<=') opFinal = '>=';
        else if (op === '>=') opFinal = '<=';
      }

      const xResultado = (-b / a).toFixed(4);

      resultadoDiv.innerHTML += `x ${opFinal} ${xResultado}\n\n`;

      resultadoDiv.innerHTML += `Resultado:\n`;
      resultadoDiv.innerHTML += `x ${opFinal} ${xResultado}`;
    }

    function descargarHTML() {
      const htmlContent = document.documentElement.outerHTML;
      const blob = new Blob([htmlContent], {type: 'text/html'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'calculadora-ecuaciones.html';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
    }
  </script>
</body>
</html>


