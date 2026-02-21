<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⭐ Звездная коллекция</title>
    <style>
        * {
            box-sizing: border-box;
            user-select: none;
        }

        body {
            margin: 0;
            min-height: 100vh;
            background: linear-gradient(145deg, #2a1f2f 0%, #151129 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
        }

        .game-container {
            background: #3a3155;
            padding: 25px 30px 30px;
            border-radius: 48px;
            box-shadow: 0 25px 35px rgba(0,0,0,0.6), inset 0 1px 4px rgba(255,220,200,0.2);
            border: 1px solid #9f7f94;
            position: relative;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #f5e7c8;
            text-shadow: 3px 3px 0 #3a2a47;
            margin-bottom: 12px;
            padding: 0 10px;
        }

        .score-box {
            background: #1e1c36;
            border-radius: 40px;
            padding: 10px 25px;
            font-size: 26px;
            font-weight: 700;
            letter-spacing: 1px;
            color: #ffddb0;
            box-shadow: inset 0 -3px 0 #5a4e8c, 0 6px 0 #0a0a1c;
            border-bottom: 2px solid #bfa5cc;
        }

        .level-box {
            background: #2a3f5a;
            border-radius: 40px;
            padding: 10px 25px;
            font-size: 22px;
            font-weight: 700;
            color: #aac8ff;
            box-shadow: inset 0 -3px 0 #1e2a45;
            border-bottom: 2px solid #7a6a9f;
        }

        .boss-health-box {
            background: #4a1e36;
            border-radius: 40px;
            padding: 10px 25px;
            font-size: 22px;
            font-weight: 700;
            color: #ffaacc;
            box-shadow: inset 0 -3px 0 #2a0a1c;
            border-bottom: 2px solid #ff6a9f;
        }

        button {
            background: #c89f6e;
            border: none;
            border-radius: 40px;
            padding: 10px 25px;
            font-size: 22px;
            font-weight: bold;
            color: #2a1e2a;
            cursor: pointer;
            box-shadow: 0 8px 0 #6f4f2c, 0 4px 15px rgba(0,0,0,0.5);
            transition: 0.07s ease;
            border: 1px solid #eecd9e;
            font-family: inherit;
        }

        button:active {
            transform: translateY(7px);
            box-shadow: 0 1px 0 #6f4f2c, 0 4px 12px black;
        }

        .music-toggle, .pause-toggle, .menu-toggle {
            background: #6b4f7f;
            color: #ffeac0;
            border: none;
            border-radius: 30px;
            padding: 5px 15px;
            font-size: 16px;
            cursor: pointer;
            box-shadow: 0 4px 0 #2a1e47;
            transition: 0.05s ease;
        }

        .music-toggle:active, .pause-toggle:active, .menu-toggle:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        canvas {
            display: block;
            margin: 0 auto;
            background: radial-gradient(circle at 30% 30%, #7c7cb0, #2e3558);
            border-radius: 36px;
            border: 5px solid #bb8b7b;
            box-shadow: inset 0 0 0 2px #e2bf9f, 0 20px 25px #0d0a24;
            width: 800px;
            height: 500px;
            cursor: pointer;
        }

        .tip {
            margin-top: 15px;
            color: #d3c0e0;
            font-size: 18px;
            display: flex;
            gap: 20px;
            justify-content: center;
            background: #2a2545;
            padding: 8px 20px;
            border-radius: 40px;
            border-left: 4px solid #f9b974;
        }

        .timer-bar-container {
            width: 100%;
            height: 6px;
            background: #1e2a45;
            border-radius: 3px;
            margin-top: 10px;
            overflow: hidden;
        }

        .timer-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #4a90e2, #a0c8ff);
            transition: width 0.1s linear;
            border-radius: 3px;
        }

        /* Стили для затемнения фона */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(3px);
        }

        /* Главное меню */
        .main-menu {
            background: #0f1e2f;
            border: 4px solid #9f8ac0;
            border-radius: 60px;
            padding: 50px 80px;
            box-shadow: 0 30px 50px rgba(0,0,0,0.8), inset 0 0 40px rgba(159, 138, 192, 0.3);
            text-align: center;
            animation: menuFadeIn 0.4s ease-out;
            max-width: 900px;
        }

        @keyframes menuFadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }

        .main-menu h1 {
            color: #ffddaa;
            font-size: 72px;
            margin: 0 0 20px 0;
            text-shadow: 0 0 25px #ffaa00, 0 0 50px #aa88ff;
            letter-spacing: 4px;
        }

        .main-menu .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 25px;
            margin: 40px 0;
        }

        .main-menu .menu-btn {
            background: #2a3f5a;
            border: 3px solid #bbaaff;
            border-radius: 60px;
            padding: 20px 60px;
            font-size: 36px;
            font-weight: bold;
            color: #f0e0ff;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 10px 0 #0a1a2a;
            min-width: 400px;
        }

        .main-menu .menu-btn:hover {
            background: #3a4f7a;
            transform: translateY(-3px);
            box-shadow: 0 13px 0 #0a1a2a;
            border-color: #d0c0ff;
        }

        .main-menu .menu-btn:active {
            transform: translateY(7px);
            box-shadow: 0 3px 0 #0a1a2a;
        }

        /* Меню ачивок */
        .achievements-menu {
            background: #0f1e2f;
            border: 4px solid #ffaa44;
            border-radius: 50px;
            padding: 40px 60px;
            box-shadow: 0 30px 50px rgba(0,0,0,0.8);
            text-align: center;
            max-width: 800px;
            max-height: 80vh;
            overflow-y: auto;
        }

        .achievements-menu h2 {
            color: #ffddaa;
            font-size: 56px;
            margin: 0 0 30px 0;
            text-shadow: 0 0 20px #ffaa44;
        }

        .achievements-grid {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin: 30px 0;
        }

        .achievement-card {
            background: #1e2a3a;
            border: 2px solid #7a6a9f;
            border-radius: 30px;
            padding: 20px 30px;
            display: flex;
            align-items: center;
            gap: 30px;
            transition: all 0.2s ease;
        }

        .achievement-card.unlocked {
            border-color: #ffaa44;
            background: #2a3a4a;
            box-shadow: 0 0 20px rgba(255, 170, 68, 0.3);
        }

        .achievement-icon {
            font-size: 48px;
            min-width: 80px;
            text-align: center;
        }

        .achievement-info {
            flex: 1;
            text-align: left;
        }

        .achievement-info h3 {
            color: #ffddaa;
            font-size: 28px;
            margin: 0 0 5px 0;
        }

        .achievement-info p {
            color: #aac8ff;
            font-size: 18px;
            margin: 0 0 10px 0;
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: #0f1e2f;
            border-radius: 5px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4a90e2, #ffaa44);
            transition: width 0.3s ease;
        }

        .progress-text {
            color: #ffddaa;
            font-size: 16px;
            margin-top: 5px;
            text-align: right;
        }

        .achievement-close-btn {
            background: #4a3f6a;
            border: 2px solid #9f8ac0;
            border-radius: 40px;
            padding: 15px 40px;
            font-size: 24px;
            color: #f0e0ff;
            cursor: pointer;
            margin-top: 20px;
            box-shadow: 0 6px 0 #2a1e4a;
        }

        .achievement-close-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 0 #2a1e4a;
        }

        .achievement-close-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #2a1e4a;
        }

        /* Всплывающее уведомление об ачивке */
        .achievement-popup {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #1e2a3a;
            border: 3px solid #ffaa44;
            border-radius: 30px;
            padding: 20px 30px;
            display: flex;
            align-items: center;
            gap: 20px;
            box-shadow: 0 10px 30px rgba(255, 170, 68, 0.3);
            transform: translateX(120%);
            transition: transform 0.3s ease;
            z-index: 2000;
            max-width: 400px;
        }

        .achievement-popup.show {
            transform: translateX(0);
        }

        .popup-icon {
            font-size: 48px;
        }

        .popup-content h3 {
            color: #ffddaa;
            font-size: 24px;
            margin: 0 0 5px 0;
        }

        .popup-content p {
            color: #aac8ff;
            font-size: 16px;
            margin: 0;
        }

        /* Меню паузы */
        .pause-menu {
            background: #0f1e2f;
            border: 3px solid #7a6a9f;
            border-radius: 40px;
            padding: 40px 70px;
            box-shadow: 0 25px 40px rgba(0,0,0,0.7), inset 0 0 30px rgba(122, 106, 159, 0.3);
            text-align: center;
            animation: pauseFadeIn 0.2s ease-out;
        }

        @keyframes pauseFadeIn {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }

        .pause-menu h2 {
            color: #dbbaff;
            font-size: 56px;
            margin: 0 0 25px 0;
            text-shadow: 0 0 20px #9f8ac0;
            letter-spacing: 3px;
        }

        .pause-menu .pause-stats {
            background: #1e2a3a;
            border-radius: 50px;
            padding: 20px 40px;
            margin: 20px 0;
            border: 2px solid #7a6a9f;
        }

        .pause-menu .pause-stats p {
            color: #e0d0ff;
            font-size: 28px;
            margin: 10px 0;
        }

        .pause-menu .pause-stats span {
            color: #ffddaa;
            font-weight: bold;
            font-size: 36px;
        }

        .volume-control {
            margin: 25px 0;
            color: #e0d0ff;
            font-size: 22px;
        }

        .volume-control label {
            display: block;
            margin-bottom: 10px;
        }

        .volume-slider {
            width: 300px;
            height: 8px;
            -webkit-appearance: none;
            background: linear-gradient(90deg, #7a6a9f, #bbaaff);
            border-radius: 10px;
            outline: none;
        }

        .volume-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 25px;
            height: 25px;
            background: #ffddaa;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid #7a6a9f;
            box-shadow: 0 0 10px #bbaaff;
        }

        .volume-slider::-moz-range-thumb {
            width: 25px;
            height: 25px;
            background: #ffddaa;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid #7a6a9f;
            box-shadow: 0 0 10px #bbaaff;
        }

        .pause-menu .pause-buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 30px;
        }

        .pause-menu .pause-btn {
            background: #2a3f5a;
            border: 2px solid #9f8ac0;
            border-radius: 50px;
            padding: 15px 35px;
            font-size: 24px;
            font-weight: bold;
            color: #f0e0ff;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 6px 0 #0a1a2a;
            min-width: 180px;
        }

        .pause-menu .pause-btn:hover {
            background: #3a4f7a;
            transform: translateY(-2px);
            box-shadow: 0 8px 0 #0a1a2a;
        }

        .pause-menu .pause-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #0a1a2a;
        }

        .pause-menu .resume-btn {
            background: #5a4f8a;
            border-color: #bbaaff;
            box-shadow: 0 6px 0 #2a1e4a;
        }

        .pause-menu .main-menu-btn {
            background: #4a3f6a;
            border-color: #9f8ac0;
        }

        /* Окно победы/проигрыша */
        .game-over-window {
            background: #0a1a2f;
            border: 3px solid #4a90e2;
            border-radius: 30px;
            padding: 40px 60px;
            box-shadow: 0 20px 40px rgba(0, 20, 40, 0.8), inset 0 0 20px rgba(74, 144, 226, 0.3);
            text-align: center;
            animation: fadeIn 0.3s ease-out;
        }

        .game-over-window.victory {
            border-color: #ffaa44;
            box-shadow: 0 20px 40px rgba(255, 170, 68, 0.3), inset 0 0 20px rgba(255, 170, 68, 0.3);
        }

        .game-over-window h2 {
            color: #e0f0ff;
            font-size: 48px;
            margin: 0 0 10px 0;
            text-shadow: 0 0 15px #4a90e2;
            letter-spacing: 2px;
        }

        .game-over-window.victory h2 {
            color: #ffddaa;
            text-shadow: 0 0 15px #ffaa44;
        }

        .game-over-window p {
            color: #aac8ff;
            font-size: 24px;
            margin: 10px 0 30px 0;
        }

        .game-over-window .final-score {
            background: #0f2a45;
            border-radius: 60px;
            padding: 15px 30px;
            margin: 20px 0;
            border: 1px solid #4a90e2;
            box-shadow: inset 0 0 15px rgba(74, 144, 226, 0.2);
        }

        .game-over-window.victory .final-score {
            border-color: #ffaa44;
        }

        .game-over-window .final-score span {
            color: #ffddb0;
            font-size: 42px;
            font-weight: bold;
            display: block;
        }

        .game-over-window .restart-btn {
            background: #1e3a5f;
            border: 2px solid #4a90e2;
            border-radius: 50px;
            padding: 15px 50px;
            font-size: 28px;
            font-weight: bold;
            color: #e0f0ff;
            cursor: pointer;
            margin: 10px;
            transition: all 0.2s ease;
            box-shadow: 0 8px 0 #0a1a2f;
        }

        .game-over-window .restart-btn:hover {
            background: #2a4a7f;
            transform: translateY(-2px);
            box-shadow: 0 10px 0 #0a1a2f;
        }

        .game-over-window .restart-btn:active {
            transform: translateY(5px);
            box-shadow: 0 3px 0 #0a1a2f;
        }

        .game-over-window .menu-btn {
            background: #4a3f6a;
            border-color: #9f8ac0;
        }

        /* Окно перехода между уровнями */
        .level-complete-window {
            background: #1a2a3f;
            border: 4px solid #ffaa44;
            border-radius: 50px;
            padding: 50px 80px;
            box-shadow: 0 30px 50px rgba(255, 170, 68, 0.3);
            text-align: center;
        }

        .level-complete-window h2 {
            color: #ffddaa;
            font-size: 56px;
            margin-bottom: 20px;
        }

        .level-complete-window p {
            color: #aac8ff;
            font-size: 28px;
            margin: 20px 0;
        }

        .level-complete-window .continue-btn {
            background: #5a4f8a;
            border: 3px solid #ffaa44;
            border-radius: 60px;
            padding: 20px 60px;
            font-size: 36px;
            font-weight: bold;
            color: #ffddaa;
            cursor: pointer;
            margin-top: 20px;
            box-shadow: 0 10px 0 #2a1e4a;
        }

        .level-complete-window .continue-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 13px 0 #2a1e4a;
        }

        .level-complete-window .continue-btn:active {
            transform: translateY(7px);
            box-shadow: 0 3px 0 #2a1e4a;
        }
    </style>
