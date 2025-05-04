<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Simple Calculator</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="calculator">
    <input type="text" id="display" disabled />
    <div class="buttons">
      <button onclick="clearDisplay()">C</button>
      <button onclick="deleteLast()">Del</button>
      <button onclick="calculatePercentage()">%</button>
      <button onclick="appendOperator('/')">/</button>

      <button onclick="appendNumber('7')">7</button>
      <button onclick="appendNumber('8')">8</button>
      <button onclick="appendNumber('9')">9</button>
      <button onclick="appendOperator('*')">*</button>

      <button onclick="appendNumber('4')">4</button>
      <button onclick="appendNumber('5')">5</button>
      <button onclick="appendNumber('6')">6</button>
      <button onclick="appendOperator('-')">-</button>

      <button onclick="appendNumber('1')">1</button>
      <button onclick="appendNumber('2')">2</button>
      <button onclick="appendNumber('3')">3</button>
      <button onclick="appendOperator('+')">+</button>

      <button onclick="appendNumber('0')">0</button>
      <button onclick="appendDecimal()">.</button>
      <button onclick="calculateSquareRoot()">√</button>
      <button class="equal-button" onclick="calculate()">=</button>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>￼Enter

body {
  font-family: sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f0f0;
}

.calculator {
  background-color: #333;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 20px;
  width: 320px;
}

#display {
  width: 100%;
  margin-bottom: 15px;
  padding: 15px;
  font-size: 24px;
  text-align: right;
  border: none;
  background-color: #444;
  color: #fff;
  border-radius: 4px;
  box-sizing: border-box;
  overflow-x: auto;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

button {
  padding: 15px;
  font-size: 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: #555;
  color: #fff;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #666;
}

.equal-button {
  background-color: #ff9800;
}

.equal-button:hover {
  background-color: #f57c00;
}

let display = document.getElementById('display');
let currentInput = '';
let operator = null;
let firstOperand = null;

function appendNumber(number) {
  currentInput += number;
  display.value = currentInput;
}

function appendOperator(op) {
  if (currentInput === '') return;
  if (firstOperand !== null && operator !== null) {
    calculate();
  }
  firstOperand = parseFloat(currentInput);
  operator = op;
  currentInput = '';
}

function appendDecimal() {
  if (!currentInput.includes('.')) {
    currentInput += '.';
    display.value = currentInput;
  }
}

function clearDisplay() {
  currentInput = '';
  operator = null;
  firstOperand = null;
  display.value = '';
}

function deleteLast() {
  currentInput = currentInput.slice(0, -1);
  display.value = currentInput;
}

function calculate() {
  if (operator === null || firstOperand === null || currentInput === '') return;
  let secondOperand = parseFloat(currentInput);
  let result;

  switch (operator) {
    case '+':
      result = firstOperand + secondOperand;
      break;
    case '-':
      result = firstOperand - secondOperand;
      break;
    case '*':
      result = firstOperand * secondOperand;
      break;
    case '/':
      if (secondOperand === 0) {
        display.value = 'Error';
        return;
      }
      result = firstOperand / secondOperand;
      break;
    default:
      return;
  }

  currentInput = String(result);
  operator = null;
  firstOperand = null;
  display.value = currentInput;
}

function calculatePercentage() {
  if (currentInput === '') return;
  currentInput = String(parseFloat(currentInput) / 100);
  display.value = currentInput;
}

function calculateSquareRoot() {
  if (currentInput === '') return;
  let value = parseFloat(currentInput);
  if (value < 0) {
    display.value = 'Error';
    return;
  }
  currentInput = String(Math.sqrt(value));
  display.value = currentInput;
}
