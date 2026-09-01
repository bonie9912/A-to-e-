<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A to Z Alphabet Game</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
        }

        body {
            background-color: #1a1a1a;
            font-family: 'Arial Black', Impact, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: white;
        }

        .pokedex {
            width: 800px;
            height: 640px;
            background-color: #dc0a2d;
            border-radius: 20px;
            box-shadow: 0 15px 0 #8b0000, 0 25px 30px rgba(0,0,0,0.5);
            position: relative;
            padding: 20px;
            border: 4px solid #500000;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .top-bar {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding-bottom: 15px;
            border-bottom: 4px solid #8b0000;
        }

        .lights-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .big-light {
            width: 60px;
            height: 60px;
            background: radial-gradient(circle at 30% 30%, #80d8ff, #0091ea, #004ecb);
            border: 5px solid #ffffff;
            border-radius: 50%;
            box-shadow: 0 0 15px #00e5ff;
            cursor: pointer;
        }

        .small-lights {
            display: flex;
            gap: 10px;
        }

        .light {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            border: 2px solid #000;
        }
        .light.red { background: radial-gradient(circle at 30% 30%, #ff8a80, #ff1744); }
        .light.yellow { background: radial-gradient(circle at 30% 30%, #ffff8d, #ffd600); }
        .light.green { background: radial-gradient(circle at 30% 30%, #b9f6ca, #00e676); }

        .header-info {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .status-badge {
            font-size: 18px;
            color: #ffcc00;
            background-color: #222;
            padding: 8px 14px;
            border-radius: 8px;
            border: 3px solid #333;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.5);
        }

        .screen-container {
            background-color: #b0b0b0;
            border-radius: 15px;
            padding: 20px;
            border: 4px solid #500000;
            box-shadow: inset 3px 3px 10px rgba(0,0,0,0.4);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .main-screen {
            width: 100%;
            height: 290px;
            background: radial-gradient(circle, #0066cc 0%, #002266 100%);
            border-radius: 10px;
            border: 4px solid #333;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            gap: 15px;
        }

        .audio-btn {
            background: #ffcc00;
            border: 4px solid #333;
            border-radius: 50%;
            width: 75px;
            height: 75px;
            font-size: 32px;
            cursor: pointer;
            box-shadow: 0 6px 0 #b38f00;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.1s ease;
        }

        .audio-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #b38f00;
        }

        .target-display {
            font-size: 72px;
            color: #ffffff;
            text-shadow: 4px 4px 0 #000;
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            width: 90%;
        }

        .option-card {
            background: #ffffff;
            color: #222;
            border: 4px solid #333;
            border-radius: 12px;
            height: 65px;
            font-size: 32px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            box-shadow: 0 5px 0 #888;
            transition: all 0.1s ease;
        }

        .option-card:active {
            transform: translateY(4px);
            box-shadow: 0 1px 0 #888;
        }

        .card-display {
            max-height: 220px;
            filter: drop-shadow(0px 10px 15px rgba(0,0,0,0.6));
            animation: popIn 0.5s ease-out;
        }

        @keyframes popIn {
            0% { transform: scale(0); }
            80% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
            margin-top: 5px;
        }

        button.action-btn {
            font-family: 'Arial Black', sans-serif;
            font-size: 18px;
            padding: 10px 25px;
            border-radius: 8px;
            border: 3px solid #333;
            background: #ffcc00;
            color: #000;
            cursor: pointer;
            box-shadow: 0 4px 0 #b38f00;
            transition: all 0.1s ease;
        }

        button.action-btn:active {
            transform: translateY(4px);
            box-shadow: 0 0 0 #b38f00;
        }

        .result-text {
            font-size: 24px;
            color: #ffcc00;
            text-shadow: 3px 3px 0 #000, -2px -2px 0 #000, 2px -2px 0 #000, -2px 2px 0 #000;
            letter-spacing: 2px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>

<div class="pokedex">
    <div class="top-bar">
        <div class="lights-container">
            <div class="big-light" id="bigLightBtn"></div>
            <div class="small-lights">
                <div class="light red"></div>
                <div class="light yellow"></div>
                <div class="light green"></div>
            </div>
        </div>
        <div class="header-info">
            <div class="status-badge" id="levelDisplay">STAGE 1</div>
            <div class="status-badge"><span id="progressDisplay">1</span>/20</div>
        </div>
    </div>

    <div class="screen-container">
        <div class="main-screen" id="mainScreen">
            <button class="audio-btn" id="playAudioBtn">🔊</button>
            <div class="target-display hidden" id="targetDisplay">A</div>
            <div class="options-grid" id="optionsGrid"></div>
            <img id="cardImg" class="card-display hidden" src="" alt="reward pokemon" />
        </div>
    </div>

    <div class="controls">
        <div id="resultDisplay" class="result-text">listen and choose!</div>
        <button id="nextBtn" class="action-btn hidden">next ></button>
        <button id="restartBtn" class="action-btn hidden">play again</button>
    </div>
</div>

<script>
    const playAudioBtn = document.getElementById('playAudioBtn');
    const targetDisplay = document.getElementById('targetDisplay');
    const optionsGrid = document.getElementById('optionsGrid');
    const cardImg = document.getElementById('cardImg');
    const nextBtn = document.getElementById('nextBtn');
    const restartBtn = document.getElementById('restartBtn');
    const resultDisplay = document.getElementById('resultDisplay');
    const levelDisplay = document.getElementById('levelDisplay');
    const progressDisplay = document.getElementById('progressDisplay');
    const bigLightBtn = document.getElementById('bigLightBtn');

    // 生成 A-Z 完整資料結構
    const ALPHABET = Array.from({ length: 26 }, (_, i) => ({
        upper: String.fromCharCode(65 + i),
        lower: String.fromCharCode(97 + i)
    }));

    const REWARD_POKEMON = [
        { name: "皮卡丘 (pikachu)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" },
        { name: "噴火龍 (charizard)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png" },
        { name: "妙蛙種子 (bulbasaur)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png" },
        { name: "傑尼龜 (squirtle)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png" },
        { name: "甲賀忍蛙 (greninja)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/658.png" },
        { name: "耿鬼 (gengar)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/94.png" },
        { name: "超夢 (mewtwo)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png" },
        { name: "伊布 (eevee)", src: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/133.png" }
    ];

    let currentStage = 1; // 1: 聽音找字, 2: 大小配對
    let gameQuestions = [];
    let currentIndex = 0;
    let isAnswered = false;

    function shuffleArray(array) {
        let arr = [...array];
        for (let i = arr.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        return arr;
    }

    function speakLetter(letter) {
        if ('speechSynthesis' in window) {
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(letter);
            utterance.lang = 'en-US';
            utterance.rate = 0.8;
            window.speechSynthesis.speak(utterance);
        }
    }

    function renderQuestion() {
        isAnswered = false;
        progressDisplay.textContent = currentIndex + 1;
        optionsGrid.innerHTML = '';
        nextBtn.classList.add('hidden');

        const currentGoal = gameQuestions[currentIndex];

        if (currentStage === 1) {
            // 第一關：聽音找字 (顯示播放按鈕，選項為 A a 樣式)
            levelDisplay.textContent = "STAGE 1";
            playAudioBtn.classList.remove('hidden');
            targetDisplay.classList.add('hidden');
            resultDisplay.textContent = "listen and choose!";

            // 生成選項 (1正確 + 3錯誤)
            const wrongList = ALPHABET.filter(item => item.upper !== currentGoal.upper);
            const wrongOptions = shuffleArray(wrongList).slice(0, 3);
            const options = shuffleArray([currentGoal, ...wrongOptions]);

            options.forEach(item => {
                const card = document.createElement('div');
                card.className = 'option-card';
                card.textContent = `${item.upper} ${item.lower}`;
                card.addEventListener('click', () => checkStage1(item, card));
                optionsGrid.appendChild(card);
            });

            setTimeout(() => speakLetter(currentGoal.upper), 300);

        } else {
            // 第二關：大小配對 (不安靜無聲音，題目隨機出大寫或小寫)
            levelDisplay.textContent = "STAGE 2";
            playAudioBtn.classList.add('hidden');
            targetDisplay.classList.remove('hidden');
            resultDisplay.textContent = "match uppercase & lowercase!";

            // 隨機決定題目要顯示大寫還是小寫
            const showUpper = Math.random() < 0.5;
            targetDisplay.textContent = showUpper ? currentGoal.upper : currentGoal.lower;
            
            // 正確答案為反向的大小寫
            const correctAnswer = showUpper ? currentGoal.lower : currentGoal.upper;

            // 產生干擾選項
            const wrongList = ALPHABET.filter(item => item.upper !== currentGoal.upper);
            const wrongOptions = shuffleArray(wrongList).slice(0, 3).map(item => showUpper ? item.lower : item.upper);
            const options = shuffleArray([correctAnswer, ...wrongOptions]);

            options.forEach(text => {
                const card = document.createElement('div');
                card.className = 'option-card';
                card.textContent = text;
                card.addEventListener('click', () => checkStage2(text, correctAnswer, card));
                optionsGrid.appendChild(card);
            });
        }
    }

    function checkStage1(selectedItem, cardElement) {
        if (isAnswered) return;

        const currentGoal = gameQuestions[currentIndex];
        if (selectedItem.upper === currentGoal.upper) {
            isAnswered = true;
            cardElement.style.backgroundColor = '#81c784';
            resultDisplay.textContent = `correct! ${currentGoal.upper} ${currentGoal.lower}`;
            nextBtn.classList.remove('hidden');
            speakLetter(currentGoal.upper);
        } else {
            cardElement.style.backgroundColor = '#e57373';
            resultDisplay.textContent = "try again!";
            setTimeout(() => cardElement.style.backgroundColor = '#ffffff', 500);
        }
    }

    function checkStage2(selectedText, correctAnswer, cardElement) {
        if (isAnswered) return;

        if (selectedText === correctAnswer) {
            isAnswered = true;
            cardElement.style.backgroundColor = '#81c784';
            resultDisplay.textContent = "correct match!";
            nextBtn.classList.remove('hidden');
        } else {
            cardElement.style.backgroundColor = '#e57373';
            resultDisplay.textContent = "try again!";
            setTimeout(() => cardElement.style.backgroundColor = '#ffffff', 500);
        }
    }

    function nextQuestion() {
        if (currentIndex < gameQuestions.length - 1) {
            currentIndex++;
            renderQuestion();
        } else {
            if (currentStage === 1) {
                // 第一關 20 題全對，自動進入第二關
                currentStage = 2;
                currentIndex = 0;
                gameQuestions = shuffleArray(ALPHABET).slice(0, 20);
                alert("🎉 第一關通關！進入第二關：大小寫配對");
                renderQuestion();
            } else {
                // 第二關 20 題完成，發放獎勵
                showReward();
            }
        }
    }

    function showReward() {
        playAudioBtn.classList.add('hidden');
        targetDisplay.classList.add('hidden');
        optionsGrid.classList.add('hidden');
        nextBtn.classList.add('hidden');

        const reward = REWARD_POKEMON[Math.floor(Math.random() * REWARD_POKEMON.length)];
        cardImg.src = reward.src;
        cardImg.classList.remove('hidden');

        resultDisplay.textContent = `通關成功！獲得：${reward.name}！`;
        restartBtn.classList.remove('hidden');
    }

    function initGame() {
        currentStage = 1;
        currentIndex = 0;
        // 隨機抽 20 個字母作為題目
        gameQuestions = shuffleArray(ALPHABET).slice(0, 20);

        cardImg.classList.add('hidden');
        optionsGrid.classList.remove('hidden');
        restartBtn.classList.add('hidden');

        renderQuestion();
    }

    playAudioBtn.addEventListener('click', () => {
        if (currentStage === 1) speakLetter(gameQuestions[currentIndex].upper);
    });

    bigLightBtn.addEventListener('click', () => {
        if (currentStage === 1) speakLetter(gameQuestions[currentIndex].upper);
    });

    nextBtn.addEventListener('click', nextQuestion);
    restartBtn.addEventListener('click', initGame);

    initGame();
</script>

</body>
</html>
