# Song
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Curitiba - Bossa Nova</title>
    <style>
        :root {
            --accent-color: #d4a373;
            --text-light: #fefae0;
            --bg-overlay: rgba(0, 0, 0, 0.6);
        }

        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            font-family: 'Georgia', serif;
            color: var(--text-light);
            background: #222;
        }

        /* Imagem de Fundo */
        .background-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('curitiba.jpg'); /* Substitua pelo nome da sua imagem */
            background-size: cover;
            background-position: center;
            filter: grayscale(30%) brightness(0.7);
            z-index: -1;
        }

        .content-wrapper {
            max-width: 900px;
            margin: 0 auto;
            padding: 40px 20px;
            background: var(--bg-overlay);
            min-height: 100vh;
            backdrop-filter: blur(5px);
            text-align: center;
        }

        h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            font-weight: normal;
            letter-spacing: 2px;
        }

        .subtitle {
            font-style: italic;
            color: var(--accent-color);
            margin-bottom: 40px;
        }

        /* Player de Áudio */
        .audio-player {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 40px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }

        .controls {
            display: flex;
            align-items: center;
            gap: 20px;
            width: 100%;
        }

        #play-pause {
            background: var(--accent-color);
            border: none;
            padding: 10px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s;
        }

        #play-pause:hover { transform: scale(1.05); }

        #seek-slider {
            flex-grow: 1;
            cursor: pointer;
        }

        /* Seção do YouTube */
        .video-container {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
            height: 0;
            overflow: hidden;
            margin-bottom: 50px;
            border: 2px solid var(--accent-color);
        }

        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        /* Letra da Música */
        .lyrics {
            line-height: 1.8;
            font-size: 1.2rem;
            white-space: pre-line;
            text-align: center;
        }

        .verse { margin-bottom: 30px; }
    </style>
</head>
<body>

    <div class="background-container"></div>

    <div class="content-wrapper">
        <h1>Curitiba</h1>
        <p class="subtitle">Bossa Nova & Garoa</p>

        <div class="audio-player">
            <audio id="bossa-audio" src="seu-audio.mp3"></audio>
            <div class="controls">
                <button id="play-pause">PLAY</button>
                <input type="range" id="seek-slider" value="0" max="100">
                <span id="current-time">0:00</span>
            </div>
        </div>

        <div class="video-container">
            <iframe src="https://www.youtube.com/embed/ID_DO_VIDEO" frameborder="0" allowfullscreen></iframe>
        </div>

        <div class="lyrics">
            <div class="verse">
                O céu acordou num tom de cinza
                A Serra do Mar se esconde no véu
                O vento lá fora é quem dita a brisa
                Pintando de névoa o azul do meu céu
            </div>
            
            <div class="verse">
                <strong>[Refrão]</strong>
                Curitiba, cidade luz em tons de prata
                Onde o silêncio do Parque Barigui se desata
                Entre pinheiros e a garoa que insiste em cair
                É o meu refúgio, o melhor lugar pra existir
            </div>
            </div>
    </div>

    <script>
        const audio = document.getElementById('bossa-audio');
        const playBtn = document.getElementById('play-pause');
        const slider = document.getElementById('seek-slider');
        const timeDisplay = document.getElementById('current-time');

        playBtn.addEventListener('click', () => {
            if (audio.paused) {
                audio.play();
                playBtn.textContent = 'PAUSE';
            } else {
                audio.pause();
                playBtn.textContent = 'PLAY';
            }
        });

        audio.addEventListener('timeupdate', () => {
            const value = (audio.currentTime / audio.duration) * 100;
            slider.value = value || 0;
            
            let mins = Math.floor(audio.currentTime / 60);
            let secs = Math.floor(audio.currentTime % 60);
            if (secs < 10) secs = '0' + secs;
            timeDisplay.textContent = `${mins}:${secs}`;
        });

        slider.addEventListener('input', () => {
            const time = (slider.value / 100) * audio.duration;
            audio.currentTime = time;
        });
    </script>
</body>
</html>