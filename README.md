<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Una Pregunta Especial! 💘</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Raleway:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Raleway', sans-serif;
        }
        body {
            background: linear-gradient(135deg, #1a0b2e, #4a1e6e);
            color: #fff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
            overflow: hidden;
            position: relative;
        }
        .container {
            max-width: 800px;
            padding: 40px;
            background-color: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            z-index: 2;
        }
        h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 4.5rem;
            margin-bottom: 30px;
            background: linear-gradient(90deg, #ff7eb3, #ff758c);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 5px 15px rgba(255, 118, 140, 0.2);
        }
        h2 {
            font-size: 2.2rem;
            margin-bottom: 20px;
            font-weight: 600;
            color: #f8d7ff;
        }
        p {
            font-size: 1.4rem;
            line-height: 1.8;
            margin-bottom: 25px;
            color: #e6c6ff;
            font-weight: 300;
        }
        .instruction {
            font-size: 1.1rem;
            color: #c996ff;
            border: 2px dashed #c996ff;
            padding: 15px 25px;
            border-radius: 15px;
            margin-top: 40px;
            display: inline-block;
            opacity: 0.9;
        }
        .hidden {
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.7s;
        }
        .screen-active {
            opacity: 1;
            pointer-events: inherit;
            transition: opacity 0.7s;
        }
        .hearts {
            font-size: 3rem;
            letter-spacing: 15px;
            margin-top: 30px;
            animation: pulse 1.5s infinite;
        }
        .bg-heart {
            position: absolute;
            font-size: 20rem;
            opacity: 0.03;
            z-index: 1;
            animation: float 20s infinite linear;
        }
        @keyframes pulse {
            0% { transform: scale(1); opacity: 0.7; }
            50% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(1); opacity: 0.7; }
        }
        @keyframes float {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(100px, -100px) rotate(360deg); }
        }
        @media (max-width: 768px) {
            h1 { font-size: 3.2rem; }
            h2 { font-size: 1.8rem; }
            p { font-size: 1.2rem; }
            .container { padding: 25px; }
        }
    </style>
    <!-- Confetti CDN -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
</head>
<body>
    <!-- Elementos decorativos de fondo -->
    <div class="bg-heart" style="top:10%; left:5%;">💖</div>
    <div class="bg-heart" style="bottom:15%; right:10%;">💕</div>

    <div class="container">
        <!-- PANTALLA 1: LA PREGUNTA -->
        <div id="screen1" class="screen-active">
            <h1>Para la persona más especial 💘</h1>
            <h2>¿Quieres ser mi cita perfecta este San Valentín?</h2>
            <p>Esta noche no se trata de planes extravagantes, sino del simple hecho de que no puedo imaginar celebrar este día sin ti a mi lado.</p>
            <p class="instruction">Presiona cualquier tecla o toca la pantalla para decir que SÍ</p>
        </div>

        <!-- PANTALLA 2: RESPUESTA (Oculta inicialmente) -->
        <div id="screen2" class="hidden">
            <h1>¡Sabía que dirías que sí! 🌟</h1>
            <h2>¡Nos vemos a las 8:00 PM en nuestro lugar favorito!</h2>
            <p>Prepárate para una velada llena de conversaciones, risas y esos momentos que solo contigo son perfectos. He estado planeando algo especial para nosotros.</p>
            <p>Esta noche incluye una sorpresa musical: una versión instrumental de "Te quiero" de Hombres G, ¡solo para ti!</p>
            <p>Prometo hacer de esta noche un recuerdo que guardaremos para siempre. No puedo esperar a verte. 💖</p>
            <div class="hearts">💕 💖 💗 💝 💞</div>
        </div>

        <!-- AUDIO ROMÁNTICO INSTRUMENTAL DE TE QUIERO DE HOMBRES G -->
        <audio id="romanticSound" preload="auto" src="https://docs.google.com/uc?export=download&id=1ZctXOc2RT5R4VDy3k53L5K5J94vkg_I_"></audio>
    </div>

    <script>
        let hasAnswered = false;

        function showScreen2() {
            if (hasAnswered) return;
            hasAnswered = true;

            const s1 = document.getElementById('screen1');
            const s2 = document.getElementById('screen2');
            s1.classList.remove('screen-active');
            s1.classList.add('hidden');

            setTimeout(() => {
                s2.classList.remove('hidden');
                s2.classList.add('screen-active');
                // Confeti
                if (typeof confetti === 'function') {
                    confetti({
                        particleCount: 150,
                        spread: 70,
                        origin: { y: 0.6 }
                    });
                }
                // Sonido instrumental de Hombres G
                const audio = document.getElementById('romanticSound');
                audio.currentTime = 0;
                audio.volume = 0.7;
                audio.play().catch((e) => {
                    console.log('El navegador no permitió reproducir el audio automáticamente.');
                });
            }, 500);
        }

        document.addEventListener('keydown', showScreen2);
        document.addEventListener('click', showScreen2);

        console.log('💖 Página cargada con amor. ¡Buena suerte con tu cita! 💖');
    </script>
</body>
</html>
