<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⭐ Звездная коллекция: Метеоритная атака</title>
    <style>
        * {
            box-sizing: border-box;
            user-select: none;
        }

        body {
            margin: 0;
            min-height: 100vh;
            background: linear-gradient(145deg, #1a0f2a 0%, #0a0515 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            overflow: hidden;
        }

        .game-container {
            background: #3a3155;
            padding: 25px 30px 30px;
            border-radius: 48px;
            box-shadow: 0 25px 35px rgba(0,0,0,0.6), inset 0 1px 4px rgba(255,220,200,0.2);
            border: 1px solid #9f7f94;
            position: relative;
            z-index: 10;
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

        .meteor-timer-box {
            background: #8b0000;
            border-radius: 40px;
            padding: 10px 25px;
            font-size: 22px;
            font-weight: 700;
            color: #ffaa00;
            box-shadow: inset 0 -3px 0 #5a0000, 0 0 20px #ff0000;
            border-bottom: 2px solid #ffaa00;
            display: none;
            animation: pulseRed 1s infinite;
        }

        @keyframes pulseRed {
            0% { box-shadow: 0 0 20px #ff0000; }
            50% { box-shadow: 0 0 40px #ff0000; }
            100% { box-shadow: 0 0 20px #ff0000; }
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
            background: transparent;
            border-radius: 36px;
            border: 5px solid #bb8b7b;
            box-shadow: inset 0 0 0 2px #e2bf9f, 0 20px 25px #0d0a24;
            width: 800px;
            height: 500px;
            cursor: pointer;
            position: relative;
            z-index: 20;
            transition: all 0.3s ease;
        }

        .canvas-meteor-active {
            border-color: #ff0000 !important;
            box-shadow: 0 0 30px #ff0000, inset 0 0 30px #ff0000 !important;
            animation: screenShake 0.1s infinite;
        }

        @keyframes screenShake {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(3px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(3px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(1px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
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

        /* Анимированный фон */
        .background-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }

        .star-bg {
            position: absolute;
            background: white;
            border-radius: 50%;
            box-shadow: 0 0 10px white;
            animation: float linear infinite;
        }

        @keyframes float {
            from {
                transform: translateY(100vh) rotate(0deg);
            }
            to {
                transform: translateY(-100px) rotate(360deg);
            }
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

        /* Меню кликера - улучшенный дизайн */
        .clicker-menu {
            background: #0f1e2f;
            border: 4px solid #ffaa44;
            border-radius: 50px;
            padding: 30px 50px;
            box-shadow: 0 30px 50px rgba(0,0,0,0.8), inset 0 0 30px rgba(255, 170, 68, 0.2);
            text-align: center;
            max-width: 1100px;
            max-height: 85vh;
            overflow-y: auto;
            backdrop-filter: blur(10px);
            animation: menuGlow 3s infinite alternate;
        }

        @keyframes menuGlow {
            0% { box-shadow: 0 30px 50px rgba(0,0,0,0.8), inset 0 0 30px rgba(255, 170, 68, 0.2); }
            100% { box-shadow: 0 30px 70px rgba(255, 170, 68, 0.4), inset 0 0 50px rgba(255, 215, 0, 0.3); }
        }

        .clicker-menu h2 {
            color: #ffddaa;
            font-size: 48px;
            margin: 0 0 15px 0;
            text-shadow: 0 0 20px #ffaa44, 0 0 40px #ffaa44;
            letter-spacing: 2px;
        }

        .clicker-stats {
            background: linear-gradient(145deg, #1e2a3a, #0f1a2a);
            border-radius: 40px;
            padding: 15px 30px;
            margin: 15px 0;
            border: 2px solid #ffaa44;
            display: flex;
            justify-content: space-around;
            box-shadow: 0 0 20px rgba(255, 170, 68, 0.3);
        }

        .clicker-stats p {
            color: #e0d0ff;
            font-size: 24px;
            margin: 5px 0;
        }

        .clicker-stats span {
            color: #ffddaa;
            font-weight: bold;
            font-size: 32px;
            text-shadow: 0 0 10px #ffaa44;
        }

        .clicker-content {
            display: flex;
            gap: 30px;
            margin: 20px 0;
            flex-wrap: wrap;
            justify-content: center;
        }

        .clicker-left {
            flex: 2;
            min-width: 350px;
            background: linear-gradient(145deg, #1a2a3a, #0a1a2a);
            border-radius: 40px;
            padding: 25px;
            border: 2px solid #7a6a9f;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
        }

        .clicker-right {
            flex: 3;
            min-width: 400px;
            background: linear-gradient(145deg, #1a2a3a, #0a1a2a);
            border-radius: 40px;
            padding: 25px;
            border: 2px solid #7a6a9f;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
        }

        .clicker-star-container {
            position: relative;
            width: 200px;
            height: 200px;
            margin: 20px auto;
        }

        .heat-bar {
            position: absolute;
            top: -25px;
            left: 0;
            width: 100%;
            height: 12px;
            background: #2a1e2a;
            border-radius: 10px;
            overflow: hidden;
            border: 2px solid #ffaa44;
            box-shadow: 0 0 15px #ffaa44;
        }

        .heat-fill {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #00ffaa, #ffff44, #ff4444);
            transition: width 0.1s linear;
            box-shadow: 0 0 20px #ffaa00;
        }

        .clicker-star {
            width: 200px;
            height: 200px;
            cursor: pointer;
            transition: transform 0.1s ease, filter 0.2s ease;
            filter: drop-shadow(0 0 30px #ffaa44);
            position: relative;
            animation: starFloat 3s infinite alternate;
        }

        @keyframes starFloat {
            0% { transform: translateY(0); }
            100% { transform: translateY(-10px); }
        }

        .clicker-star:active {
            transform: scale(0.95) translateY(-5px);
        }

        .clicker-star.overheated {
            filter: drop-shadow(0 0 40px #ff4444) drop-shadow(0 0 80px #ff0000);
            animation: starShake 0.2s infinite;
        }

        @keyframes starShake {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(5deg); }
            75% { transform: rotate(-5deg); }
            100% { transform: rotate(0deg); }
        }

        .clicker-star svg {
            width: 100%;
            height: 100%;
            transition: all 0.2s ease;
        }

        /* Пульсирующий эффект при клике */
        .clicker-star.pulse {
            animation: starPulse 0.2s ease;
        }

        @keyframes starPulse {
            0% { transform: scale(1) translateY(0); filter: drop-shadow(0 0 30px #ffaa44); }
            50% { transform: scale(1.2) translateY(-15px); filter: drop-shadow(0 0 60px #ffaa00); }
            100% { transform: scale(1) translateY(0); filter: drop-shadow(0 0 30px #ffaa44); }
        }

        .click-power-display {
            font-size: 24px;
            color: #ffddaa;
            margin: 15px 0;
            text-align: center;
            background: #1e2a3a;
            padding: 10px;
            border-radius: 30px;
            border: 2px solid #ffaa44;
            display: inline-block;
            width: 100%;
        }

        .click-power-display span {
            color: #4a90e2;
            font-weight: bold;
            font-size: 28px;
        }

        /* Упрощенная рулетка - круг с 4 зонами разных размеров */
        .roulette-container {
            background: linear-gradient(145deg, #1e2a3a, #0f1a2a);
            border: 3px solid #4a90e2;
            border-radius: 40px;
            padding: 25px;
            margin: 15px 0;
            box-shadow: 0 0 30px rgba(74, 144, 226, 0.5);
            position: relative;
        }

        .roulette-container h3 {
            color: #4a90e2;
            font-size: 28px;
            margin: 0 0 20px 0;
            text-shadow: 0 0 15px rgba(74, 144, 226, 0.8);
        }

        .wheel-simple {
            width: 220px;
            height: 220px;
            margin: 0 auto 20px;
            position: relative;
            cursor: pointer;
            border-radius: 50%;
            background: #1a2a3a;
            border: 4px solid #4a90e2;
            box-shadow: 0 0 30px rgba(74, 144, 226, 0.5);
            transition: transform 0.3s ease;
            overflow: hidden;
        }

        .wheel-simple:active {
            transform: scale(0.95);
        }

        /* Сектора рулетки с разными размерами */
        .wheel-segment {
            position: absolute;
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
            clip-path: polygon(50% 50%, 50% 0%, var(--x1) 0%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            font-weight: bold;
            color: white;
            text-shadow: 0 0 10px black;
        }

        /* Синий сектор (10⭐) - самый большой - 40% */
        .segment-0 {
            background: linear-gradient(135deg, #4a90e2, #1a4a8a);
            --x1: 100%;
            transform: rotate(0deg);
            clip-path: polygon(50% 50%, 50% 0%, 100% 0%);
        }

        /* Красный сектор (50⭐) - средний - 30% */
        .segment-2 {
            background: linear-gradient(135deg, #ff4444, #aa2222);
            --x1: 70%;
            transform: rotate(144deg);
            clip-path: polygon(50% 50%, 50% 0%, 70% 0%);
        }

        /* Желтый сектор (100⭐) - меньше красного - 20% */
        .segment-1 {
            background: linear-gradient(135deg, #ffaa00, #aa5500);
            --x1: 50%;
            transform: rotate(252deg);
            clip-path: polygon(50% 50%, 50% 0%, 50% 0%);
        }

        /* Фиолетовый сектор (500⭐) - самый маленький - 10% */
        .segment-3 {
            background: linear-gradient(135deg, #9b59b6, #4a1e6a);
            --x1: 30%;
            transform: rotate(324deg);
            clip-path: polygon(50% 50%, 50% 0%, 30% 0%);
        }

        /* Текстовые метки для секторов */
        .segment-text {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            transform: rotate(var(--rot)) translate(70px, 0);
            font-size: 16px;
            text-align: center;
            white-space: nowrap;
        }

        .segment-0 .segment-text {
            --rot: 20deg;
        }
        .segment-1 .segment-text {
            --rot: 70deg;
        }
        .segment-2 .segment-text {
            --rot: 130deg;
        }
        .segment-3 .segment-text {
            --rot: 190deg;
        }

        .wheel-arrow {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 15px solid transparent;
            border-right: 15px solid transparent;
            border-top: 25px solid #4a90e2;
            filter: drop-shadow(0 0 10px #4a90e2);
            z-index: 10;
            pointer-events: none;
        }

        .wheel-arrow::after {
            content: '';
            position: absolute;
            top: -30px;
            left: -5px;
            width: 10px;
            height: 10px;
            background: #4a90e2;
            border-radius: 50%;
            box-shadow: 0 0 15px #4a90e2;
        }

        .roulette-result {
            background: linear-gradient(145deg, #2a3a4a, #1a2a3a);
            border: 2px solid #4a90e2;
            border-radius: 30px;
            padding: 12px 20px;
            margin: 15px 0;
            font-size: 22px;
            color: #4a90e2;
            text-shadow: 0 0 10px rgba(74, 144, 226, 0.5);
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.5);
        }

        .roulette-result span {
            color: #fff;
            font-weight: bold;
        }

        .roulette-probabilities {
            font-size: 15px;
            color: #aac8ff;
            margin-top: 15px;
            text-align: left;
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 20px;
            border: 1px solid #4a90e2;
        }

        .upgrades-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin: 15px 0;
            max-height: 300px;
            overflow-y: auto;
            padding-right: 5px;
        }

        .upgrades-grid::-webkit-scrollbar {
            width: 8px;
        }

        .upgrades-grid::-webkit-scrollbar-track {
            background: #1e2a3a;
            border-radius: 10px;
        }

        .upgrades-grid::-webkit-scrollbar-thumb {
            background: #ffaa44;
            border-radius: 10px;
        }

        .upgrade-card {
            background: linear-gradient(145deg, #1e2a3a, #0f1a2a);
            border: 2px solid #7a6a9f;
            border-radius: 25px;
            padding: 12px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.2s ease;
            box-shadow: 0 4px 0 #2a1e4a;
        }

        .upgrade-card:hover {
            border-color: #ffaa44;
            background: #2a3a4a;
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #2a1e4a;
        }

        .upgrade-info {
            text-align: left;
        }

        .upgrade-info h3 {
            color: #ffddaa;
            font-size: 20px;
            margin: 0 0 3px 0;
        }

        .upgrade-info p {
            color: #aac8ff;
            font-size: 14px;
            margin: 0;
        }

        .upgrade-cost {
            background: #4a3f6a;
            border: 2px solid #ffaa44;
            border-radius: 25px;
            padding: 8px 20px;
            font-size: 20px;
            font-weight: bold;
            color: #ffddaa;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 0 #2a1e4a;
        }

        .upgrade-cost:hover {
            background: #5a4f8a;
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #2a1e4a;
        }

        .upgrade-cost:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        .upgrade-cost.disabled {
            opacity: 0.5;
            cursor: not-allowed;
            pointer-events: none;
        }

        .clicker-buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 20px;
        }

        .clicker-btn {
            background: #4a3f6a;
            border: 2px solid #9f8ac0;
            border-radius: 35px;
            padding: 12px 35px;
            font-size: 22px;
            color: #f0e0ff;
            cursor: pointer;
            box-shadow: 0 6px 0 #2a1e4a;
        }

        .clicker-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 0 #2a1e4a;
        }

        .clicker-btn:active {
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

        /* Новая фишка: счетчик комбо */
        .combo-counter {
            position: absolute;
            top: 10px;
            right: 20px;
            background: #1e2a3a;
            border: 2px solid #ffaa44;
            border-radius: 30px;
            padding: 10px 20px;
            color: #ffddaa;
            font-size: 20px;
            font-weight: bold;
            box-shadow: 0 0 20px #ffaa44;
            display: flex;
            align-items: center;
            gap: 5px;
            z-index: 100;
        }

        .combo-counter span {
            color: #ff4444;
            font-size: 24px;
            margin-left: 5px;
        }

        /* Затемнение во время метеорита */
        .meteor-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 0, 0, 0.2);
            pointer-events: none;
            z-index: 500;
            display: none;
            animation: meteorPulse 2s infinite;
        }

        @keyframes meteorPulse {
            0% { background: rgba(255, 0, 0, 0.1); }
            50% { background: rgba(255, 0, 0, 0.3); }
            100% { background: rgba(255, 0, 0, 0.1); }
        }
    </style>
</head>
<body>
<!-- Анимированный фон -->
<div class="background-animation" id="bgAnimation"></div>

<!-- Затемнение метеорита -->
<div class="meteor-overlay" id="meteorOverlay"></div>

<!-- Главное меню -->
<div class="overlay" id="mainMenu" style="display: flex;">
    <div class="main-menu">
        <h1>⭐ ЗВЕЗДНАЯ ЛЕГЕНДА</h1>
        <div class="menu-buttons">
            <button class="menu-btn" id="infiniteModeBtn">♾️ Бесконечный режим</button>
            <button class="menu-btn" id="campaignModeBtn">📜 Кампания</button>
            <button class="menu-btn" id="clickerModeBtn">🖱️ Мега Кликер</button>
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

<!-- Меню кликера -->
<div class="overlay" id="clickerMenu" style="display: none;">
    <div class="clicker-menu">
        <h2>🖱️ МЕГА ЗВЕЗДНЫЙ КЛИКЕР</h2>
        <div class="clicker-stats">
            <p>⭐ Баллы: <span id="clickerPoints">0</span></p>
            <p>🖱️ Кликов: <span id="clickerClicks">0</span></p>
            <p>🔥 Перегрев: <span id="heatPercent">0%</span></p>
        </div>
        
        <!-- Счетчик комбо -->
        <div class="combo-counter" id="comboCounter">
            🔥 Комбо: <span id="comboValue">x1</span>
        </div>
        
        <div class="clicker-content">
            <div class="clicker-left">
                <div class="clicker-star-container">
                    <div class="heat-bar">
                        <div class="heat-fill" id="heatFill"></div>
                    </div>
                    <div class="clicker-star" id="clickerStar">
                        <svg viewBox="0 0 100 100" id="starSvg">
                            <defs>
                                <radialGradient id="starGradient" cx="30%" cy="30%" r="70%">
                                    <stop offset="0%" stop-color="#fffde0"/>
                                    <stop offset="50%" stop-color="#ffd966"/>
                                    <stop offset="100%" stop-color="#f5b542"/>
                                </radialGradient>
                                <radialGradient id="hotStarGradient" cx="30%" cy="30%" r="70%">
                                    <stop offset="0%" stop-color="#ffaa00"/>
                                    <stop offset="50%" stop-color="#ff4444"/>
                                    <stop offset="100%" stop-color="#aa2222"/>
                                </radialGradient>
                                <filter id="glow">
                                    <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
                                    <feMerge>
                                        <feMergeNode in="coloredBlur"/>
                                        <feMergeNode in="SourceGraphic"/>
                                    </feMerge>
                                </filter>
                            </defs>
                            <path d="M50 5 L63 38 L98 38 L69 57 L82 92 L50 72 L18 92 L31 57 L2 38 L37 38 Z" 
                                  fill="url(#starGradient)" 
                                  stroke="#fff2b0" 
                                  stroke-width="2"
                                  filter="url(#glow)"/>
                        </svg>
                    </div>
                </div>
                
                <div class="click-power-display">
                    ⚡ Сила клика: <span id="clickPowerValue">1</span>
                </div>
                
                <h3 style="color: #ffddaa; font-size: 28px; margin: 15px 0;">⚙️ УЛУЧШЕНИЯ</h3>
                <div class="upgrades-grid" id="upgradesGrid">
                    <!-- Улучшения будут добавляться динамически -->
                </div>
            </div>
            
            <div class="clicker-right">
                <div class="roulette-container">
                    <h3>🎰 РУЛЕТКА С ШАНСАМИ</h3>
                    <div style="position: relative; width: 220px; margin: 0 auto;">
                        <div class="wheel-simple" id="simpleWheel">
                            <div class="wheel-segment segment-0">
                                <span class="segment-text">10⭐</span>
                            </div>
                            <div class="wheel-segment segment-1">
                                <span class="segment-text">100⭐</span>
                            </div>
                            <div class="wheel-segment segment-2">
                                <span class="segment-text">50⭐</span>
                            </div>
                            <div class="wheel-segment segment-3">
                                <span class="segment-text">500⭐</span>
                            </div>
                        </div>
                        <div class="wheel-arrow"></div>
                    </div>
                    <div class="roulette-result" id="simpleRouletteResult">
                        🎲 Нажми на круг!
                    </div>
                    <div class="roulette-probabilities">
                        🎰 Шансы (разные размеры секторов):<br>
                        <span style="color: #4a90e2">🔵 Синий (10⭐) - 40%</span><br>
                        <span style="color: #ff4444">🔴 Красный (50⭐) - 30%</span><br>
                        <span style="color: #ffaa00">🟡 Желтый (100⭐) - 20%</span><br>
                        <span style="color: #9b59b6">💜 Фиолетовый (500⭐) - 10%</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="clicker-buttons">
            <button class="clicker-btn" id="resetClickerBtn">🔄 Сбросить</button>
            <button class="clicker-btn" id="pauseClickerBtn">⏸️ Пауза</button>
            <button class="clicker-btn" id="closeClickerBtn">🔙 Назад</button>
        </div>
    </div>
</div>

<!-- Меню паузы для кликера -->
<div class="overlay" id="clickerPauseMenu" style="display: none;">
    <div class="pause-menu">
        <h2>⏸️ ПАУЗА</h2>
        <div class="pause-stats">
            <p>⭐ Баллы: <span id="clickerPausePoints">0</span></p>
            <p>🖱️ Кликов: <span id="clickerPauseClicks">0</span></p>
        </div>
        
        <div class="volume-control">
            <label>🎵 Выберите музыку:</label>
            <select id="clickerMusicSelect" style="width: 100%; padding: 10px; border-radius: 20px; background: #2a3f5a; color: #ffddaa; border: 2px solid #ffaa44;">
                <option value="menu">🏠 Музыка меню</option>
                <option value="clicker">🎮 Музыка кликера</option>
                <option value="campaign">📜 Музыка кампании</option>
                <option value="infinite">♾️ Музыка бесконечного режима</option>
                <option value="silent">🔇 Без музыки</option>
            </select>
        </div>
        
        <div class="volume-control">
            <label>🎵 Громкость музыки</label>
            <input type="range" id="clickerVolumeSlider" class="volume-slider" min="0" max="1" step="0.01" value="0.25">
        </div>
        
        <div class="pause-buttons">
            <button class="pause-btn resume-btn" id="resumeClickerBtn">▶ Продолжить</button>
            <button class="pause-btn main-menu-btn" id="clickerToMenuBtn">🏠 В меню</button>
            <button class="pause-btn" id="resetFromPauseBtn">↻ Новая игра</button>
        </div>
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
        <div style="display: flex; gap: 20px; align-items: center;">
            <span class="score-box" id="scoreDisplay">0 ⭐</span>
            <span class="level-box" id="levelDisplay" style="display: none;">Уровень 1</span>
            <span class="boss-health-box" id="bossHealthDisplay" style="display: none;">👾 Босс: 50</span>
            <span class="meteor-timer-box" id="meteorTimer">☄️ Атака!</span>
        </div>
        <div style="display: flex; gap: 10px;">
            <button id="menuButton" class="menu-toggle">🏠 Меню</button>
            <button id="pauseButton" class="pause-toggle">⏸️ Пауза</button>
            <button id="resetButton">⟳ Новая игра</button>
            <button id="musicToggle" class="music-toggle">🔊 Музыка</button>
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

<!-- Меню паузы для основной игры -->
<div class="overlay" id="pauseMenu" style="background: rgba(0,0,0,0.6); display: none;">
    <div class="pause-menu">
        <h2>⏸️ ПАУЗА</h2>
        <div class="pause-stats">
            <p>Собрано звёзд: <span id="pauseScore">0</span></p>
            <p>Звёзд на поле: <span id="pauseStarsCount">0</span>/25</p>
            <p id="pauseLevel" style="display: none;">Уровень: <span id="pauseLevelNum">1</span></p>
        </div>
        
        <div class="volume-control">
            <label>🎵 Выберите музыку:</label>
            <select id="musicSelect" style="width: 100%; padding: 10px; border-radius: 20px; background: #2a3f5a; color: #ffddaa; border: 2px solid #ffaa44;">
                <option value="menu">🏠 Музыка меню</option>
                <option value="campaign">📜 Музыка кампании</option>
                <option value="infinite">♾️ Музыка бесконечного режима</option>
                <option value="clicker">🖱️ Музыка кликера</option>
                <option value="silent">🔇 Без музыки</option>
            </select>
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
        const meteorTimerSpan = document.getElementById('meteorTimer');
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
        const musicSelect = document.getElementById('musicSelect');
        const tip = document.getElementById('tip');
        const meteorOverlay = document.getElementById('meteorOverlay');
        
        // Элементы меню
        const mainMenu = document.getElementById('mainMenu');
        const gameContainer = document.getElementById('gameContainer');
        const infiniteModeBtn = document.getElementById('infiniteModeBtn');
        const campaignModeBtn = document.getElementById('campaignModeBtn');
        const clickerModeBtn = document.getElementById('clickerModeBtn');
        const achievementsMenuBtn = document.getElementById('achievementsMenuBtn');
        const achievementsMenu = document.getElementById('achievementsMenu');
        const closeAchievementsBtn = document.getElementById('closeAchievementsBtn');
        const achievementsGrid = document.getElementById('achievementsGrid');
        
        // Элементы кликера
        const clickerMenu = document.getElementById('clickerMenu');
        const clickerStar = document.getElementById('clickerStar');
        const clickerPoints = document.getElementById('clickerPoints');
        const clickerClicks = document.getElementById('clickerClicks');
        const heatPercent = document.getElementById('heatPercent');
        const upgradesGrid = document.getElementById('upgradesGrid');
        const resetClickerBtn = document.getElementById('resetClickerBtn');
        const pauseClickerBtn = document.getElementById('pauseClickerBtn');
        const closeClickerBtn = document.getElementById('closeClickerBtn');
        const heatFill = document.getElementById('heatFill');
        const starSvg = document.getElementById('starSvg');
        const clickPowerValue = document.getElementById('clickPowerValue');
        const comboCounter = document.getElementById('comboCounter');
        const comboValue = document.getElementById('comboValue');
        
        // Элементы упрощенной рулетки
        const simpleWheel = document.getElementById('simpleWheel');
        const simpleRouletteResult = document.getElementById('simpleRouletteResult');
        
        // Элементы паузы кликера
        const clickerPauseMenu = document.getElementById('clickerPauseMenu');
        const resumeClickerBtn = document.getElementById('resumeClickerBtn');
        const clickerToMenuBtn = document.getElementById('clickerToMenuBtn');
        const resetFromPauseBtn = document.getElementById('resetFromPauseBtn');
        const clickerPausePoints = document.getElementById('clickerPausePoints');
        const clickerPauseClicks = document.getElementById('clickerPauseClicks');
        const clickerMusicSelect = document.getElementById('clickerMusicSelect');
        const clickerVolumeSlider = document.getElementById('clickerVolumeSlider');
        
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
        const menuMusic = new Audio();
        menuMusic.loop = true;
        menuMusic.volume = 0.25;
        menuMusic.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3';
        
        const campaignMusic = new Audio();
        campaignMusic.loop = true;
        campaignMusic.volume = 0.25;
        campaignMusic.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-17.mp3';
        
        const infiniteMusic = new Audio();
        infiniteMusic.loop = true;
        infiniteMusic.volume = 0.25;
        infiniteMusic.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-14.mp3';
        
        const clickerMusic = new Audio();
        clickerMusic.loop = true;
        clickerMusic.volume = 0.2;
        clickerMusic.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3';
        
        // Тревожная музыка для метеорита
        const meteorMusic = new Audio();
        meteorMusic.loop = true;
        meteorMusic.volume = 0.3;
        meteorMusic.src = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3';
        
        const coinAudio = new Audio();
        coinAudio.volume = 1.0;
        coinAudio.src = 'https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3';
        
        const redCoinAudio = new Audio();
        redCoinAudio.volume = 0.8;
        redCoinAudio.src = 'https://www.soundjay.com/misc/sounds/bell-ringing-06.mp3';
        
        const clickerAudio = new Audio();
        clickerAudio.volume = 0.4;
        clickerAudio.src = 'https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3';
        
        menuMusic.load();
        campaignMusic.load();
        infiniteMusic.load();
        clickerMusic.load();
        meteorMusic.load();
        coinAudio.load();
        redCoinAudio.load();
        clickerAudio.load();

        // Константы игры
        const MAX_STARS = 25;
        const STAR_RADIUS = 30;
        const RED_STAR_RADIUS = 28;
        const SPAWN_DELAY = 500; // Уменьшено с 1500 до 500 для более быстрого возрождения
        const INITIAL_TIME = 3;
        const MAX_TIME = 10;
        const TIME_BONUS = 0.5;
        
        // Варианты внешнего вида звёзд
        const STAR_VARIANTS = [
            {
                name: 'Золотая',
                gradient: ['#fffde0', '#ffd966', '#f5b542', '#d48d2b'],
                shadowColor: '#fff7b0',
                strokeColor: '#fff2b0'
            },
            {
                name: 'Серебряная',
                gradient: ['#f0f0ff', '#c0c0e0', '#a0a0c0', '#8080a0'],
                shadowColor: '#e0e0ff',
                strokeColor: '#c0c0ff'
            },
            {
                name: 'Розовая',
                gradient: ['#fff0f5', '#ffb6c1', '#ff69b4', '#c71585'],
                shadowColor: '#ffb6c1',
                strokeColor: '#ff69b4'
            }
        ];

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
            },
            METEOR_HUNTER: {
                id: 'meteorHunter',
                name: 'Охотник за метеорами',
                description: 'Наберите 50 очков во время метеоритного дождя',
                icon: '☄️',
                condition: (stats) => stats.meteorScore >= 50,
                progress: (stats) => Math.min(100, Math.floor((stats.meteorScore / 50) * 100)),
                current: (stats) => stats.meteorScore,
                target: 50,
                unlocked: false
            },
            CLICKER_STARTER: {
                id: 'clickerStarter',
                name: 'Начинающий кликер',
                description: 'Сделайте 100 кликов',
                icon: '👆',
                condition: (stats) => stats.clickerClicks >= 100,
                progress: (stats) => Math.min(100, Math.floor((stats.clickerClicks / 100) * 100)),
                current: (stats) => stats.clickerClicks,
                target: 100,
                unlocked: false
            },
            CLICKER_PRO: {
                id: 'clickerPro',
                name: 'Профессиональный кликер',
                description: 'Сделайте 1000 кликов',
                icon: '👆👆',
                condition: (stats) => stats.clickerClicks >= 1000,
                progress: (stats) => Math.min(100, Math.floor((stats.clickerClicks / 1000) * 100)),
                current: (stats) => stats.clickerClicks,
                target: 1000,
                unlocked: false
            },
            CLICKER_MASTER: {
                id: 'clickerMaster',
                name: 'Мастер кликера',
                description: 'Сделайте 10000 кликов',
                icon: '👑',
                condition: (stats) => stats.clickerClicks >= 10000,
                progress: (stats) => Math.min(100, Math.floor((stats.clickerClicks / 10000) * 100)),
                current: (stats) => stats.clickerClicks,
                target: 10000,
                unlocked: false
            },
            POWER_COLLECTOR: {
                id: 'powerCollector',
                name: 'Коллекционер силы',
                description: 'Накопите 1000 баллов',
                icon: '💰',
                condition: (stats) => stats.clickerPoints >= 1000,
                progress: (stats) => Math.min(100, Math.floor((stats.clickerPoints / 1000) * 100)),
                current: (stats) => stats.clickerPoints,
                target: 1000,
                unlocked: false
            },
            POWER_MASTER: {
                id: 'powerMaster',
                name: 'Мастер богатства',
                description: 'Накопите 10000 баллов',
                icon: '💎',
                condition: (stats) => stats.clickerPoints >= 10000,
                progress: (stats) => Math.min(100, Math.floor((stats.clickerPoints / 10000) * 100)),
                current: (stats) => stats.clickerPoints,
                target: 10000,
                unlocked: false
            },
            UPGRADE_COLLECTOR: {
                id: 'upgradeCollector',
                name: 'Коллекционер улучшений',
                description: 'Купите 10 улучшений',
                icon: '🔧',
                condition: (stats) => stats.upgradesBought >= 10,
                progress: (stats) => Math.min(100, Math.floor((stats.upgradesBought / 10) * 100)),
                current: (stats) => stats.upgradesBought,
                target: 10,
                unlocked: false
            },
            UPGRADE_MASTER: {
                id: 'upgradeMaster',
                name: 'Мастер улучшений',
                description: 'Купите 50 улучшений',
                icon: '⚙️',
                condition: (stats) => stats.upgradesBought >= 50,
                progress: (stats) => Math.min(100, Math.floor((stats.upgradesBought / 50) * 100)),
                current: (stats) => stats.upgradesBought,
                target: 50,
                unlocked: false
            }
        };

        // Статистика игрока для ачивок
        let playerStats = {
            infiniteScore: 0,
            completedLevels: 0,
            bossDefeated: false,
            maxScorePerGame: 0,
            maxStarsCollected: 0,
            meteorScore: 0,
            clickerClicks: 0,
            clickerPoints: 0,
            upgradesBought: 0
        };

        function loadAchievements() {
            try {
                const savedUnlocked = localStorage.getItem('achievements_unlocked');
                if (savedUnlocked) {
                    unlockedAchievements = new Set(JSON.parse(savedUnlocked));
                }
                
                const savedStats = localStorage.getItem('achievements_stats');
                if (savedStats) {
                    const parsedStats = JSON.parse(savedStats);
                    playerStats = { ...playerStats, ...parsedStats };
                }
                
                for (let key in ACHIEVEMENTS) {
                    ACHIEVEMENTS[key].unlocked = unlockedAchievements.has(key);
                }
            } catch (e) {
                console.log('Не удалось загрузить достижения', e);
            }
        }

        function saveAchievements() {
            try {
                localStorage.setItem('achievements_unlocked', JSON.stringify([...unlockedAchievements]));
                localStorage.setItem('achievements_stats', JSON.stringify(playerStats));
            } catch (e) {
                console.log('Не удалось сохранить достижения', e);
            }
        }

        let unlockedAchievements = new Set();
        loadAchievements();

        function showAchievementPopup(achievement) {
            popupIcon.textContent = achievement.icon;
            popupTitle.textContent = '🎉 Достижение получено!';
            popupDescription.textContent = `${achievement.name}: ${achievement.description}`;
            
            achievementPopup.classList.add('show');
            
            setTimeout(() => {
                achievementPopup.classList.remove('show');
            }, 5000);
        }

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
            
            if (achievementsMenu.style.display === 'flex') {
                renderAchievements();
            }
        }

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

        function updateStats() {
            if (gameMode === 'infinite') {
                const oldInfiniteScore = playerStats.infiniteScore;
                const oldMaxScorePerGame = playerStats.maxScorePerGame;
                const oldMaxStarsCollected = playerStats.maxStarsCollected;
                
                playerStats.infiniteScore = Math.max(playerStats.infiniteScore, score);
                playerStats.maxScorePerGame = Math.max(playerStats.maxScorePerGame, score);
                playerStats.maxStarsCollected = Math.max(playerStats.maxStarsCollected, stars.length);
                
                if (oldInfiniteScore !== playerStats.infiniteScore || 
                    oldMaxScorePerGame !== playerStats.maxScorePerGame || 
                    oldMaxStarsCollected !== playerStats.maxStarsCollected) {
                    saveAchievements();
                }
            }
            
            checkAchievements();
        }

        // ------ Система кликера с нагревом и комбо ------
        let clickerData = {
            points: 0,
            clicks: 0,
            clickPower: 1,
            autoClicker: 0,
            critChance: 0,
            critMultiplier: 2,
            clickCombo: 1,
            comboMultiplier: 1,
            lastClickTime: 0,
            heat: 0,
            maxHeat: 100,
            heatMultiplier: 1,
            autoClickerInterval: null,
            upgradeLevels: {
                clickPower: 0,
                autoClicker: 0,
                clickPower2: 0,
                autoClicker2: 0,
                critChance: 0,
                critMultiplier: 0,
                clickCombo: 0,
                megaClick: 0
            }
        };

        let clickerIsPaused = false;

        function loadClickerData() {
            try {
                const saved = localStorage.getItem('clicker_data');
                if (saved) {
                    const parsed = JSON.parse(saved);
                    clickerData = { ...clickerData, ...parsed };
                }
                updateClickerDisplay();
                startAutoClicker();
            } catch (e) {
                console.log('Не удалось загрузить данные кликера', e);
            }
        }

        function saveClickerData() {
            try {
                localStorage.setItem('clicker_data', JSON.stringify(clickerData));
            } catch (e) {
                console.log('Не удалось сохранить данные кликера', e);
            }
        }

        function updateClickerDisplay() {
            clickerPoints.textContent = clickerData.points;
            clickerClicks.textContent = clickerData.clicks;
            clickerPausePoints.textContent = clickerData.points;
            clickerPauseClicks.textContent = clickerData.clicks;
            clickPowerValue.textContent = clickerData.clickPower;
            
            const heatPercentValue = Math.min(100, Math.floor((clickerData.heat / clickerData.maxHeat) * 100));
            heatPercent.textContent = heatPercentValue + '%';
            
            const heatPercentWidth = (clickerData.heat / clickerData.maxHeat) * 100;
            heatFill.style.width = heatPercentWidth + '%';
            
            // Обновление комбо
            const timeSinceLastClick = Date.now() - clickerData.lastClickTime;
            if (timeSinceLastClick < 1000 && clickerData.clickCombo > 1) {
                comboCounter.style.display = 'flex';
                comboValue.textContent = 'x' + clickerData.clickCombo;
            } else {
                comboCounter.style.display = 'none';
            }
            
            if (clickerData.heat >= clickerData.maxHeat) {
                clickerStar.classList.add('overheated');
                starSvg.querySelector('path').setAttribute('fill', 'url(#hotStarGradient)');
            } else {
                clickerStar.classList.remove('overheated');
                starSvg.querySelector('path').setAttribute('fill', 'url(#starGradient)');
            }
            
            playerStats.clickerClicks = clickerData.clicks;
            playerStats.clickerPoints = clickerData.points;
            checkAchievements();
            
            renderUpgrades();
        }

        function updateHeat() {
            if (clickerIsPaused) return;
            
            const now = Date.now();
            const timeDiff = now - clickerData.lastClickTime;
            
            // Медленное остывание, быстрый нагрев только при частых кликах
            if (timeDiff < 100) {
                clickerData.heat = Math.min(clickerData.maxHeat, clickerData.heat + 2);
            } else if (timeDiff < 200) {
                clickerData.heat = Math.min(clickerData.maxHeat, clickerData.heat + 1);
            } else {
                clickerData.heat = Math.max(0, clickerData.heat - 0.5);
            }
            
            clickerData.heatMultiplier = clickerData.heat >= clickerData.maxHeat ? 2 : 1;
            
            updateClickerDisplay();
        }

        function startAutoClicker() {
            if (clickerData.autoClickerInterval) {
                clearInterval(clickerData.autoClickerInterval);
            }
            if (clickerData.autoClicker > 0) {
                clickerData.autoClickerInterval = setInterval(() => {
                    if (!clickerIsPaused) {
                        let points = clickerData.autoClicker;
                        if (Math.random() * 100 < clickerData.critChance) {
                            points *= clickerData.critMultiplier;
                        }
                        clickerData.points += points;
                        saveClickerData();
                        updateClickerDisplay();
                    }
                }, 1000);
            }
        }

        function playClickSound() {
            if (!audioUnlocked) return;
            const sound = new Audio(clickerAudio.src);
            sound.volume = clickerAudio.volume;
            sound.play().catch(e => {});
        }

        function handleClickerStar() {
            if (clickerIsPaused) return;
            
            const now = Date.now();
            const timeSinceLast = now - clickerData.lastClickTime;
            
            // Система комбо
            if (timeSinceLast < 1000) {
                clickerData.clickCombo = Math.min(10, clickerData.clickCombo + 1);
            } else {
                clickerData.clickCombo = 1;
            }
            
            clickerData.lastClickTime = now;
            
            updateHeat();
            
            clickerStar.classList.add('pulse');
            setTimeout(() => {
                clickerStar.classList.remove('pulse');
            }, 200);
            
            let points = clickerData.clickPower;
            
            // Множитель комбо
            points *= clickerData.clickCombo;
            
            if (Math.random() * 100 < clickerData.critChance) {
                points *= clickerData.critMultiplier;
            }
            
            points *= clickerData.heatMultiplier;
            
            // Мега клик
            if (clickerData.upgradeLevels.megaClick > 0 && clickerData.clicks % 10 === 0 && clickerData.clicks > 0) {
                points *= 1.5;
            }
            
            clickerData.points += Math.floor(points);
            clickerData.clicks++;
            
            playClickSound();
            
            saveClickerData();
            updateClickerDisplay();
        }

        function getUpgradeCost(baseCost, level) {
            return Math.floor(baseCost * Math.pow(1.5, level));
        }

        const UPGRADES = [
            {
                id: 'clickPower',
                name: '⚡ Сила клика',
                description: (level) => `+1 балл за клик (уровень ${level + 1})`,
                baseCost: 10,
                getLevel: () => clickerData.upgradeLevels.clickPower,
                getCost: () => getUpgradeCost(10, clickerData.upgradeLevels.clickPower),
                buy: () => {
                    clickerData.upgradeLevels.clickPower++;
                    clickerData.clickPower++;
                    playerStats.upgradesBought++;
                }
            },
            {
                id: 'autoClicker',
                name: '🤖 Автокликер',
                description: (level) => `+1 балл в секунду (уровень ${level + 1})`,
                baseCost: 50,
                getLevel: () => clickerData.upgradeLevels.autoClicker,
                getCost: () => getUpgradeCost(50, clickerData.upgradeLevels.autoClicker),
                buy: () => {
                    clickerData.upgradeLevels.autoClicker++;
                    clickerData.autoClicker++;
                    playerStats.upgradesBought++;
                    startAutoClicker();
                }
            },
            {
                id: 'critChance',
                name: '🎯 Шанс крита',
                description: (level) => `+2% шанс крита (уровень ${level + 1})`,
                baseCost: 30,
                getLevel: () => clickerData.upgradeLevels.critChance,
                getCost: () => getUpgradeCost(30, clickerData.upgradeLevels.critChance),
                buy: () => {
                    clickerData.upgradeLevels.critChance++;
                    clickerData.critChance += 2;
                    playerStats.upgradesBought++;
                }
            },
            {
                id: 'critMultiplier',
                name: '💥 Множитель крита',
                description: (level) => `+0.5x крит (уровень ${level + 1})`,
                baseCost: 40,
                getLevel: () => clickerData.upgradeLevels.critMultiplier,
                getCost: () => getUpgradeCost(40, clickerData.upgradeLevels.critMultiplier),
                buy: () => {
                    clickerData.upgradeLevels.critMultiplier++;
                    clickerData.critMultiplier += 0.5;
                    playerStats.upgradesBought++;
                }
            },
            {
                id: 'clickCombo',
                name: '⏱️ Усилитель комбо',
                description: (level) => `Макс. комбо +1 (уровень ${level + 1})`,
                baseCost: 60,
                getLevel: () => clickerData.upgradeLevels.clickCombo,
                getCost: () => getUpgradeCost(60, clickerData.upgradeLevels.clickCombo),
                buy: () => {
                    clickerData.upgradeLevels.clickCombo++;
                    playerStats.upgradesBought++;
                }
            },
            {
                id: 'clickPower2',
                name: '⚡⚡ Мега сила',
                description: (level) => `+5 баллов за клик (уровень ${level + 1})`,
                baseCost: 200,
                condition: () => clickerData.clickPower >= 10,
                getLevel: () => clickerData.upgradeLevels.clickPower2,
                getCost: () => getUpgradeCost(200, clickerData.upgradeLevels.clickPower2),
                buy: () => {
                    clickerData.upgradeLevels.clickPower2++;
                    clickerData.clickPower += 5;
                    playerStats.upgradesBought++;
                }
            },
            {
                id: 'autoClicker2',
                name: '🤖🤖 Мега автокликер',
                description: (level) => `+5 баллов в секунду (уровень ${level + 1})`,
                baseCost: 1000,
                condition: () => clickerData.autoClicker >= 10,
                getLevel: () => clickerData.upgradeLevels.autoClicker2,
                getCost: () => getUpgradeCost(1000, clickerData.upgradeLevels.autoClicker2),
                buy: () => {
                    clickerData.upgradeLevels.autoClicker2++;
                    clickerData.autoClicker += 5;
                    playerStats.upgradesBought++;
                    startAutoClicker();
                }
            },
            {
                id: 'megaClick',
                name: '💫 Мега клик',
                description: (level) => `Каждый 10-й клик даёт +50% (уровень ${level + 1})`,
                baseCost: 500,
                getLevel: () => clickerData.upgradeLevels.megaClick,
                getCost: () => getUpgradeCost(500, clickerData.upgradeLevels.megaClick),
                buy: () => {
                    clickerData.upgradeLevels.megaClick++;
                    playerStats.upgradesBought++;
                }
            }
        ];

        function renderUpgrades() {
            upgradesGrid.innerHTML = '';
            
            for (let upgrade of UPGRADES) {
                const level = upgrade.getLevel();
                const cost = upgrade.getCost();
                const canBuy = upgrade.condition ? upgrade.condition() : true;
                const hasEnoughPoints = clickerData.points >= cost;
                const isDisabled = !canBuy || !hasEnoughPoints;
                
                const card = document.createElement('div');
                card.className = 'upgrade-card';
                
                card.innerHTML = `
                    <div class="upgrade-info">
                        <h3>${upgrade.name} ${level > 0 ? `+${level}` : ''}</h3>
                        <p>${upgrade.description(level)}</p>
                    </div>
                    <div class="upgrade-cost ${isDisabled ? 'disabled' : ''}" data-id="${upgrade.id}">
                        ${cost} ⭐
                    </div>
                `;
                
                upgradesGrid.appendChild(card);
                
                if (!isDisabled) {
                    const costElement = card.querySelector('.upgrade-cost');
                    costElement.addEventListener('click', () => {
                        if (clickerData.points >= cost) {
                            clickerData.points -= cost;
                            upgrade.buy();
                            saveClickerData();
                            updateClickerDisplay();
                        }
                    });
                }
            }
        }

        function resetClicker() {
            if (clickerData.autoClickerInterval) {
                clearInterval(clickerData.autoClickerInterval);
            }
            clickerData = {
                points: 0,
                clicks: 0,
                clickPower: 1,
                autoClicker: 0,
                critChance: 0,
                critMultiplier: 2,
                clickCombo: 1,
                comboMultiplier: 1,
                lastClickTime: 0,
                heat: 0,
                maxHeat: 100,
                heatMultiplier: 1,
                autoClickerInterval: null,
                upgradeLevels: {
                    clickPower: 0,
                    autoClicker: 0,
                    clickPower2: 0,
                    autoClicker2: 0,
                    critChance: 0,
                    critMultiplier: 0,
                    clickCombo: 0,
                    megaClick: 0
                }
            };
            saveClickerData();
            updateClickerDisplay();
        }

        function openClickerPauseMenu() {
            clickerIsPaused = true;
            clickerPauseMenu.style.display = 'flex';
            if (currentMusic) currentMusic.pause();
            updateClickerDisplay();
        }

        function closeClickerPauseMenu() {
            clickerIsPaused = false;
            clickerPauseMenu.style.display = 'none';
            if (musicEnabled && audioUnlocked && currentMusic) {
                currentMusic.play().catch(e => console.log('Не удалось возобновить музыку'));
            }
        }

        loadClickerData();

        // ------ Упрощенная рулетка с разными шансами ------
        const SEGMENTS = [
            { name: 'Зона 1', points: 10, color: '#4a90e2', weight: 40 },
            { name: 'Зона 2', points: 100, color: '#ffaa00', weight: 20 },
            { name: 'Зона 3', points: 50, color: '#ff4444', weight: 30 },
            { name: 'Зона 4', points: 500, color: '#9b59b6', weight: 10 }
        ];

        function getWeightedRandomReward() {
            const totalWeight = SEGMENTS.reduce((sum, seg) => sum + seg.weight, 0);
            let random = Math.random() * totalWeight;
            let cumulative = 0;
            
            for (let segment of SEGMENTS) {
                cumulative += segment.weight;
                if (random < cumulative) {
                    return segment;
                }
            }
            return SEGMENTS[0];
        }

        // Обработчик для простой рулетки
        simpleWheel.addEventListener('click', () => {
            if (clickerIsPaused) return;
            
            // Анимация вращения
            simpleWheel.style.transition = 'transform 0.5s ease';
            simpleWheel.style.transform = 'rotate(360deg)';
            
            setTimeout(() => {
                simpleWheel.style.transition = 'none';
                simpleWheel.style.transform = 'rotate(0deg)';
            }, 500);
            
            // Выбираем случайный приз с учетом весов
            const reward = getWeightedRandomReward();
            clickerData.points += reward.points;
            saveClickerData();
            updateClickerDisplay();
            
            simpleRouletteResult.innerHTML = `🎉 Вы выиграли: <span style="color: ${reward.color}">${reward.name} (${reward.points}⭐)</span>`;
            
            playClickSound();
            
            // Эффект джекпота для 500
            if (reward.points === 500) {
                startJackpotEffect();
            }
        });

        function startJackpotEffect() {
            for (let i = 0; i < 50; i++) {
                jackpotStars.push({
                    x: 400 + (Math.random() - 0.5) * 150,
                    y: 300,
                    size: 4 + Math.random() * 10,
                    speedX: (Math.random() - 0.5) * 3,
                    speedY: Math.random() * 4 + 2,
                    rotation: Math.random() * 360,
                    rotationSpeed: (Math.random() - 0.5) * 8,
                    alpha: 0.9,
                    color: `hsl(${Math.random() * 60 + 200}, 100%, 70%)`
                });
            }
            
            function animateJackpot() {
                if (jackpotStars.length === 0) return;
                
                const canvas = document.createElement('canvas');
                canvas.style.position = 'fixed';
                canvas.style.top = '0';
                canvas.style.left = '0';
                canvas.style.width = '100%';
                canvas.style.height = '100%';
                canvas.style.pointerEvents = 'none';
                canvas.style.zIndex = '9999';
                document.body.appendChild(canvas);
                
                const ctx = canvas.getContext('2d');
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
                
                let frames = 0;
                const maxFrames = 250;
                
                function draw() {
                    if (frames >= maxFrames || jackpotStars.length === 0) {
                        canvas.remove();
                        jackpotStars = [];
                        return;
                    }
                    
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                    
                    for (let i = jackpotStars.length - 1; i >= 0; i--) {
                        const star = jackpotStars[i];
                        
                        star.x += star.speedX;
                        star.y += star.speedY;
                        star.rotation += star.rotationSpeed;
                        star.alpha *= 0.98;
                        
                        if (star.y > canvas.height + 100 || star.alpha < 0.01) {
                            jackpotStars.splice(i, 1);
                            continue;
                        }
                        
                        ctx.save();
                        ctx.translate(star.x, star.y);
                        ctx.rotate(star.rotation * Math.PI / 180);
                        ctx.globalAlpha = star.alpha;
                        ctx.fillStyle = star.color;
                        ctx.shadowColor = '#9b59b6';
                        ctx.shadowBlur = 20;
                        
                        ctx.beginPath();
                        for (let j = 0; j < 5; j++) {
                            const angle = (j * 72 - 90) * Math.PI / 180;
                            const x1 = Math.cos(angle) * star.size;
                            const y1 = Math.sin(angle) * star.size;
                            const x2 = Math.cos(angle + 36 * Math.PI / 180) * (star.size * 0.4);
                            const y2 = Math.sin(angle + 36 * Math.PI / 180) * (star.size * 0.4);
                            
                            if (j === 0) {
                                ctx.moveTo(x1, y1);
                            } else {
                                ctx.lineTo(x1, y1);
                            }
                            ctx.lineTo(x2, y2);
                        }
                        ctx.closePath();
                        ctx.fill();
                        ctx.restore();
                    }
                    
                    frames++;
                    requestAnimationFrame(draw);
                }
                
                draw();
            }
            
            animateJackpot();
        }

        let jackpotStars = [];

        function createBackgroundAnimation() {
            const bg = document.getElementById('bgAnimation');
            bg.innerHTML = '';
            
            for (let i = 0; i < 50; i++) {
                const star = document.createElement('div');
                star.className = 'star-bg';
                star.style.left = Math.random() * 100 + '%';
                star.style.width = Math.random() * 3 + 1 + 'px';
                star.style.height = star.style.width;
                star.style.animationDuration = Math.random() * 5 + 3 + 's';
                star.style.animationDelay = Math.random() * 5 + 's';
                star.style.background = `hsl(${Math.random() * 60 + 200}, 70%, 70%)`;
                star.style.boxShadow = `0 0 ${Math.random() * 10 + 5}px currentColor`;
                bg.appendChild(star);
            }
        }

        createBackgroundAnimation();

        // ------ Система метеорита (исправленная) ------
        let meteor = null;
        let meteorTimer = null;
        let meteorActive = false;
        let meteorClicks = 0;
        let savedStars = [];
        let meteorTimeLeft = 0;
        let wasTimerRunning = false;

        function spawnMeteor() {
            console.log('Попытка спавна метеорита');
            if (meteorActive || gameMode !== 'infinite' || !gameActive) {
                console.log('Спавн отменен:', { meteorActive, gameMode, gameActive });
                return;
            }
            
            console.log('МЕТЕОРИТ ПОЯВИЛСЯ!');
            
            // Сохраняем текущие звезды
            savedStars = [...stars];
            // Очищаем поле от звезд
            stars = [];
            
            // Создаем метеор на весь экран
            meteor = {
                x: canvas.width / 2,
                y: canvas.height / 2,
                width: canvas.width * 2,
                height: canvas.height * 2,
                rotation: 0,
                flameOffset: 0,
                flameTimer: 0,
                alpha: 1
            };
            
            meteorActive = true;
            meteorClicks = 0;
            meteorTimeLeft = 10; // Метеор активен 10 секунд
            
            // Останавливаем таймер игры
            if (timerInterval) {
                wasTimerRunning = true;
                clearInterval(timerInterval);
                timerInterval = null;
            }
            
            // Включаем визуальные эффекты
            meteorTimerSpan.style.display = 'inline-block';
            canvas.classList.add('canvas-meteor-active');
            meteorOverlay.style.display = 'block';
            
            // Меняем музыку на тревожную
            if (musicEnabled && audioUnlocked) {
                if (currentMusic) currentMusic.pause();
                currentMusic = meteorMusic;
                currentMusic.play().catch(e => console.log('Не удалось запустить тревожную музыку'));
            }
            
            updateMeteorTimer();
            
            if (meteorTimer) clearInterval(meteorTimer);
            meteorTimer = setInterval(() => {
                meteorTimeLeft -= 0.1;
                if (meteorTimeLeft <= 0) {
                    endMeteor();
                }
                updateMeteorTimer();
            }, 100);
        }

        function updateMeteorTimer() {
            meteorTimerSpan.textContent = `☄️ ${meteorTimeLeft.toFixed(1)}с`;
        }

        function endMeteor() {
            console.log('МЕТЕОРИТ ИСЧЕЗ');
            meteorActive = false;
            // Возвращаем звезды
            stars = savedStars;
            savedStars = [];
            meteor = null;
            
            // Убираем визуальные эффекты
            meteorTimerSpan.style.display = 'none';
            canvas.classList.remove('canvas-meteor-active');
            meteorOverlay.style.display = 'none';
            
            if (meteorTimer) {
                clearInterval(meteorTimer);
                meteorTimer = null;
            }
            
            // Возвращаем обычную музыку
            if (musicEnabled && audioUnlocked) {
                if (currentMusic) currentMusic.pause();
                if (gameMode === 'infinite') {
                    currentMusic = infiniteMusic;
                } else if (gameMode === 'campaign') {
                    currentMusic = campaignMusic;
                }
                if (currentMusic) {
                    currentMusic.play().catch(e => console.log('Не удалось возобновить музыку'));
                }
            }
            
            // Возобновляем таймер игры
            if (wasTimerRunning && gameActive && !isPaused) {
                lastTime = Date.now();
                startTimer();
                wasTimerRunning = false;
            }
        }

        function checkMeteorSpawn() {
            if (gameMode !== 'infinite' || meteorActive) return;
            
            // Каждые 15 звезд с 20% шансом (убрал гарантированный спавн)
            if (score > 0 && score % 15 === 0) {
                if (Math.random() < 0.2) { // 20% шанс
                    console.log('Условия выполнены, спавним метеорит');
                    spawnMeteor();
                }
            }
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
        let pauseStartTime = 0;
        let audioUnlocked = false;
        let musicEnabled = true;
        let currentMusic = null;
        
        let boss = null;
        let bossHealth = 50;
        let bossMaxHealth = 50;
        let redStarSpawnTimer = 0;
        let bossAnimationFrame = 0;
        
        let gameMode = null;
        let currentLevel = 0;
        let levelTarget = 0;

        function changeMusic(type) {
            if (meteorActive) return; // Не меняем музыку во время метеорита
            
            menuMusic.pause();
            campaignMusic.pause();
            infiniteMusic.pause();
            clickerMusic.pause();
            meteorMusic.pause();
            
            menuMusic.currentTime = 0;
            campaignMusic.currentTime = 0;
            infiniteMusic.currentTime = 0;
            clickerMusic.currentTime = 0;
            meteorMusic.currentTime = 0;
            
            if (type === 'silent' || !musicEnabled || !audioUnlocked) {
                currentMusic = null;
                return;
            }
            
            switch(type) {
                case 'menu':
                    currentMusic = menuMusic;
                    break;
                case 'campaign':
                    currentMusic = campaignMusic;
                    break;
                case 'infinite':
                    currentMusic = infiniteMusic;
                    break;
                case 'clicker':
                    currentMusic = clickerMusic;
                    break;
                default:
                    currentMusic = null;
            }
            
            if (currentMusic && !isPaused && gameActive && !clickerIsPaused) {
                currentMusic.play().catch(e => console.log('Не удалось запустить музыку'));
            }
        }

        function tryPlayMusic() {
            if (!audioUnlocked) {
                unlockAudio();
            }
            
            if (musicEnabled && !isPaused && gameActive && !clickerIsPaused) {
                if (mainMenu.style.display === 'flex') {
                    changeMusic('menu');
                } else if (gameMode === 'campaign') {
                    changeMusic('campaign');
                } else if (gameMode === 'infinite') {
                    changeMusic('infinite');
                } else if (clickerMenu.style.display === 'flex') {
                    changeMusic('clicker');
                }
            }
        }

        function startInfiniteMode() {
            gameMode = 'infinite';
            levelSpan.style.display = 'none';
            bossHealthSpan.style.display = 'none';
            pauseLevel.style.display = 'none';
            tip.innerHTML = '🖱️ Кликай по звёздам  ✨ +1 очко  🌟 Макс. 25 звёзд  ⏳ +0.5 сек  ☄️ 20% шанс метеора каждые 15 очков!';
            resetGame();
            changeMusic('infinite');
        }

        function startCampaignMode() {
            gameMode = 'campaign';
            currentLevel = 0;
            levelSpan.style.display = 'inline-block';
            pauseLevel.style.display = 'block';
            startLevel(0);
            changeMusic('campaign');
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
                rotation: 0,
                floatOffset: 0
            };
            
            stars = [];
            redStars = [];
            score = 0;
            gameActive = true;
            redStarSpawnTimer = 0;
            
            if (isPaused) closePauseMenu();
            
            updateScore();
            
            if (timerInterval) clearInterval(timerInterval);
            
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
                    playerStats.bossDefeated = true;
                    gameActive = false;
                    clearInterval(timerInterval);
                    if (currentMusic) currentMusic.pause();
                    saveAchievements();
                    showVictory('ПОБЕДА!', 'Вы победили босса!');
                    checkAchievements();
                }
                return;
            }
            
            if (score >= level.target) {
                gameActive = false;
                clearInterval(timerInterval);
                if (currentMusic) currentMusic.pause();
                
                playerStats.completedLevels = Math.max(playerStats.completedLevels, currentLevel + 1);
                saveAchievements();
                checkAchievements();
                
                if (currentLevel < CAMPAIGN_LEVELS.length - 1) {
                    showLevelComplete(currentLevel + 1);
                } else {
                    showVictory('ПОБЕДА!', 'Вы прошли всю кампанию!');
                }
            }
        }

        function showLevelComplete(nextLevel) {
            levelCompleteMessage.textContent = `Переход на уровень ${nextLevel + 1}`;
            levelCompleteOverlay.style.display = 'flex';
            
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

        function updatePauseStats() {
            pauseScore.textContent = score;
            pauseStarsCount.textContent = stars.length + redStars.length;
        }

        function openPauseMenu() {
            if (!gameActive || isPaused) return;
            
            isPaused = true;
            pauseStartTime = Date.now();
            updatePauseStats();
            pauseMenu.style.display = 'flex';
            pauseOverlay.style.display = 'flex';
            
            if (currentMusic) currentMusic.pause();
            
            if (timerInterval) {
                clearInterval(timerInterval);
                timerInterval = null;
            }
        }

        function closePauseMenu() {
            if (!isPaused) return;
            
            isPaused = false;
            pauseMenu.style.display = 'none';
            pauseOverlay.style.display = 'none';
            
            if (musicEnabled && audioUnlocked && currentMusic && !meteorActive) {
                currentMusic.play().catch(e => console.log('Не удалось возобновить музыку'));
            }
            
            if (gameActive && !meteorActive) {
                lastTime = Date.now();
                startTimer();
            }
        }

        function returnToMainMenu() {
            if (timerInterval) clearInterval(timerInterval);
            if (currentMusic) currentMusic.pause();
            gameActive = false;
            
            gameContainer.style.display = 'none';
            pauseMenu.style.display = 'none';
            pauseOverlay.style.display = 'none';
            resultOverlay.style.display = 'none';
            levelCompleteOverlay.style.display = 'none';
            achievementsMenu.style.display = 'none';
            clickerMenu.style.display = 'none';
            clickerPauseMenu.style.display = 'none';
            
            mainMenu.style.display = 'flex';
            changeMusic('menu');
        }

        function addTime() {
            if (!gameActive || isPaused || !timerInterval || meteorActive) return;
            
            timeLeft = Math.min(MAX_TIME, timeLeft + TIME_BONUS);
            updateTimerBar();
            
            timerBar.style.transition = 'width 0.1s linear, background 0.3s';
            timerBar.style.background = 'linear-gradient(90deg, #44ff44, #88ff88)';
            setTimeout(() => updateTimerBar(), 300);
        }

        function startTimer() {
            if (timerInterval) clearInterval(timerInterval);
            
            timerInterval = setInterval(() => {
                if (!gameActive || isPaused || meteorActive) return;
                
                const now = Date.now();
                const delta = (now - lastTime) / 1000;
                lastTime = now;
                
                timeLeft = Math.max(0, timeLeft - delta);
                updateTimerBar();
                
                if (timeLeft <= 0) {
                    gameActive = false;
                    clearInterval(timerInterval);
                    if (currentMusic) currentMusic.pause();
                    
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

        function updateTimerBar() {
            if (!timerInterval && !boss) {
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

        function generateStar() {
            const minX = STAR_RADIUS + 5;
            const maxX = canvas.width - STAR_RADIUS - 5;
            const minY = STAR_RADIUS + 5;
            const maxY = canvas.height - STAR_RADIUS - 5;
            
            const variant = Math.floor(Math.random() * 3);
            
            return {
                x: Math.floor(Math.random() * (maxX - minX + 1)) + minX,
                y: Math.floor(Math.random() * (maxY - minY + 1)) + minY,
                rotation: 0,
                pulse: 0,
                alpha: 0,
                spawnProgress: 0,
                variant: variant
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
            if (meteorActive) endMeteor();
            
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
                checkMeteorSpawn();
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
            
            if (musicEnabled && !isPaused && gameActive && currentMusic && !clickerIsPaused) {
                currentMusic.play().catch(e => console.log('Не удалось запустить музыку'));
                musicToggle.textContent = '🔇 Музыка';
            } else {
                if (currentMusic) currentMusic.pause();
                musicToggle.textContent = '🔊 Музыка';
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
                
                if (musicEnabled && !isPaused && gameActive && currentMusic && !clickerIsPaused) {
                    currentMusic.play().catch(e => console.log('Не удалось запустить музыку'));
                }
            }).catch(e => {
                console.log('Не удалось разблокировать аудио');
                audioUnlocked = true;
            });
        }

        function spawnNewStar() {
            if (!gameActive || isPaused || boss || meteorActive) return;
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

            // Проверка клика по метеориту
            if (meteorActive && meteor) {
                meteorClicks++;
                score += 2;
                playerStats.meteorScore += 2;
                updateScore();
                
                // Эффект при клике
                meteor.flameTimer = 10;
                return;
            }

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
                        speed: 0.2 + Math.random() * 0.2,
                        variant: star.variant
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
            const volume = parseFloat(volumeSlider.value);
            menuMusic.volume = volume;
            campaignMusic.volume = volume;
            infiniteMusic.volume = volume;
            clickerMusic.volume = volume;
            meteorMusic.volume = volume * 1.2;
        }

        function updateClickerVolume() {
            const volume = parseFloat(clickerVolumeSlider.value);
            menuMusic.volume = volume;
            campaignMusic.volume = volume;
            infiniteMusic.volume = volume;
            clickerMusic.volume = volume;
            meteorMusic.volume = volume * 1.2;
        }

        function drawBoss() {
            if (!boss) return;
            
            bossAnimationFrame += 0.02;
            boss.floatOffset = Math.sin(bossAnimationFrame) * 10;
            boss.rotation = Math.sin(bossAnimationFrame * 0.5) * 0.1;
            
            ctx.save();
            ctx.translate(boss.x, boss.y + boss.floatOffset);
            ctx.rotate(boss.rotation);
            
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
                const blink = Math.sin(bossAnimationFrame * 2 + i) * 0.3 + 0.7;
                ctx.globalAlpha = blink;
                ctx.beginPath();
                ctx.arc(i * 25, 15, 5, 0, Math.PI * 2);
                ctx.fill();
            }
            
            ctx.globalAlpha = 1;
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

        function drawMeteor() {
            if (!meteorActive || !meteor) return;
            
            meteor.flameOffset = Math.sin(meteor.flameTimer) * 20;
            meteor.flameTimer += 0.3;
            
            ctx.save();
            ctx.translate(meteor.x, meteor.y);
            ctx.rotate(Math.sin(Date.now() * 0.01) * 0.1);
            
            // Тень
            ctx.shadowColor = '#ff6600';
            ctx.shadowBlur = 80;
            
            // Пламя
            ctx.fillStyle = '#ffaa00';
            ctx.beginPath();
            ctx.ellipse(-150, 0, 120, 60 + meteor.flameOffset, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#ff6600';
            ctx.beginPath();
            ctx.ellipse(-200, 0, 90, 45 + meteor.flameOffset * 0.8, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#ff3300';
            ctx.beginPath();
            ctx.ellipse(-250, 0, 60, 30 + meteor.flameOffset * 0.6, 0, 0, Math.PI * 2);
            ctx.fill();
            
            // Тело метеорита
            ctx.fillStyle = '#8B4513';
            ctx.shadowColor = '#442200';
            ctx.beginPath();
            ctx.ellipse(0, 0, 200, 120, 0, 0, Math.PI * 2);
            ctx.fill();
            
            // Кратеры
            ctx.fillStyle = '#5D3A1A';
            ctx.shadowBlur = 40;
            ctx.beginPath();
            ctx.arc(-50, -30, 40, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.beginPath();
            ctx.arc(60, 40, 35, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.beginPath();
            ctx.arc(30, -50, 30, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.beginPath();
            ctx.arc(-80, 50, 25, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.restore();
            
            // Счетчик кликов по метеориту
            ctx.fillStyle = '#fff';
            ctx.font = 'bold 24px Arial';
            ctx.shadowBlur = 15;
            ctx.shadowColor = '#ff6600';
            ctx.fillText(`☄️ КЛИКОВ: ${meteorClicks}`, canvas.width/2 - 80, 100);
            
            // Предупреждение
            ctx.fillStyle = '#ff0000';
            ctx.font = 'bold 36px Arial';
            ctx.shadowBlur = 20;
            ctx.shadowColor = '#ff0000';
            ctx.fillText('⚠️ МЕТЕОРИТНАЯ АТАКА ⚠️', canvas.width/2 - 300, 200);
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
            
            const variant = STAR_VARIANTS[star.variant || 0];
            
            ctx.save();
            ctx.translate(star.x, star.y);
            ctx.rotate(star.rotation);
            ctx.scale(pulseScale, pulseScale);
            ctx.globalAlpha = star.alpha;
            
            ctx.shadowColor = variant.shadowColor;
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
            gradient.addColorStop(0, variant.gradient[0]);
            gradient.addColorStop(0.4, variant.gradient[1]);
            gradient.addColorStop(0.8, variant.gradient[2]);
            gradient.addColorStop(1, variant.gradient[3]);
            
            ctx.fillStyle = gradient;
            ctx.fill();
            
            ctx.shadowBlur = 15;
            ctx.strokeStyle = variant.strokeColor;
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
            drawMeteor();

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
                
                const variant = STAR_VARIANTS[star.variant || 0];
                const gradient = ctx.createRadialGradient(-5, -5, 5, 0, 0, STAR_RADIUS);
                gradient.addColorStop(0, variant.gradient[0]);
                gradient.addColorStop(0.5, variant.gradient[1]);
                gradient.addColorStop(1, variant.gradient[2]);
                
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
            } else if (!meteorActive) {
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
                    if (currentMusic) currentMusic.pause();
                    showDefeat('ПОРАЖЕНИЕ', 'Красная звезда достигла земли!');
                    return;
                }
            }
        }

        function animate() {
            if (!isPaused && gameActive && !clickerIsPaused) {
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
            
            if (clickerMenu.style.display === 'flex' && !clickerIsPaused) {
                updateHeat();
            }
            
            requestAnimationFrame(animate);
        }

        function init() {
            animate();

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
            
            clickerModeBtn.addEventListener('click', () => {
                mainMenu.style.display = 'none';
                clickerMenu.style.display = 'flex';
                updateClickerDisplay();
                changeMusic('clicker');
            });
            
            achievementsMenuBtn.addEventListener('click', () => {
                mainMenu.style.display = 'none';
                achievementsMenu.style.display = 'flex';
                renderAchievements();
            });
            
            closeAchievementsBtn.addEventListener('click', () => {
                achievementsMenu.style.display = 'none';
                mainMenu.style.display = 'flex';
                changeMusic('menu');
            });

            clickerStar.addEventListener('click', handleClickerStar);
            resetClickerBtn.addEventListener('click', resetClicker);
            pauseClickerBtn.addEventListener('click', openClickerPauseMenu);
            closeClickerBtn.addEventListener('click', () => {
                clickerMenu.style.display = 'none';
                mainMenu.style.display = 'flex';
                changeMusic('menu');
            });
            
            resumeClickerBtn.addEventListener('click', closeClickerPauseMenu);
            clickerToMenuBtn.addEventListener('click', () => {
                closeClickerPauseMenu();
                clickerMenu.style.display = 'none';
                mainMenu.style.display = 'flex';
                changeMusic('menu');
            });
            resetFromPauseBtn.addEventListener('click', () => {
                closeClickerPauseMenu();
                resetClicker();
            });
            
            clickerMusicSelect.addEventListener('change', (e) => {
                changeMusic(e.target.value);
            });
            
            clickerVolumeSlider.addEventListener('input', updateClickerVolume);

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
            
            musicSelect.addEventListener('change', (e) => {
                changeMusic(e.target.value);
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
                        changeMusic('menu');
                        return;
                    }
                    if (clickerPauseMenu.style.display === 'flex') {
                        closeClickerPauseMenu();
                        return;
                    }
                    if (clickerMenu.style.display === 'flex') {
                        openClickerPauseMenu();
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
            
            // Запускаем музыку меню при загрузке
            changeMusic('menu');
        }

        window.addEventListener('load', init);
    })();
</script>
</body>
</html>
