* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #667eea, #764ba2);
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.container {
  background: white;
  border-radius: 15px;
  padding: 30px;
  max-width: 700px;
  width: 100%;
  box-shadow: 0 10px 40px rgba(0,0,0,0.2);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 6px;
}

button {
  padding: 12px 20px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background: #5568d3;
}

.hidden {
  display: none;
}

#weather {
  text-align: center;
  margin-bottom: 20px;
}

#temp {
  font-size: 32px;
  font-weight: bold;
  color: #667eea;
}

/* FORECAST GRID */
#forecast {
  margin-top: 20px;
}

.forecast-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 10px;
}

.forecast-card {
  background: #f4f4f4;
  padding: 10px;
  border-radius: 8px;
  text-align: center;
  font-size: 14px;
}