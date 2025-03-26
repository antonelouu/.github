<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Temporizador con Ubicación</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        #countdown {
            font-size: 2em;
            margin: 20px;
        }
        #map {
            width: 100%;
            height: 400px;
            display: none;
        }
    </style>
</head>
<body>
    <h1>Temporizador con Ubicación</h1>
    <label for="time">Selecciona la hora:</label>
    <input type="time" id="time">
    <button onclick="startCountdown()">Iniciar</button>

    <p id="countdown"></p>

    <div id="map-container">
        <iframe id="map" src="" allowfullscreen></iframe>
    </div>

    <script>
        function startCountdown() {
            let timeInput = document.getElementById("time").value;
            if (!timeInput) {
                alert("Por favor, selecciona una hora.");
                return;
            }

            let now = new Date();
            let targetTime = new Date();
            let [hours, minutes] = timeInput.split(":");
            targetTime.setHours(hours, minutes, 0, 0);

            if (targetTime <= now) {
                alert("La hora debe ser en el futuro.");
                return;
            }

            let countdownElement = document.getElementById("countdown");
            let interval = setInterval(() => {
                let now = new Date();
                let timeLeft = targetTime - now;

                if (timeLeft <= 0) {
                    clearInterval(interval);
                    countdownElement.textContent = "¡Es hora!";
                    showLocation();
                } else {
                    let h = Math.floor(timeLeft / (1000 * 60 * 60));
                    let m = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
                    let s = Math.floor((timeLeft % (1000 * 60)) / 1000);
                    countdownElement.textContent = `${h}h ${m}m ${s}s`;
                }
            }, 1000);
        }

        function showLocation() {
            let map = document.getElementById("map");
            map.src = "https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d10000!2d-98.842459!3d19.233141!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMTnCsDEzJzU5LjMiTiA5OMKwNTAnMzIuOCJX!5e0!3m2!1ses!2sus!4v1649115220412!5m2!1ses!2sus";
            map.style.display = "block";
        }
    </script>
</body>
</html>
