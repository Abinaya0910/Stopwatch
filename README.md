# Stopwatch
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch with Milliseconds & Laps - ProDigy Infotech</title>
  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #1d2b64, #f8cdda);
      background-size: 400% 400%;
      animation: gradientMove 10s ease infinite;
      color: white;
    }

    @keyframes gradientMove {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }

    .container {
      text-align: center;
      padding: 30px;
      border-radius: 20px;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      box-shadow: 0 0 25px rgba(0, 0, 0, 0.2);
      max-width: 420px;
      width: 100%;
    }

    .circle-border {
      width: 220px;
      height: 220px;
      border-radius: 50%;
      background: conic-gradient(#00feba, #5b548a, #f0a6ca, #00feba);
      padding: 10px;
      margin: 0 auto 30px auto;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .time-display {
      background: rgba(0, 0, 0, 0.4);
      border-radius: 50%;
      width: 200px;
      height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.8rem;
      font-weight: bold;
      text-shadow: 1px 1px 4px #000;
      flex-direction: column;
    }

    .time-display span {
      font-size: 2.2rem;
    }

    .buttons {
      margin-top: 20px;
    }

    .buttons button {
      padding: 10px 20px;
      margin: 8px 5px;
      font-size: 1rem;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.3s;
    }

    .buttons button:hover {
      transform: scale(1.05);
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
    }

    .start { background-color: #00c853; color: white; }
    .pause { background-color: #ffca28; color: black; }
    .reset { background-color: #d32f2f; color: white; }
    .lap   { background-color: #3949ab; color: white; }

    .laps {
      margin-top: 25px;
      max-height: 150px;
      overflow-y: auto;
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      padding: 10px;
      text-align: left;
      font-size: 0.95rem;
    }

    .lap-item {
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      padding: 5px 0;
    }

    footer {
      margin-top: 20px;
      font-size: 0.85rem;
      color: #ccc;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="circle-border">
      <div class="time-display" id="display">
        <span id="timeText">00:00:00</span>:<small id="msText">00</small>
      </div>
    </div>
    <div class="buttons">
      <button class="start" onclick="startTimer()">Start</button>
      <button class="pause" onclick="pauseTimer()">Pause</button>
      <button class="reset" onclick="resetTimer()">Reset</button>
      <button class="lap" onclick="recordLap()">Lap</button>
    </div>
    <div class="laps" id="laps">
      <!-- Lap list -->
    </div>
    <footer>
      Task-02 | ProDigy Infotech | Millisecond Stopwatch
    </footer>
  </div>

  <script>
    let [hours, minutes, seconds, milliseconds] = [0, 0, 0, 0];
    let timer = null;
    const timeText = document.getElementById("timeText");
    const msText = document.getElementById("msText");
    const lapsContainer = document.getElementById("laps");

    function updateDisplay() {
      const h = String(hours).padStart(2, '0');
      const m = String(minutes).padStart(2, '0');
      const s = String(seconds).padStart(2, '0');
      const ms = String(milliseconds).padStart(2, '0');
      timeText.textContent = `${h}:${m}:${s}`;
      msText.textContent = ms;
    }

    function stopwatch() {
      milliseconds += 1;
      if (milliseconds === 100) {
        milliseconds = 0;
        seconds++;
      }
      if (seconds === 60) {
        seconds = 0;
        minutes++;
      }
      if (minutes === 60) {
        minutes = 0;
        hours++;
      }
      updateDisplay();
    }

    function startTimer() {
      if (timer === null) {
        timer = setInterval(stopwatch, 10);
      }
    }

    function pauseTimer() {
      clearInterval(timer);
      timer = null;
    }

    function resetTimer() {
      clearInterval(timer);
      timer = null;
      [hours, minutes, seconds, milliseconds] = [0, 0, 0, 0];
      updateDisplay();
      lapsContainer.innerHTML = '';
    }

    function recordLap() {
      if (hours === 0 && minutes === 0 && seconds === 0 && milliseconds === 0) return;
      const h = String(hours).padStart(2, '0');
      const m = String(minutes).padStart(2, '0');
      const s = String(seconds).padStart(2, '0');
      const ms = String(milliseconds).padStart(2, '0');
      const lapItem = document.createElement("div");
      lapItem.className = "lap-item";
      lapItem.textContent = `Lap ${lapsContainer.children.length + 1}: ${h}:${m}:${s}:${ms}`;
      lapsContainer.prepend(lapItem);
    }
  </script>
</body>
</html>
