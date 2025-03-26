<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calorie & Macro Calculator</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Fredoka', sans-serif;
            text-align: center;
            padding: 20px;
            background: #fff5f0;
        }
        .container {
            max-width: 400px;
            margin: auto;
            padding: 20px;
            border-radius: 10px;
            background: #ffbe99;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input, select, button {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: none;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background: #ff7f50;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }
        button:hover {
            background: #ff6347;
        }
        #results {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Calorie & Macro Calculator</h2>
        <label>Age: <input type="number" id="age"></label>
        <label>Gender: 
            <select id="gender">
                <option value="male">Male</option>
                <option value="female">Female</option>
            </select>
        </label>
        <label>Weight (kg): <input type="number" id="weight"></label>
        <label>Height (cm): <input type="number" id="height"></label>
        <label>Activity Level:
            <select id="activity">
                <option value="1.2">Sedentary</option>
                <option value="1.375">Lightly Active</option>
                <option value="1.55">Moderately Active</option>
                <option value="1.725">Very Active</option>
                <option value="1.9">Super Active</option>
            </select>
        </label>
        <label>Goal:
            <select id="goal">
                <option value="-500">Fat Loss</option>
                <option value="0">Maintenance</option>
                <option value="500">Muscle Gain</option>
            </select>
        </label>
        <button onclick="calculateMacros()">Calculate</button>
        <div id="results"></div>
    </div>

    <script>
        function calculateMacros() {
            let age = document.getElementById('age').value;
            let gender = document.getElementById('gender').value;
            let weight = document.getElementById('weight').value;
            let height = document.getElementById('height').value;
            let activity = document.getElementById('activity').value;
            let goal = parseInt(document.getElementById('goal').value);

            if (!age || !weight || !height) {
                alert("Please fill in all fields.");
                return;
            }

            let BMR;
            if (gender === 'male') {
                BMR = 10 * weight + 6.25 * height - 5 * age + 5;
            } else {
                BMR = 10 * weight + 6.25 * height - 5 * age - 161;
            }

            let TDEE = BMR * activity;
            let targetCalories = TDEE + goal;

            let protein = weight * 2;
            let fats = (targetCalories * 0.25) / 9;
            let carbs = (targetCalories - (protein * 4) - (fats * 9)) / 4;

            document.getElementById('results').innerHTML = `
                <h3>Results:</h3>
                <p>Daily Calories: <strong>${Math.round(targetCalories)}</strong></p>
                <p>Protein: <strong>${Math.round(protein)}g</strong></p>
                <p>Fats: <strong>${Math.round(fats)}g</strong></p>
                <p>Carbs: <strong>${Math.round(carbs)}g</strong></p>
            `;
        }
    </script>
</body>
</html>