</head>
<body>
<!-- Главное меню -->
<div class="overlay" id="mainMenu" style="display: flex;">
    <div class="main-menu">
        <h1>⭐ ЗВЕЗДНАЯ КОЛЛЕКЦИЯ</h1>
        <div class="menu-buttons">
            <button class="menu-btn" id="infiniteModeBtn">♾️ Бесконечный режим</button>
            <button class="menu-btn" id="campaignModeBtn">📜 Кампания</button>
            <button class="menu-btn" id="achievementsMenuBtn">🏆 Достижения</button>
        </div>
    </div>
</div>

<!-- Меню ачивок -->
<div class="overlay" id="achievementsMenu" style="display: none;">
    <div class="achievements-menu">
        <h2>🏆 ДОСТИЖЕНИЯ</h2>
        <div class="achievements-grid" id="achievementsGrid">
            <!-- Ачивки будут добавляться динамически -->
        </div>
        <button class="achievement-close-btn" id="closeAchievementsBtn">ЗАКРЫТЬ</button>
    </div>
</div>

<!-- Всплывающее уведомление об ачивке -->
<div class="achievement-popup" id="achievementPopup">
    <div class="popup-icon" id="popupIcon">🏆</div>
    <div class="popup-content">
        <h3 id="popupTitle">Достижение получено!</h3>
        <p id="popupDescription"></p>
    </div>
