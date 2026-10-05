# streter

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Atrápalo</title>
  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #0f172a, #1e293b);
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    .game {
      text-align: center;
      background: rgba(255,255,255,0.08);
      border: 1px solid rgba(255,255,255,0.2);
      border-radius: 18px;
      padding: 20px;
      box-shadow: 0 15px 35px rgba(0,0,0,0.35);
    }

    h1 {
      margin-top: 0;
      font-size: 2rem;
    }

    .stats {
      margin: 12px 0 18px;
      font-size: 1.1rem;
    }

    button {
      background: #22c55e;
      color: white;
      border: none;
      border-radius: 10px;
      padding: 12px 22px;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.2s ease;
    }

    button:hover {
      background: #16a34a;
    }

    #gameArea {
      position: relative;
      width: 500px;
      height: 400px;
      background: linear-gradient(180deg, #1f2937, #111827);
      border-radius: 14px;
      overflow: hidden;
      border: 2px solid rgba(255,255,255,0.15);
      margin: 0 auto;
    }

    #target {
      position: absolute;
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background: radial-gradient(circle at 35% 35%, #fef08a, #facc15, #f59e0b);
      box-shadow: 0 0 18px rgba(250, 204, 21, 0.8);
      cursor: pointer;
      border: 3px solid rgba(255,255,255,0.5);
      transition: transform 0.12s ease;
    }

    #target:hover {
      transform: scale(1.08);
    }

    .message {
      margin-top: 16px;
      font-size: 1.1rem;
      min-height: 24px;
      color: #fcd34d;
    }
  </style>
</head>
<body>
  <div class="game">
    <h1>Atrápalo</h1>

    <div class="stats">
      <span>Puntaje: <strong id="score">0</strong></span>
      &nbsp; | &nbsp;
      <span>Tiempo: <strong id="time">30</strong>s</span>
    </div>

    <button id="startBtn">Iniciar juego</button>

    <div id="gameArea">
      <div id="target"></div>
    </div>

    <div id="message" class="message"></div>
  </div>

  <script>
    const scoreEl = document.getElementById("score");
    const timeEl = document.getElementById("time");
    const startBtn = document.getElementById("startBtn");
    const gameArea = document.getElementById("gameArea");
    const target = document.getElementById("target");
    const messageEl = document.getElementById("message");

    let score = 0;
    let timeLeft = 30;
    let timer = null;
    let playing = false;

    function randomPosition() {
      const maxX = gameArea.clientWidth - target.offsetWidth;
      const maxY = gameArea.clientHeight - target.offsetHeight;
      const x = Math.random() * maxX;
      const y = Math.random() * maxY;
      target.style.left = `${x}px`;
      target.style.top = `${y}px`;
    }

    function updateScore() {
      scoreEl.textContent = score;
    }

    function updateTime() {
      timeEl.textContent = timeLeft;
    }

    function endGame() {
      playing = false;
      clearInterval(timer);
      target.style.display = "none";
      messageEl.textContent = `¡Juego terminado! Tu puntaje final fue: ${score}`;
      startBtn.textContent = "Jugar otra vez";
    }

    function moveTarget() {
      if (!playing) return;
      randomPosition();
    }

    target.addEventListener("click", () => {
      if (!playing) return;
      score++;
      updateScore();
      messageEl.textContent = "¡Buen golpe!";
      moveTarget();
    });

    function tick() {
      timeLeft--;
      updateTime();

      if (timeLeft <= 0) {
        endGame();
      }
    }

    function startGame() {
      score = 0;
      timeLeft = 30;
      updateScore();
      updateTime();
      messageEl.textContent = "";
      target.style.display = "block";
      playing = true;
      randomPosition();

      clearInterval(timer);
      timer = setInterval(tick, 1000);
    }

    startBtn.addEventListener("click", startGame);

    target.style.display = "none";
    updateScore();
    updateTime();
  </script>
</body>
</html>
```

Cómo usarlo:
- Guarda el código en un archivo llamado `juego.html`
- Abre ese archivo en tu navegador
- Haz clic en “Iniciar juego”
- Clickea el círculo que aparece para sumar puntos antes de que termine el tiempo

Si quieres, puedo hacerte otro tipo de juego:
- Snake
- Pong
- Adivina el número
- Memoria
- Tetris
- Un juego más visual con emojis y sonidos