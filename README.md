<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Derivada Logarítmica</title>
  <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
  <script id="MathJax-script" async
          src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
  </script>
</head>
<body>
  <h1>Derivada de una Función Logarítmica</h1>

  <p>Queremos derivar la función:</p>
  <p>\[ f(x) = \ln(x^2 + 1) \]</p>

  <p>Aplicamos la regla de la derivada del logaritmo natural:</p>
  <p>\[ \frac{d}{dx}[\ln(u)] = \frac{1}{u} \cdot \frac{du}{dx} \]</p>

  <p>Identificamos:</p>
  <p>\[ u(x) = x^2 + 1 \]</p>

  <p>Derivamos \( u(x) \):</p>
  <p>\[ \frac{du}{dx} = 2x \]</p>

  <p>Entonces:</p>
  <p>\[ \frac{d}{dx}[\ln(x^2 + 1)] = \frac{1}{x^2 + 1} \cdot 2x \]</p>

  <p>Resultado final:</p>
  <p>\[ f'(x) = \frac{2x}{x^2 + 1} \]</p>

</body>
</html>
