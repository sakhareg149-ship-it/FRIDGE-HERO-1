# FRIDGE-HERO-1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fridge Hero - AI Recipe Generator</title>
  <!-- Google Fonts for premium typography -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;800&family=Playfair+Display:ital,wght@0,700;1,400&display=swap" rel="stylesheet">
  
  <style>
    :root {
      /* Warm food-inspired colors */
      --color-primary: #D32F2F;      /* Rich Red */
      --color-secondary: #E64A19;    /* Brick Red / Dark Orange */
      --color-accent: #1976D2;       /* Warm Blue accent */
      --color-bg: #FAF6F0;           /* Soft Cream/Oatmeal background */
      --color-card-bg: #FFFFFF;
      --color-text-dark: #2B2D42;    /* Dark Charcoal for text */
      --color-text-light: #6C757D;
      --font-sans: 'Outfit', sans-serif;
      --font-serif: 'Playfair Display', serif;
      --shadow-sm: 0 4px 6px -1px rgba(0, 0, 0, 0.05), 0 2px 4px -1px rgba(0, 0, 0, 0.03);
      --shadow-md: 0 10px 15px -3px rgba(211, 47, 47, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.02);
      --shadow-lg: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
      --border-radius: 20px;
      --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      font-family: var(--font-sans);
      background-color: var(--color-bg);
      color: var(--color-text-dark);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      line-height: 1.5;
      background-image: 
        radial-gradient(var(--color-primary) 0.5px, transparent 0.5px), 
        radial-gradient(var(--color-secondary) 0.5px, var(--color-bg) 0.5px);
      background-size: 20px 20px;
      background-position: 0 0, 10px 10px;
      opacity: 0.98;
    }
    /* Container Card */
    .app-card {
      background: var(--color-card-bg);
      width: 100%;
      max-width: 600px;
      border-radius: var(--border-radius);
      box-shadow: var(--shadow-lg);
      padding: 40px;
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(211, 47, 47, 0.08);
      transition: var(--transition);
    }
    /* Decorative Top Bar */
    .app-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 8px;
      background: linear-gradient(90deg, var(--color-primary), var(--color-secondary), var(--color-accent));
    }
    /* Header styling */
    header {
      text-align: center;
      margin-bottom: 35px;
    }
    .logo-container {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 64px;
      height: 64px;
      background: rgba(211, 47, 47, 0.1);
      border-radius: 50%;
      margin-bottom: 15px;
      color: var(--color-primary);
      font-size: 28px;
    }
    h1 {
      font-family: var(--font-serif);
      font-size: 2.5rem;
      font-weight: 700;
      color: var(--color-primary);
      margin-bottom: 8px;
      letter-spacing: -0.5px;
    }
    .subtitle {
      color: var(--color-text-light);
      font-size: 0.95rem;
    }
    /* Form control styling */
    .form-group {
      margin-bottom: 24px;
      position: relative;
    }
    label {
      display: block;
      font-weight: 600;
      font-size: 0.85rem;
      text-transform: uppercase;
      letter-spacing: 1px;
      color: var(--color-text-dark);
      margin-bottom: 8px;
      transition: var(--transition);
    }
    .input-wrapper {
      position: relative;
      display: flex;
      align-items: center;
    }
    .input-icon {
      position: absolute;
      left: 16px;
      color: var(--color-text-light);
      font-size: 1.1rem;
      pointer-events: none;
      transition: var(--transition);
    }
    input[type="text"] {
      width: 100%;
      padding: 16px 16px 16px 48px;
      font-family: var(--font-sans);
      font-size: 1rem;
      background: #FDFBF7;
      border: 2px solid #EAE2D5;
      border-radius: 12px;
      outline: none;
      transition: var(--transition);
      color: var(--color-text-dark);
    }
    input[type="text"]:focus {
      border-color: var(--color-primary);
      background: #FFFFFF;
      box-shadow: 0 0 0 4px rgba(211, 47, 47, 0.1);
    }
    input[type="text"]:focus + .input-icon,
    input[type="text"]:not(:placeholder-shown) + .input-icon {
      color: var(--color-primary);
    }
    /* Optional API Key configuration in UI */
    .api-key-config {
      margin-bottom: 24px;
      background: #F5F7FA;
      border: 1px dashed #D0D7DE;
      padding: 12px 16px;
      border-radius: 12px;
    }
    
    .api-key-config label {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }
    .api-key-config input {
      width: 100%;
      padding: 8px 12px;
      font-size: 0.85rem;
      border: 1px solid #CCD2D9;
      border-radius: 6px;
    }
    /* Submit Button styling */
    .btn-submit {
      width: 100%;
      padding: 18px;
      background: linear-gradient(135deg, var(--color-primary), var(--color-secondary));
      color: white;
      border: none;
      border-radius: 12px;
      font-family: var(--font-sans);
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(211, 47, 47, 0.3);
      transition: var(--transition);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }
    .btn-submit:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(211, 47, 47, 0.4);
    }
    .btn-submit:active {
      transform: translateY(1px);
    }
    .btn-submit:disabled {
      background: #CCCCCC;
      box-shadow: none;
      cursor: not-allowed;
      transform: none;
    }
    /* Spinner Animation */
    .spinner {
      width: 20px;
      height: 20px;
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      border-top-color: white;
      animation: spin 1s ease-in-out infinite;
      display: none;
    }
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
    /* Recipe Output Card styling */
    .recipe-card {
      display: none; /* Hidden by default */
      margin-top: 35px;
      padding-top: 30px;
      border-top: 2px dashed #EAE2D5;
      animation: fadeIn 0.5s ease-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .dish-title-wrapper {
      text-align: center;
      margin-bottom: 25px;
    }
    .dish-badge {
      display: inline-block;
      padding: 6px 12px;
      background: rgba(25, 118, 210, 0.1);
      color: var(--color-accent);
      border-radius: 20px;
      font-size: 0.75rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 10px;
    }
    .dish-name {
      font-family: var(--font-serif);
      font-size: 2rem;
      font-weight: 700;
      color: var(--color-text-dark);
      line-height: 1.2;
    }
    .steps-list {
      list-style-type: none;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }
    .step-item {
      display: flex;
      gap: 16px;
      background: #FDFBF7;
      padding: 16px;
      border-radius: 12px;
      border-left: 4px solid var(--color-primary);
      transition: var(--transition);
    }
    .step-item:hover {
      transform: translateX(4px);
      box-shadow: var(--shadow-sm);
    }
    .step-number {
      display: flex;
      align-items: center;
      justify-content: center;
      min-width: 32px;
      height: 32px;
      background: var(--color-primary);
      color: white;
      border-radius: 50%;
      font-weight: 700;
      font-size: 0.9rem;
    }
    .step-text {
      font-size: 0.95rem;
      color: var(--color-text-dark);
      padding-top: 4px;
    }
    /* Error Message styling */
    .error-message {
      display: none;
      margin-top: 20px;
      padding: 16px;
      background: #FFEBEE;
      color: #C62828;
      border-left: 4px solid #D32F2F;
      border-radius: 8px;
      font-size: 0.9rem;
      align-items: center;
      gap: 10px;
      animation: fadeIn 0.3s ease-out;
    }
    /* Responsive adjustments */
    @media (max-width: 600px) {
      body {
        padding: 12px;
      }
      .app-card {
        padding: 24px 16px;
      }
      h1 {
        font-size: 2rem;
      }
      .dish-name {
        font-size: 1.6rem;
      }
    }
  </style>
</head>
<body>
  <div class="app-card">
    <header>
      <div class="logo-container">
        🍳
      </div>
      <h1 id="app-title">Fridge Hero</h1>
      <p class="subtitle">Enter 3 ingredients from your fridge to whip up magic</p>
    </header>
    <!-- Optional API Key Input for testing/ease of use -->
    <div class="api-key-config">
      <label for="input-api-key">
        <span>Gemini API Key</span>
        <small style="color: var(--color-text-light)">Saves locally in browser</small>
      </label>
      <input type="password" id="input-api-key" placeholder="AQ.Ab8RN6JrtfjHBCb8d5Y_7JAAqyW3rQ_EN8GFgaOyvy4_2W2ZWQ" />
    </div>
    <form id="recipe-form" onsubmit="generateRecipe(event)">
      <div class="form-group">
        <label for="ingredient-1">Ingredient 1</label>
        <div class="input-wrapper">
          <input type="text" id="ingredient-1" placeholder="e.g., Eggs" required>
          <span class="input-icon">🥚</span>
        </div>
      </div>
      <div class="form-group">
        <label for="ingredient-2">Ingredient 2</label>
        <div class="input-wrapper">
          <input type="text" id="ingredient-2" placeholder="e.g., Bread" required>
          <span class="input-icon">🍞</span>
        </div>
      </div>
      <div class="form-group">
        <label for="ingredient-3">Ingredient 3</label>
        <div class="input-wrapper">
          <input type="text" id="ingredient-3" placeholder="e.g., Peanut Butter" required>
          <span class="input-icon">🥜</span>
        </div>
      </div>
      <button type="submit" id="btn-cook" class="btn-submit">
        <span class="spinner" id="btn-spinner"></span>
        <span id="btn-text">Cook Magic</span>
      </button>
    </form>
    <!-- Error message banner -->
    <div id="error-banner" class="error-message">
      <span>⚠️</span>
      <span id="error-text">An error occurred while generating your recipe. Please check your API key and try again.</span>
    </div>
    <!-- Recipe Output Card -->
    <div id="recipe-output" class="recipe-card">
      <div class="dish-title-wrapper">
        <span class="dish-badge">✨ Chef's Suggestion</span>
        <div id="recipe-dish-name" class="dish-name">Gourmet French Toast Duo</div>
      </div>
      
      <ol class="steps-list">
        <li class="step-item">
          <div class="step-number">1</div>
          <div id="recipe-step-1" class="step-text">Whisk the eggs in a shallow dish, dip the bread slices until fully coated, and fry in a hot pan.</div>
        </li>
        <li class="step-item">
          <div class="step-number">2</div>
          <div id="recipe-step-2" class="step-text">Spread peanut butter generously over the warm toast slices.</div>
        </li>
        <li class="step-item">
          <div class="step-number">3</div>
          <div id="recipe-step-3" class="step-text">Serve stacked high and enjoy your quick magic dish!</div>
        </li>
      </ol>
    </div>
  </div>
  <script>
    // Store API key requirement: const GEMINI_API_KEY = '';
    const GEMINI_API_KEY = '';
    // Load key from localStorage on start if saved previously
    const apiKeyInput = document.getElementById('input-api-key');
    if (localStorage.getItem('FRIDGE_HERO_KEY')) {
      apiKeyInput.value = localStorage.getItem('FRIDGE_HERO_KEY');
    }
    // Save key to localStorage when changed
    apiKeyInput.addEventListener('input', (e) => {
      localStorage.setItem('FRIDGE_HERO_KEY', e.target.value.trim());
    });
    async function generateRecipe(event) {
      event.preventDefault();
      // UI elements
      const btnCook = document.getElementById('btn-cook');
      const btnText = document.getElementById('btn-text');
      const btnSpinner = document.getElementById('btn-spinner');
      const recipeOutput = document.getElementById('recipe-output');
      const errorBanner = document.getElementById('error-banner');
      const errorText = document.getElementById('error-text');
      const ing1 = document.getElementById('ingredient-1').value.trim();
      const ing2 = document.getElementById('ingredient-2').value.trim();
      const ing3 = document.getElementById('ingredient-3').value.trim();
      // Retrieve API key: Code-defined constant first, then UI input
      let apiKey = GEMINI_API_KEY;
      if (!apiKey) {
        apiKey = apiKeyInput.value.trim();
      }
      if (!apiKey) {
        showError("Please enter your Gemini API Key in the input field above, or set const GEMINI_API_KEY in the source code.");
        return;
      }
      // Hide previous outputs and errors
      recipeOutput.style.display = 'none';
      errorBanner.style.display = 'none';
      // Set button to loading state
      btnCook.disabled = true;
      btnSpinner.style.display = 'inline-block';
      btnText.textContent = 'Cooking...';
      try {
        const prompt = `I have these 3 ingredients: ${ing1}, ${ing2}, ${ing3}. Suggest one creative fancy dish name and give me exactly 3 simple cooking steps. Format: Dish name: ... Step 1: ... Step 2: ... Step 3 ...`;
        const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            contents: [{
              parts: [{
                text: prompt
              }]
            }]
          })
        });
        if (!response.ok) {
          const errData = await response.json().catch(() => ({}));
          const errMsg = errData.error?.message || `HTTP error! status: ${response.status}`;
          throw new Error(errMsg);
        }
        const data = await response.json();
        const responseText = data.candidates?.[0]?.content?.parts?.[0]?.text;
        if (!responseText) {
          throw new Error("Received empty response from the AI model.");
        }
        // Parse response content
        parseAndPopulateRecipe(responseText);
      } catch (error) {
        console.error(error);
        showError(error.message || "Failed to fetch response from Gemini API. Please check your network connection and API key.");
      } finally {
        // Re-enable button
        btnCook.disabled = false;
        btnSpinner.style.display = 'none';
        btnText.textContent = 'Cook Magic';
      }
    }
    function parseAndPopulateRecipe(text) {
      // Regex parsing for the expected format:
      // Dish name: ... Step 1: ... Step 2: ... Step 3 ...
      
      const cleanText = text.replace(/\*/g, '').replace(/\n/g, ' ').trim();
      
      // Matchers for Dish Name and Steps
      const dishMatch = cleanText.match(/Dish\s+name:\s*(.*?)(?=Step\s*1:)/i);
      const step1Match = cleanText.match(/Step\s*1:\s*(.*?)(?=Step\s*2:)/i);
      const step2Match = cleanText.match(/Step\s*2:\s*(.*?)(?=Step\s*3:)/i);
      const step3Match = cleanText.match(/Step\s*3:\s*(.*)/i);
      let dishName = '';
      let step1 = '';
      let step2 = '';
      let step3 = '';
      if (dishMatch && step1Match && step2Match && step3Match) {
        dishName = dishMatch[1].trim();
        step1 = step1Match[1].trim();
        step2 = step2Match[1].trim();
        step3 = step3Match[1].trim();
      } else {
        // Fallback robust parser in case response structure is slightly different
        const lines = text.split('\n').map(l => l.replace(/^\s*[\-\*•]\s*/, '').trim()).filter(Boolean);
        
        // Let's look for parts
        dishName = lines.find(l => l.toLowerCase().includes('dish name')) || 'Gourmet Surprise';
        dishName = dishName.replace(/dish name:/i, '').trim();
        step1 = lines.find(l => l.toLowerCase().includes('step 1')) || 'Prepare ingredients.';
        step1 = step1.replace(/step 1:/i, '').trim();
        step2 = lines.find(l => l.toLowerCase().includes('step 2')) || 'Combine and cook the dish.';
        step2 = step2.replace(/step 2:/i, '').trim();
        step3 = lines.find(l => l.toLowerCase().includes('step 3')) || 'Serve hot and enjoy!';
        step3 = step3.replace(/step 3:/i, '').trim();
        
        // If still empty or default, grab first lines
        if (dishName === 'Gourmet Surprise' && lines.length > 0) {
          dishName = lines[0].replace(/dish name:/i, '').trim();
        }
      }
      // Populate DOM elements
      document.getElementById('recipe-dish-name').textContent = dishName;
      document.getElementById('recipe-step-1').textContent = step1;
      document.getElementById('recipe-step-2').textContent = step2;
      document.getElementById('recipe-step-3').textContent = step3;
      // Show output card
      const recipeOutput = document.getElementById('recipe-output');
      recipeOutput.style.display = 'block';
      
      // Smooth scroll to output
      recipeOutput.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }
    function showError(message) {
      const errorBanner = document.getElementById('error-banner');
      const errorText = document.getElementById('error-text');
      errorText.textContent = message;
      errorBanner.style.display = 'flex';
      errorBanner.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }
  </script>
</body>
</html>
