<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>SKY AVIA · BET</title>
    <!-- Font Awesome 6 (free) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: #0b0f17;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 12px;
        }

        /* main app container – mobile first, card look */
        .app {
            max-width: 1280px;
            width: 100%;
            background: #131b26;
            border-radius: 36px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(255, 255, 255, 0.03);
            padding: 20px 18px;
            display: flex;
            flex-direction: column;
            gap: 18px;
            transition: all 0.2s;
        }

        /* top bar */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 6px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .logo-icon {
            background: linear-gradient(145deg, #f5b342, #e08b1e);
            width: 34px;
            height: 34px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: #0b0f17;
            font-weight: 700;
            box-shadow: 0 6px 12px rgba(245, 179, 66, 0.3);
        }

        .logo-text {
            font-weight: 700;
            font-size: 20px;
            letter-spacing: -0.5px;
            color: #fff;
        }

        .logo-text span {
            color: #f5b342;
        }

        .balance-pill {
            background: #1f2a37;
            padding: 8px 16px;
            border-radius: 100px;
            display: flex;
            align-items: center;
            gap: 10px;
            border: 1px solid #2e3c4c;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.4);
        }

        .balance-pill i {
            color: #f5b342;
            font-size: 16px;
        }

        .balance-pill .amount {
            font-weight: 700;
            color: #fff;
            font-size: 16px;
            letter-spacing: 0.3px;
        }

        .balance-pill .currency {
            color: #8f9eb0;
            font-size: 12px;
            font-weight: 500;
        }

        /* main two column layout */
        .dashboard {
            display: flex;
            flex-wrap: wrap;
            gap: 18px;
        }

        /* left column – aviator game */
        .aviator-section {
            flex: 2 1 500px;
            background: #0e141d;
            border-radius: 28px;
            padding: 22px 18px 22px 18px;
            border: 1px solid #202b38;
            box-shadow: 0 8px 0 rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .game-header h2 {
            font-size: 18px;
            font-weight: 600;
            color: #d6e2f0;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .game-header h2 i {
            color: #f5b342;
            font-size: 20px;
        }

        .multiplier-badge {
            background: #1e2b3a;
            padding: 6px 14px;
            border-radius: 40px;
            font-weight: 700;
            font-size: 20px;
            color: #f5b342;
            letter-spacing: 0.5px;
            border: 1px solid #31465c;
        }

        /* plane canvas area */
        .canvas-wrap {
            background: #060a0f;
            border-radius: 24px;
            padding: 12px;
            box-shadow: inset 0 0 20px #000000;
            border: 1px solid #253241;
            position: relative;
            overflow: hidden;
        }

        #aviatorCanvas {
            width: 100%;
            height: auto;
            display: block;
            border-radius: 16px;
            background: radial-gradient(circle at 30% 40%, #172230, #070b10);
            aspect-ratio: 2 / 1;
            cursor: pointer;
        }

        /* stats row under canvas */
        .game-stats {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #0b1119;
            border-radius: 80px;
            padding: 8px 16px;
            border: 1px solid #26313f;
        }

        .stat-item {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #9fb0c3;
            font-size: 14px;
            font-weight: 500;
        }

        .stat-item i {
            color: #f5b342;
        }

        .stat-value {
            color: #fff;
            font-weight: 700;
            margin-left: 4px;
        }

        /* bet controls */
        .bet-controls {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .bet-input-row {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .bet-amount {
            flex: 1;
            background: #1b2531;
            border-radius: 60px;
            display: flex;
            align-items: center;
            padding: 0 10px 0 18px;
            border: 1px solid #2d3d4e;
            transition: 0.2s;
            min-width: 150px;
        }

        .bet-amount:focus-within {
            border-color: #f5b342;
            box-shadow: 0 0 0 2px rgba(245, 179, 66, 0.2);
        }

        .bet-amount i {
            color: #7f8f9f;
            font-size: 16px;
        }

        .bet-amount input {
            background: transparent;
            border: none;
            padding: 16px 8px 16px 12px;
            font-size: 18px;
            font-weight: 600;
            color: #fff;
            width: 100%;
            outline: none;
        }

        .bet-amount input::placeholder {
            color: #5c6d7e;
            font-weight: 400;
            font-size: 15px;
        }

        .quick-bet {
            display: flex;
            gap: 6px;
        }

        .quick-bet button {
            background: #1f2b37;
            border: none;
            color: #b7c7d9;
            font-weight: 600;
            font-size: 13px;
            padding: 8px 12px;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.15s;
            border: 1px solid #2a3b4b;
        }

        .quick-bet button:hover {
            background: #2d3f52;
            color: #f5b342;
            border-color: #f5b342;
        }

        .action-buttons {
            display: flex;
            gap: 14px;
        }

        .btn-bet, .btn-cashout {
            flex: 1;
            border: none;
            border-radius: 60px;
            padding: 18px 10px;
            font-weight: 800;
            font-size: 18px;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            cursor: pointer;
            transition: 0.15s;
            box-shadow: 0 8px 0 #0a0f14;
            text-transform: uppercase;
        }

        .btn-bet {
            background: #f5b342;
            color: #0b0f17;
            box-shadow: 0 6px 0 #b87d1c;
        }

        .btn-bet:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #b87d1c;
        }

        .btn-cashout {
            background: #2dc78f;
            color: #0b0f17;
            box-shadow: 0 6px 0 #1e8a62;
        }

        .btn-cashout:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #1e8a62;
        }

        .btn-cashout:disabled {
            background: #2a3a47;
            color: #6b7d8d;
            box-shadow: 0 6px 0 #1b252e;
            cursor: not-allowed;
            transform: none;
        }

        /* right column – payment & withdraw */
        .payment-section {
            flex: 1 1 280px;
            display: flex;
            flex-direction: column;
            gap: 18px;
        }

        .card-panel {
            background: #0e141d;
            border-radius: 28px;
            padding: 22px 18px;
            border: 1px solid #202b38;
            box-shadow: 0 8px 0 rgba(0, 0, 0, 0.3);
        }

        .card-panel h3 {
            font-size: 18px;
            font-weight: 600;
            color: #d6e2f0;
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 18px;
        }

        .card-panel h3 i {
            color: #f5b342;
            font-size: 20px;
        }

        .payment-methods {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 18px;
        }

        .method {
            background: #1b2531;
            border-radius: 18px;
            padding: 12px 12px;
            flex: 1 0 70px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 6px;
            border: 1px solid #2d3d4e;
            cursor: pointer;
            transition: 0.15s;
            color: #b7c7d9;
        }

        .method i {
            font-size: 24px;
            color: #f5b342;
        }

        .method span {
            font-size: 12px;
            font-weight: 500;
        }

        .method:hover {
            background: #25323f;
            border-color: #f5b342;
        }

        .method.active {
            border-color: #f5b342;
            background: #1f2b37;
            box-shadow: 0 0 0 1px #f5b342;
        }

        .amount-input {
            background: #1b2531;
            border-radius: 60px;
            display: flex;
            align-items: center;
            padding: 0 10px 0 18px;
            border: 1px solid #2d3d4e;
            margin-bottom: 16px;
        }

        .amount-input i {
            color: #7f8f9f;
        }

        .amount-input input {
            background: transparent;
            border: none;
            padding: 16px 8px;
            font-size: 16px;
            font-weight: 600;
            color: #fff;
            width: 100%;
            outline: none;
        }

        .action-pay {
            background: #f5b342;
            border: none;
            border-radius: 60px;
            padding: 18px;
            width: 100%;
            font-weight: 800;
            font-size: 18px;
            color: #0b0f17;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            box-shadow: 0 6px 0 #b87d1c;
            transition: 0.1s;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .action-pay:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #b87d1c;
        }

        /* withdrawal card specific */
        .withdraw-card {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .withdraw-options {
            display: flex;
            gap: 12px;
            margin-bottom: 12px;
        }

        .withdraw-option {
            flex: 1;
            background: #1b2531;
            border: 1px solid #2d3d4e;
            border-radius: 16px;
            padding: 12px 6px;
            text-align: center;
            font-size: 13px;
            font-weight: 600;
            color: #b7c7d9;
            cursor: pointer;
            transition: 0.15s;
        }

        .withdraw-option i {
            display: block;
            font-size: 20px;
            margin-bottom: 6px;
            color: #f5b342;
        }

        .withdraw-option:hover {
            background: #25323f;
            border-color: #f5b342;
        }

        .withdraw-option.active {
            border-color: #f5b342;
            background: #1f2b37;
            color: #fff;
        }

        .btn-withdraw {
            background: #2dc78f;
            border: none;
            border-radius: 60px;
            padding: 16px;
            font-weight: 800;
            font-size: 16px;
            color: #0b0f17;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            box-shadow: 0 6px 0 #1e8a62;
            transition: 0.1s;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-top: 8px;
        }

        .btn-withdraw:active {
            transform: translateY(3px);
            box-shadow: 0 3px 0 #1e8a62;
        }

        .btn-withdraw:disabled {
            background: #2a3a47;
            color: #6b7d8d;
            box-shadow: 0 6px 0 #1b252e;
            cursor: not-allowed;
            transform: none;
        }

        /* message toast */
        .toast-msg {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: #1e2b3a;
            color: #f5b342;
            padding: 14px 28px;
            border-radius: 60px;
            font-weight: 600;
            font-size: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7);
            border: 1px solid #f5b342;
            z-index: 999;
            opacity: 0;
            transition: opacity 0.2s;
            pointer-events: none;
            white-space: nowrap;
        }

        .toast-msg.show {
            opacity: 1;
        }

        /* responsive tweaks */
        @media (max-width: 720px) {
            .app {
                padding: 14px 12px;
                border-radius: 28px;
            }

            .dashboard {
                flex-direction: column;
            }

            .aviator-section {
                flex: 1 1 auto;
                padding: 16px 12px;
            }

            .payment-section {
                flex: 1 1 auto;
            }

            .btn-bet, .btn-cashout {
                font-size: 16px;
                padding: 16px 8px;
            }

            .multiplier-badge {
                font-size: 17px;
                padding: 4px 12px;
            }

            .balance-pill .amount {
                font-size: 14px;
            }

            .toast-msg {
                white-space: normal;
                text-align: center;
                max-width: 90%;
                font-size: 13px;
            }
        }

        @media (max-width: 400px) {
            .quick-bet button {
                padding: 6px 8px;
                font-size: 12px;
            }

            .action-buttons {
                flex-direction: column;
            }

            .withdraw-options {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="app">
        <!-- header -->
        <div class="header">
            <div class="logo">
                <div class="logo-icon"><i class="fas fa-plane"></i></div>
                <div class="logo-text">SKY<span>AVIA</span></div>
            </div>
            <div class="balance-pill">
                <i class="fas fa-wallet"></i>
                <span class="amount" id="balanceDisplay">$1,250.00</span>
                <span class="currency">USD</span>
            </div>
        </div>

        <!-- main dashboard -->
        <div class="dashboard">
            <!-- left: aviator game -->
            <div class="aviator-section">
                <div class="game-header">
                    <h2><i class="fas fa-chart-line"></i> AVIATOR</h2>
                    <div class="multiplier-badge" id="multiplierDisplay">1.00x</div>
                </div>

                <!-- canvas graph -->
                <div class="canvas-wrap">
                    <canvas id="aviatorCanvas" width="800" height="400"></canvas>
                </div>

                <!-- game info -->
                <div class="game-stats">
                    <div class="stat-item"><i class="fas fa-clock"></i> Next round: <span class="stat-value" id="countdownDisplay">5.0s</span></div>
                    <div class="stat-item"><i class="fas fa-history"></i> Last: <span class="stat-value" id="lastMultiplier">2.41x</span></div>
                </div>

                <!-- bet controls -->
                <div class="bet-controls">
                    <div class="bet-input-row">
                        <div class="bet-amount">
                            <i class="fas fa-dollar-sign"></i>
                            <input type="number" id="betAmount" value="10.00" step="1" min="1" placeholder="Bet amount">
                        </div>
                        <div class="quick-bet">
                            <button data-bet="5">$5</button>
                            <button data-bet="10">$10</button>
                            <button data-bet="50">$50</button>
                            <button data-bet="100">$100</button>
                        </div>
                    </div>
                    <div class="action-buttons">
                        <button class="btn-bet" id="placeBetBtn"><i class="fas fa-play"></i> BET</button>
                        <button class="btn-cashout" id="cashoutBtn" disabled><i class="fas fa-hand-holding-usd"></i> CASHOUT</button>
                    </div>
                </div>
            </div>

            <!-- right: payments & withdraw -->
            <div class="payment-section">
                <!-- deposit card -->
                <div class="card-panel">
                    <h3><i class="fas fa-credit-card"></i> Deposit</h3>
                    <div class="payment-methods">
                        <div class="method active" data-method="visa">
                            <i class="fab fa-cc-visa"></i>
                            <span>Visa</span>
                        </div>
                        <div class="method" data-method="mastercard">
                            <i class="fab fa-cc-mastercard"></i>
                            <span>Mastercard</span>
                        </div>
                        <div class="method" data-method="crypto">
                            <i class="fab fa-bitcoin"></i>
                            <span>Crypto</span>
                        </div>
                    </div>
                    <div class="amount-input">
                        <i class="fas fa-dollar-sign"></i>
                        <input type="number" id="depositAmount" value="50.00" step="1" min="5" placeholder="Deposit amount">
                    </div>
                    <button class="action-pay" id="payNowBtn"><i class="fas fa-lock"></i> PAY NOW</button>
                </div>

                <!-- withdraw card -->
                <div class="card-panel withdraw-card">
                    <h3><i class="fas fa-money-bill-wave"></i> Withdraw</h3>
                    <div class="withdraw-options">
                        <div class="withdraw-option active" data-withdraw="bank">
                            <i class="fas fa-university"></i> Bank
                        </div>
                        <div class="withdraw-option" data-withdraw="card">
                            <i class="fas fa-credit-card"></i> Card
                        </div>
                        <div class="withdraw-option" data-withdraw="crypto">
                            <i class="fab fa-bitcoin"></i> Crypto
                        </div>
                    </div>
                    <div class="amount-input">
                        <i class="fas fa-dollar-sign"></i>
                        <input type="number" id="withdrawAmount" value="20.00" step="1" min="10" placeholder="Withdraw amount">
                    </div>
                    <button class="btn-withdraw" id="withdrawBtn"><i class="fas fa-arrow-up"></i> WITHDRAW</button>
                </div>
            </div>
        </div>
    </div>

    <!-- toast message -->
    <div id="toast" class="toast-msg">Message</div>

    <script>
        (function() {
            // ---------- STATE ----------
            let balance = 1250.00;
            const balanceDisplay = document.getElementById('balanceDisplay');
            const multiplierDisplay = document.getElementById('multiplierDisplay');
            const countdownDisplay = document.getElementById('countdownDisplay');
            const lastMultiplierEl = document.getElementById('lastMultiplier');
            const betAmountInput = document.getElementById('betAmount');
            const placeBetBtn = document.getElementById('placeBetBtn');
            const cashoutBtn = document.getElementById('cashoutBtn');
            const canvas = document.getElementById('aviatorCanvas');
            const ctx = canvas.getContext('2d');

            // game state
            let currentMultiplier = 1.00;
            let gameState = 'waiting'; // 'waiting' | 'flying' | 'crashed'
            let countdown = 5.0;
            let crashMultiplier = 2.50; // will be set each round
            let hasActiveBet = false;
            let betAmount = 10.00;
            let animationFrame = null;
            let flightStartTime = 0;
            let flightDuration = 4000; // ms until crash
            let lastMultiplier = 2.41;

            // UI update
            function updateBalanceUI() {
                balanceDisplay.textContent = `$${balance.toFixed(2)}`;
            }

            // toast helper
            const toastEl = document.getElementById('toast');
            let toastTimeout;
            function showToast(msg, isError = false) {
                toastEl.textContent = msg;
                toastEl.style.color = isError ? '#ff7b7b' : '#f5b342';
                toastEl.classList.add('show');
                clearTimeout(toastTimeout);
                toastTimeout = setTimeout(() => {
                    toastEl.classList.remove('show');
                }, 2200);
            }

            // ---------- DRAW CANVAS (Aviator curve) ----------
            function drawCanvas(multiplier = 1.0, crashed = false) {
                const w = canvas.width;
                const h = canvas.height;
                ctx.clearRect(0, 0, w, h);

                // background grid
                ctx.strokeStyle = '#1e2d3b';
                ctx.lineWidth = 1;
                for (let i = 0; i < w; i += 40) {
                    ctx.beginPath();
                    ctx.moveTo(i, 0);
                    ctx.lineTo(i, h);
                    ctx.strokeStyle = '#15212b';
                    ctx.stroke();
                }
                for (let i = 0; i < h; i += 40) {
                    ctx.beginPath();
                    ctx.moveTo(0, i);
                    ctx.lineTo(w, i);
                    ctx.strokeStyle = '#15212b';
                    ctx.stroke();
                }

                // draw flight path (aviator style curve)
                const progress = Math.min((multiplier - 1) / 2.5, 1.0); // 0..1
                const points = [];
                const maxPoints = 80;
                for (let i = 0; i <= maxPoints; i++) {
                    const t = i / maxPoints;
                    const x = 60 + t * (w - 160);
                    // exponential-ish curve
                    const y = h - 60 - Math.pow(t, 1.8) * (h - 120) * 0.9 * (crashed ? 0.8 : 1);
                    points.push({ x, y });
                }

                // draw filled area under curve
                ctx.beginPath();
                ctx.moveTo(60, h - 60);
                points.forEach(p => ctx.lineTo(p.x, p.y));
                ctx.lineTo(w - 100, h - 60);
                ctx.closePath();
                const gradient = ctx.createLinearGradient(0, h, 0, 100);
                gradient.addColorStop(0, 'rgba(245, 179, 66, 0.15)');
                gradient.addColorStop(1, 'rgba(245, 179, 66, 0.01)');
                ctx.fillStyle = gradient;
                ctx.fill();

                // draw the line
                ctx.beginPath();
                ctx.moveTo(points[0].x, points[0].y);
                points.forEach(p => ctx.lineTo(p.x, p.y));
                ctx.strokeStyle = crashed ? '#ff5e5e' : '#f5b342';
                ctx.lineWidth = 4;
                ctx.shadowColor = crashed ? '#ff5e5e' : '#f5b342';
                ctx.shadowBlur = 18;
                ctx.stroke();

                // plane icon at end
                const last = points[points.length - 1];
                ctx.shadowBlur = 24;
                ctx.font = '30px "Font Awesome 6 Free"';
                ctx.fillStyle = crashed ? '#ff5e5e' : '#f5b342';
                ctx.fillText('\uf072', last.x - 12, last.y - 12);

                // reset shadow
                ctx.shadowBlur = 0;
                ctx.shadowColor = 'transparent';

                // axis labels
                ctx.font = '12px monospace';
                ctx.fillStyle = '#62788c';
                ctx.fillText('1.0x', 20, h - 20);
                ctx.fillText('2.0x', w - 80, h - 20);
                ctx.fillText('3.0x', w - 30, h - 20);
            }

            // ---------- GAME LOOP ----------
            function startFlight() {
                gameState = 'flying';
                currentMultiplier = 1.00;
                flightStartTime = performance.now();
                crashMultiplier = 1.8 + Math.random() * 4.2; // 1.8 .. 6.0
                if (crashMultiplier < 1.5) crashMultiplier = 1.5;
                flightDuration = 2500 + (crashMultiplier * 600); // dynamic duration
                if (hasActiveBet) {
                    cashoutBtn.disabled = false;
                } else {
                    cashoutBtn.disabled = true;
                }
                placeBetBtn.disabled = true;
                updateCountdown(0);
                animateFlight();
            }

            function animateFlight() {
                if (gameState !== 'flying') return;

                const now = performance.now();
                const elapsed = now - flightStartTime;
                const progress = Math.min(elapsed / flightDuration, 1.0);
                // multiplier curve: 1.0 -> crashMultiplier
                const eased = Math.pow(progress, 1.6);
                currentMultiplier = 1.0 + (crashMultiplier - 1.0) * eased;
                if (currentMultiplier > crashMultiplier) currentMultiplier = crashMultiplier;

                multiplierDisplay.textContent = currentMultiplier.toFixed(2) + 'x';
                drawCanvas(currentMultiplier, false);

                if (progress >= 1.0) {
                    // crash
                    gameState = 'crashed';
                    currentMultiplier = crashMultiplier;
                    multiplierDisplay.textContent = currentMultiplier.toFixed(2) + 'x';
                    drawCanvas(currentMultiplier, true);
                    lastMultiplier = currentMultiplier;
                    lastMultiplierEl.textContent = lastMultiplier.toFixed(2) + 'x';

                    // if bet active -> lost
                    if (hasActiveBet) {
                        hasActiveBet = false;
                        betAmount = 0;
                        cashoutBtn.disabled = true;
                        showToast(`Crashed at ${crashMultiplier.toFixed(2)}x — bet lost`, true);
                    }

                    // reset countdown
                    gameState = 'waiting';
                    countdown = 5.0;
                    updateCountdown(countdown);
                    placeBetBtn.disabled = false;
                    // schedule next round
                    setTimeout(() => {
                        if (gameState === 'waiting') {
                            startFlight();
                        }
                    }, 5200);
                    return;
                }

                animationFrame = requestAnimationFrame(animateFlight);
            }

            function updateCountdown(value) {
                countdown = value;
                countdownDisplay.textContent = countdown.toFixed(1) + 's';
            }

            // countdown timer for waiting state
            let countdownInterval = null;
            function startCountdownTimer() {
                if (countdownInterval) clearInterval(countdownInterval);
                countdownInterval = setInterval(() => {
                    if (gameState === 'waiting' && countdown > 0) {
                        countdown = Math.max(0, countdown - 0.1);
                        updateCountdown(countdown);
                        if (countdown <= 0.05) {
                            // start flight
                            if (gameState === 'waiting') {
                                startFlight();
                            }
                        }
                    }
                }, 100);
            }

            // ---------- PLACE BET / CASHOUT ----------
            function placeBet() {
                if (gameState === 'flying') {
                    showToast('Cannot bet while flying', true);
                    return;
                }
                if (gameState === 'waiting' && countdown < 1.2) {
                    showToast('Too late to bet', true);
                    return;
                }
                const amt = parseFloat(betAmountInput.value);
                if (isNaN(amt) || amt < 1) {
                    showToast('Minimum bet is $1', true);
                    return;
                }
                if (amt > balance) {
                    showToast('Insufficient balance', true);
                    return;
                }
                if (hasActiveBet) {
                    showToast('Already have an active bet', true);
                    return;
                }

                // deduct
                balance -= amt;
                updateBalanceUI();
                hasActiveBet = true;
                betAmount = amt;
                cashoutBtn.disabled = false;
                showToast(`Bet $${amt.toFixed(2)} placed!`);

                // if game already waiting, we might start soon
                if (gameState === 'waiting' && countdown <= 0.1) {
                    // will auto start in next tick
                }
            }

            function cashout() {
                if (!hasActiveBet || gameState !== 'flying') {
                    showToast('No active bet to cashout', true);
                    return;
                }
                const winAmount = betAmount * currentMultiplier;
                balance += winAmount;
                updateBalanceUI();
                hasActiveBet = false;
                cashoutBtn.disabled = true;
                showToast(`Cashed out at ${currentMultiplier.toFixed(2)}x — won $${winAmount.toFixed(2)}!`);
                // continue flight (no more bet)
            }

            // ---------- PAYMENT & WITHDRAWAL ----------
            document.getElementById('payNowBtn').addEventListener('click', function() {
                const depAmount = parseFloat(document.getElementById('depositAmount').value);
                if (isNaN(depAmount) || depAmount < 5) {
                    showToast('Minimum deposit is $5', true);
                    return;
                }
                if (depAmount > 5000) {
                    showToast('Maximum deposit $5000', true);
                    return;
                }
                balance += depAmount;
                updateBalanceUI();
                showToast(`Deposit of $${depAmount.toFixed(2)} successful!`);
            });

            document.getElementById('withdrawBtn').addEventListener('click', function() {
                const wAmount = parseFloat(document.getElementById('withdrawAmount').value);
                if (isNaN(wAmount) || wAmount < 10) {
                    showToast('Minimum withdrawal is $10', true);
                    return;
                }
                if (wAmount > balance) {
                    showToast('Insufficient balance', true);
                    return;
                }
                balance -= wAmount;
                updateBalanceUI();
                showToast(`Withdrawal request of $${wAmount.toFixed(2)} submitted.`);
            });

            // ---------- INIT & EVENT LISTENERS ----------
            function initGame() {
                updateBalanceUI();
                drawCanvas(1.0, false);
                multiplierDisplay.textContent = '1.00x';
                updateCountdown(5.0);

                // start countdown then flight
                startCountdownTimer();

                // First round will start after countdown
                // also schedule initial flight
                setTimeout(() => {
                    if (gameState === 'waiting' && countdown <= 0.1) {
                        startFlight();
                    }
                }, 5200);
            }

            // bet button
            placeBetBtn.addEventListener('click', placeBet);
            cashoutBtn.addEventListener('click', cashout);

            // quick bet buttons
            document.querySelectorAll('.quick-bet button').forEach(btn => {
                btn.addEventListener('click', function() {
                    const val = this.getAttribute('data-bet');
                    betAmountInput.value = val;
                });
            });

            // payment method selection (visual only)
            document.querySelectorAll('.method').forEach(m => {
                m.addEventListener('click', function() {
                    document.querySelectorAll('.method').forEach(mm => mm.classList.remove('active'));
                    this.classList.add('active');
                });
            });

            // withdraw selection
            document.querySelectorAll('.withdraw-option').forEach(opt => {
                opt.addEventListener('click', function() {
                    document.querySelectorAll('.withdraw-option').forEach(o => o.classList.remove('active'));
                    this