<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para mi amor 🧡</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #ffb3b3;
            --grid-color: #ff9999;
            --card-bg: #fffbf2;
            --border-color: #5d4037;
            --accent-orange: #ff8c42;
            --text-main: #5d4037;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Press Start 2P', cursive; }

        body {
            /* Fondo de cuadros Pixel Art */
            background-color: var(--bg-color);
            background-image: 
                linear-gradient(45deg, var(--grid-color) 25%, transparent 25%), 
                linear-gradient(-45deg, var(--grid-color) 25%, transparent 25%), 
                linear-gradient(45deg, transparent 75%, var(--grid-color) 75%), 
                linear-gradient(-45deg, transparent 75%, var(--grid-color) 75%);
            background-size: 60px 60px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Corazones flotantes decorativos */
        .floating-heart {
            position: absolute;
            color: white;
            opacity: 0.6;
            font-size: 20px;
            animation: float 6s infinite linear;
            z-index: 1;
            pointer-events: none;
        }

        @keyframes float {
            0% { transform: translateY(110vh) rotate(0deg); opacity: 0; }
            50% { opacity: 0.8; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        /* Interfaz tipo Ventana de Videojuego */
        .window {
            background: var(--card-bg);
            border: 6px solid var(--border-color);
            box-shadow: 12px 12px 0px rgba(0,0,0,0.1);
            width: 90%;
            max-width: 500px;
            position: relative;
            z-index: 10;
            padding: 0;
            image-rendering: pixelated;
        }

        .window-header {
            background: var(--accent-orange);
            border-bottom: 6px solid var(--border-color);
            padding: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header-dot {
            width: 15px; height: 15px;
            background: var(--border-color);
            box-shadow: 4px 4px 0px rgba(0,0,0,0.1);
        }

        .content {
            padding: 30px 20px;
            text-align: center;
        }

        h1 { font-size: 0.9rem; color: var(--text-main); line-height: 1.6; margin-bottom: 20px; }
        .subtitle { font-size: 0.55rem; color: var(--text-main); line-height: 1.8; margin-bottom: 25px; }

        /* Botones Pixel */
        .btn-container { display: flex; justify-content: center; gap: 15px; flex-wrap: wrap; }

        .pixel-btn {
            background: white;
            border: 4px solid var(--border-color);
            padding: 15px;
            font-size: 0.55rem;
            cursor: pointer;
            box-shadow: 6px 6px 0px var(--border-color);
            transition: all 0.1s;
            color: var(--text-main);
            outline: none;
        }

        .pixel-btn:active { transform: translate(4px, 4px); box-shadow: 0px 0px 0px; }
        .pixel-btn.primary { background: var(--accent-orange); color: white; }

        /* Contador y Carta */
        #countdown {
            font-size: 0.7rem;
            color: #d35400;
            background: #fdf2e9;
            border: 4px solid var(--border-color);
            padding: 15px;
            margin: 20px 0;
            display: inline-block;
            width: 100%;
        }

        .letter-box {
            font-size: 0.5rem;
            line-height: 1.8;
            text-align: left;
            padding: 20px;
            background: #fff;
            border: 4px solid var(--border-color);
            max-height: 250px;
            overflow-y: auto;
            color: var(--text-main);
        }

        #patience-msg {
            color: #e74c3c;
            font-size: 0.55rem;
            height: 25px;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="hearts-container"></div>

    <div id="screen1" class="window">
        <div class="window-header">
            <div class="header-dot"></div>
            <span style="font-size: 0.5rem; color: white;">MENSAJE_NUEVO.EXE</span>
            <div class="header-dot"></div>
        </div>
        <div class="content">
            <h1>¡HOLA, MI GORDA! 🧡</h1>
            <p class="subtitle">¿QUISIERAS PASAR UN SAN VALENTÍN INOLVIDABLE A MI LADO?</p>
            <div class="btn-container">
                <button class="pixel-btn primary" onclick="accept()">¡SÍ, ACEPTO! ❤️</button>
                <button id="noBtn" class="pixel-btn" onmouseover="moveNo()">NO 🙈</button>
            </div>
        </div>
    </div>

    <div id="screen2" class="window hidden">
        <div class="window-header">
            <div class="header-dot"></div>
            <span style="font-size: 0.5rem; color: white;">CONFIRMADO.EXE</span>
            <div class="header-dot"></div>
        </div>
        <div class="content">
            <h1>¡SABÍA QUE SÍ!</h1>
            <div style="font-size: 4rem; margin: 20px 0; cursor: pointer;" onclick="tryOpen()">✉️</div>
            <div id="patience-msg"></div>
            <button class="pixel-btn primary" onclick="tryOpen()">ABRIR CARTA</button>
        </div>
    </div>

    <div id="screen3" class="window hidden">
        <div class="window-header">
            <div class="header-dot"></div>
            <span id="window-title" style="font-size: 0.5rem; color: white;">ESPERANDO...</span>
            <div class="header-dot"></div>
        </div>
        <div class="content">
            <div id="countdownBox">
                <p class="subtitle">SE REVELARÁ EL 14 A LAS 8:00 PM</p>
                <div id="countdown">00:00:00</div>
            </div>
            
            <div id="fullLetter" class="letter-box hidden">
                Mi amor,<br><br>
                Hoy me detuve a pensar en todo el camino que hemos recorrido. Eres el hilo conductor de mis mejores recuerdos.<br><br>
                San Valentín ya no es solo flores, es saber que nuestra historia es real. Gracias por ser mi paz y mi risa. Te elijo cada mañana.<br><br>
                Eres mi hogar. Te amo hoy más que nunca.
            </div>
            
            <button class="pixel-btn" onclick="goBack()" style="margin-top: 20px;">VOLVER</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <script>
        // CONFIGURACIÓN: 14 de Febrero a las 8:00 PM (20:00:00)
        const targetDate = new Date("February 14, 2026 20:00:00").getTime();

        // Generar corazones flotantes de fondo
        const heartsContainer = document.getElementById('hearts-container');
        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'floating-heart';
            heart.innerHTML = '❤';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
            heartsContainer.appendChild(heart);
            setTimeout(() => heart.remove(), 6000);
        }
        setInterval(createHeart, 400);

        function moveNo() {
            const btn = document.getElementById('noBtn');
            btn.style.position = 'absolute';
            btn.style.left = Math.random() * 80 + '%';
            btn.style.top = Math.random() * 80 + '%';
        }

        function accept() {
            document.getElementById('screen1').classList.add('hidden');
            document.getElementById('screen2').classList.remove('hidden');
            confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 }, colors: ['#ff8c42', '#ffffff', '#ffb3b3'] });
        }

        function tryOpen() {
            const now = new Date().getTime();
            const msg = document.getElementById('patience-msg');
            
            if (now < targetDate) {
                msg.innerText = "SE PACIENTE GORDA 🧡";
                setTimeout(() => { msg.innerText = ""; }, 3000);
            }
            
            document.getElementById('screen2').classList.add('hidden');
            document.getElementById('screen3').classList.remove('hidden');
            updateClock();
            setInterval(updateClock, 1000);
        }

        function updateClock() {
            const now = new Date().getTime();
            const diff = targetDate - now;
            const display = document.getElementById('countdown');
            const letter = document.getElementById('fullLetter');
            const box = document.getElementById('countdownBox');
            const title = document.getElementById('window-title');

            if (diff <= 0) {
                box.classList.add('hidden');
                letter.classList.remove('hidden');
                title.innerText = "TU CARTA DE AMOR.EXE";
            } else {
                const d = Math.floor(diff / (1000 * 60 * 60 * 24));
                const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                const s = Math.floor((diff % (1000 * 60)) / 1000);
                display.innerText = `${d}D ${h}H ${m}M ${s}S`;
                title.innerText = "ESPERANDO...";
            }
        }

        function goBack() {
            document.getElementById('screen3').classList.add('hidden');
            document.getElementById('screen2').classList.remove('hidden');
        }
    </script>
</body>
</html>
