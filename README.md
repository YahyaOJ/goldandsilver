<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Affan Assets Management</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.0/chart.min.js"></script>
    <style>
        /* Apple-like minimalist theme */
        :root {
            --background-light: #f5f5f7;
            --text-dark: #1d1d1f;
            --accent-blue: #0071e3;
            --accent-gray: #e5e5ea;
            --accent-gold: #d4af37;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--background-light);
            color: var(--text-dark);
            line-height: 1.6;
        }
        
        .nav {
            background: var(--background-light);
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            padding: 10px 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .nav-content {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }
        
        .logo {
            font-size: 1.5em;
            font-weight: 600;
            color: var(--text-dark);
        }
        
        .hero {
            padding: 150px 20px 60px;
            text-align: center;
            background: var(--background-light);
        }
        
        .hero h1 {
            font-size: 4em;
            font-weight: 700;
            color: var(--text-dark);
            margin: 0;
        }
        
        .hero p {
            font-size: 1.5em;
            color: var(--accent-gray);
            margin: 10px 0 30px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 60px 20px;
        }
        
        .calculator-section {
            background: var(--accent-gray);
            border-radius: 20px;
            padding: 50px;
            margin: 60px 0;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        
        input[type="number"] {
            width: 100%;
            padding: 20px;
            border: 2px solid var(--accent-blue);
            border-radius: 12px;
            background: #ffffff;
            color: var(--text-dark);
            font-size: 18px;
            margin-bottom: 25px;
        }
        
        input[type="number"]:focus {
            outline: none;
            border-color: var(--accent-gold);
        }
        
        button {
            background-color: var(--accent-blue);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease;
            width: 100%;
        }
        
        button:hover {
            background-color: #005bb5;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin: 60px 0;
        }
        
        .info-card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease;
        }
        
        .info-card:hover {
            transform: scale(1.03);
        }
        
        .info-card h3 {
            color: var(--accent-blue);
            font-size: 1.8em;
            margin-bottom: 20px;
        }
        
        .charts {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 40px;
            margin-top: 50px;
        }
        
        .chart-container {
            background: white;
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
        }
        
        .results {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
            margin-top: 40px;
        }
        
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 3em;
            }
            .hero p {
                font-size: 1.2em;
            }
        }
    </style>
