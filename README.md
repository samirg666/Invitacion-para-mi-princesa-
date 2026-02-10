<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para mi persona favorita 💘</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff4d6d;
            --secondary: #ff758c;
            --accent: #80ffdb;
            --bg-gradient: linear-gradient(45deg, #1a0b2e, #4a1e6e, #2a0944);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: var(--bg-gradient);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Corazones flotantes de fondo */
        .heart-particle {
            position: absolute;
            color: rgba(255, 77, 109, 0.4);
            pointer-events: none;
            z-index: 1;
            animation: floatUp linear infinite;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0); opacity: 0; }
            50% { opacity: 0.8; }
            100% { transform: translateY(-10vh) scale(1.5); opacity: 0; }
        }

        .container {
            max-width: 600px;
            width: 90%;
            padding: 50px 30px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            border-radius: 40px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
            z-index: 10;
            text-align: center;
            transition: all 0.5s ease;
        }

        h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 4rem;
            margin-bottom: 20px;
            background: linear-gradient(to right, #ff8fa3, #ff4d6d, #c9184a);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 5px #ff4d6d); }
            to { filter: drop-shadow(0 0 15px #ff8fa3); }
        }

        p {
            font-size: 1.2rem;
            line-height: 1.6;
            margin-bottom: 30px;
            color: #fce4ec;
        }

        .btn-container {
            display: flex;
            gap: 20px;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            margin-top: 30px;
        }

        button {
            padding: 15px 35px;
            font-size: 1.2rem;
            font-weight: 600;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        #yesBtn {
            background: #ff4d6d;
            color: white;
            box-shadow: 0 10px 20px rgba(255, 77, 109, 0.4);
        }

        #yesBtn:hover {
            transform: scale(1.1);
            background: #ff758c;
            box-shadow: 0 15px 30px rgba(255, 77, 109, 0.6);
        }

        #noBtn {
            background: #6c757d;
            color: white;
            position: relative;
            z-index: 11;
        }

        .hidden { display: none; }

        .fade-in {
            animation: fadeIn 1s forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .hearts-final {
            font-size: 3rem;
            margin-top: 20px;
        }

        @media (max-width: 480px) {
            h1 { font-size: 2.8rem; }
            .container { padding: 30px 20px; }
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
</head>
<body>

    <div id="screen1" class="container fade-in">
        <h1>¡Hola, especial! 💘</h1>
        <p>Tengo algo muy importante que preguntarte... <br> ¿Te gustaría ser mi cita perfecta para este San Valentín?</p>
        
        <div class="btn-container">
            <button id="yesBtn" onclick="celebrate()">¡SÍ, ACEPTO! 😍</button>
            <button id="noBtn" onmouseover="moveNoButton()">No 😢</button>
        </div>
    </div>

    <div id="screen2" class="container hidden">
        <h1>¡SABÍA QUE SÍ! 🌟</h1>
        <p>Has hecho mi día el más feliz de todos. <br> 
        Nos vemos a las <b>8:00 PM</b> en nuestro lugar favorito. <br>
        ¡Prepárate para una noche inolvidable!</p>
        <div class="hearts-final">💑 ✨ 🎁 🌹 💖</div>
    </div>

    <audio id="romanticSound" loop>
        <source src="https://docs.google.com/uc?export=download&id=1ZctXOc2RT5R4VDy3k53L5K5J94vkg_I_" type="audio/mpeg">
    </audio>

    <script>
        // Iniciar corazones de fondo al cargar
        function createHearts() {
            const container = document.body;
            for (let i = 0; i < 25; i++) {
                const heart = document.createElement('div');
                heart.className = 'heart-particle';
                heart.innerHTML = '❤️';
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.fontSize = (Math.random() * 20 + 10) + 'px';
                heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
                heart.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(heart);
            }
        }
        createHearts();

        // Mover el botón "No" aleatoriamente
        function moveNoButton() {
            const btn = document.getElementById('noBtn');
            const x = Math.random() * (window.innerWidth - btn.offsetWidth);
            const y = Math.random() * (window.innerHeight - btn.offsetHeight);
            
            btn.style.position = 'absolute';
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';
        }

        // Función de celebración
        function celebrate() {
            // Cambiar pantallas
            document.getElementById('screen1').classList.add('hidden');
            const s2 = document.getElementById('screen2');
            s2.classList.remove('hidden');
            s2.classList.add('fade-in');

            // Reproducir música (los navegadores permiten audio tras este click)
            const audio = document.getElementById('romanticSound');
            audio.volume = 0.5;
            audio.play();

            // Lanzar confeti continuo
            const duration = 15 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            function randomInRange(min, max) {
              return Math.random() * (max - min) + min;
            }

            const interval = setInterval(function() {
              const timeLeft = animationEnd - Date.now();

              if (timeLeft <= 0) {
                return clearInterval(interval);
              }

              const particleCount = 50 * (timeLeft / duration);
              confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
              confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
            }, 250);
        }

        // Activar música al primer toque en cualquier parte (por si acaso no dan clic al botón rápido)
        document.body.addEventListener('click', () => {
            const audio = document.getElementById('romanticSound');
            if (audio.paused && !document.getElementById('screen2').classList.contains('hidden')) {
                audio.play();
            }
        }, { once: true });

    </script>
</body>
</html>
