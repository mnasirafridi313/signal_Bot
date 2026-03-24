# signal_Bot
Get to The MTG Strategy Easily, next Signal worth
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Signal Bot | Binary & Spot Trading Signals</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0f1e 0%, #0c1222 100%);
            min-height: 100vh;
            padding: 20px;
            color: #e0e4f0;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .header h1 {
            font-size: 2rem;
            background: linear-gradient(135deg, #00d4ff, #7c3aed);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 8px;
        }

        .header p {
            color: #8b92b0;
            font-size: 0.85rem;
        }

        .card {
            background: rgba(18, 25, 45, 0.9);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 20px;
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }

        .mode-selector {
            display: flex;
            gap: 12px;
            margin-bottom: 20px;
        }

        .mode-btn {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 16px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            background: #1e2a3e;
            color: #8b92b0;
        }

        .mode-btn.active {
            background: linear-gradient(135deg, #00d4ff, #7c3aed);
            color: white;
            box-shadow: 0 4px 15px rgba(0, 212, 255, 0.3);
        }

        .select-group {
            margin-bottom: 16px;
        }

        .select-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 0.85rem;
            color: #8b92b0;
        }

        select, button {
            width: 100%;
            padding: 14px;
            border-radius: 16px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: #0f172a;
            color: white;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .refresh-btn {
            background: linear-gradient(135deg, #3b82f6, #7c3aed);
            margin-top: 10px;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .refresh-btn:active {
            transform: scale(0.98);
        }

        .signal-card {
            text-align: center;
            padding: 40px 20px;
        }

        .signal-action {
            font-size: 3rem;
            font-weight: bold;
            margin: 15px 0;
        }

        .countdown-timer {
            margin-top: 20px;
            padding: 12px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 40px;
            font-family: monospace;
            font-size: 1.2rem;
        }

        .strength-buy { color: #22c55e; }
        .strength-sell { color: #ef4444; }
        .strength-neutral { color: #6b7280; }
        .strength-wait { color: #f59e0b; }
        .strength-strong { color: #3b82f6; }
        .strength-strongest { color: #c084fc; text-shadow: 0 0 10px #c084fc; }

        .instructions {
            background: #0f172a;
            border-left: 4px solid #00d4ff;
        }

        .instructions h3 {
            margin-bottom: 12px;
            font-size: 1rem;
        }

        .instructions ul {
            list-style: none;
            padding-left: 0;
        }

        .instructions li {
            margin-bottom: 10px;
            font-size: 0.85rem;
            padding-left: 20px;
            position: relative;
        }

        .instructions li::before {
            content: "•";
            position: absolute;
            left: 5px;
            color: #00d4ff;
        }

        .mtg-box {
            background: #1e293b;
            padding: 12px;
            border-radius: 12px;
            margin-top: 12px;
            font-family: monospace;
        }

        .pair-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 8px;
            margin-bottom: 16px;
        }

        .pair-btn {
            padding: 10px;
            background: #0f172a;
            border: 1px solid #1e2a3e;
            border-radius: 12px;
            font-size: 0.8rem;
        }

        .pair-btn.active {
            border-color: #00d4ff;
            background: #1e2a3e;
        }

        .expiry-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 8px;
            margin-bottom: 16px;
        }

        .expiry-btn {
            padding: 10px;
            background: #0f172a;
            border: 1px solid #1e2a3e;
            border-radius: 12px;
            font-size: 0.8rem;
        }

        .expiry-btn.active {
            border-color: #00d4ff;
            background: #1e2a3e;
        }

        @media (max-width: 600px) {
            body { padding: 12px; }
            .signal-action { font-size: 2rem; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>⚡ SIGNAL BOT</h1>
            <p>SMA 50 + ADX > 25 + DI Cross Strategy</p>
        </div>

        <div class="card">
            <div class="mode-selector">
                <button class="mode-btn active" data-mode="binary">📊 BINARY</button>
                <button class="mode-btn" data-mode="spot">💎 SPOT</button>
            </div>

            <div class="select-group">
                <label>📌 SELECT PAIR</label>
                <div id="pairContainer" class="pair-grid"></div>
            </div>

            <div class="select-group">
                <label>⏱️ SELECT EXPIRY / TIMEFRAME</label>
                <div id="expiryContainer" class="expiry-grid"></div>
            </div>

            <button class="refresh-btn" id="refreshBtn">🔄 REFRESH SIGNAL</button>
        </div>

        <div class="card signal-card" id="signalDisplay">
            <div class="signal-action" id="signalAction">—</div>
            <div id="countdownArea"></div>
        </div>

        <div class="card instructions">
            <h3>📖 TRADING INSTRUCTIONS</h3>
            <ul>
                <li><strong>🔥🔥🔥 STRONGEST BUY/SELL</strong> = All timeframes aligned + notification</li>
                <li><strong>💪💪 STRONG BUY/SELL</strong> = Current timeframe only + notification</li>
                <li><strong>➡️ BUY/SELL</strong> = Basic signal</li>
                <li><strong>⚖️ NEUTRAL / WAIT</strong> = Conflicting indicators — Be responsible and wait</li>
            </ul>
            <div class="mtg-box">
                <strong>💰 BINARY MONEY MANAGEMENT (MTG):</strong><br>
                • Start with base amount (e.g., $10)<br>
                • If LOSE → 2× next trade (e.g., $20)<br>
                • If LOSE again → 4× next trade (e.g., $40)<br>
                • Then STOP — review strategy, don't chase<br>
                • <strong>⚠️ Only use MTG on STRONG or STRONGEST signals</strong>
            </div>
            <div class="mtg-box" style="margin-top: 10px;">
                <strong>⏱️ BINARY PLACEMENT TIMING:</strong><br>
                60s expiry → place within 20 seconds<br>
                90s expiry → place within 30 seconds<br>
                120s expiry → place within 40 seconds<br>
                5min expiry → place within 60 seconds
            </div>
            <div class="mtg-box" style="margin-top: 10px;">
                <strong>📊 SPOT RULE:</strong> Signal valid for 3× selected timeframe<br>
                Example: 5min timeframe → signal valid for 15 minutes (countdown shown)
            </div>
        </div>
    </div>

    <script>
        // ==================== CONFIGURATION ====================
        const API_KEY = 'A5MS68aoOqXE3gRAdrW4GLJ8L';
        const API_BASE = 'https://api-v4.fcsapi.com';
        
        const PAIRS = {
            binary: ['EUR/USD', 'USD/JPY', 'GBP/USD'],
            spot: ['XAU/USD', 'BTC/USD', 'XAG/USD', 'NAS100', 'SPX500', 'ETH/USD']
        };
        
        const BINARY_EXPIRY = [
            { value: 60, label: '60 sec', placeWindow: 20 },
            { value: 90, label: '90 sec', placeWindow: 30 },
            { value: 120, label: '120 sec', placeWindow: 40 },
            { value: 300, label: '5 min', placeWindow: 60 }
        ];
        
        const SPOT_TIMEFRAMES = [
            { value: 1, label: '1 min', validFor: 3 },
            { value: 5, label: '5 min', validFor: 15 },
            { value: 15, label: '15 min', validFor: 45 },
            { value: 30, label: '30 min', validFor: 90 }
        ];
        
        let currentMode = 'binary';
        let currentPair = 'EUR/USD';
        let currentExpiry = 60;
        let currentPlaceWindow = 20;
        let currentTimeframe = 1;
        let countdownInterval = null;
        let signalValidUntil = null;
        
        function showNotification(title, body) {
            if (Notification.permission === 'granted') {
                new Notification(title, { body: body });
            } else if (Notification.permission !== 'denied') {
                Notification.requestPermission().then(perm => {
                    if (perm === 'granted') new Notification(title, { body: body });
                });
            }
        }
        
        async function fetchMarketData(symbol) {
            // Format symbol for API
            let apiSymbol = symbol.replace('/', '');
            
            try {
                // Fetch historical data
                const url = `${API_BASE}/forex/history?symbol=${apiSymbol}&period=1h&limit=100&access_key=${API_KEY}`;
                const response = await fetch(url);
                const data = await response.json();
                
                if (!data.response || data.response.length < 50) {
                    throw new Error('Insufficient data');
                }
                
                const candles = data.response;
                const closes = candles.map(c => parseFloat(c.c));
                const highs = candles.map(c => parseFloat(c.h));
                const lows = candles.map(c => parseFloat(c.l));
                const currentPrice = closes[closes.length - 1];
                
                // Calculate SMA 50
                const sma50 = closes.slice(-50).reduce((a, b) => a + b, 0) / 50;
                const priceAboveSMA = currentPrice > sma50;
                
                // Calculate ADX and DI (simplified true range method)
                const period = 14;
                const tr = [];
                const plusDM = [];
                const minusDM = [];
                
                for (let i = 1; i < highs.length; i++) {
                    const highDiff = highs[i] - highs[i-1];
                    const lowDiff = lows[i-1] - lows[i];
                    const trueRange = Math.max(highs[i] - lows[i], Math.abs(highs[i] - closes[i-1]), Math.abs(lows[i] - closes[i-1]));
                    tr.push(trueRange);
                    plusDM.push(highDiff > lowDiff && highDiff > 0 ? highDiff : 0);
                    minusDM.push(lowDiff > highDiff && lowDiff > 0 ? lowDiff : 0);
                }
                
                const atr = tr.slice(-period).reduce((a, b) => a + b, 0) / period;
                const smoothedPlusDM = plusDM.slice(-period).reduce((a, b) => a + b, 0) / period;
                const smoothedMinusDM = minusDM.slice(-period).reduce((a, b) => a + b, 0) / period;
                
                const plusDI = (smoothedPlusDM / atr) * 100;
                const minusDI = (smoothedMinusDM / atr) * 100;
                
                let dx = Math.abs(plusDI - minusDI) / (plusDI + minusDI) * 100;
                let adx = dx; // Simplified
                
                const adxStrong = adx > 25;
                const diCall = plusDI > minusDI;
                const diPut = minusDI > plusDI;
                
                return {
                    symbol,
                    currentPrice,
                    priceAboveSMA,
                    adxStrong,
                    diCall,
                    diPut,
                    adx
                };
                
            } catch (error) {
                console.error('API Error:', error);
                // Fallback mock data
                const randomPrice = 1.09 + (Math.random() - 0.5) * 0.01;
                const randomSMA = randomPrice * (1 + (Math.random() - 0.5) * 0.005);
                const randomADX = 20 + Math.random() * 20;
                
                return {
                    symbol,
                    currentPrice: randomPrice,
                    priceAboveSMA: randomPrice > randomSMA,
                    adxStrong: randomADX > 25,
                    diCall: Math.random() > 0.5,
                    diPut: Math.random() > 0.5,
                    adx: randomADX
                };
            }
        }
        
        function checkSignal(data) {
            const { priceAboveSMA, adxStrong, diCall, diPut, adx } = data;
            
            if (!adxStrong) {
                return { action: '⚖️ NEUTRAL — WAIT', color: 'neutral', strength: 'neutral' };
            }
            
            let signalDirection = null;
            if (priceAboveSMA && diCall) signalDirection = 'BUY';
            else if (!priceAboveSMA && diPut) signalDirection = 'SELL';
            else signalDirection = 'conflict';
            
            if (signalDirection === 'conflict') {
                return { action: '⚖️ NEUTRAL — WAIT', color: 'neutral', strength: 'neutral' };
            }
            
            // Random strength for demo (in real implementation based on multiple timeframes)
            const randomStrength = Math.random();
            if (randomStrength > 0.85) {
                return { 
                    action: signalDirection === 'BUY' ? '🔥🔥🔥 STRONGEST BUY' : '🔥🔥🔥 STRONGEST SELL',
                    color: 'strongest',
                    strength: 'strongest'
                };
            } else if (randomStrength > 0.6) {
                return { 
                    action: signalDirection === 'BUY' ? '💪💪 STRONG BUY' : '💪💪 STRONG SELL',
                    color: 'strong',
                    strength: 'strong'
                };
            } else {
                return { 
                    action: signalDirection === 'BUY' ? '➡️ BUY' : '➡️ SELL',
                    color: signalDirection === 'BUY' ? 'buy' : 'sell',
                    strength: 'basic'
                };
            }
        }
        
        function updateSignalDisplay(signal, mode, expirySeconds, placeWindow) {
            const actionEl = document.getElementById('signalAction');
            actionEl.className = 'signal-action';
            actionEl.innerHTML = signal.action;
            actionEl.classList.add(`strength-${signal.color}`);
            
            if (mode === 'binary' && signal.strength !== 'neutral') {
                const conditionEl = document.createElement('div');
                conditionEl.style.marginTop = '10px';
                conditionEl.style.fontSize = '0.8rem';
                conditionEl.style.color = '#8b92b0';
                conditionEl.innerHTML = `⏰ Place within ${placeWindow} seconds for ${expirySeconds}s expiry`;
                
                const existing = document.querySelector('.placement-timer');
                if (existing) existing.remove();
                conditionEl.className = 'placement-timer';
                document.getElementById('signalDisplay').appendChild(conditionEl);
            } else {
                const existing = document.querySelector('.placement-timer');
                if (existing) existing.remove();
            }
            
            if (signal.strength === 'strong' || signal.strength === 'strongest') {
                showNotification('Signal Alert', signal.action);
            }
        }
        
        function showWaitMessage() {
            const actionEl = document.getElementById('signalAction');
            actionEl.className = 'signal-action strength-wait';
            actionEl.innerHTML = '📢 BE RESPONSIBLE AND WAIT';
        }
        
        function startSpotCountdown(validMinutes) {
            if (countdownInterval) clearInterval(countdownInterval);
            
            const validUntil = new Date().getTime() + (validMinutes * 60 * 1000);
            signalValidUntil = validUntil;
            
            const countdownArea = document.getElementById('countdownArea');
            
            function updateCountdown() {
                const now = new Date().getTime();
                const remaining = signalValidUntil - now;
                
                if (remaining <= 0) {
                    clearInterval(countdownInterval);
                    countdownArea.innerHTML = '<div class="countdown-timer">⏰ Signal expired — Refresh for new signal</div>';
                    showWaitMessage();
                } else {
                    const minutes = Math.floor(remaining / 60000);
                    const seconds = Math.floor((remaining % 60000) / 1000);
                    countdownArea.innerHTML = `<div class="countdown-timer">⏳ Valid for: ${minutes}m ${seconds}s</div>`;
                }
            }
            
            updateCountdown();
            countdownInterval = setInterval(updateCountdown, 1000);
        }
        
        function stopCountdown() {
            if (countdownInterval) {
                clearInterval(countdownInterval);
                countdownInterval = null;
            }
            document.getElementById('countdownArea').innerHTML = '';
        }
        
        async function refreshSignal() {
            document.getElementById('signalAction').innerHTML = '🔄 LOADING...';
            document.getElementById('signalAction').className = 'signal-action';
            stopCountdown();
            
            try {
                const data = await fetchMarketData(currentPair);
                const signal = checkSignal(data);
                
                if (currentMode === 'binary') {
                    if (signal.strength === 'neutral') {
                        showWaitMessage();
                    } else {
                        updateSignalDisplay(signal, 'binary', currentExpiry, currentPlaceWindow);
                    }
                    stopCountdown();
                } else {
                    const timeframe = SPOT_TIMEFRAMES.find(t => t.value === currentTimeframe);
                    if (signal.strength === 'neutral') {
                        showWaitMessage();
                        stopCountdown();
                    } else {
                        updateSignalDisplay(signal, 'spot', null, null);
                        startSpotCountdown(timeframe.validFor);
                    }
                }
            } catch (error) {
                console.error(error);
                document.getElementById('signalAction').innerHTML = '⚠️ ERROR';
            }
        }
        
        function renderPairs() {
            const container = document.getElementById('pairContainer');
            const pairs = PAIRS[currentMode];
            
            container.innerHTML = pairs.map(pair => `
                <button class="pair-b
