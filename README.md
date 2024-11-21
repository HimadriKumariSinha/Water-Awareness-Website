# Water-Awareness-Website
Water Conservation Website
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Water Conservation Awareness</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #e0f7fa;
            color: #00796b;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            flex-direction: column;
        }
        .container {
            background-color: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.1);
            width: 80%;
            max-width: 800px;
            margin-top: 20px;
        }
        h1 {
            text-align: center;
            color: #004d40;
            font-size: 32px;
            margin-bottom: 20px;
        }
        input, button {
            width: 100%;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
            border: 1px solid #00796b;
            font-size: 16px;
        }
        button {
            background-color: #00796b;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #004d40;
        }
        .tips-container, .results-container {
            background-color: #f1f8e9;
            padding: 20px;
            margin-top: 20px;
            border-radius: 8px;
        }
        .tip {
            background-color: #ffffff;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .tip:hover {
            background-color: #e0f7fa;
        }
        .chart-container {
            width: 100%;
            margin-top: 30px;
            height: 300px;
        }
        .result-text {
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Water Conservation Awareness</h1>
        <p>Calculate how much water you can save by reducing your daily consumption!</p>

        <label for="waterConsumption">Enter Your Water Consumption (in Liters)</label>
        <input type="number" id="waterConsumption" placeholder="e.g., 50" min="1" required />

        <label for="daysTracked">Enter Number of Days to Track</label>
        <input type="number" id="daysTracked" placeholder="e.g., 7" min="1" required />

        <button onclick="calculateWaterSavings()">Calculate Savings</button>

        <div class="results-container" id="results">
            <h3>Results:</h3>
            <p id="resultMessage"></p>
            <p id="suggestionMessage"></p>
        </div>

        <div class="tips-container" id="tips">
            <h3>Water Conservation Tips</h3>
            <div class="tip">Take shorter showers to reduce water usage by up to 50%.</div>
            <div class="tip">Turn off the tap while brushing your teeth.</div>
            <div class="tip">Fix any leaks to save hundreds of liters each year.</div>
            <div class="tip">Use a water-efficient washing machine.</div>
        </div>

        <div class="chart-container" id="chart"></div>

    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Variables
        let waterUsageData = [];
        let dateLabels = [];
        
        // Function to calculate water savings
        function calculateWaterSavings() {
            const waterUsed = parseInt(document.getElementById('waterConsumption').value);
            const daysTracked = parseInt(document.getElementById('daysTracked').value);

            if (!waterUsed || waterUsed <= 0 || !daysTracked || daysTracked <= 0) {
                alert("Please enter valid inputs.");
                return;
            }

            // Calculate water savings based on a 10% reduction target
            const targetReduction = 10;
            const reducedUsage = waterUsed * (1 - targetReduction / 100);
            const waterSavedPerDay = waterUsed - reducedUsage;
            const totalWaterSaved = waterSavedPerDay * daysTracked;

            // Update the results message
            document.getElementById('resultMessage').innerHTML = `
                If you reduce your daily water usage by ${targetReduction}%:
                <br><span class="result-text">You could save ${totalWaterSaved} liters of water over ${daysTracked} days!</span>
            `;
            document.getElementById('suggestionMessage').innerHTML = `
                <span class="result-text">Total water used for ${daysTracked} days:</span> ${waterUsed * daysTracked} liters
            `;

            // Update the chart data for the user
            waterUsageData.push(waterUsed);
            dateLabels.push(`Day ${dateLabels.length + 1}`);
            displayChart();
        }

        // Function to display the chart
        function displayChart() {
            const ctx = document.getElementById('chart').getContext('2d');
            const chart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: dateLabels,
                    datasets: [{
                        label: 'Water Usage (Liters)',
                        data: waterUsageData,
                        borderColor: '#00796b',
                        backgroundColor: 'rgba(0, 121, 107, 0.2)',
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });
        }
    </script>

</body>
</html>