</div>

<div class="game-container" style="display: none;" id="gameContainer">
    <div class="header">
        <div style="display: flex; gap: 20px;">
            <span class="score-box" id="scoreDisplay">0 ⭐</span>
            <span class="level-box" id="levelDisplay" style="display: none;">Уровень 1</span>
            <span class="boss-health-box" id="bossHealthDisplay" style="display: none;">👾 Босс: 50</span>
        </div>
        <div style="display: flex; gap: 10px;">
            <button id="menuButton" class="menu-toggle">🏠 Меню</button>
            <button id="pauseButton" class="pause-toggle">⏸️ Пауза</button>
            <button id="resetButton">⟳ Новая игра</button>
            <button id="musicToggle" class="music-toggle">🔊 Джаз</button>
        </div>
    </div>
    <canvas id="gameCanvas" width="800" height="500"></canvas>
    <div class="tip" id="tip"></div>
    <div class="timer-bar-container">
        <div class="timer-bar" id="timerBar"></div>
    </div>
</div>

<!-- Затемнение фона при паузе -->
<div class="overlay" id="pauseOverlay"></div>

<!-- Меню паузы -->
<div class="overlay" id="pauseMenu" style="background: rgba(0,0,0,0.6); display: none;">
    <div class="pause-menu">
        <h2>⏸️ ПАУЗА</h2>
        <div class="pause-stats">
            <p>Собрано звёзд: <span id="pauseScore">0</span></p>
            <p>Звёзд на поле: <span id="pauseStarsCount">0</span>/25</p>
            <p id="pauseLevel" style="display: none;">Уровень: <span id="pauseLevelNum">1</span></p>
        </div>
        
        <div class="volume-control">
            <label>🎵 Громкость музыки</label>
            <input type="range" id="volumeSlider" class="volume-slider" min="0" max="1" step="0.01" value="0.25">
        </div>
        
        <div class="pause-buttons">
            <button class="pause-btn resume-btn" id="resumeButton">▶ Продолжить</button>
            <button class="pause-btn main-menu-btn" id="pauseToMenuButton">🏠 В меню</button>
            <button class="pause-btn" id="pauseResetButton">↻ Новая игра</button>
        </div>
    </div>
</div>

<!-- Окно результата -->
<div class="overlay" id="resultOverlay">
    <div class="game-over-window" id="resultWindow">
        <h2 id="resultTitle">ВРЕМЯ ВЫШЛО</h2>
        <p id="resultMessage"></p>
        <div class="final-score">
            <span id="resultScore">0</span> ⭐ звёзд собрано
        </div>
        <div>
            <button class="restart-btn" id="resultRestart">↻ ИГРАТЬ СНОВА</button>
            <button class="restart-btn menu-btn" id="resultToMenu">🏠 В МЕНЮ</button>
        </div>
    </div>
</div>

<!-- Окно завершения уровня -->
<div class="overlay" id="levelCompleteOverlay" style="display: none;">
    <div class="level-complete-window">
        <h2>⭐ УРОВЕНЬ ПРОЙДЕН!</h2>
        <p id="levelCompleteMessage"></p>
        <button class="continue-btn" id="continueButton">▶ ПРОДОЛЖИТЬ</button>
    </div>
</div>

