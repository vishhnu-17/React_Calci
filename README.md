# Ex04 Simple Calculator - React Project
## Date: 30-05-26

## AIM
To  develop a Simple Calculator using React.js with clean and responsive design, ensuring a smooth user experience across different screen sizes.

## ALGORITHM
### STEP 1
Create a React App.

### STEP 2
Open a terminal and run:
  <ul><li>npx create-react-app simple-calculator</li>
  <li>cd simple-calculator</li>
  <li>npm start</li></ul>

### STEP 3
Inside the src/ folder, create a new file Calculator.js and define the basic structure.

### STEP 4
Plan the UI: Display screen, number buttons (0-9), operators (+, -, *, /), clear (C), and equal (=).

### STEP 5
Create a new file Calculator.css in src/ and add the styling.

### STEP 6
Open src/App.js and modify it.

### STEP 7
Start the development server.
  npm start

### STEP 8
Open http://localhost:3000/ in the browser.

### STEP 9
Test the calculator by entering numbers and operations.

### STEP 10
Fix styling issues and refine content placement.

### STEP 11
Deploy the website.

### STEP 12
Upload to GitHub Pages for free hosting.

## PROGRAM
### App.jsx
```jsx
import React from 'react';
import Calculator from './Calculator';
import './Calculator.css';

function App() {
  return (
    <div className="App">
      <Calculator />
    </div>
  );
}

export default App;
```
### Calculator.css
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f0f0f0;
  font-family: Arial, sans-serif;
}

.App {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.calculator {
  background-color: #1c1c1e;
  border-radius: 20px;
  padding: 20px;
  width: 320px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.4);
}

.display {
  background-color: transparent;
  padding: 16px 10px 10px;
  text-align: right;
  min-height: 80px;
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  overflow: hidden;
}

.display-text {
  color: #ffffff;
  font-size: 52px;
  font-weight: 300;
  word-break: break-all;
  line-height: 1;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-top: 12px;
}

.btn {
  border: none;
  border-radius: 50%;
  width: 64px;
  height: 64px;
  font-size: 22px;
  cursor: pointer;
  font-family: Arial, sans-serif;
  transition: opacity 0.1s ease;
}

.btn:active {
  opacity: 0.7;
}

.btn-number {
  background-color: #505050;
  color: #ffffff;
}

.btn-light {
  background-color: #a5a5a5;
  color: #1c1c1e;
}

.btn-operator {
  background-color: #ff9f0a;
  color: #ffffff;
}

.btn-equals {
  background-color: #ff9f0a;
  color: #ffffff;
  border-radius: 50%;
  width: 64px;
  height: 64px;
  font-size: 22px;
}

.btn-zero {
  grid-column: span 2;
  width: 100%;
  border-radius: 32px;
  text-align: left;
  padding-left: 24px;
}
```
### Calculator.js
```js
import React, { useState } from 'react';
import './Calculator.css';

function Calculator() {
  const [display, setDisplay] = useState('0');
  const [firstOperand, setFirstOperand] = useState(null);
  const [operator, setOperator] = useState(null);
  const [waitingForSecond, setWaitingForSecond] = useState(false);

  function handleNumber(num) {
    if (waitingForSecond) {
      setDisplay(String(num));
      setWaitingForSecond(false);
    } else {
      setDisplay(display === '0' ? String(num) : display + num);
    }
  }

  function handleDecimal() {
    if (waitingForSecond) {
      setDisplay('0.');
      setWaitingForSecond(false);
      return;
    }
    if (!display.includes('.')) {
      setDisplay(display + '.');
    }
  }

  function handleOperator(op) {
    const current = parseFloat(display);
    if (firstOperand !== null && !waitingForSecond) {
      const result = calculate(firstOperand, current, operator);
      setDisplay(String(result));
      setFirstOperand(result);
    } else {
      setFirstOperand(current);
    }
    setOperator(op);
    setWaitingForSecond(true);
  }

  function calculate(a, b, op) {
    if (op === '+') return a + b;
    if (op === '-') return a - b;
    if (op === '*') return a * b;
    if (op === '/') return b !== 0 ? a / b : 'Error';
    return b;
  }

  function handleEquals() {
    if (operator === null || waitingForSecond) return;
    const current = parseFloat(display);
    const result = calculate(firstOperand, current, operator);
    setDisplay(String(result));
    setFirstOperand(null);
    setOperator(null);
    setWaitingForSecond(false);
  }

  function handleClear() {
    setDisplay('0');
    setFirstOperand(null);
    setOperator(null);
    setWaitingForSecond(false);
  }

  function handleToggleSign() {
    setDisplay(String(parseFloat(display) * -1));
  }

  function handlePercent() {
    setDisplay(String(parseFloat(display) / 100));
  }

  return (
    <div className="calculator">
      <div className="display">
        <span className="display-text">{display}</span>
      </div>

      <div className="buttons">
        <button className="btn btn-light" id="btn-clear" onClick={handleClear}>C</button>
        <button className="btn btn-light" id="btn-sign" onClick={handleToggleSign}>+/-</button>
        <button className="btn btn-light" id="btn-percent" onClick={handlePercent}>%</button>
        <button className="btn btn-operator" id="btn-divide" onClick={() => handleOperator('/')}>÷</button>

        <button className="btn btn-number" id="btn-7" onClick={() => handleNumber('7')}>7</button>
        <button className="btn btn-number" id="btn-8" onClick={() => handleNumber('8')}>8</button>
        <button className="btn btn-number" id="btn-9" onClick={() => handleNumber('9')}>9</button>
        <button className="btn btn-operator" id="btn-multiply" onClick={() => handleOperator('*')}>×</button>

        <button className="btn btn-number" id="btn-4" onClick={() => handleNumber('4')}>4</button>
        <button className="btn btn-number" id="btn-5" onClick={() => handleNumber('5')}>5</button>
        <button className="btn btn-number" id="btn-6" onClick={() => handleNumber('6')}>6</button>
        <button className="btn btn-operator" id="btn-subtract" onClick={() => handleOperator('-')}>−</button>

        <button className="btn btn-number" id="btn-1" onClick={() => handleNumber('1')}>1</button>
        <button className="btn btn-number" id="btn-2" onClick={() => handleNumber('2')}>2</button>
        <button className="btn btn-number" id="btn-3" onClick={() => handleNumber('3')}>3</button>
        <button className="btn btn-operator" id="btn-add" onClick={() => handleOperator('+')}>+</button>

        <button className="btn btn-number btn-zero" id="btn-0" onClick={() => handleNumber('0')}>0</button>
        <button className="btn btn-number" id="btn-dot" onClick={handleDecimal}>.</button>
        <button className="btn btn-equals" id="btn-equals" onClick={handleEquals}>=</button>
      </div>
    </div>
  );
}

export default Calculator;
```

## OUTPUT
<img width="1914" height="1079" alt="image" src="https://github.com/user-attachments/assets/eb8ab89a-08b6-4d3c-8ad3-eb9cb842e7fb" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dbebde52-ef57-4919-9b08-be4734733913" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/eeb2407e-f47f-4dfa-a322-e0d9946b05fe" />


## RESULT
The program for developing a simple calculator in React.js is executed successfully.
