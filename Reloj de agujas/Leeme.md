Quiero generar un reloj de agujas con el circulo interior del reloj con una imagen de una marca de relojes, html, CSS, javascript 


Puedes generar un reloj de agujas usando HTML, CSS y JavaScript, y colocar la imagen de una marca de relojes en el círculo interior del reloj. Aquí tienes un ejemplo sencillo de cómo hacerlo:

Estructura HTML

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Reloj de Agujas</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="clock">
    <div class="clock-face">
      <img src="tu_imagen_de_marca.png" alt="Marca de reloj" class="clock-logo">
      <div class="hand hour" id="hour"></div>
      <div class="hand minute" id="minute"></div>
      <div class="hand second" id="second"></div>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
Estilos CSS
css

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.clock {
  width: 300px;
  height: 300px;
  border: 5px solid black;
  border-radius: 50%;
  position: relative;
}

.clock-face {
  width: 100%;
  height: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.clock-logo {
  position: absolute;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  z-index: 10;
}

.hand {
  position: absolute;
  width: 50%;
  height: 2px;
  background-color: black;
  top: 50%;
  transform-origin: 100%;
  transform: rotate(90deg);
  transition: all 0.05s cubic-bezier(0.1, 2.7, 0.58, 1);
}

.second {
  height: 1px;
  background-color: red;
}

.hour {
  width: 35%;
}

.minute {
  width: 45%;
}
JavaScript
javascript
Copiar código
const secondHand = document.getElementById('second');
const minuteHand = document.getElementById('minute');
const hourHand = document.getElementById('hour');

function setClock() {
  const now = new Date();
  const seconds = now.getSeconds();
  const minutes = now.getMinutes();
  const hours = now.getHours();

  const secondDegrees = ((seconds / 60) * 360) + 90;
  const minuteDegrees = ((minutes / 60) * 360) + ((seconds / 60) * 6) + 90;
  const hourDegrees = ((hours % 12) / 12) * 360 + ((minutes / 60) * 30) + 90;

  secondHand.style.transform = `rotate(${secondDegrees}deg)`;
  minuteHand.style.transform = `rotate(${minuteDegrees}deg)`;
  hourHand.style.transform = `rotate(${hourDegrees}deg)`;
}

setInterval(setClock, 1000);

Explicación:
HTML: Estructuramos el reloj con un div .clock y dentro de él colocamos otro div .clock-face, donde están las agujas del reloj (hour, minute, second). También añadimos una imagen (clock-logo) para que se vea en el centro del reloj. Asegúrate de reemplazar tu_imagen_de_marca.png por la ruta de la imagen de tu marca.

CSS: El estilo define el aspecto del reloj. Las agujas se posicionan con position: absolute y la propiedad transform-origin se asegura de que giren desde el centro del reloj.

JavaScript: Usamos la función setClock para obtener la hora actual y calcular el ángulo de cada aguja en función de los segundos, minutos y horas. Cada aguja rota usando CSS transform con el ángulo calculado.