</head>
<body>
    <nav class="nav">
        <div class="nav-content">
            <div class="logo">Affan Assets Management</div>
        </div>
    </nav>

    <div class="hero">
        <h1>Precious Metals Portfolio</h1>
        <p>Strategic wealth preservation through gold and silver allocation</p>
    </div>

    <div class="container">
        <div class="info-grid">
            <div class="info-card">
                <h3>Why Gold?</h3>
                <p>Gold has been a store of value for over 5,000 years. As a hedge against inflation and economic uncertainty, gold typically performs well during market volatility.</p>
            </div>
            <div class="info-card">
                <h3>Why Silver?</h3>
                <p>Silver offers both investment potential and industrial utility, making it uniquely positioned in a diversified portfolio.</p>
            </div>
            <div class="info-card">
                <h3>Strategic Allocation</h3>
                <p>Experts recommend a 5-15% allocation to precious metals for risk management and wealth preservation.</p>
            </div>
        </div>

        <div class="calculator-section">
            <h2>Portfolio Calculator</h2>
            <div class="form-group">
                <label for="totalAssets">Total Portfolio Value (USD)</label>
                <input type="number" id="totalAssets" placeholder="Enter total assets value" min="0">
                
                <label for="goldPercent">Desired Gold Allocation (%)</label>
                <input type="number" id="goldPercent" placeholder="Enter gold percentage" min="0" max="100" value="5">
                
                <label for="silverPercent">Desired Silver Allocation (%)</label>
                <input type="number" id="silverPercent" placeholder="Enter silver percentage" min="0" max="100" value="2">
                
                <button onclick="calculateAllocation()">Calculate Allocation</button>
            </div>

            <div class="results" id="results" style="display: none;">
                <h2>Your Portfolio Breakdown</h2>
                <p id="summaryText"></p>
                
                <div class="charts">
                    <div class="chart-container">
                        <canvas id="pieChart"></canvas>
                    </div>
                    <div class="chart-container">
                        <canvas id="barChart"></canvas>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let pieChart = null;
        let barChart = null;

        function calculateAllocation() {
            const totalAssets = parseFloat(document.getElementById('totalAssets').value);
            const goldPercent = parseFloat(document.getElementById('goldPercent').value);
            const silverPercent = parseFloat(document.getElementById('silverPercent').value);

            if (!totalAssets || goldPercent + silverPercent > 100) {
                alert('Please enter valid values. Total metal allocation cannot exceed 100%');
                return;
            }

            const goldAllocation = (totalAssets * goldPercent / 100).toFixed(2);
            const silverAllocation = (totalAssets * silverPercent / 100).toFixed(2);
            const remainingAllocation = (totalAssets - goldAllocation - silverAllocation).toFixed(2);

            document.getElementById('results').style.display = 'block';
            document.getElementById('summaryText').innerHTML = `
                <strong>Total Portfolio:</strong> $${totalAssets.toLocaleString()}<br>
                <strong>Gold Allocation:</strong> $${parseFloat(goldAllocation).toLocaleString()} (${goldPercent}%)<br>
                <strong>Silver Allocation:</strong> $${parseFloat(silverAllocation).toLocaleString()} (${silverPercent}%)<br>
                <strong>Remaining Portfolio:</strong> $${parseFloat(remainingAllocation).toLocaleString()} (${(100 - goldPercent - silverPercent).toFixed(1)}%)
            `;

            updateCharts(goldAllocation, silverAllocation, remainingAllocation);
        }

        function updateCharts(gold, silver, remaining) {
            const ctx1 = document.getElementById('pieChart').getContext('2d');
            const ctx2 = document.getElementById('barChart').getContext('2d');

            const chartColors = {
                gold: '#D4AF37',
                silver: '#C0C0C0',
                other: '#4f4f4f'
            };

            if (pieChart) pieChart.destroy();
            if (barChart) barChart.destroy();

            pieChart = new Chart(ctx1, {
                type: 'pie',
                data: {
                    labels: ['Gold', 'Silver', 'Other Assets'],
                    datasets: [{
                        data: [gold, silver, remaining],
                        backgroundColor: [chartColors.gold, chartColors.silver, chartColors.other]
                    }]
                },
                options: {
                    plugins: {
                        title: {
                            display: true,
                            text: 'Portfolio Distribution',
                            color: var(--text-dark)
                        },
                        legend: {
                            labels: {
                                color: var(--text-dark)
                            }
                        }
                    }
                }
            });

            barChart = new Chart(ctx2, {
                type: 'bar',
                data: {
                    labels: ['Asset Allocation'],
                    datasets: [
                        {
                            label: 'Gold',
                            data: [gold],
                            backgroundColor: chartColors.gold
                        },
                        {
                            label: 'Silver',
                            data: [silver],
                            backgroundColor: chartColors.silver
                        },
                        {
                            label: 'Other Assets',
                            data: [remaining],
                            backgroundColor: chartColors.other
                        }
                    ]
                },
                options: {
                    plugins: {
                        title: {
                            display: true,
                            text: 'Asset Values (USD)',
                            color: var(--text-dark)
                        },
                        legend: {
                            labels: {
                                color: var(--text-dark)
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                color: var(--accent-gray)
                            },
                            ticks: {
                                color: var(--text-dark)
                            }
                        },
                        x: {
                            grid: {
                                color: var(--accent-gray)
                            },
                            ticks: {
                                color: var(--text-dark)
                            }
                        }
                    }
                }
            });
        }
    </script>
</body>
</html>
