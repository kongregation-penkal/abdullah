<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Irmandade</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            padding: 0;
            background: linear-gradient(rgba(10, 10, 10, 0.95), rgba(0, 0, 0, 0.95)),
                        url('https://i.imgur.com/V7s78QI.jpeg') no-repeat center center fixed;
            background-size: cover;
            font-family: 'Cinzel Decorative', serif;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            font-size: 4.5rem;
            color: white;
            text-align: center;
            font-style: italic;
            margin: 30px 0;
            text-transform: uppercase;
            text-shadow: 2px 2px 0 black, -2px -2px 0 black, 2px -2px 0 black, -2px 2px 0 black;
            letter-spacing: 5px;
        }

        .circle-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 40px;
            justify-content: center;
            align-items: center;
            max-width: 80%;
            margin: 20px 0;
        }

        .circle-wrapper {
            text-align: center;
        }

        .circle {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            border: 8px solid;
            display: flex;
            justify-content: center;
            align-items: center;
            background: rgba(255, 255, 255, 0.1);
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            margin: 0 auto;
        }

        .circle img {
            width: 90%;
            height: 90%;
            object-fit: cover;
            border-radius: 50%;
            filter: grayscale(100%);
            transition: filter 0.3s ease-in-out;
        }

        .circle:hover {
            transform: scale(1.1);
            box-shadow: 0 0 25px rgba(255, 255, 255, 0.8);
        }

        .circle:hover img {
            filter: grayscale(0%);
        }

        .verse {
            font-size: 1rem;
            color: #ddd;
            font-style: italic;
            margin-top: 10px;
        }

        /* Modal */
        #toggle {
            display: none;
        }

        .character-card {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 70%;
            max-width: 800px;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            z-index: 999;
            padding: 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            color: #333;
        }

        #toggle:checked ~ .character-card {
            display: grid;
        }

        #toggle:checked ~ .overlay {
            display: block;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 998;
        }

        .close-label {
            position: absolute;
            top: 10px;
            left: 10px;
            background: #b22222;
            color: white;
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            line-height: 1;
            text-align: center;
            z-index: 999;
        }

        .info {
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            border-right: 2px solid #333;
        }

        .info h2, .info p {
            margin: 5px 0;
            text-align: center;
        }

        .info h2 {
            font-size: 1.5rem;
            color: #b22222;
            font-weight: bold;
        }

        .info p {
            font-size: 1rem;
            color: black;
        }

        .info .bold {
            font-weight: bold;
        }

        .image {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .image img {
            height: 100%;
            max-height: 350px;
            border-radius: 10px;
        }

        .cross {
            position: absolute;
            top: 50px;
            left: 20px;
            width: 40px;
            height: 40px;
            background-color: #b22222;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            transform-origin: center;
            animation: rotateCross 8s linear infinite;
        }

        .cross img {
            width: 100%;
            height: 100%;
        }

        @keyframes rotateCross {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(180deg);
            }
        }

        /* Player de áudio */
        .audio-player {
            width: 100%;
            background-color: #800000;
            padding: 10px;
            border-radius: 5px;
            display: flex;
            justify-content: center;
            margin-top: 10px;
        }

        .audio-player audio {
            width: 100%;
            border: none;
            outline: none;
        }
    </style>
</head>
<body>
    <h1>OS ANJOS</h1>

    <div class="circle-container">
        <div class="circle-wrapper">
            <div class="circle">
                <label for="toggle">
                    <img src="https://i.imgur.com/wRmo5P1.jpeg" alt="Sister Image 1">
                </label>
            </div>
            <p class="verse">"I will fear no evil, for You are with me." Psalm 23:4</p>
        </div>
        <div class="circle-wrapper">
            <div class="circle">
                <label for="toggle">
                    <img src="https://i.imgur.com/wRmo5P1.jpeg" alt="Sister Image 2">
                </label>
            </div>
            <p class="verse">"The Lord is my strength and my shield." Psalm 28:7</p>
        </div>
    </div>

    <!-- Modal -->
    <input type="checkbox" id="toggle">
    <div class="overlay"></div>
    <div class="character-card">
        <label for="toggle" class="close-label" onclick="closeCard()">×</label>
        <div class="info">
            <h2><span class="bold">Nome Completo:</span> Sabrina da Cruz Penitente</h2>
            <h2><span class="bold">Pacote:</span> Ordem das Irmãs da Penitência</h2>
            <h2><span class="bold">Idade:</span> 28 anos</h2>
            <h2><span class="bold">Santo de Devoção:</span> Santa Ágata</h2>
            <p>Sabrina foi acolhida pela Ordem após fugir de um passado de pecado. Seus dias são preenchidos com oração e mistério, mas os rumores sobre sua busca por redenção permeiam cada sombra que a segue.</p>
            <div class="audio-player">
                <audio id="audio" controls>
                    <source src="audio/sister-sabrina-theme.mp3" type="audio/mpeg">
                    Seu navegador não suporta o elemento de áudio.
                </audio>
            </div>
        </div>
        <div class="image">
            <img src="https://i.imgur.com/3KmJK3O.jpg" alt="Sister Sabrina Image">
        </div>
    </div>

    <div class="cross">
        <img src="https://static.vecteezy.com/system/resources/previews/014/475/015/non_2x/silhouette-of-the-cross-of-jesus-religious-christians-png.png" alt="Cross">
    </div>

    <script>
        function closeCard() {
            document.querySelector('.character-card').style.display = 'none';
        }
    </script>
</body>
</html>
