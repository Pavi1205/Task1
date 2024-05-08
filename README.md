<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        .weather-container {
            text-align: center;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            background-color: #fff;
        }
        .weather-icon {
            width: 100px;
            height: 100px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="weather-container">
        <h2>Current Weather</h2>
        <div id="weather-icon"></div>
        <h3 id="weather-condition"></h3>
        <p id="temperature"></p>
        <p id="other-info"></p>
    </div>

    <script>
        window.addEventListener('load', () => {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(position => {
                    const { latitude, longitude } = position.coords;
                    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&appid=YOUR_API_KEY&units=metric`)
                        .then(response => response.json())
                        .then(data => {
                            const weatherIcon = document.getElementById('weather-icon');
                            const weatherCondition = document.getElementById('weather-condition');
                            const temperature = document.getElementById('temperature');
                            const otherInfo = document.getElementById('other-info');

                            weatherIcon.innerHTML = `<img src="http://openweathermap.org/img/wn/${data.weather[0].icon}.png" class="weather-icon" alt="Weather Icon">`;
                            weatherCondition.textContent = data.weather[0].main;
                            temperature.textContent = `Temperature: ${data.main.temp}°C`;
                            otherInfo.textContent = `Humidity: ${data.main.humidity}%`;
                        })
                        .catch(error => {
                            console.error('Error fetching weather data:', error);
                        });
                });
            } else {
                console.error('Geolocation is not supported by this browser.');
            }
        });
    </script>
</body>
</html>
