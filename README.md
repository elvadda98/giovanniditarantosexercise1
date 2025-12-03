<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Life Words</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #8e44ad 0%, #3498db 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #7d3c98, #8e44ad);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #7d3c98, #8e44ad);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(125, 60, 152, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5eef8, #e8f4f8);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .word-bank h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #8e44ad, #9b59b6);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(142, 68, 173, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(142, 68, 173, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #8e44ad;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .option.selected {
            background: #8e44ad;
            color: white;
            border-color: #8e44ad;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #8e44ad;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #8e44ad;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .match-item.selected {
            background: #e8f4f8;
            border-color: #8e44ad;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #8e44ad, #9b59b6);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142, 68, 173, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #8e44ad, #9b59b6);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #8e44ad;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #8e44ad;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #8e44ad;
            margin-top: 10px;
        }

        .story-box {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            border: 2px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .story-box h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .story-box p {
            line-height: 1.8;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .highlight {
            background-color: #ffeaa7;
            padding: 2px 5px;
            border-radius: 3px;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/6</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Life Words</h1>
            <p>Practice these useful English words in different contexts!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('story')">Read the Story</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #8e44ad;">Vocabulary Words and Meanings</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>honest</h3>
                    <p><strong>Definition:</strong> Truthful, sincere, and free of deceit; not lying, cheating, or stealing.</p>
                    <p><strong>Usage:</strong> Describes someone who tells the truth or something that is fair and genuine.</p>
                    <p class="example"><strong>Example:</strong> "She was honest about her mistake and apologized immediately."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>here</h3>
                    <p><strong>Definition:</strong> In, at, or to this place or position.</p>
                    <p><strong>Usage:</strong> Indicates location near the speaker; opposite of "there."</p>
                    <p class="example"><strong>Example:</strong> "Please come here and look at this beautiful view."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>rush hour</h3>
                    <p><strong>Definition:</strong> The times at the beginning and end of the working day when many people are traveling to or from work.</p>
                    <p><strong>Usage:</strong> Typically refers to heavy traffic periods, usually 7-9 AM and 5-7 PM.</p>
                    <p class="example"><strong>Example:</strong> "I avoid driving during rush hour because the traffic is terrible."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>owner</h3>
                    <p><strong>Definition:</strong> A person who owns something; a proprietor.</p>
                    <p><strong>Usage:</strong> Can refer to business owners, property owners, or pet owners.</p>
                    <p class="example"><strong>Example:</strong> "The shop owner opens his store every day at 8 AM."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>countryside</h3>
                    <p><strong>Definition:</strong> Land that is away from towns and cities, with fields, forests, and farms.</p>
                    <p><strong>Usage:</strong> The rural areas outside urban centers; often associated with nature and agriculture.</p>
                    <p class="example"><strong>Example:</strong> "We love walking in the countryside on weekends to enjoy the fresh air."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>belly</h3>
                    <p><strong>Definition:</strong> The front part of the human body below the chest; stomach or abdomen.</p>
                    <p><strong>Usage:</strong> Informal word for stomach or abdomen; also used for animals.</p>
                    <p class="example"><strong>Example:</strong> "After the big meal, my belly felt very full."</p>
                </div>
            </div>
        </div>

        <!-- Story Section -->
        <div id="story" class="game-section">
            <div class="story-box">
                <h3><i class="fas fa-book-open icon"></i> A Day in the City and Country</h3>
                <p>Mark was an <span class="highlight">honest</span> man who owned a small bakery in the city. As the <span class="highlight">owner</span>, he worked hard every day, waking up early to avoid the morning <span class="highlight">rush hour</span>. The streets would be packed with cars if he left any later.</p>
                
                <p>"Come over <span class="highlight">here</span>!" he would call to his customers as they entered the shop. His friendly voice and fresh pastries made his bakery popular in the neighborhood.</p>
                
                <p>After a long day at work, Mark loved to escape to the peaceful <span class="highlight">countryside</span>. He would drive out of the city, leaving the noise and traffic behind. In the quiet fields, he could relax and clear his mind.</p>
                
                <p>One evening, after enjoying a large homemade dinner at a countryside inn, he rubbed his full <span class="highlight">belly</span> contentedly. "Nothing beats honest work followed by honest food in beautiful surroundings," he thought to himself.</p>
                
                <p>Whether in the busy city during rush hour or the quiet countryside, Mark found happiness in simple, honest living.</p>
            </div>
            
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Vocabulary Words from the Story</h3>
                <div class="word-options">
                    <span class="word-option">honest</span>
                    <span class="word-option">here</span>
                    <span class="word-option">rush hour</span>
                    <span class="word-option">owner</span>
                    <span class="word-option">countryside</span>
                    <span class="word-option">belly</span>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">honest</span>
                    <span class="word-option">here</span>
                    <span class="word-option">rush hour</span>
                    <span class="word-option">owner</span>
                    <span class="word-option">countryside</span>
                    <span class="word-option">belly</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #8e44ad;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="honest" onclick="selectMatch(this)">honest</div>
                    <div class="match-item" data-word="here" onclick="selectMatch(this)">here</div>
                    <div class="match-item" data-word="rush hour" onclick="selectMatch(this)">rush hour</div>
                    <div class="match-item" data-word="owner" onclick="selectMatch(this)">owner</div>
                    <div class="match-item" data-word="countryside" onclick="selectMatch(this)">countryside</div>
                    <div class="match-item" data-word="belly" onclick="selectMatch(this)">belly</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "honest", text: "Truthful, sincere, and free of deceit" },
            { meaning: "here", text: "In, at, or to this place or position" },
            { meaning: "rush hour", text: "Time when many people travel to/from work" },
            { meaning: "owner", text: "A person who owns something" },
            { meaning: "countryside", text: "Land away from towns and cities" },
            { meaning: "belly", text: "The front part of the body below the chest" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "She was <input type='text' class='fill-blank' data-answer='honest' placeholder='answer'> about her mistake and apologized immediately.", answer: "honest" },
            { text: "Please come <input type='text' class='fill-blank' data-answer='here' placeholder='answer'> and look at this beautiful view.", answer: "here" },
            { text: "I avoid driving during <input type='text' class='fill-blank' data-answer='rush hour' placeholder='answer'> because the traffic is terrible.", answer: "rush hour" },
            { text: "The shop <input type='text' class='fill-blank' data-answer='owner' placeholder='answer'> opens his store every day at 8 AM.", answer: "owner" },
            { text: "We love walking in the <input type='text' class='fill-blank' data-answer='countryside' placeholder='answer'> on weekends to enjoy the fresh air.", answer: "countryside" },
            { text: "After the big meal, my <input type='text' class='fill-blank' data-answer='belly' placeholder='answer'> felt very full.", answer: "belly" },
            { text: "An <input type='text' class='fill-blank' data-answer='honest' placeholder='answer'> opinion is always appreciated, even if it's critical.", answer: "honest" },
            { text: "Is everyone <input type='text' class='fill-blank' data-answer='here' placeholder='answer'>? We can start the meeting now.", answer: "here" },
            { text: "The subway is most crowded during the evening <input type='text' class='fill-blank' data-answer='rush hour' placeholder='answer'>.", answer: "rush hour" },
            { text: "The restaurant <input type='text' class='fill-blank' data-answer='owner' placeholder='answer'> personally checks on every table.", answer: "owner" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences and take only 6
            const shuffledSentences = shuffleArray([...sentences]).slice(0, 6);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Fill in the blank ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score from all sections
            score = fillBlanksCorrect + matchingCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
