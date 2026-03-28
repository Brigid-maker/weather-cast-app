const API_KEY = "YOUR_API_KEY"; // 🔥 PUT YOUR KEY HERE

const form = document.getElementById("searchForm");
const input = document.getElementById("cityInput");
const loading = document.getElementById("loading");
const error = document.getElementById("error");
const weatherDiv = document.getElementById("weather");
const forecastDiv = document.getElementById("forecast");

form.addEventListener("submit", async (e) => {
  e.preventDefault();

  const city = input.value.trim();
  if (!city) return;

  try {
    showLoading();

    const coords = await getCoordinates(city);
    const weather = await getCurrentWeather(city);
    const forecast = await getForecast(coords.lat, coords.lon);

    displayWeather(weather);
    displayForecast(forecast);

  } catch (err) {
    showError(err.message);
  } finally {
    hideLoading();
  }
});


// 📍 GET COORDINATES
async function getCoordinates(city) {
  const res = await fetch(
    `https://api.openweathermap.org/geo/1.0/direct?q=${city}&limit=1&appid=${API_KEY}`
  );

  const data = await res.json();

  if (!data.length) throw new Error("City not found");

  return data[0];
}


// 🌡️ CURRENT WEATHER
async function getCurrentWeather(city) {
  const res = await fetch(
    `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${API_KEY}`
  );

  if (!res.ok) throw new Error("Weather not found");

  return await res.json();
}


// 📅 FORECAST (8 DAYS)
async function getForecast(lat, lon) {
  const res = await fetch(
    `https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${lon}&exclude=current,minutely,hourly,alerts&units=metric&appid=${API_KEY}`
  );

  return await res.json();
}


// 🎯 DISPLAY CURRENT WEATHER
function displayWeather(data) {
  document.getElementById("cityName").textContent =
    `${data.name}, ${data.sys.country}`;

  document.getElementById("temp").textContent =
    `${Math.round(data.main.temp)}°C`;

  document.getElementById("description").textContent =
    data.weather[0].description;

  document.getElementById("details").textContent =
    `Humidity: ${data.main.humidity}% • Wind: ${data.wind.speed} m/s`;

  weatherDiv.classList.remove("hidden");
}


// 📊 DISPLAY FORECAST
function displayForecast(data) {
  forecastDiv.classList.remove("hidden");

  const days = data.daily.slice(0, 8);

  forecastDiv.innerHTML = "<h3>8-Day Forecast</h3><div class='forecast-grid'></div>";

  const grid = forecastDiv.querySelector(".forecast-grid");

  days.forEach(day => {
    const date = new Date(day.dt * 1000);
    const dayName = date.toLocaleDateString("en-US", { weekday: "short" });

    const card = document.createElement("div");
    card.className = "forecast-card";

    card.innerHTML = `
      <strong>${dayName}</strong>
      <p>${Math.round(day.temp.day)}°C</p>
      <p>${day.weather[0].main}</p>
    `;

    grid.appendChild(card);
  });
}


// ⏳ UI STATES
function showLoading() {
  loading.classList.remove("hidden");
  error.classList.add("hidden");
}

function hideLoading() {
  loading.classList.add("hidden");
}

function showError(message) {
  error.textContent = message;
  error.classList.remove("hidden");
}