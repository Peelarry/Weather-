<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="app-container">
    <h1>Weather App</h1>
    <input type="text" id="cityInput" placeholder="Enter city name">
    <button onclick="getWeather()">Get Weather</button>
    <div id="weatherResult"></div>
  </div>
  <script src="script.js"></script>
</body>
</html>
    body {
  font-family: Arial, sans-serif;
  background: #e0f7fa;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.app-container {
  text-align: center;
  background: white;
  padding: 20px;
  border-radius: 10px;
}

input {
  padding: 10px;
  width: 200px;
}

button {
  padding: 10px;
  margin-left: 10px;
  cursor: pointer;
}

#weatherResult {
  margin-top: 20px;
  font-size: 18px;
}
const apiKey = 'YOUR_API_KEY_HERE'; // Get this from openweathermap.org

function getWeather() {
  const city = document.getElementById('cityInput').value;
  if (!city) {
    alert("Please enter a city name.");
    return;
  }

  fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`)
    .then(response => {
      if (!response.ok) throw new Error("City not found");
      return response.json();
    })
    .then(data => {
      const weatherDiv = document.getElementById('weatherResult');
      weatherDiv.innerHTML = `
        <h2>${data.name}</h2>
        <p>Temperature: ${data.main.temp}°C</p>
        <p>Weather: ${data.weather[0].description}</p>
        <p>Humidity: ${data.main.humidity}%</p>
      `;
    })
    .catch(error => {
      document.getElementById('weatherResult').innerHTML = `<p>${error.message}</p>`;
    });
}
    
