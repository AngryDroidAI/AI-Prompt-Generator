<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Prompt Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4361ee;
            --primary-dark: #3a56d4;
            --secondary: #7209b7;
            --accent: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --light-gray: #e9ecef;
            --success: #4cc9f0;
            --border-radius: 12px;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7ff;
            color: var(--dark);
            line-height: 1.6;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 30px;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            margin-bottom: 10px;
        }
        
        h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        h1 i {
            color: var(--success);
        }
        
        .tagline {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 800px;
            margin: 0 auto;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        @media (max-width: 900px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .card {
            background: white;
            border-radius: var(--border-radius);
            padding: 30px;
            box-shadow: var(--shadow);
            transition: var(--transition);
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }
        
        .card-title {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 20px;
            color: var(--primary);
            font-size: 1.5rem;
        }
        
        .card-title i {
            color: var(--accent);
        }
        
        .input-section textarea {
            width: 100%;
            min-height: 200px;
            padding: 20px;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            font-size: 1.1rem;
            resize: vertical;
            transition: var(--transition);
            margin-bottom: 20px;
        }
        
        .input-section textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        .generation-controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .control-group {
            flex: 1;
            min-width: 200px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        select, .slider-container {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            font-size: 1rem;
            background-color: white;
            transition: var(--transition);
        }
        
        select:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .slider-container {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 12px 15px;
        }
        
        .slider-value {
            font-weight: 600;
            color: var(--primary);
            min-width: 40px;
        }
        
        input[type="range"] {
            flex: 1;
            height: 8px;
            -webkit-appearance: none;
            background: var(--light-gray);
            border-radius: 4px;
            outline: none;
        }
        
        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 22px;
            height: 22px;
            background: var(--primary);
            border-radius: 50%;
            cursor: pointer;
            transition: var(--transition);
        }
        
        input[type="range"]::-webkit-slider-thumb:hover {
            background: var(--primary-dark);
            transform: scale(1.1);
        }
        
        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .checkbox-item input {
            width: 18px;
            height: 18px;
            accent-color: var(--primary);
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
        }
        
        button {
            padding: 15px 30px;
            border: none;
            border-radius: var(--border-radius);
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
            flex: 2;
        }
        
        .btn-primary:hover {
            background-color: var(--primary-dark);
        }
        
        .btn-secondary {
            background-color: var(--light-gray);
            color: var(--dark);
            flex: 1;
        }
        
        .btn-secondary:hover {
            background-color: #d8d9da;
        }
        
        .result-section textarea {
            width: 100%;
            min-height: 300px;
            padding: 20px;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            font-size: 1.1rem;
            resize: vertical;
            transition: var(--transition);
            background-color: #fafbff;
            margin-bottom: 20px;
        }
        
        .result-section textarea:focus {
            outline: none;
            border-color: var(--success);
        }
        
        .result-actions {
            display: flex;
            justify-content: space-between;
            gap: 15px;
        }
        
        .btn-success {
            background-color: var(--success);
            color: var(--dark);
        }
        
        .btn-success:hover {
            background-color: #3ab4d6;
        }
        
        .btn-accent {
            background-color: var(--accent);
            color: white;
        }
        
        .btn-accent:hover {
            background-color: #e11571;
        }
        
        .process-steps {
            display: flex;
            justify-content: space-between;
            margin-top: 40px;
            flex-wrap: wrap;
            gap: 20px;
        }
        
        .step {
            flex: 1;
            min-width: 220px;
            background: white;
            border-radius: var(--border-radius);
            padding: 25px;
            box-shadow: var(--shadow);
            text-align: center;
            border-top: 5px solid var(--primary);
        }
        
        .step:nth-child(2) {
            border-top-color: var(--secondary);
        }
        
        .step:nth-child(3) {
            border-top-color: var(--accent);
        }
        
        .step:nth-child(4) {
            border-top-color: var(--success);
        }
        
        .step-number {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            background-color: var(--primary);
            color: white;
            border-radius: 50%;
            font-weight: 700;
            margin-bottom: 15px;
        }
        
        .step:nth-child(2) .step-number {
            background-color: var(--secondary);
        }
        
        .step:nth-child(3) .step-number {
            background-color: var(--accent);
        }
        
        .step:nth-child(4) .step-number {
            background-color: var(--success);
        }
        
        .step h3 {
            margin-bottom: 10px;
            color: var(--dark);
        }
        
        .step p {
            color: var(--gray);
            font-size: 0.95rem;
        }
        
        .guidelines {
            margin-top: 40px;
            background: white;
            border-radius: var(--border-radius);
            padding: 30px;
            box-shadow: var(--shadow);
        }
        
        .guidelines h2 {
            color: var(--primary);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .guidelines-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .guideline-item {
            background: var(--light);
            padding: 20px;
            border-radius: var(--border-radius);
            border-left: 4px solid var(--primary);
        }
        
        .guideline-item h4 {
            color: var(--primary);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        footer {
            text-align: center;
            padding: 30px 0;
            color: var(--gray);
            margin-top: 40px;
            border-top: 1px solid var(--light-gray);
        }
        
        .notification {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--success);
            color: var(--dark);
            padding: 15px 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            display: flex;
            align-items: center;
            gap: 10px;
            transform: translateY(100px);
            opacity: 0;
            transition: transform 0.5s ease, opacity 0.5s ease;
            z-index: 1000;
        }
        
        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }
        
        .character-count {
            text-align: right;
            margin-top: 5px;
            color: var(--gray);
            font-size: 0.9rem;
        }
        
        .character-count.warning {
            color: var(--accent);
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-robot"></i> AI Prompt Generator</h1>
            <p class="tagline">Craft high-quality, effective prompts for AI models without any API or backend. Generate robust prompts that yield better responses.</p>
        </header>
        
        <div class="main-content">
            <div class="input-section card">
                <h2 class="card-title"><i class="fas fa-keyboard"></i> Input Your Idea</h2>
                <textarea id="userInput" placeholder="Describe your idea, problem statement, or topic here... For example: 'Create a story about environmental conservation in a small town' or 'Explain quantum computing to a beginner'">Create a story about environmental conservation in a small town</textarea>
                <div class="character-count">Characters: <span id="inputCount">0</span></div>
                
                <div class="generation-controls">
                    <div class="control-group">
                        <label for="promptType"><i class="fas fa-list-alt"></i> Prompt Type</label>
                        <select id="promptType">
                            <option value="creative">Creative Writing</option>
                            <option value="technical">Technical Explanation</option>
                            <option value="analytical">Analytical/Research</option>
                            <option value="conversational">Conversational/Dialogue</option>
                            <option value="instructional">Instructional/How-to</option>
                        </select>
                    </div>
                    
                    <div class="control-group">
                        <label for="detailLevel"><i class="fas fa-sliders-h"></i> Detail Level</label>
                        <div class="slider-container">
                            <input type="range" id="detailLevel" min="1" max="5" value="3">
                            <span class="slider-value" id="detailValue">3</span>
                        </div>
                    </div>
                </div>
                
                <div class="checkbox-group">
                    <div class="checkbox-item">
                        <input type="checkbox" id="includeContext" checked>
                        <label for="includeContext">Include Context/Setting</label>
                    </div>
                    <div class="checkbox-item">
                        <input type="checkbox" id="includeConstraints" checked>
                        <label for="includeConstraints">Include Constraints</label>
                    </div>
                    <div class="checkbox-item">
                        <input type="checkbox" id="includeTone" checked>
                        <label for="includeTone">Specify Tone</label>
                    </div>
                    <div class="checkbox-item">
                        <input type="checkbox" id="includeExamples" checked>
                        <label for="includeExamples">Include Examples</label>
                    </div>
                </div>
                
                <div class="button-group">
                    <button class="btn-primary" id="generateBtn">
                        <i class="fas fa-magic"></i> Generate Prompt
                    </button>
                    <button class="btn-secondary" id="clearBtn">
                        <i class="fas fa-trash-alt"></i> Clear
                    </button>
                </div>
            </div>
            
            <div class="result-section card">
                <h2 class="card-title"><i class="fas fa-file-alt"></i> Generated Prompt</h2>
                <textarea id="generatedPrompt" placeholder="Your generated prompt will appear here..." readonly></textarea>
                <div class="character-count">Characters: <span id="outputCount">0</span></div>
                
                <div class="result-actions">
                    <button class="btn-success" id="copyBtn">
                        <i class="far fa-copy"></i> Copy Prompt
                    </button>
                    <button class="btn-accent" id="refineBtn">
                        <i class="fas fa-sync-alt"></i> Refine Further
                    </button>
                </div>
            </div>
        </div>
        
        <div class="process-steps">
            <div class="step">
                <div class="step-number">1</div>
                <h3>Input</h3>
                <p>Provide your general idea, problem statement, or topic that you want to explore with AI.</p>
            </div>
            <div class="step">
                <div class="step-number">2</div>
                <h3>Analysis</h3>
                <p>The generator identifies core elements, themes, and potential challenges in your input.</p>
            </div>
            <div class="step">
                <div class="step-number">3</div>
                <h3>Drafting</h3>
                <p>Multiple prompt variations are created with focused questions and specific instructions.</p>
            </div>
            <div class="step">
                <div class="step-number">4</div>
                <h3>Review & Refine</h3>
                <p>You can refine the generated prompts based on your needs for clarity and precision.</p>
            </div>
        </div>
        
        <div class="guidelines">
            <h2><i class="fas fa-lightbulb"></i> Prompt Crafting Guidelines</h2>
            <div class="guidelines-grid">
                <div class="guideline-item">
                    <h4><i class="fas fa-bullseye"></i> Clarity</h4>
                    <p>Clearly outline your goals and what you expect from the AI response.</p>
                </div>
                <div class="guideline-item">
                    <h4><i class="fas fa-cogs"></i> Functionality</h4>
                    <p>Aim to solve specific problems or achieve particular outcomes with your prompt.</p>
                </div>
                <div class="guideline-item">
                    <h4><i class="fas fa-ruler"></i> Precision</h4>
                    <p>Avoid ambiguity and focus on measurable results and specific details.</p>
                </div>
                <div class="guideline-item">
                    <h4><i class="fas fa-balance-scale"></i> Balanced Themes</h4>
                    <p>Include both physical/technical aspects and emotional/human elements.</p>
                </div>
                <div class="guideline-item">
                    <h4><i class="fas fa-heart"></i> Ethical Considerations</h4>
                    <p>Use open-ended prompts that encourage ethical reasoning without assumptions.</p>
                </div>
                <div class="guideline-item">
                    <h4><i class="fas fa-comments"></i> Tone & Sensitivity</h4>
                    <p>Maintain an appropriate tone and be mindful of sensitive topics.</p>
                </div>
            </div>
        </div>
        
        <footer>
            <p>AI Prompt Generator | Works entirely in your browser - no API calls, no backend required</p>
            <p>Use this tool to create effective prompts for AI models like ChatGPT, Claude, Gemini, and others</p>
        </footer>
        
        <div class="notification" id="notification">
            <i class="fas fa-check-circle"></i>
            <span id="notificationText">Prompt copied to clipboard!</span>
        </div>
    </div>

    <script>
        // DOM Elements
        const userInput = document.getElementById('userInput');
        const generatedPrompt = document.getElementById('generatedPrompt');
        const generateBtn = document.getElementById('generateBtn');
        const clearBtn = document.getElementById('clearBtn');
        const copyBtn = document.getElementById('copyBtn');
        const refineBtn = document.getElementById('refineBtn');
        const promptType = document.getElementById('promptType');
        const detailLevel = document.getElementById('detailLevel');
        const detailValue = document.getElementById('detailValue');
        const includeContext = document.getElementById('includeContext');
        const includeConstraints = document.getElementById('includeConstraints');
        const includeTone = document.getElementById('includeTone');
        const includeExamples = document.getElementById('includeExamples');
        const inputCount = document.getElementById('inputCount');
        const outputCount = document.getElementById('outputCount');
        const notification = document.getElementById('notification');
        const notificationText = document.getElementById('notificationText');
        
        // Initialize character counts
        inputCount.textContent = userInput.value.length;
        outputCount.textContent = generatedPrompt.value.length;
        
        // Update detail value when slider changes
        detailLevel.addEventListener('input', function() {
            detailValue.textContent = this.value;
        });
        
        // Update character count for input
        userInput.addEventListener('input', function() {
            inputCount.textContent = this.value.length;
        });
        
        // Update character count for output
        generatedPrompt.addEventListener('input', function() {
            outputCount.textContent = this.value.length;
        });
        
        // Clear button functionality
        clearBtn.addEventListener('click', function() {
            userInput.value = '';
            generatedPrompt.value = '';
            inputCount.textContent = '0';
            outputCount.textContent = '0';
            showNotification('Cleared all inputs and results');
        });
        
        // Copy button functionality
        copyBtn.addEventListener('click', function() {
            if (generatedPrompt.value.trim() === '') {
                showNotification('No prompt to copy! Generate one first.', 'error');
                return;
            }
            
            generatedPrompt.select();
            generatedPrompt.setSelectionRange(0, 99999); // For mobile devices
            
            try {
                navigator.clipboard.writeText(generatedPrompt.value);
                showNotification('Prompt copied to clipboard!');
            } catch (err) {
                // Fallback for older browsers
                document.execCommand('copy');
                showNotification('Prompt copied to clipboard!');
            }
        });
        
        // Refine button functionality
        refineBtn.addEventListener('click', function() {
            if (generatedPrompt.value.trim() === '') {
                showNotification('No prompt to refine! Generate one first.', 'error');
                return;
            }
            
            // Use the current generated prompt as the new input
            userInput.value = generatedPrompt.value;
            inputCount.textContent = userInput.value.length;
            
            // Generate a refined version
            generatePrompt();
            showNotification('Refining prompt...');
        });
        
        // Generate prompt button functionality
        generateBtn.addEventListener('click', generatePrompt);
        
        // Main prompt generation function
        function generatePrompt() {
            const inputText = userInput.value.trim();
            
            if (inputText === '') {
                showNotification('Please enter your idea or problem statement first!', 'error');
                return;
            }
            
            // Get all user settings
            const type = promptType.value;
            const detail = parseInt(detailLevel.value);
            const context = includeContext.checked;
            const constraints = includeConstraints.checked;
            const tone = includeTone.checked;
            const examples = includeExamples.checked;
            
            // Analyze the input to identify themes and elements
            const analysis = analyzeInput(inputText, type);
            
            // Generate the prompt based on analysis and settings
            const prompt = createPrompt(analysis, {
                type,
                detail,
                context,
                constraints,
                tone,
                examples
            });
            
            // Display the generated prompt
            generatedPrompt.value = prompt;
            outputCount.textContent = prompt.length;
            
            showNotification('Prompt generated successfully!');
        }
        
        // Analyze the user input to identify themes and elements
        function analyzeInput(input, type) {
            const analysis = {
                themes: [],
                keywords: [],
                potentialChallenges: [],
                context: '',
                goal: ''
            };
            
            // Extract keywords (simple approach - in a real app, this would be more sophisticated)
            const words = input.toLowerCase().split(/\s+/);
            const stopWords = ['the', 'a', 'an', 'and', 'or', 'but', 'in', 'on', 'at', 'to', 'for', 'of', 'with', 'by', 'about'];
            const filteredWords = words.filter(word => 
                word.length > 3 && !stopWords.includes(word)
            );
            
            analysis.keywords = [...new Set(filteredWords)].slice(0, 10);
            
            // Identify themes based on keywords and prompt type
            const themeKeywords = {
                environmental: ['environment', 'conservation', 'nature', 'sustainable', 'climate', 'eco', 'green', 'earth', 'planet'],
                social: ['social', 'community', 'society', 'people', 'human', 'relationship', 'family', 'friends', 'culture'],
                technical: ['technology', 'software', 'code', 'algorithm', 'data', 'system', 'computer', 'digital', 'app', 'program'],
                creative: ['story', 'creative', 'narrative', 'plot', 'character', 'scene', 'setting', 'imagine', 'fiction'],
                educational: ['explain', 'teach', 'learn', 'understand', 'concept', 'principle', 'theory', 'educate', 'student']
            };
            
            for (const [theme, keywords] of Object.entries(themeKeywords)) {
                if (keywords.some(keyword => input.toLowerCase().includes(keyword))) {
                    analysis.themes.push(theme);
                }
            }
            
            // If no themes detected, add default based on type
            if (analysis.themes.length === 0) {
                if (type === 'technical') analysis.themes.push('technical');
                else if (type === 'creative') analysis.themes.push('creative');
                else analysis.themes.push('general');
            }
            
            // Identify potential challenges based on input
            if (input.includes('?')) {
                analysis.potentialChallenges.push('Answering specific questions');
            }
            
            if (input.length < 20) {
                analysis.potentialChallenges.push('Lack of specific details');
            }
            
            if (analysis.keywords.length < 3) {
                analysis.potentialChallenges.push('Broad/vague topic');
            }
            
            // Determine context and goal
            if (input.includes('story') || input.includes('narrative') || input.includes('tale')) {
                analysis.context = 'Creative writing/narrative';
                analysis.goal = 'Create an engaging story';
            } else if (input.includes('explain') || input.includes('how') || input.includes('teach')) {
                analysis.context = 'Educational/instructional';
                analysis.goal = 'Explain a concept clearly';
            } else if (input.includes('analyze') || input.includes('research') || input.includes('compare')) {
                analysis.context = 'Analytical/research';
                analysis.goal = 'Provide in-depth analysis';
            } else if (input.includes('create') || input.includes('generate') || input.includes('design')) {
                analysis.context = 'Creative/generative';
                analysis.goal = 'Generate new content';
            } else {
                analysis.context = 'General inquiry';
                analysis.goal = 'Address the topic comprehensively';
            }
            
            return analysis;
        }
        
        // Create the prompt based on analysis and settings
        function createPrompt(analysis, settings) {
            const { type, detail, context, constraints, tone, examples } = settings;
            
            // Prompt templates based on type
            const templates = {
                creative: `As a creative writing assistant, craft a ${detail > 3 ? 'detailed' : 'concise'} narrative based on the following idea.`,
                technical: `As a technical expert, provide a ${detail > 3 ? 'comprehensive' : 'clear and concise'} explanation of the following topic.`,
                analytical: `As an analytical researcher, examine the following topic with ${detail > 3 ? 'thorough' : 'focused'} analysis.`,
                conversational: `As a conversational partner, engage in a ${detail > 3 ? 'detailed' : 'natural'} dialogue about the following topic.`,
                instructional: `As an instructional guide, provide ${detail > 3 ? 'step-by-step' : 'clear'} instructions for the following task.`
            };
            
            let prompt = templates[type] || templates.creative;
            
            // Add context if requested
            if (context) {
                prompt += `\n\nCONTEXT: ${analysis.context}. ${analysis.goal}.`;
                
                if (analysis.themes.length > 0) {
                    prompt += ` Key themes include: ${analysis.themes.join(', ')}.`;
                }
            }
            
            // Add the user's input
            prompt += `\n\nUSER INPUT: "${userInput.value.trim()}"`;
            
            // Add constraints if requested
            if (constraints) {
                prompt += `\n\nCONSTRAINTS:`;
                
                if (detail <= 2) {
                    prompt += ` Keep the response concise (under 300 words).`;
                } else if (detail >= 4) {
                    prompt += ` Provide a comprehensive response (500+ words).`;
                } else {
                    prompt += ` Provide a balanced response (300-500 words).`;
                }
                
                if (analysis.potentialChallenges.length > 0) {
                    prompt += ` Address these aspects: ${analysis.potentialChallenges.join(', ')}.`;
                }
                
                // Add constraints based on type
                if (type === 'creative') {
                    prompt += ` Include vivid descriptions, character development, and a compelling narrative arc.`;
                } else if (type === 'technical') {
                    prompt += ` Use accurate terminology but explain complex concepts accessibly.`;
                } else if (type === 'analytical') {
                    prompt += ` Present balanced perspectives with evidence-based reasoning.`;
                }
            }
            
            // Add tone if requested
            if (tone) {
                prompt += `\n\nTONE: `;
                
                if (type === 'creative') {
                    prompt += `Engaging, vivid, and immersive.`;
                } else if (type === 'technical') {
                    prompt += `Professional, precise, and clear.`;
                } else if (type === 'analytical') {
                    prompt += `Objective, balanced, and evidence-based.`;
                } else if (type === 'conversational') {
                    prompt += `Friendly, natural, and engaging.`;
                } else {
                    prompt += `Helpful, clear, and informative.`;
                }
                
                // Add ethical considerations
                prompt += ` Avoid bias, stereotypes, and speculative assumptions. Focus on factual accuracy and ethical considerations.`;
            }
            
            // Add examples if requested
            if (examples && detail >= 3) {
                prompt += `\n\nEXAMPLES: Include relevant examples, analogies, or case studies to illustrate key points.`;
                
                if (type === 'creative' && detail >= 4) {
                    prompt += ` Provide sample dialogue or descriptive passages when appropriate.`;
                }
            }
            
            // Add final instructions
            prompt += `\n\nSTRUCTURE: Organize the response logically with clear sections or narrative flow.`;
            prompt += `\n\nRESPONSE: Provide a well-structured, comprehensive response that addresses all aspects of the input.`;
            
            // Add focus on effectiveness
            prompt += ` Ensure the response is actionable, detailed, and contextually relevant.`;
            
            return prompt;
        }
        
        // Show notification
        function showNotification(message, type = 'success') {
            notificationText.textContent = message;
            
            if (type === 'error') {
                notification.style.background = 'var(--accent)';
            } else {
                notification.style.background = 'var(--success)';
            }
            
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // Generate a prompt on page load with the example text
        window.addEventListener('DOMContentLoaded', function() {
            // Auto-generate a prompt with the example text after a short delay
            setTimeout(() => {
                if (userInput.value.trim() !== '') {
                    generatePrompt();
                }
            }, 500);
        });
        
        // Add some sample prompts for inspiration on click
        userInput.addEventListener('click', function() {
            if (this.value === 'Create a story about environmental conservation in a small town') {
                // Show some examples in a tooltip-like way
                showNotification('Try other ideas like: "Explain quantum computing to a beginner" or "Analyze the social impact of remote work"');
            }
        });
    </script>
</body>
</html>
