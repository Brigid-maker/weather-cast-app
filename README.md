<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <div class="container">
    <h1>🌦️ Weather App</h1>

    <form id="searchForm">
      <input
        type="text"
        id="cityInput"
        placeholder="Enter city name..."
        required
      >
      <button type="submit">Search</button>
    </form>

    <div id="loading" class="hidden">Loading...</div>
    <div id="error" class="hidden"></div>

    <!-- CURRENT WEATHER -->
    <div id="weather" class="hidden">
      <h2 id="cityName"></h2>
      <p id="temp"></p>
      <p id="description"></p>
      <p id="details"></p>
    </div>

    <!-- FORECAST -->
    <div id="forecast" class="hidden"></div>
  </div>

  <script src="main.js"></script>
</body>
</html>