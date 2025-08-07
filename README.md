<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Calculadora de Ecuaciones e Inecuaciones</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    input, select, button { font-size: 1.2em; padding: 5px; margin: 5px; }
    #resultado { margin-top: 20px; background: #f0f0f0; padding: 15px; border-radius: 5px; }
    .paso { margin-bottom: 10px; }
  </style>
</head>
<body>
  <h1>Calculadora de Ecuaciones e Inecuaciones Lineales</h1>
  <p>Resuelve ecuaciones o inecuaciones del tipo: <strong>ax + b [operador] 0</strong></p>

  <label for="a">a (coeficiente de x): </label>
  <input type="number" id="a" step="any" /><br/>

  <label for="b">b (término independiente): </label>
  <input type="number" id="b" step="any" /><br/>

  <label for="operador">Operador: </label>
  <select id="operador">
    <option value="=">=</option>
    <option value="<">&lt;</option>
    <option value=">">&gt;</option>
    <option value="<=">&le;</option>
    <option value=">=">&ge;</option>
  </select><br/>

  <button onclick="resolver()">Resolver</button>

  <div id="resultado"></div>

  <script>
    function resolver() {
      const a = parseFloat(document.getElementById('a').value);
      const b = parseFloat(document.getElementById('b').value);
      const op = document.getElementById('operador').value;
      const resultadoDiv = document.getElementById('resultado');
      resultadoDiv.innerHTML = '';

      if (isNaN(a) || isNaN(b)) {
        resultadoDiv.innerHTML = '<p style="color:red;">Por favor ingresa valores válidos para a y b.</p>';
        return;
      }

      // Mostrar la ecuación o inecuación dada
      resultadoDiv.innerHTML += `<div class="paso"><b>Ecuación/Inecuación dada:</b> ${a}x ${b >= 0 ? '+ ' + b : '- ' + (-b)} ${op} 0</div>`;

      // Caso a = 0 (no depende de x)
      if (a === 0) {
        if (op === '=') {
          if (b === 0) {
            resultadoDiv.innerHTML += `<div class="paso">Como a=0 y b=0, la ecuación es <i>0 = 0</i>. Por lo tanto, cualquier valor de x es solución.</div>`;
          } else {
            resultadoDiv.innerHTML += `<div class="paso">Como a=0 y b=${b}, la ecuación es <i>${b} = 0</i>, lo cual es falso. No hay solución.</div>`;
          }
        } else {
          // Inecuación
          let desigualdadValida;
          switch(op) {
            case '<': desigualdadValida = (b < 0); break;
            case '>': desigualdadValida = (b > 0); break;
            case '<=': desigualdadValida = (b <= 0); break;
            case '>=': desigualdadValida = (b >= 0); break;
          }
          if (desigualdadValida) {
            resultadoDiv.innerHTML += `<div class="paso">Como a=0, la inecuación es <i>${b} ${op} 0</i> que es verdadera. Cualquier valor de x es solución.</div>`;
          } else {
            resultadoDiv.innerHTML += `<div class="paso">Como a=0, la inecuación es <i>${b} ${op} 0</i> que es falsa. No hay solución.</div>`;
          }
        }
        return;
      }

      // Resolver ax + b [op] 0 despejando x:
      // Pasos:
      resultadoDiv.innerHTML += `<div class="paso">Paso 1: Restar ${b} en ambos lados:</div>`;
      resultadoDiv.innerHTML += `<div class="paso">${a}x ${op} ${-b}</div>`;

      resultadoDiv.innerHTML += `<div class="paso">Paso 2: Dividir ambos lados entre ${a} (${a > 0 ? "positivo" : "negativo"}, esto puede cambiar la dirección de la desigualdad):</div>`;

      // Si a < 0, cambia la desigualdad de sentido
      let opFinal = op;
      if (a < 0 && op !== '=') {
        // Cambiamos el símbolo de la desigualdad
        if (op === '<') opFinal = '>';
        else if (op === '>') opFinal = '<';
        else if (op === '<=') opFinal = '>=';
        else if (op === '>=') opFinal = '<=';
      }

      const xResultado = (-b / a).toFixed(4);

      resultadoDiv.innerHTML += `<div class="paso">x ${opFinal} ${xResultado}</div>`;

      resultadoDiv.innerHTML += `<div class="paso" style="font-weight:bold;">Resultado:</div>`;
      resultadoDiv.innerHTML += `<div class="paso">x ${opFinal} ${xResultado}</div>`;
    }
  </script>
</body>
</html>
