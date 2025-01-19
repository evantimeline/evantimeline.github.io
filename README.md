<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz: ¿Eres BOUBA o KIKI?</title>
    <style>
        body {
            font-family: "Courier New", Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #000;
            color: #fff;
        }
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            padding: 20px;
            width: 100%;
        }
        .question {
            font-size: 1.8rem;
            margin-bottom: 20px;
        }
        .answer {
            display: block;
            margin: 10px auto;
            padding: 15px 30px;
            font-size: 1.2rem;
            cursor: pointer;
            background: none;
            color: #fff;
            border: 2px solid #fff;
            border-radius: 5px;
            transition: background-color 0.3s, color 0.3s;
        }
        .answer:hover {
            background-color: #fff;
            color: #000;
        }
        .restart {
            margin-top: 20px;
            padding: 15px 30px;
            font-size: 1.2rem;
            cursor: pointer;
            background: none;
            color: #fff;
            border: 2px solid #28a745;
            border-radius: 5px;
            transition: background-color 0.3s, color 0.3s;
        }
        .restart:hover {
            background-color: #28a745;
            color: #fff;
        }
        .result {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .result-image {
            margin: 20px 0;
            max-width: 200px;
            height: auto;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div id="quiz">
            <p class="question" id="question">Pulse cualquier tecla o haga clic para proceder al cuestionario</p>
        </div>
    </div>

    <script>
        const questions = [
            {
                text: "En un debate:",
                options: [
                    { answer: "Intento encontrar un acuerdo para evitar el conflicto", value: 'a' },
                    { answer: "Defiendo mi punto de vista aunque los demás no estén de acuerdo conmigo", value: 'b' }
                ]
            },
            {
                text: "Si estoy muy enfadadx:",
                options: [
                    { answer: "Necesito que me apoyen y me escuchen", value: 'a' },
                    { answer: "Necesito que los demás respeten mi espacio y no me molesten hasta que me relaje", value: 'b' }
                ]
            },
            {
                text: "Soy más de:",
                options: [
                    { answer: "Dulce", value: 'a' },
                    { answer: "Salado", value: 'b' }
                ]
            },
            {
                text: "Los cambios de planes:",
                options: [
                    { answer: "No me suelen molestar, soy flexible", value: 'a' },
                    { answer: "Me ponen nerviosx", value: 'b' }
                ]
            },
            {
                text: "Si tengo que tomar una decisión importante:",
                options: [
                    { answer: "Confío en mi intuición y lo que dice mi corazón", value: 'a' },
                    { answer: "Prefiero tomarme mi tiempo para pensar lógicamente las cosas", value: 'b' }
                ]
            },
            {
                text: "Cuando estoy conociendo a alguien nuevo:",
                options: [
                    { answer: "Cojo confianza muy rápido. Me suele caer bien le gente de primeras", value: 'a' },
                    { answer: "Suelo ser desconfiadx hasta conocerlx mejor", value: 'b' }
                ]
            },
            {
                text: "Prefiero",
                options: [
                    { answer: "La playa", value: 'a' },
                    { answer: "La montaña", value: 'b' }
                ]
            },
            {
                text: "Prefiero que me regalen",
                options: [
                    { answer: "Algo con valor personal", value: 'a' },
                    { answer: "Dinero", value: 'b' }
                ]
            },
            {
                text: "Soy más de",
                options: [
                    { answer: "Té", value: 'a' },
                    { answer: "Café", value: 'b' }
                ]
            },
            {
                text: "Si estoy organizando una salida con amigos:",
                options: [
                    { answer: "Me adapto a lo que quieran hacer los demás, aunque no me entusiasme el plan", value: 'a' },
                    { answer: "Me gusta tomar las riendas y proponer planes nuevos", value: 'b' }
                ]
            },
            {
                text: "Me gusta más el:",
                options: [
                    { answer: "Reggaeton", value: 'a' },
                    { answer: "Techno", value: 'b' }
                ]
            }
        ];

        let currentQuestionIndex = -1;
        let scoreA = 0;
        let scoreB = 0;

        const quizDiv = document.getElementById("quiz");

        document.body.addEventListener("keydown", startQuiz);
        document.body.addEventListener("click", startQuiz);

        function startQuiz() {
            if (currentQuestionIndex === -1) {
                document.body.removeEventListener("keydown", startQuiz);
                document.body.removeEventListener("click", startQuiz);
                showNextQuestion();
            }
        }

        function showNextQuestion() {
            currentQuestionIndex++;

            if (currentQuestionIndex < questions.length) {
                const question = questions[currentQuestionIndex];
                quizDiv.innerHTML = `
                    <p class="question">${question.text}</p>
                    ${question.options.map(option => `
                        <button class="answer" onclick="selectAnswer('${option.value}')">${option.answer}</button>
                    `).join('')}
                `;
            } else {
                showResult();
            }
        }

        function selectAnswer(answer) {
            if (answer === 'a') {
                scoreA++;
            } else if (answer === 'b') {
                scoreB++;
            }

            showNextQuestion();
        }

        function showResult() {
            const isBouba = scoreA > scoreB;
            const result = isBouba ? "Eres BOUBA" : "Eres KIKI";
            const imageUrl = isBouba 
                ? "https://i.im.ge/2025/01/19/HMFEaG.2.jpeg"
                : "https://i.im.ge/2025/01/19/HMFtiT.1.jpeg";
            quizDiv.innerHTML = `
                <div class="result">
                    <p class="question">${result}</p>
                    <img src="${imageUrl}" alt="${result}" class="result-image">
                    <button class="restart" onclick="restartQuiz()">Retomar el cuestionario</button>
                </div>
            `;
        }

        function restartQuiz() {
            currentQuestionIndex = -1;
            scoreA = 0;
            scoreB = 0;
            showNextQuestion();
        }
    </script>
</body>
</html>