<script>
    (function() {
        // ------ настройки игры ------
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreSpan = document.getElementById('scoreDisplay');
        const levelSpan = document.getElementById('levelDisplay');
        const bossHealthSpan = document.getElementById('bossHealthDisplay');
        const musicToggle = document.getElementById('musicToggle');
        const resetButton = document.getElementById('resetButton');
        const pauseButton = document.getElementById('pauseButton');
        const menuButton = document.getElementById('menuButton');
        const pauseMenu = document.getElementById('pauseMenu');
        const pauseOverlay = document.getElementById('pauseOverlay');
        const resumeButton = document.getElementById('resumeButton');
        const pauseResetButton = document.getElementById('pauseResetButton');
        const pauseToMenuButton = document.getElementById('pauseToMenuButton');
        const pauseScore = document.getElementById('pauseScore');
        const pauseStarsCount = document.getElementById('pauseStarsCount');
        const pauseLevel = document.getElementById('pauseLevel');
        const pauseLevelNum = document.getElementById('pauseLevelNum');
        const timerBar = document.getElementById('timerBar');
        const volumeSlider = document.getElementById('volumeSlider');
        const tip = document.getElementById('tip');
        
        // Элементы меню
        const mainMenu = document.getElementById('mainMenu');
        const gameContainer = document.getElementById('gameContainer');
        const infiniteModeBtn = document.getElementById('infiniteModeBtn');
        const campaignModeBtn = document.getElementById('campaignModeBtn');
        const achievementsMenuBtn = document.getElementById('achievementsMenuBtn');
        const achievementsMenu = document.getElementById('achievementsMenu');
        const closeAchievementsBtn = document.getElementById('closeAchievementsBtn');
        const achievementsGrid = document.getElementById('achievementsGrid');
        
        // Элементы результата
        const resultOverlay = document.getElementById('resultOverlay');
        const resultWindow = document.getElementById('resultWindow');
        const resultTitle = document.getElementById('resultTitle');
        const resultMessage = document.getElementById('resultMessage');
        const resultScore = document.getElementById('resultScore');
        const resultRestart = document.getElementById('resultRestart');
        const resultToMenu = document.getElementById('resultToMenu');
        
        // Элементы завершения уровня
        const levelCompleteOverlay = document.getElementById('levelCompleteOverlay');
        const levelCompleteMessage = document.getElementById('levelCompleteMessage');
        const continueButton = document.getElementById('continueButton');
        
        // Элементы ачивок
        const achievementPopup = document.getElementById('achievementPopup');
        const popupIcon = document.getElementById('popupIcon');
        const popupTitle = document.getElementById('popupTitle');
        const popupDescription = document.getElementById('popupDescription');
        
        // Создаём аудио элементы
        const jazzAudio = new Audio();
        jazzAudio.loop = true;
        jazzAudio.volume = 0.25;
        jazzAudio.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-17.mp3';
        
        const coinAudio = new Audio();
        coinAudio.volume = 1.0;
        coinAudio.src = 'https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3';
        
        const redCoinAudio = new Audio();
        redCoinAudio.volume = 0.8;
        redCoinAudio.src = 'https://www.soundjay.com/misc/sounds/bell-ringing-06.mp3';
        
        jazzAudio.load();
        coinAudio.load();
        redCoinAudio.load();

        // Константы игры
        const MAX_STARS = 25;
        const STAR_RADIUS = 30;
        const RED_STAR_RADIUS = 28;
        const SPAWN_DELAY = 1500;
        const INITIAL_TIME = 3;
        const MAX_TIME = 10;
        const TIME_BONUS = 0.5;
        
        // Уровни кампании
        const CAMPAIGN_LEVELS = [
            { target: 5, time: 5, name: "Уровень 1 - Разминка" },
            { target: 10, time: 8, name: "Уровень 2 - Начинающий" },
            { target: 15, time: 10, name: "Уровень 3 - Опытный" },
            { target: 20, time: 12, name: "Уровень 4 - Профессионал" },
            { target: 25, time: 15, name: "Уровень 5 - Мастер" },
            { target: 0, time: 0, name: "Уровень 6 - БИТВА С БОССОМ", isBoss: true }
        ];

        // ------ Система ачивок ------
        const ACHIEVEMENTS = {
            COSMONAUT: {
                id: 'cosmonaut',
                name: 'Космонавт',
                description: 'Собрать 30 звезд в бесконечном режиме',
                icon: '🚀',
                condition: (stats) => stats.infiniteScore >= 30,
                progress: (stats) => Math.min(100, Math.floor((stats.infiniteScore / 30) * 100)),
                current: (stats) => stats.infiniteScore,
                target: 30,
                unlocked: false
            },
            COLLECTOR: {
                id: 'collector',
                name: 'Коллекционер',
                description: 'Собрать 50 звезд в бесконечном режиме',
                icon: '📦',
                condition: (stats) => stats.infiniteScore >= 50,
                progress: (stats) => Math.min(100, Math.floor((stats.infiniteScore / 50) * 100)),
                current: (stats) => stats.infiniteScore,
                target: 50,
                unlocked: false
            },
            STAR_MASTER: {
                id: 'starMaster',
                name: 'Звездный мастер',
                description: 'Собрать 100 звезд в бесконечном режиме',
                icon: '👑',
                condition: (stats) => stats.infiniteScore >= 100,
                progress: (stats) => Math.min(100, Math.floor((stats.infiniteScore / 100) * 100)),
                current: (stats) => stats.infiniteScore,
                target: 100,
                unlocked: false
            },
            CAMPAIGN_STARTER: {
                id: 'campaignStarter',
                name: 'Начинающий путешественник',
                description: 'Пройдите первый уровень кампании',
                icon: '🌍',
                condition: (stats) => stats.completedLevels >= 1,
                progress: (stats) => Math.min(100, Math.floor((stats.completedLevels / 1) * 100)),
                current: (stats) => stats.completedLevels,
                target: 1,
                unlocked: false
            },
            CAMPAIGN_PRO: {
                id: 'campaignPro',
                name: 'Опытный исследователь',
                description: 'Пройдите 3 уровня кампании',
                icon: '🗺️',
                condition: (stats) => stats.completedLevels >= 3,
                progress: (stats) => Math.min(100, Math.floor((stats.completedLevels / 3) * 100)),
                current: (stats) => stats.completedLevels,
                target: 3,
                unlocked: false
            },
            CAMPAIGN_MASTER: {
                id: 'campaignMaster',
                name: 'Мастер кампании',
                description: 'Пройдите все уровни кампании',
                icon: '🏆',
                condition: (stats) => stats.completedLevels >= 6,
                progress: (stats) => Math.min(100, Math.floor((stats.completedLevels / 6) * 100)),
                current: (stats) => stats.completedLevels,
                target: 6,
                unlocked: false
            },
            BOSS_SLAYER: {
                id: 'bossSlayer',
                name: 'Победитель босса',
                description: 'Победите босса на 6 уровне',
                icon: '👾',
                condition: (stats) => stats.bossDefeated,
                progress: (stats) => stats.bossDefeated ? 100 : 0,
                current: (stats) => stats.bossDefeated ? 1 : 0,
                target: 1,
                unlocked: false
            },
            QUICK_FINGERS: {
                id: 'quickFingers',
                name: 'Быстрые пальцы',
                description: 'Соберите 10 звезд за одну игру в бесконечном режиме',
                icon: '⚡',
                condition: (stats) => stats.maxScorePerGame >= 10,
                progress: (stats) => Math.min(100, Math.floor((stats.maxScorePerGame / 10) * 100)),
                current: (stats) => stats.maxScorePerGame,
                target: 10,
                unlocked: false
            },
            STAR_COLLECTOR: {
                id: 'starCollector',
                name: 'Звездный коллекционер',
                description: 'Соберите 25 звезд за одну игру в бесконечном режиме',
                icon: '💫',
                condition: (stats) => stats.maxScorePerGame >= 25,
                progress: (stats) => Math.min(100, Math.floor((stats.maxScorePerGame / 25) * 100)),
                current: (stats) => stats.maxScorePerGame,
                target: 25,
                unlocked: false
            },
            PERFECTIONIST: {
                id: 'perfectionist',
                name: 'Перфекционист',
                description: 'Соберите все звезды на уровне (макс. 25)',
                icon: '✨',
                condition: (stats) => stats.maxStarsCollected >= 25,
                progress: (stats) => Math.min(100, Math.floor((stats.maxStarsCollected / 25) * 100)),
                current: (stats) => stats.maxStarsCollected,
                target: 25,
                unlocked: false
            }
        };

        // Статистика игрока для ачивок
        let playerStats = {
            infiniteScore: 0,
            completedLevels: 0,
            bossDefeated: false,
            maxScorePerGame: 0,
            maxStarsCollected: 0
        };

        // Загружаем сохраненные ачивки и статистику
        function loadAchievements() {
            try {
                // Загружаем разблокированные достижения
                const savedUnlocked = localStorage.getItem('achievements_unlocked');
                if (savedUnlocked) {
                    unlockedAchievements = new Set(JSON.parse(savedUnlocked));
                }
                
                // Загружаем статистику игрока
                const savedStats = localStorage.getItem('achievements_stats');
                if (savedStats) {
                    const parsedStats = JSON.parse(savedStats);
                    playerStats = { ...playerStats, ...parsedStats };
                }
                
                // Обновляем статус ачивок
                for (let key in ACHIEVEMENTS) {
                    ACHIEVEMENTS[key].unlocked = unlockedAchievements.has(key);
                }
            } catch (e) {
                console.log('Не удалось загрузить достижения', e);
            }
        }

        // Сохраняем ачивки и статистику
        function saveAchievements() {
            try {
                localStorage.setItem('achievements_unlocked', JSON.stringify([...unlockedAchievements]));
                localStorage.setItem('achievements_stats', JSON.stringify(playerStats));
            } catch (e) {
                console.log('Не удалось сохранить достижения', e);
            }
        }

        // Загружаем сохраненные ачивки
        let unlockedAchievements = new Set();
        loadAchievements();

        // Функция показа уведомления об ачивке
        function showAchievementPopup(achievement) {
            popupIcon.textContent = achievement.icon;
            popupTitle.textContent = '🎉 Достижение получено!';
            popupDescription.textContent = `${achievement.name}: ${achievement.description}`;
            
            achievementPopup.classList.add('show');
            
            setTimeout(() => {
                achievementPopup.classList.remove('show');
            }, 5000);
        }

        // Функция проверки ачивок
        function checkAchievements() {
            let newUnlocks = false;
            
            for (let key in ACHIEVEMENTS) {
                const ach = ACHIEVEMENTS[key];
                if (!ach.unlocked && ach.condition(playerStats)) {
                    ach.unlocked = true;
                    unlockedAchievements.add(key);
                    showAchievementPopup(ach);
                    newUnlocks = true;
                }
            }
            
            if (newUnlocks) {
                saveAchievements();
            }
            
            // Обновляем отображение ачивок, если меню открыто
            if (achievementsMenu.style.display === 'flex') {
                renderAchievements();
            }
        }

        // Функция отрисовки ачивок
        function renderAchievements() {
            achievementsGrid.innerHTML = '';
            
            for (let key in ACHIEVEMENTS) {
                const ach = ACHIEVEMENTS[key];
                const progress = ach.progress(playerStats);
                const current = ach.current(playerStats);
                
                const card = document.createElement('div');
                card.className = `achievement-card ${ach.unlocked ? 'unlocked' : ''}`;
                
                card.innerHTML = `
                    <div class="achievement-icon">${ach.unlocked ? '🏆' : ach.icon}</div>
                    <div class="achievement-info">
                        <h3>${ach.name}</h3>
                        <p>${ach.description}</p>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${progress}%"></div>
                        </div>
                        <div class="progress-text">${current}/${ach.target} (${progress}%)</div>
                    </div>
                `;
                
                achievementsGrid.appendChild(card);
            }
        }

        // Функция обновления статистики
        function updateStats() {
            if (gameMode === 'infinite') {
                const oldInfiniteScore = playerStats.infiniteScore;
                const oldMaxScorePerGame = playerStats.maxScorePerGame;
                const oldMaxStarsCollected = playerStats.maxStarsCollected;
                
                playerStats.infiniteScore = Math.max(playerStats.infiniteScore, score);
                playerStats.maxScorePerGame = Math.max(playerStats.maxScorePerGame, score);
                playerStats.maxStarsCollected = Math.max(playerStats.maxStarsCollected, stars.length);
                
                // Сохраняем только если статистика изменилась
                if (oldInfiniteScore !== playerStats.infiniteScore || 
                    oldMaxScorePerGame !== playerStats.maxScorePerGame || 
                    oldMaxStarsCollected !== playerStats.maxStarsCollected) {
                    saveAchievements();
                }
            }
            
            checkAchievements();
        }

        // Переменные состояния
        let stars = [];
        let redStars = [];
        let score = 0;
        let gameActive = true;
        let isPaused = false;
        let collectedStars = [];
        let timerInterval = null;
        let timeLeft = INITIAL_TIME;
        let lastTime = Date.now();
        let audioUnlocked = false;
        let musicEnabled = true;
        
        // Переменные для босса
        let boss = null;
        let bossHealth = 50;
        let bossMaxHealth = 50;
        let redStarSpawnTimer = 0;
        
        // Режим игры: 'infinite' или 'campaign'
        let gameMode = null;
        let currentLevel = 0;
        let levelTarget = 0;

        // ------ Функции режимов ------
        function startInfiniteMode() {
            gameMode = 'infinite';
            levelSpan.style.display = 'none';
            bossHealthSpan.style.display = 'none';
            pauseLevel.style.display = 'none';
            tip.innerHTML = '🖱️ Кликай по звёздам  ✨ +1 очко  🌟 Макс. 25 звёзд  ⏳ +0.5 сек';
            resetGame();
        }

        function startCampaignMode() {
            gameMode = 'campaign';
            currentLevel = 0;
            levelSpan.style.display = 'inline-block';
            pauseLevel.style.display = 'block';
            startLevel(0);
        }

        function startLevel(levelIndex) {
            currentLevel = levelIndex;
            const level = CAMPAIGN_LEVELS[levelIndex];
            levelSpan.textContent = level.name;
            pauseLevelNum.textContent = levelIndex + 1;
            
            if (level.isBoss) {
                startBossLevel();
            } else {
                tip.innerHTML = `🎯 Цель: собрать ${level.target} ⭐  Время: ${level.time} сек`;
                boss = null;
                bossHealthSpan.style.display = 'none';
                stars = generateInitialStars(10);
                redStars = [];
                score = 0;
                gameActive = true;
                levelTarget = level.target;
                
                if (isPaused) closePauseMenu();
                
                updateScore();
                
                if (timerInterval) clearInterval(timerInterval);
                
                lastTime = Date.now();
                timeLeft = level.time;
                updateTimerBar();
                
                startTimer();
                tryPlayMusic();
            }
        }

        function startBossLevel() {
            bossHealthSpan.style.display = 'inline-block';
            bossHealth = 50;
            bossMaxHealth = 50;
            updateBossHealth();
            
            tip.innerHTML = `👾 БОСС: Инопланетная тарелка  🔫 Нужно попасть 50 раз!  🔴 Красные звезды (макс. 5) падают со скоростью 0.7 - уничтожай их!`;
            
            boss = {
                x: canvas.width / 2,
                y: 100,
                width: 120,
                height: 60,
                rotation: 0
            };
            
            stars = [];
            redStars = [];
            score = 0;
            gameActive = true;
            redStarSpawnTimer = 0;
            
            if (isPaused) closePauseMenu();
            
            updateScore();
            
            if (timerInterval) clearInterval(timerInterval);
            
            // Для босса таймер не используется
            timeLeft = 0;
            updateTimerBar();
            
            tryPlayMusic();
        }

        function updateBossHealth() {
            bossHealthSpan.textContent = `👾 Босс: ${bossHealth}`;
        }

        function checkCampaignProgress() {
            if (gameMode !== 'campaign' || !gameActive) return;
            
            const level = CAMPAIGN_LEVELS[currentLevel];
            
            if (level.isBoss) {
                if (bossHealth <= 0) {
                    // Победа над боссом
                    playerStats.bossDefeated = true;
                    gameActive = false;
                    clearInterval(timerInterval);
                    jazzAudio.pause();
                    saveAchievements();
                    showVictory('ПОБЕДА!', 'Вы победили босса!');
                    checkAchievements();
                }
                return;
            }
            
            if (score >= level.target) {
                // Победа на уровне
                gameActive = false;
                clearInterval(timerInterval);
                jazzAudio.pause();
                
                playerStats.completedLevels = Math.max(playerStats.completedLevels, currentLevel + 1);
                saveAchievements();
                checkAchievements();
                
                if (currentLevel < CAMPAIGN_LEVELS.length - 1) {
                    // Показываем окно продолжения
                    showLevelComplete(currentLevel + 1);
                } else {
                    showVictory('ПОБЕДА!', 'Вы прошли всю кампанию!');
                }
            }
        }

        function showLevelComplete(nextLevel) {
            levelCompleteMessage.textContent = `Переход на уровень ${nextLevel + 1}`;
            levelCompleteOverlay.style.display = 'flex';
            
            // Сохраняем следующий уровень
            continueButton.onclick = () => {
                levelCompleteOverlay.style.display = 'none';
                startLevel(nextLevel);
            };
        }

        function showVictory(title, message) {
            resultWindow.className = 'game-over-window victory';
            resultTitle.textContent = title;
            resultMessage.textContent = message;
            resultScore.textContent = score;
            resultOverlay.style.display = 'flex';
        }

        // ------ обновление статистики в меню паузы ------
        function updatePauseStats() {
            pauseScore.textContent = score;
            pauseStarsCount.textContent = stars.length + redStars.length;
        }

        // ------ открыть меню паузы ------
        function openPauseMenu() {
            if (!gameActive || isPaused) return;
            
            isPaused = true;
            updatePauseStats();
            pauseMenu.style.display = 'flex';
            pauseOverlay.style.display = 'flex';
            
            jazzAudio.pause();
            
            if (timerInterval) {
                clearInterval(timerInterval);
                timerInterval = null;
            }
        }

        // ------ закрыть меню паузы ------
        function closePauseMenu() {
            if (!isPaused) return;
            
            isPaused = false;
            pauseMenu.style.display = 'none';
            pauseOverlay.style.display = 'none';
            
            if (musicEnabled && audioUnlocked) {
                jazzAudio.play().catch(e => console.log('Не удалось возобновить музыку'));
            }
            
            if (gameActive) {
                if (timerInterval) {
                    lastTime = Date.now();
                    startTimer();
                }
            }
        }

        // ------ возврат в главное меню ------
        function returnToMainMenu() {
            if (timerInterval) clearInterval(timerInterval);
            jazzAudio.pause();
            gameActive = false;
            
            gameContainer.style.display = 'none';
            pauseMenu.style.display = 'none';
            pauseOverlay.style.display = 'none';
            resultOverlay.style.display = 'none';
            levelCompleteOverlay.style.display = 'none';
            achievementsMenu.style.display = 'none';
            
            mainMenu.style.display = 'flex';
        }

        // ------ добавление времени ------
        function addTime() {
            if (!gameActive || isPaused || !timerInterval) return;
            
            timeLeft = Math.min(MAX_TIME, timeLeft + TIME_BONUS);
            updateTimerBar();
            
            timerBar.style.transition = 'width 0.1s linear, background 0.3s';
            timerBar.style.background = 'linear-gradient(90deg, #44ff44, #88ff88)';
            setTimeout(() => updateTimerBar(), 300);
        }

        // ------ запуск таймера ------
        function startTimer() {
            if (timerInterval) clearInterval(timerInterval);
            
            timerInterval = setInterval(() => {
                if (!gameActive || isPaused) return;
                
                const now = Date.now();
                const delta = (now - lastTime) / 1000;
                lastTime = now;
                
                timeLeft = Math.max(0, timeLeft - delta);
                updateTimerBar();
                
                if (timeLeft <= 0) {
                    gameActive = false;
                    clearInterval(timerInterval);
                    jazzAudio.pause();
                    
                    if (gameMode === 'campaign') {
                        showDefeat('ВРЕМЯ ВЫШЛО', 'Попробуйте снова');
                    } else {
                        showDefeat('ВРЕМЯ ВЫШЛО', 'Начните новую игру');
                    }
                }
            }, 100);
        }

        function showDefeat(title, message) {
            resultWindow.className = 'game-over-window';
            resultTitle.textContent = title;
            resultMessage.textContent = message;
            resultScore.textContent = score;
            resultOverlay.style.display = 'flex';
        }

        // ------ обновление полосы таймера ------
        function updateTimerBar() {
            if (!timerInterval) {
                timerBar.style.width = '0%';
                return;
            }
            
            const maxTime = gameMode === 'campaign' && !CAMPAIGN_LEVELS[currentLevel].isBoss ? 
                CAMPAIGN_LEVELS[currentLevel].time : MAX_TIME;
            const percent = (timeLeft / maxTime) * 100;
            timerBar.style.width = percent + '%';
            
            timerBar.style.transition = 'width 0.1s linear';
            
            if (percent < 25) {
                timerBar.style.background = 'linear-gradient(90deg, #ff4444, #ff8888)';
            } else if (percent < 50) {
                timerBar.style.background = 'linear-gradient(90deg, #ffaa44, #ffcc88)';
            } else {
                timerBar.style.background = 'linear-gradient(90deg, #4a90e2, #a0c8ff)';
            }
        }

        // ------ генерация звезды ------
        function generateStar() {
            const minX = STAR_RADIUS + 5;
            const maxX = canvas.width - STAR_RADIUS - 5;
            const minY = STAR_RADIUS + 5;
            const maxY = canvas.height - STAR_RADIUS - 5;
            
            return {
                x: Math.floor(Math.random() * (maxX - minX + 1)) + minX,
                y: Math.floor(Math.random() * (maxY - minY + 1)) + minY,
                rotation: 0,
                pulse: 0,
                alpha: 0,
                spawnProgress: 0
            };
        }

        function generateRedStar() {
            const minX = RED_STAR_RADIUS + 5;
            const maxX = canvas.width - RED_STAR_RADIUS - 5;
            
            return {
                x: Math.floor(Math.random() * (maxX - minX + 1)) + minX,
                y: 50,
                rotation: 0,
                alpha: 1,
                speed: 0.7
            };
        }

        function generateInitialStars(count) {
            const newStars = [];
            for (let i = 0; i < count; i++) {
                const star = generateStar();
                star.alpha = 1;
                star.spawnProgress = 1;
                newStars.push(star);
            }
            return newStars;
        }

        function resetGame() {
            stars = generateInitialStars(10);
            redStars = [];
            score = 0;
            gameActive = true;
            boss = null;
            bossHealthSpan.style.display = 'none';
            
            if (isPaused) closePauseMenu();
            
            updateScore();
            
            if (timerInterval) clearInterval(timerInterval);
            
            lastTime = Date.now();
            timeLeft = gameMode === 'campaign' && !CAMPAIGN_LEVELS[currentLevel].isBoss ? 
                CAMPAIGN_LEVELS[currentLevel].time : INITIAL_TIME;
            updateTimerBar();
            
            if (gameMode !== 'campaign' || !CAMPAIGN_LEVELS[currentLevel].isBoss) {
                startTimer();
            }
            
            tryPlayMusic();
        }

        function updateScore() {
            scoreSpan.textContent = score + ' ⭐';
            if (gameMode === 'campaign') {
                checkCampaignProgress();
            } else {
                updateStats();
            }
        }

        function playSound(audioElement) {
            if (!audioUnlocked || !gameActive || isPaused) return;
            const soundClone = new Audio(audioElement.src);
            soundClone.volume = audioElement.volume;
            soundClone.play().catch(e => console.log('Не удалось воспроизвести звук'));
        }

        function playCoinSound(isRed) {
            playSound(isRed ? redCoinAudio : coinAudio);
        }

        function toggleMusic() {
            if (!audioUnlocked) unlockAudio();
            
            musicEnabled = !musicEnabled;
            
            if (musicEnabled && !isPaused && gameActive) {
                jazzAudio.play().catch(e => console.log('Не удалось запустить джаз'));
                musicToggle.textContent = '🔇 Джаз';
            } else {
                jazzAudio.pause();
                musicToggle.textContent = '🔊 Джаз';
            }
        }

        function unlockAudio() {
            if (audioUnlocked) return;
            
            const silentContext = new (window.AudioContext || window.webkitAudioContext)();
            silentContext.resume().then(() => console.log('Аудио контекст разблокирован'));
            
            coinAudio.volume = 0.01;
            coinAudio.play().then(() => {
                coinAudio.pause();
                coinAudio.currentTime = 0;
                coinAudio.volume = 1.0;
                audioUnlocked = true;
                console.log('Аудио разблокировано!');
                
                if (musicEnabled && !isPaused && gameActive) {
                    jazzAudio.play().catch(e => console.log('Не удалось запустить музыку'));
                }
            }).catch(e => {
                console.log('Не удалось разблокировать аудио');
                audioUnlocked = true;
            });
        }

        function spawnNewStar() {
            if (!gameActive || isPaused || boss) return;
            if (stars.length < MAX_STARS) {
                stars.push(generateStar());
            }
        }

        function handleCanvasClick(e) {
            if (!gameActive || isPaused) return;
            if (!audioUnlocked) unlockAudio();

            const rect = canvas.getBoundingClientRect();
            const scaleX = canvas.width / rect.width;
            const scaleY = canvas.height / rect.height;
            const mouseX = (e.clientX - rect.left) * scaleX;
            const mouseY = (e.clientY - rect.top) * scaleY;

            // Проверка клика по боссу
            if (boss) {
                const dx = mouseX - boss.x;
                const dy = mouseY - boss.y;
                if (Math.abs(dx) < boss.width/2 && Math.abs(dy) < boss.height/2) {
                    playCoinSound(false);
                    bossHealth--;
                    updateBossHealth();
                    checkCampaignProgress();
                    return;
                }
            }

            // Проверка клика по красным звездам
            for (let i = redStars.length - 1; i >= 0; i--) {
                const star = redStars[i];
                const dx = mouseX - star.x;
                const dy = mouseY - star.y;
                const dist = Math.sqrt(dx*dx + dy*dy);

                if (dist <= RED_STAR_RADIUS) {
                    playCoinSound(true);
                    redStars.splice(i, 1);
                    return;
                }
            }

            // Проверка клика по обычным звездам
            for (let i = stars.length - 1; i >= 0; i--) {
                const star = stars[i];
                if (star.alpha < 0.5) continue;
                
                const dx = mouseX - star.x;
                const dy = mouseY - star.y;
                const dist = Math.sqrt(dx*dx + dy*dy);

                if (dist <= STAR_RADIUS) {
                    playCoinSound(false);
                    
                    collectedStars.push({
                        x: star.x, y: star.y,
                        rotation: 0, scale: 1, alpha: 1,
                        speed: 0.2 + Math.random() * 0.2
                    });
                    
                    stars.splice(i, 1);
                    score++;
                    updateScore();
                    addTime();
                    
                    setTimeout(() => spawnNewStar(), SPAWN_DELAY);
                    break;
                }
            }
        }

        function updateVolume() {
            jazzAudio.volume = parseFloat(volumeSlider.value);
        }

        // ------ отрисовка босса ------
        function drawBoss() {
            if (!boss) return;
            
            boss.rotation += 0.002;
            
            ctx.save();
            ctx.translate(boss.x, boss.y);
            ctx.rotate(Math.sin(boss.rotation) * 0.05);
            
            ctx.shadowColor = '#44aaff';
            ctx.shadowBlur = 30;
            
            ctx.fillStyle = '#446688';
            ctx.beginPath();
            ctx.ellipse(0, 10, 70, 30, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#88aadd';
            ctx.beginPath();
            ctx.ellipse(0, -10, 50, 25, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#ffaa44';
            ctx.shadowColor = '#ffaa44';
            for (let i = -2; i <= 2; i++) {
                if (i === 0) continue;
                ctx.beginPath();
                ctx.arc(i * 25, 15, 5, 0, Math.PI * 2);
                ctx.fill();
            }
            
            ctx.strokeStyle = '#aaccff';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(20, -25);
            ctx.lineTo(35, -40);
            ctx.stroke();
            
            ctx.beginPath();
            ctx.arc(38, -43, 5, 0, Math.PI * 2);
            ctx.fillStyle = '#ffaa44';
            ctx.fill();
            
            ctx.restore();
        }

        function drawRedStar(star) {
            ctx.save();
            ctx.translate(star.x, star.y);
            ctx.rotate(star.rotation);
            ctx.globalAlpha = star.alpha;
            
            ctx.shadowColor = '#ff4444';
            ctx.shadowBlur = 20;
            
            ctx.beginPath();
            for (let i = 0; i < 10; i++) {
                const radius = i % 2 === 0 ? RED_STAR_RADIUS : RED_STAR_RADIUS * 0.4;
                const angle = (Math.PI / 5) * i - Math.PI / 2;
                const x = Math.cos(angle) * radius;
                const y = Math.sin(angle) * radius;
                
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            ctx.closePath();
            
            const gradient = ctx.createRadialGradient(-3, -3, 3, 0, 0, RED_STAR_RADIUS);
            gradient.addColorStop(0, '#ffaaaa');
            gradient.addColorStop(0.5, '#ff4444');
            gradient.addColorStop(1, '#aa2222');
            
            ctx.fillStyle = gradient;
            ctx.fill();
            
            ctx.restore();
        }

        function drawStar(star) {
            const points = 5;
            const outerRadius = STAR_RADIUS;
            const innerRadius = STAR_RADIUS * 0.4;
            const pulseScale = 1 + Math.sin(star.pulse) * 0.03;
            
            ctx.save();
            ctx.translate(star.x, star.y);
            ctx.rotate(star.rotation);
            ctx.scale(pulseScale, pulseScale);
            ctx.globalAlpha = star.alpha;
            
            ctx.shadowColor = '#fff7b0';
            ctx.shadowBlur = 25;
            
            ctx.beginPath();
            for (let i = 0; i < points * 2; i++) {
                const radius = i % 2 === 0 ? outerRadius : innerRadius;
                const angle = (Math.PI / points) * i - Math.PI / 2;
                const x = Math.cos(angle) * radius;
                const y = Math.sin(angle) * radius;
                
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            ctx.closePath();
            
            const gradient = ctx.createRadialGradient(-5, -5, 5, 0, 0, outerRadius);
            gradient.addColorStop(0, '#fffde0');
            gradient.addColorStop(0.4, '#ffd966');
            gradient.addColorStop(0.8, '#f5b542');
            gradient.addColorStop(1, '#d48d2b');
            
            ctx.fillStyle = gradient;
            ctx.fill();
            
            ctx.shadowBlur = 15;
            ctx.strokeStyle = '#fff2b0';
            ctx.lineWidth = 2;
            ctx.stroke();
            
            ctx.restore();
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = '#5f4f6f';
            ctx.globalAlpha = 0.2;
            ctx.beginPath();
            for (let i = 0; i < 5; i++) {
                ctx.ellipse(150 + i*170, 470, 130, 25, 0, 0, Math.PI*2);
            }
            ctx.fill();
            ctx.globalAlpha = 1.0;

            for (let star of stars) {
                if (star.alpha < 1) {
                    star.spawnProgress = Math.min(1, star.spawnProgress + 0.01);
                    star.alpha = Math.min(1, star.alpha + 0.02);
                }
                star.pulse = (star.pulse + 0.02) % (Math.PI * 2);
                drawStar(star);
            }

            for (let star of redStars) {
                star.rotation += 0.02;
                drawRedStar(star);
            }

            drawBoss();

            for (let i = collectedStars.length - 1; i >= 0; i--) {
                const star = collectedStars[i];
                star.rotation += star.speed;
                star.scale *= 0.97;
                star.alpha *= 0.96;
                
                ctx.save();
                ctx.translate(star.x, star.y);
                ctx.rotate(star.rotation);
                ctx.scale(star.scale, star.scale);
                ctx.globalAlpha = star.alpha;
                
                ctx.shadowColor = '#fff5d0';
                ctx.shadowBlur = 20;
                
                const gradient = ctx.createRadialGradient(-5, -5, 5, 0, 0, STAR_RADIUS);
                gradient.addColorStop(0, '#fffdd0');
                gradient.addColorStop(0.5, '#ffe066');
                gradient.addColorStop(1, '#ffaa33');
                
                ctx.beginPath();
                for (let j = 0; j < 10; j++) {
                    const radius = j % 2 === 0 ? STAR_RADIUS * 0.8 : STAR_RADIUS * 0.3;
                    const angle = (Math.PI / 5) * j - Math.PI / 2;
                    const x = Math.cos(angle) * radius;
                    const y = Math.sin(angle) * radius;
                    if (j === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                }
                ctx.closePath();
                ctx.fillStyle = gradient;
                ctx.fill();
                
                ctx.restore();
                
                if (star.alpha < 0.02 || star.scale < 0.02) {
                    collectedStars.splice(i, 1);
                }
            }

            ctx.shadowBlur = 0;
            ctx.shadowColor = 'transparent';
            ctx.globalAlpha = 1.0;

            ctx.font = '18px "Segoe UI", monospace';
            ctx.fillStyle = '#e6d0ff';
            ctx.shadowBlur = 8;
            ctx.shadowColor = '#1b1a55';
            
            if (boss) {
                ctx.fillText('👾 Здоровье босса: ' + bossHealth + '/' + bossMaxHealth, 450, 70);
            } else {
                ctx.fillText('⭐ ' + stars.length + '/' + MAX_STARS, 650, 70);
                
                if (gameMode === 'campaign' && !CAMPAIGN_LEVELS[currentLevel].isBoss) {
                    const level = CAMPAIGN_LEVELS[currentLevel];
                    ctx.fillText('🎯 ' + score + '/' + level.target, 500, 70);
                }
            }
            
            ctx.shadowBlur = 0;
        }

        function updateBossLevel() {
            if (!boss || !gameActive || isPaused) return;
            
            redStarSpawnTimer++;
            if (redStarSpawnTimer > 40) {
                redStarSpawnTimer = 0;
                if (redStars.length < 5) {
                    redStars.push(generateRedStar());
                }
            }
            
            for (let i = redStars.length - 1; i >= 0; i--) {
                const star = redStars[i];
                star.y += star.speed;
                
                if (star.y > canvas.height - RED_STAR_RADIUS) {
                    gameActive = false;
                    jazzAudio.pause();
                    showDefeat('ПОРАЖЕНИЕ', 'Красная звезда достигла земли!');
                    return;
                }
            }
        }

        function animate() {
            if (!isPaused && gameActive) {
                if (boss) {
                    updateBossLevel();
                }
                
                for (let star of stars) {
                    star.rotation += 0.001;
                }
                
                draw();
            } else {
                draw();
            }
            requestAnimationFrame(animate);
        }

        // ------ инициализация ------
        function init() {
            animate();

            // Обработчики главного меню
            infiniteModeBtn.addEventListener('click', () => {
                mainMenu.style.display = 'none';
                gameContainer.style.display = 'block';
                startInfiniteMode();
            });
            
            campaignModeBtn.addEventListener('click', () => {
                mainMenu.style.display = 'none';
                gameContainer.style.display = 'block';
                startCampaignMode();
            });
            
            achievementsMenuBtn.addEventListener('click', () => {
                mainMenu.style.display = 'none';
                achievementsMenu.style.display = 'flex';
                renderAchievements();
            });
            
            closeAchievementsBtn.addEventListener('click', () => {
                achievementsMenu.style.display = 'none';
                mainMenu.style.display = 'flex';
            });

            // Игровые обработчики
            canvas.addEventListener('click', handleCanvasClick);
            resetButton.addEventListener('click', resetGame);
            menuButton.addEventListener('click', returnToMainMenu);
            canvas.addEventListener('contextmenu', (e) => e.preventDefault());
            
            musicToggle.addEventListener('click', toggleMusic);
            
            pauseButton.addEventListener('click', openPauseMenu);
            resumeButton.addEventListener('click', closePauseMenu);
            
            pauseResetButton.addEventListener('click', () => {
                closePauseMenu();
                resetGame();
            });
            
            pauseToMenuButton.addEventListener('click', () => {
                closePauseMenu();
                returnToMainMenu();
            });
            
            resultRestart.addEventListener('click', () => {
                resultOverlay.style.display = 'none';
                if (gameMode === 'campaign') {
                    if (CAMPAIGN_LEVELS[currentLevel].isBoss) {
                        startBossLevel();
                    } else {
                        startLevel(currentLevel);
                    }
                } else {
                    resetGame();
                }
            });
            
            resultToMenu.addEventListener('click', () => {
                resultOverlay.style.display = 'none';
                returnToMainMenu();
            });
            
            canvas.addEventListener('mouseenter', function tryUnlock() {
                if (!audioUnlocked) unlockAudio();
            }, { once: true });
            
            document.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') {
                    if (mainMenu.style.display === 'flex') return;
                    if (achievementsMenu.style.display === 'flex') {
                        achievementsMenu.style.display = 'none';
                        mainMenu.style.display = 'flex';
                        return;
                    }
                    if (isPaused) {
                        closePauseMenu();
                    } else if (gameActive && resultOverlay.style.display !== 'flex' && levelCompleteOverlay.style.display !== 'flex') {
                        openPauseMenu();
                    }
                }
            });
            
            volumeSlider.addEventListener('input', updateVolume);
            
            document.addEventListener('click', function unlockOnFirstClick() {
                unlockAudio();
                document.removeEventListener('click', unlockOnFirstClick);
            }, { once: true });
        }

        window.addEventListener('load', init);
    })();
</script>
</body>
</html>
