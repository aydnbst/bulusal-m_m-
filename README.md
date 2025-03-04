<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Buluşalım mı?</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
            text-align: center;
            overflow: hidden;
            position: relative;
        }
        .container {
            max-width: 600px;
            width: 100%;
            padding: 20px;
            box-sizing: border-box;
            position: relative;
            z-index: 2;
        }
        .question {
            font-size: 2.5em;
            margin-bottom: 20px;
            color: #333;
        }
        .buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .button {
            padding: 15px 30px;
            font-size: 1.2em;
            cursor: pointer;
            border: none;
            border-radius: 10px;
            transition: all 0.3s ease;
            outline: none;
        }
        .button.yes {
            background-color: #4CAF50;
            color: white;
        }
        .button.no {
            background-color: #f44336;
            color: white;
            position: relative; /* Fare ile kaçmak için */
        }
        .final-message {
            font-size: 4em;
            color: #ff4081;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 3;
            display: none;
        }
        .heart {
            position: absolute;
            font-size: 2em;
            animation: float 5s infinite ease-in-out;
            z-index: 1;
        }
        @keyframes float {
            0%, 100% {
                transform: translateY(0) rotate(0deg);
            }
            50% {
                transform: translateY(-20px) rotate(20deg);
            }
        }
        @media (max-width: 600px) {
            .question {
                font-size: 2em;
            }
            .button {
                padding: 10px 20px;
                font-size: 1em;
            }
            .final-message {
                font-size: 3em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="question" id="question">Buluşalım mı?</div>
        <div class="buttons" id="buttons">
            <button class="button yes" id="yesButton">Evet</button>
            <button class="button no" id="noButton">Hayır</button>
        </div>
    </div>

    <!-- Final Message -->
    <div class="final-message" id="finalMessage">Oleyyyyyy!</div>

    <!-- Kalpler -->
    <div id="heartsContainer"></div>

    <script>
        const questionElement = document.getElementById('question');
        const yesButton = document.getElementById('yesButton');
        const noButton = document.getElementById('noButton');
        const buttonsContainer = document.getElementById('buttons');
        const finalMessage = document.getElementById('finalMessage');
        const heartsContainer = document.getElementById('heartsContainer');

        let noCount = 0;

        // Soruların listesi
        const questions = [
            "Buluşalım mı?",
            "Hadi ümmüş kırma beni, buluşalım!",
            "Buluşuyor muyuz?"
        ];

        // Kalp oluşturma fonksiyonu
        function createHearts() {
            for (let i = 0; i < 20; i++) {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.innerText = '❤️';
                heart.style.left = `${Math.random() * 100}vw`;
                heart.style.top = `${Math.random() * 100}vh`;
                heart.style.animationDuration = `${Math.random() * 3 + 2}s`;
                heartsContainer.appendChild(heart);
            }
        }

        // Final ekranını göster
        function showFinalMessage() {
            finalMessage.style.display = 'block';
            buttonsContainer.style.display = 'none';
            questionElement.style.display = 'none';
            createHearts();
        }

        // Hayır butonuna tıklandığında
        noButton.addEventListener('click', () => {
            noCount++;
            if (noCount < questions.length) {
                questionElement.innerText = questions[noCount]; // Soruyu güncelle
                yesButton.style.transform = `scale(${1 + noCount * 0.5})`; // Evet butonunu büyüt
            } else {
                // Son aşamada hayır butonunu fare ile kaçır
                noButton.style.position = 'absolute';
                noButton.addEventListener('mousemove', (e) => {
                    const x = Math.random() * window.innerWidth;
                    const y = Math.random() * window.innerHeight;
                    noButton.style.left = `${x}px`;
                    noButton.style.top = `${y}px`;
                });
            }
        });

        // Evet butonuna tıklandığında
        yesButton.addEventListener('click', showFinalMessage);
    </script>
</body>
</html>
