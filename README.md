<!DOCTYPE html>
<html>
<head>
    <title>Trivia Bíblica</title>
    <style>
        body { font-family: 'Arial', sans-serif; background-color: #e9ecef; margin: 0; padding: 0; }
        .container { max-width: 700px; margin: 50px auto; background: #fff; padding: 30px; border-radius: 10px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); }
        h1 { text-align: center; color: #343a40; margin-bottom: 20px; }
        .question { margin-bottom: 20px; display: none; }
        .question.active { display: block; }
        .options { list-style-type: none; padding: 0; }
        .options li { margin-bottom: 10px; }
        .button { display: block; width: 100%; padding: 12px; background-color: #007bff; color: white; text-align: center; border: none; border-radius: 5px; cursor: pointer; margin-top: 20px; }
        .button:hover { background-color: #0056b3; }
        .hidden { display: none; }
        .result { text-align: center; font-size: 1.2em; margin-top: 20px; }
        .player-list { margin-top: 20px; }
        .player-list li { margin-bottom: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Trivia Bíblica</h1>
        <div id="registration" class="registration">
            <p>Ingresa tu nombre para empezar:</p>
            <input type="text" id="playerName" placeholder="Tu nombre" style="padding: 10px; width: calc(100% - 22px); border: 1px solid #ced4da; border-radius: 5px; margin-bottom: 20px;" />
            <button class="button" onclick="startGame()">Empezar Juego</button>
        </div>
        <div id="questions" class="hidden">
            <div class="question active">
                <p>¿Quién construyó el arca para sobrevivir al diluvio?</p>
                <ul class="options">
                    <li><input type="radio" name="q1" value="Moisés"> Moisés</li>
                    <li><input type="radio" name="q1" value="Noé"> Noé</li>
                    <li><input type="radio" name="q1" value="Abraham"> Abraham</li>
                </ul>
            </div>
            <div class="question">
                <p>¿En cuál libro de la Biblia se narra la historia de David y Goliat?</p>
                <ul class="options">
                    <li><input type="radio" name="q2" value="Génesis"> Génesis</li>
                    <li><input type="radio" name="q2" value="Éxodo"> Éxodo</li>
                    <li><input type="radio" name="q2" value="Samuel"> Samuel</li>
                </ul>
            </div>
            <div class="question">
                <p>¿Cuál fue el primer milagro de Jesús según el Nuevo Testamento?</p>
                <ul class="options">
                    <li><input type="radio" name="q3" value="Curar a un ciego"> Curar a un ciego</li>
                    <li><input type="radio" name="q3" value="Convertir el agua en vino"> Convertir el agua en vino</li>
                    <li><input type="radio" name="q3" value="Resucitar a Lázaro"> Resucitar a Lázaro</li>
                </ul>
            </div>
        </div>
        <button class="button hidden" onclick="nextQuestion()">Siguiente</button>
        <button class="button hidden" onclick="redirectToResults()">Ver Resultados</button>
        <div id="results" class="hidden"></div>
    </div>

    <script>
        let players = [];
        let currentQuestion = 0;

        function startGame() {
            const playerName = document.getElementById('playerName').value;
            if (playerName) {
                players.push({ name: playerName, score: 0 });
                document.getElementById('registration').classList.add('hidden');
                document.getElementById('questions').classList.remove('hidden');
                document.querySelector('.button[onclick="nextQuestion()"]').classList.remove('hidden');
            } else {
                alert('Por favor ingresa tu nombre.');
            }
        }

        function nextQuestion() {
            const questions = document.querySelectorAll('.question');
            if (currentQuestion < questions.length - 1) {
                questions[currentQuestion].classList.remove('active');
                currentQuestion++;
                questions[currentQuestion].classList.add('active');
            }
            if (currentQuestion === questions.length - 1) {
                document.querySelector('.button[onclick="nextQuestion()"]').classList.add('hidden');
                document.querySelector('.button[onclick="redirectToResults()"]').classList.remove('hidden');
            }
        }

        function calculateScores() {
            const answers = ['Noé', 'Samuel', 'Convertir el agua en vino'];
            for (let i = 0; i < answers.length; i++) {
                const selected = document.querySelector(`input[name="q${i + 1}"]:checked`);
                if (selected && selected.value === answers[i]) {
                    players[0].score++;
                }
            }
            localStorage.setItem('players', JSON.stringify(players));
        }

        function redirectToResults() {
            calculateScores();
            window.location.href = "resultados.html"; // Aquí puedes agregar la dirección de la página de resultados
        }
    </script>
</body>
</html>
