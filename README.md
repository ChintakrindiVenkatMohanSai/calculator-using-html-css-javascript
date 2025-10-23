<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Advanced Calculator</title>
  <style>
    :root {
      --bg-color: linear-gradient(135deg, #1e3c72, #2a5298);
      --calc-bg: #ffffff10;
      --btn-bg: #0d1b2a;
      --btn-hover: #00ffcc;
      --text-color: #00ffcc;
      --display-bg: #000;
    }

    body.dark {
      --bg-color: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      --calc-bg: #00000050;
      --btn-bg: #1b263b;
      --btn-hover: #00ffcc;
      --text-color: #00ffcc;
      --display-bg: #111;
    }

    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: var(--bg-color);
      font-family: 'Poppins', sans-serif;
      transition: background 0.5s ease;
    }

    .calculator {
      background: var(--calc-bg);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
      padding: 20px;
      width: 300px;
      transition: 0.4s;
    }

    .display {
      width: 100%;
      height: 60px;
      background: var(--display-bg);
      color: var(--text-color);
      border: none;
      border-radius: 10px;
      text-align: right;
      font-size: 2rem;
      padding: 10px;
      margin-bottom: 15px;
      transition: background 0.3s, color 0.3s;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      background: var(--btn-bg);
      color: #fff;
      border: none;
      border-radius: 10px;
      padding: 15px;
      font-size: 1.2rem;
      cursor: pointer;
      transition: transform 0.1s, background 0.3s, color 0.3s;
    }

    button:hover {
      background: var(--btn-hover);
      color: #000;
      transform: scale(1.05);
    }

    .equal {
      grid-column: span 2;
      background: var(--btn-hover);
      color: #000;
      font-weight: 600;
    }

    .theme-toggle {
      display: flex;
      justify-content: center;
      margin-bottom: 10px;
    }

    .theme-toggle button {
      background: var(--btn-bg);
      color: #fff;
      border-radius: 50px;
      padding: 8px 20px;
      font-size: 1rem;
      transition: 0.3s;
    }

    .theme-toggle button:hover {
      background: var(--btn-hover);
      color: #000;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <div class="theme-toggle">
      <button onclick="toggleTheme()">🌙 Dark / ☀️ Light</button>
    </div>
    <input type="text" id="display" class="display" disabled />
    <div class="buttons">
      <button onclick="clearDisplay()">C</button>
      <button onclick="deleteLast()">⌫</button>
      <button onclick="appendOperator('/')">÷</button>
      <button onclick="appendOperator('*')">×</button>
      <button onclick="appendNumber('7')">7</button>
      <button onclick="appendNumber('8')">8</button>
      <button onclick="appendNumber('9')">9</button>
      <button onclick="appendOperator('-')">−</button>
      <button onclick="appendNumber('4')">4</button>
      <button onclick="appendNumber('5')">5</button>
      <button onclick="appendNumber('6')">6</button>
      <button onclick="appendOperator('+')">+</button>
      <button onclick="appendNumber('1')">1</button>
      <button onclick="appendNumber('2')">2</button>
      <button onclick="appendNumber('3')">3</button>
      <button onclick="calculate()" class="equal">=</button>
      <button onclick="appendNumber('0')">0</button>
      <button onclick="appendDot()">.</button>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');

    function appendNumber(num) {
      display.value += num;
    }

    function appendOperator(op) {
      const lastChar = display.value.slice(-1);
      if ('+-*/'.includes(lastChar)) return;
      display.value += op;
    }

    function appendDot() {
      const lastNumber = display.value.split(/[-+*/]/).pop();
      if (!lastNumber.includes('.')) display.value += '.';
    }

    function clearDisplay() {
      display.value = '';
    }

    function deleteLast() {
      display.value = display.value.slice(0, -1);
    }

    function calculate() {
      try {
        display.value = eval(display.value) || '';
      } catch {
        display.value = 'Error';
      }
    }

    function toggleTheme() {
      document.body.classList.toggle('dark');
    }
  </script>
</body>
</html>
