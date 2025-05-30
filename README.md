# Ex06 BMI Calculator
## Date: 30/05/2025

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
app.js
```
import React, { useState } from 'react';
import './App.css';

function App() {
  const [weight, setWeight] = useState('');
  const [height, setHeight] = useState('');
  const [bmi, setBmi] = useState(null);
  const [message, setMessage] = useState('');

  const calculateBMI = () => {
    if (!weight || !height) {
      alert("Please enter both weight and height!");
      return;
    }

    const heightInMeters = height / 100;
    const bmiValue = (weight / (heightInMeters * heightInMeters)).toFixed(2);
    setBmi(bmiValue);

    if (bmiValue < 18.5) {
      setMessage("Underweight");
    } else if (bmiValue >= 18.5 && bmiValue < 24.9) {
      setMessage("Normal weight");
    } else if (bmiValue >= 25 && bmiValue < 29.9) {
      setMessage("Overweight");
    } else {
      setMessage("Obese");
    }
  };

  return (
    <div className="container">
      <h1>BMI Calculator</h1>
      <div className="form">
        <input
          type="number"
          placeholder="Weight (kg)"
          value={weight}
          onChange={(e) => setWeight(e.target.value)}
        />
        <input
          type="number"
          placeholder="Height (cm)"
          value={height}
          onChange={(e) => setHeight(e.target.value)}
        />
        <button onClick={calculateBMI}>Calculate</button>
      </div>

      {bmi && (
        <div className="result">
          <h2>Your BMI is: {bmi}</h2>
          <p>{message}</p>
        </div>
    
      )}
      <div>
        <footer>
          Mohamed athif rahuman J 212223220058
        </footer>
      </div>
    </div>
  );
}

export default App;
```
app.css
```
body {
  margin: 0;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  position: relative;
}

/* Overlay for readability */
body::before {
  content: '';
  position: fixed;
  top: 0; left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(44, 62, 80, 0.45);
  z-index: 0;
  pointer-events: none;
}

.container {
  position: relative;
  z-index: 1;
  background: rgba(255, 255, 255, 0.97);
  backdrop-filter: blur(10px);
  border-radius: 28px;
  box-shadow: 0 10px 40px rgba(52, 152, 219, 0.18);
  width: 95%;
  max-width: 400px;
  min-height: 420px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 32px 24px 24px 24px;
  text-align: center;
  animation: fadeIn 1s;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(40px);}
  to { opacity: 1; transform: translateY(0);}
}

h1 {
  margin-bottom: 24px;
  color: #3a6073;
  font-weight: 700;
  letter-spacing: 1px;
  font-size: 2.1rem;
  text-shadow: 0 2px 8px rgba(52, 152, 219, 0.08);
}

.form {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 18px;
}

.form input {
  width: 90%;
  padding: 14px;
  border: 1.5px solid #7f8fa6;
  border-radius: 12px;
  font-size: 17px;
  background: rgba(236, 240, 241, 0.7);
  box-shadow: 0 2px 8px rgba(52, 152, 219, 0.06);
  outline: none;
  transition: border 0.2s, box-shadow 0.2s;
  color: #34495e;
}

.form input:focus {
  border: 1.5px solid #00b894;
  box-shadow: 0 0 0 2px #00b89433;
  background: #fff;
}

button {
  width: 95%;
  background: linear-gradient(90deg, #00b894 0%, #6c5ce7 100%);
  color: #fff;
  padding: 14px 0;
  border: none;
  font-size: 17px;
  font-weight: 600;
  border-radius: 10px;
  cursor: pointer;
  box-shadow: 0 4px 16px rgba(76, 201, 240, 0.13);
  transition: all 0.2s;
  margin-top: 8px;
  letter-spacing: 0.5px;
}

button:hover, button:focus {
  background: linear-gradient(90deg, #0984e3, #00b894);
  transform: translateY(-2px) scale(1.04);
  box-shadow: 0 8px 24px rgba(0,184,148,0.18);
}

.result {
  margin-top: 28px;
  padding: 22px 18px;
  background: linear-gradient(120deg, #e0c3fc 70%, #8ec5fc 100%);
  border-radius: 16px;
  box-shadow: 0 2px 16px rgba(76,201,240,0.07);
  animation: fadeIn 0.8s;
}

.result h2 {
  color: #6c5ce7;
  font-size: 25px;
  margin-bottom: 10px;
  font-weight: 700;
}

.result p {
  font-size: 18px;
  color: #34495e;
  margin: 6px 0;
}

footer {
  margin-top: 32px;
  color: #636e72;
  font-size: 15px;
  font-style: italic;
  letter-spacing: 0.5px;
  opacity: 0.85;
}

.error {
  color: #d63031;
  background: #ffeaea;
  border: 1px solid #d63031;
  border-radius: 8px;
  padding: 8px 0;
  margin-top: 10px;
  width: 90%;
  font-size: 15px;
  animation: shake 0.3s;
}

@keyframes shake {
  0% { transform: translateX(0);}
  25% { transform: translateX(-4px);}
  50% { transform: translateX(4px);}
  75% { transform: translateX(-4px);}
  100% { transform: translateX(0);}
}

/* Responsive Design */
@media (max-width: 500px) {
  .container {
    padding: 18px 6px 12px 6px;
    min-height: 340px;
  }
  .form input, button, .result, .error {
    width: 98%;
    font-size: 15px;
  }
  h1 {
    font-size: 1.3rem;
  }
}
```

## OUTPUT

![image](https://github.com/user-attachments/assets/b31629a0-79ae-431e-815d-ac48d3be3b0c)



## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
