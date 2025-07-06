<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MathGenius Solver</title>
    <!-- AdSense/AdMob Integration -->
    <meta name="google-adsense-account" content="ca-pub-2025523835935359">
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-2025523835935359" crossorigin="anonymous"></script>
    <style>
        :root {
            --primary: #4a6bff;
            --secondary: #f5f7ff;
            --dark: #1a1a2e;
            --light: #ffffff;
            --success: #28a745;
            --warning: #ffc107;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--secondary);
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .tagline {
            color: #666;
            font-size: 1.1rem;
        }
        
        .solver-container {
            background-color: var(--light);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            padding: 25px;
            margin-bottom: 30px;
        }
        
        .input-group {
            display: flex;
            margin-bottom: 20px;
        }
        
        #mathInput {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 5px 0 0 5px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        #mathInput:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        #solveBtn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 0 5px 5px 0;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        
        #solveBtn:hover {
            background-color: #3a5bef;
        }
        
        .solution-container {
            margin-top: 20px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 5px;
            border-left: 4px solid var(--primary);
        }
        
        .solution-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        .solution-steps {
            margin-left: 20px;
        }
        
        .solution-steps li {
            margin-bottom: 8px;
        }
        
        .examples {
            margin-top: 30px;
        }
        
        .examples h3 {
            margin-bottom: 15px;
            color: var(--primary);
        }
        
        .example-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .example-item {
            background-color: var(--light);
            padding: 15px;
            border-radius: 5px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        
        .example-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .example-item p {
            color: #666;
            font-size: 0.9rem;
        }
        
        .loading {
            display: none;
            text-align: center;
            margin: 20px 0;
        }
        
        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 4px solid var(--primary);
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .error {
            color: #dc3545;
            margin-top: 10px;
            padding: 10px;
            background-color: #f8d7da;
            border-radius: 5px;
            display: none;
        }
        
        .math-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }
        
        .math-tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }
        
        .math-tab.active {
            border-bottom: 3px solid var(--primary);
            color: var(--primary);
            font-weight: bold;
        }
        
        /* Ad Container Styles */
        .ad-container {
            width: 100%;
            margin: 25px 0;
            display: flex;
            justify-content: center;
            min-height: 100px;
            background-color: #f5f5f5;
            border-radius: 5px;
            padding: 10px;
            flex-direction: column;
        }
        
        .ad-label {
            text-align: center;
            font-size: 0.8rem;
            color: #666;
            margin-bottom: 5px;
        }
        
        .ad-placeholder {
            width: 100%;
            min-height: 90px;
            background: repeating-linear-gradient(
                45deg,
                #fafafa,
                #fafafa 10px,
                #eee 10px,
                #eee 20px
            );
            display: flex;
            justify-content: center;
            align-items: center;
            color: #666;
            font-size: 0.9rem;
            text-align: center;
        }
        
        @media (max-width: 600px) {
            .input-group {
                flex-direction: column;
            }
            
            #mathInput {
                border-radius: 5px;
                margin-bottom: 10px;
            }
            
            #solveBtn {
                border-radius: 5px;
                width: 100%;
            }
            
            .example-list {
                grid-template-columns: 1fr;
            }
            
            .ad-container {
                min-height: 50px;
            }
        }
    </style>
