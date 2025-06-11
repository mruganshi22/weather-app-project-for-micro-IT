<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
            background-color: #ecddf1; /* Slightly darker lavender */
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        input {
            padding: 10px;
            width: 250px;
            margin: 10px;
        }
        button {
            padding: 10px 20px;
            cursor: pointer;
        }
        .weather-info {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Weather App</h1>
    <input type="text" id="location" placeholder="Enter location">
    <button onclick="getWeather()">Get Weather</button>
    <div class="weather-info" id="weather"></div>

    <script>
        async function getWeather() {
            const location = document.getElementById('location').value;
            if (!location) {
                alert('Please enter a location');
                return;
            }
            
            const apiKey = 'dafb4e62fb704230850111733252603';
            const url = `http://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${location}&aqi=yes`;
            
            try {
                const response = await fetch(url);
                const data = await response.json();
                
                if (data.error) {
                    document.getElementById('weather').innerHTML = `<p>${data.error.message}</p>`;
                    return;
                }
                
                document.getElementById('weather').innerHTML = `
                    <h2>Weather in ${data.location.name}, ${data.location.country}</h2>
                    <p>Temperature: ${data.current.temp_c}°C</p>
                    <p>Condition: ${data.current.condition.text}</p>
                    <p>Humidity: ${data.current.humidity}%</p>
                    <p>Wind Speed: ${data.current.wind_kph} kph</p>
                    <img src="${data.current.condition.icon}" alt="Weather icon">
                `;
            } catch (error) {
                document.getElementById('weather').innerHTML = `<p>Error fetching data. Please try again.</p>`;
            }
        }
    </script>
</body>
</html>