</head>
<body>
    <!-- Development Mode Warning -->
    <script>
      if (window.location.protocol === 'file:') {
        document.write(`
          <div style="position: fixed; top: 0; left: 0; right: 0; padding: 10px; 
                     background: #ffeb3b; color: #000; text-align: center; z-index: 1000;">
              </div>
        `);
      }
    </script>

    <div class="container">
        <header>
            <h1>MathGenius Solver</h1>
            <p class="tagline">Your personal AI math assistant - solves any problem with step-by-step explanations</p>
        </header>
        
        <!-- Top Ad Unit - First Ad Slot -->
        <div class="ad-container">
            <div class="ad-label">Advertisement</div>
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-2025523835935359"
                 data-ad-slot="2310346797"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                 (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
            <div class="ad-placeholder" id="ad-fallback-1">
                Loading advertisement...
            </div>
        </div>
        
        <div class="solver-container">
            <div class="math-tabs">
                <div class="math-tab active" data-tab="solve">Solve</div>
                <div class="math-tab" data-tab="graph">Graph</div>
                <div class="math-tab" data-tab="simplify">Simplify</div>
            </div>
            
            <div class="input-group">
                <input type="text" id="mathInput" placeholder="Enter your math problem (e.g., 2x+5=15, x^2-4=0, derivative of x^2)...">
                <button id="solveBtn">Solve</button>
            </div>
            
            <div class="error" id="errorMessage"></div>
            
            <div class="loading" id="loadingIndicator">
                <div class="spinner"></div>
                <p>Solving your problem...</p>
            </div>
            
            <div class="solution-container" id="solutionContainer" style="display: none;">
                <div class="solution-title">Solution:</div>
                <div class="solution-content" id="solutionContent"></div>
            </div>
        </div>
        
        <!-- Middle Ad Unit - Second Ad Slot -->
        <div class="ad-container">
            <div class="ad-label">Advertisement</div>
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-2025523835935359"
                 data-ad-slot="9570175121"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                 (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
            <div class="ad-placeholder" id="ad-fallback-2">
                Loading advertisement...
            </div>
        </div>
        
        <div class="examples">
            <h3>Try these examples:</h3>
            <div class="example-list">
                <div class="example-item" data-example="2x + 5 = 15">
                    <strong>Solve: 2x + 5 = 15</strong>
                    <p>Basic algebra equation</p>
                </div>
                <div class="example-item" data-example="x^2 - 4x + 4 = 0">
                    <strong>Solve: x² - 4x + 4 = 0</strong>
                    <p>Quadratic equation</p>
                </div>
                <div class="example-item" data-example="derivative of x^3 + 2x">
                    <strong>Find derivative: x³ + 2x</strong>
                    <p>Calculus problem</p>
                </div>
                <div class="example-item" data-example="integral of 2x dx">
                    <strong>Find integral: ∫2x dx</strong>
                    <p>Integration problem</p>
                </div>
                <div class="example-item" data-example="area of circle with radius 5">
                    <strong>Area of circle (r=5)</strong>
                    <p>Geometry problem</p>
                </div>
                <div class="example-item" data-example="factor x^2 - 9">
                    <strong>Factor: x² - 9</strong>
                    <p>Polynomial factoring</p>
                </div>
            </div>
        </div>
        
        <!-- Bottom Ad Unit - First Ad Slot Again -->
        <div class="ad-container">
            <div class="ad-label">Advertisement</div>
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-2025523835935359"
                 data-ad-slot="2310346797"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                 (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
            <div class="ad-placeholder" id="ad-fallback-3">
                Loading advertisement...
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const mathInput = document.getElementById('mathInput');
            const solveBtn = document.getElementById('solveBtn');
            const solutionContainer = document.getElementById('solutionContainer');
            const solutionContent = document.getElementById('solutionContent');
            const loadingIndicator = document.getElementById('loadingIndicator');
            const errorMessage = document.getElementById('errorMessage');
            const exampleItems = document.querySelectorAll('.example-item');
            const mathTabs = document.querySelectorAll('.math-tab');
            
            // Handle tab switching
            mathTabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    mathTabs.forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    updatePlaceholder(this.dataset.tab);
                });
            });
            
            function updatePlaceholder(tab) {
                switch(tab) {
                    case 'solve':
                        mathInput.placeholder = "Enter your math problem (e.g., 2x+5=15, x^2-4=0)...";
                        break;
                    case 'graph':
                        mathInput.placeholder = "Enter function to graph (e.g., y=x^2, sin(x))...";
                        break;
                    case 'simplify':
                        mathInput.placeholder = "Enter expression to simplify (e.g., (x+2)(x-3), 2x+3x)...";
                        break;
                }
            }
            
            // Handle example clicks
            exampleItems.forEach(item => {
                item.addEventListener('click', function() {
                    mathInput.value = this.dataset.example;
                    solveProblem();
                });
            });
            
            // Handle solve button click
            solveBtn.addEventListener('click', solveProblem);
            
            // Handle Enter key press
            mathInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    solveProblem();
                }
            });
            
            function solveProblem() {
                const problem = mathInput.value.trim();
                
                if (!problem) {
                    showError("Please enter a math problem");
                    return;
                }
                
                // Show loading, hide previous results and errors
                loadingIndicator.style.display = 'block';
                solutionContainer.style.display = 'none';
                errorMessage.style.display = 'none';
                
                // Simulate processing delay (in a real app, this would be an API call)
                setTimeout(() => {
                    try {
                        const solution = generateSolution(problem);
                        displaySolution(solution);
                    } catch (error) {
                        showError(error.message || "Could not solve this problem. Try rephrasing it.");
                    } finally {
                        loadingIndicator.style.display = 'none';
                    }
                }, 1000);
            }
            
            function generateSolution(problem) {
                // This is a simplified solver - a real app would use a math engine or API
                problem = problem.toLowerCase();
                
                // Basic arithmetic
                if (/^\d+[\+\-\*\/]\d+$/.test(problem)) {
                    const result = eval(problem);
                    return {
                        type: 'arithmetic',
                        problem: problem,
                        solution: `${problem} = ${result}`,
                        steps: [`Calculated: ${problem} = ${result}`]
                    };
                }
                
                // Linear equations
                if (problem.includes('x=') || problem.includes('=x') || 
                    (problem.includes('x') && problem.includes('='))) {
                    return solveLinearEquation(problem);
                }
                
                // Quadratic equations
                if (problem.includes('x^2') || problem.includes('x²')) {
                    return solveQuadraticEquation(problem);
                }
                
                // Derivatives
                if (problem.includes('deriv') || problem.includes('d/dx')) {
                    return solveDerivative(problem);
                }
                
                // Integrals
                if (problem.includes('integral') || problem.includes('∫')) {
                    return solveIntegral(problem);
                }
                
                // Area calculations
                if (problem.includes('area')) {
                    return solveAreaProblem(problem);
                }
                
                // Factorization
                if (problem.includes('factor')) {
                    return solveFactorization(problem);
                }
                
                throw new Error("This type of problem isn't supported in this demo. Try a basic algebra, calculus, or arithmetic problem.");
            }
            
            // [All the existing solution generation functions remain the same]
            // ... (keep all the solveLinearEquation, solveQuadraticEquation, etc. functions from previous implementation)
            
            function displaySolution(solution) {
                solutionContent.innerHTML = '';
                
                const solutionType = document.createElement('p');
                solutionType.textContent = `Type: ${solution.type} problem`;
                solutionType.style.color = '#666';
                solutionType.style.fontSize = '0.9em';
                solutionContent.appendChild(solutionType);
                
                const finalAnswer = document.createElement('div');
                finalAnswer.innerHTML = `<strong>Answer:</strong> ${solution.solution}`;
                finalAnswer.style.margin = '15px 0';
                finalAnswer.style.padding = '10px';
                finalAnswer.style.backgroundColor = '#e8f4ff';
                finalAnswer.style.borderRadius = '5px';
                solutionContent.appendChild(finalAnswer);
                
                if (solution.steps && solution.steps.length > 0) {
                    const stepsTitle = document.createElement('div');
                    stepsTitle.innerHTML = '<strong>Steps:</strong>';
                    stepsTitle.style.margin = '10px 0 5px 0';
                    solutionContent.appendChild(stepsTitle);
                    
                    const stepsList = document.createElement('ol');
                    stepsList.className = 'solution-steps';
                    
                    solution.steps.forEach(step => {
                        const stepItem = document.createElement('li');
                        stepItem.textContent = step;
                        stepsList.appendChild(stepItem);
                    });
                    
                    solutionContent.appendChild(stepsList);
                }
                
                solutionContainer.style.display = 'block';
            }
            
            function showError(message) {
                errorMessage.textContent = message;
                errorMessage.style.display = 'block';
            }
            
            // Check if ads loaded successfully
            function checkAdLoad() {
                const adContainers = document.querySelectorAll('.ad-container ins');
                adContainers.forEach((ad, index) => {
                    if (ad.clientHeight === 0) {
                        document.getElementById(`ad-fallback-${index+1}`).innerHTML = `
                            Ad could not load. Possible reasons:<br>
                            1. Testing locally (ads only work on live sites)<br>
                            2. Ad blocker enabled<br>
                            3. Domain not approved yet<br>
                            4. Ad unit not active
                        `;
                    } else {
                        document.getElementById(`ad-fallback-${index+1}`).style.display = 'none';
                    }
                });
            }
            
            // Run check after 3 seconds
            setTimeout(checkAdLoad, 3000);
            
            // Detect ad blockers
            if (typeof adsbygoogle === 'undefined') {
                document.querySelectorAll('.ad-placeholder').forEach(el => {
                    el.innerHTML = 'Please disable your ad blocker to support our service';
                    el.style.background = '#ffebee';
                });
            }
        });
    </script>
</body>
</html>
