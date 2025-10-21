<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kuis Matematika Interaktif</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');

        :root {
            --primary-color: #4A90E2;
            --secondary-color: #50E3C2;
            --background-light: #F4F7F9;
            --card-background: #FFFFFF;
            --text-dark: #333333;
            --text-light: #666666;
            --shadow: rgba(0, 0, 0, 0.1);
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--background-light);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            color: var(--text-dark);
        }

        .container {
            width: 90%;
            max-width: 600px;
            padding: 40px;
            background-color: var(--card-background);
            border-radius: 20px;
            box-shadow: 0 10px 30px var(--shadow);
            text-align: center;
            transition: all 0.3s ease-in-out;
        }

        .container h1 {
            color: var(--primary-color);
            margin-bottom: 20px;
            font-weight: 700;
        }

        .container h2 {
            color: var(--text-dark);
            margin-bottom: 20px;
            font-weight: 600;
        }

        .login-form input {
            width: 100%;
            padding: 15px;
            margin-bottom: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            font-size: 16px;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }

        .login-form input:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        .quiz-question {
            margin-bottom: 25px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 15px;
            border-left: 5px solid var(--secondary-color);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .quiz-question p {
            font-size: 1.5em;
            font-weight: 600;
            margin: 0 0 10px 0;
            color: var(--primary-color);
        }

        .quiz-question input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 16px;
        }

        .button {
            padding: 15px 30px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 18px;
            font-weight: 600;
            transition: background-color 0.3s, transform 0.2s;
            box-shadow: 0 4px 10px rgba(74, 144, 226, 0.3);
            margin-top: 15px;
        }
        
        .button:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .button:hover:not(:disabled) {
            background-color: #3870b9;
            transform: translateY(-2px);
        }

        .results-container {
            text-align: center;
        }

        .results-container h2 {
            color: var(--primary-color);
            font-size: 2em;
        }

        .results-container h3 {
            color: var(--secondary-color);
            font-size: 1.5em;
            margin-top: -10px;
        }

        .results-container #score {
            font-size: 3.5em;
            font-weight: 700;
            color: var(--primary-color);
            margin: 20px 0;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .results-container #motivation {
            font-style: italic;
            color: var(--text-light);
            font-size: 1.1em;
            line-height: 1.6;
            margin-top: 15px;
        }

        .results-container #time-spent {
            font-size: 1.1em;
            font-weight: 600;
            color: var(--text-dark);
            margin-top: 20px;
        }
        
        #question-counter {
            margin-top: 20px;
            color: var(--text-light);
            font-size: 1em;
        }
        
        #results-title {
            font-size: 1.5em;
            font-weight: 600;
            color: var(--primary-color);
            margin-bottom: 10px;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container" id="loginPage">
        <h1>Selamat Datang di Kuis Pembagian</h1>
        <p>Silakan masukkan data diri Anda untuk memulai.</p>
        <div class="login-form">
            <input type="text" id="nameInput" placeholder="Nama Lengkap">
            <input type="text" id="classInput" placeholder="Kelas">
            <input type="text" id="schoolInput" placeholder="Sekolah">
            <button class="button" onclick="startQuiz()">Mulai Kuis</button>
        </div>
    </div>

    <div class="container hidden" id="quizPage">
        <h2>Kuis Pembagian</h2>
        <div class="quiz-container">
            <div id="quizForm">
                </div>
            <p id="question-counter"></p>
        </div>
        <button class="button" id="next-button" onclick="nextQuestion()">Lanjut</button>
        <button class="button hidden" id="finish-button" onclick="submitQuiz()">Selesai Mengerjakan</button>
    </div>

    <div class="container hidden" id="resultsPage">
        <div class="results-container">
            <h2 id="resultName"></h2>
            <h3 id="results-title">PEMBAGIAN</h3>
            <div id="score"></div>
            <p id="time-spent"></p>
            <p id="motivation"></p>
            <button class="button" onclick="restartQuiz()">Mulai Lagi</button>
        </div>
    </div>

    <script>
        const allQuestions = [
            { question: "1 ÷ 1 = ", answer: 1 }, { question: "2 ÷ 1 = ", answer: 2 }, { question: "3 ÷ 1 = ", answer: 3 }, { question: "4 ÷ 1 = ", answer: 4 }, { question: "5 ÷ 1 = ", answer: 5 },
            { question: "6 ÷ 1 = ", answer: 6 }, { question: "7 ÷ 1 = ", answer: 7 }, { question: "8 ÷ 1 = ", answer: 8 }, { question: "9 ÷ 1 = ", answer: 9 }, { question: "10 ÷ 1 = ", answer: 10 },
            { question: "2 ÷ 2 = ", answer: 1 }, { question: "4 ÷ 2 = ", answer: 2 }, { question: "6 ÷ 2 = ", answer: 3 }, { question: "6 ÷ 3 = ", answer: 2 }, { question: "8 ÷ 2 = ", answer: 4 },
            { question: "8 ÷ 4 = ", answer: 2 }, { question: "10 ÷ 2 = ", answer: 5 }, { question: "10 ÷ 5 = ", answer: 2 }, { question: "12 ÷ 2 = ", answer: 6 }, { question: "12 ÷ 6 = ", answer: 2 },
            { question: "14 ÷ 2 = ", answer: 7 }, { question: "14 ÷ 7 = ", answer: 2 }, { question: "16 ÷ 2 = ", answer: 8 }, { question: "16 ÷ 8 = ", answer: 2 }, { question: "18 ÷ 2 = ", answer: 9 },
            { question: "18 ÷ 9 = ", answer: 2 }, { question: "20 ÷ 2 = ", answer: 10 }, { question: "20 ÷ 10 = ", answer: 2 }, { question: "3 ÷ 3 = ", answer: 1 }, { question: "9 ÷ 3 = ", answer: 3 },
            { question: "12 ÷ 3 = ", answer: 4 }, { question: "12 ÷ 4 = ", answer: 3 }, { question: "15 ÷ 3 = ", answer: 5 }, { question: "15 ÷ 5 = ", answer: 3 }, { question: "18 ÷ 3 = ", answer: 6 },
            { question: "18 ÷ 6 = ", answer: 3 }, { question: "21 ÷ 3 = ", answer: 7 }, { question: "21 ÷ 7 = ", answer: 3 }, { question: "24 ÷ 3 = ", answer: 8 }, { question: "24 ÷ 8 = ", answer: 3 },
            { question: "27 ÷ 3 = ", answer: 9 }, { question: "27 ÷ 9 = ", answer: 3 }, { question: "30 ÷ 3 = ", answer: 10 }, { question: "30 ÷ 10 = ", answer: 3 }, { question: "4 ÷ 4 = ", answer: 1 },
            { question: "16 ÷ 4 = ", answer: 4 }, { question: "20 ÷ 4 = ", answer: 5 }, { question: "20 ÷ 5 = ", answer: 4 }, { question: "24 ÷ 4 = ", answer: 6 }, { question: "24 ÷ 6 = ", answer: 4 },
            { question: "28 ÷ 4 = ", answer: 7 }, { question: "28 ÷ 7 = ", answer: 4 }, { question: "32 ÷ 4 = ", answer: 8 }, { question: "32 ÷ 8 = ", answer: 4 }, { question: "36 ÷ 4 = ", answer: 9 },
            { question: "36 ÷ 9 = ", answer: 4 }, { question: "40 ÷ 4 = ", answer: 10 }, { question: "40 ÷ 10 = ", answer: 4 }, { question: "5 ÷ 5 = ", answer: 1 }, { question: "25 ÷ 5 = ", answer: 5 },
            { question: "30 ÷ 5 = ", answer: 6 }, { question: "30 ÷ 6 = ", answer: 5 }, { question: "35 ÷ 5 = ", answer: 7 }, { question: "35 ÷ 7 = ", answer: 5 }, { question: "40 ÷ 5 = ", answer: 8 },
            { question: "40 ÷ 8 = ", answer: 5 }, { question: "45 ÷ 5 = ", answer: 9 }, { question: "45 ÷ 9 = ", answer: 5 }, { question: "50 ÷ 5 = ", answer: 10 }, { question: "50 ÷ 10 = ", answer: 5 },
            { question: "6 ÷ 6 = ", answer: 1 }, { question: "36 ÷ 6 = ", answer: 6 }, { question: "42 ÷ 6 = ", answer: 7 }, { question: "42 ÷ 7 = ", answer: 6 }, { question: "48 ÷ 6 = ", answer: 8 },
            { question: "48 ÷ 8 = ", answer: 6 }, { question: "54 ÷ 6 = ", answer: 9 }, { question: "54 ÷ 9 = ", answer: 6 }, { question: "60 ÷ 6 = ", answer: 10 }, { question: "60 ÷ 10 = ", answer: 6 },
            { question: "7 ÷ 7 = ", answer: 1 }, { question: "49 ÷ 7 = ", answer: 7 }, { question: "56 ÷ 7 = ", answer: 8 }, { question: "56 ÷ 8 = ", answer: 7 }, { question: "63 ÷ 7 = ", answer: 9 },
            { question: "63 ÷ 9 = ", answer: 7 }, { question: "70 ÷ 7 = ", answer: 10 }, { question: "70 ÷ 10 = ", answer: 7 }, { question: "8 ÷ 8 = ", answer: 1 }, { question: "64 ÷ 8 = ", answer: 8 },
            { question: "72 ÷ 8 = ", answer: 9 }, { question: "72 ÷ 9 = ", answer: 8 }, { question: "80 ÷ 8 = ", answer: 10 }, { question: "80 ÷ 10 = ", answer: 8 }, { question: "9 ÷ 9 = ", answer: 1 },
            { question: "81 ÷ 9 = ", answer: 9 }, { question: "90 ÷ 9 = ", answer: 10 }, { question: "90 ÷ 10 = ", answer: 9 }, { question: "10 ÷ 10 = ", answer: 1 }, { question: "100 ÷ 10 = ", answer: 10 }
        ];

        let quizQuestions = [];
        let userAnswers = [];
        let currentQuestionIndex = 0;
        let userName = "";
        let startTime = 0;

        function startQuiz() {
            userName = document.getElementById("nameInput").value.trim();
            const userClass = document.getElementById("classInput").value.trim();
            const userSchool = document.getElementById("schoolInput").value.trim();

            if (userName === "" || userClass === "" || userSchool === "") {
                alert("Semua kolom harus diisi!");
                return;
            }

            document.getElementById("loginPage").classList.add("hidden");
            document.getElementById("quizPage").classList.remove("hidden");

            // Ambil 20 soal acak
            quizQuestions = allQuestions.sort(() => 0.5 - Math.random()).slice(0, 20);
            userAnswers = new Array(quizQuestions.length).fill(null);
            currentQuestionIndex = 0;
            
            // Mulai timer
            startTime = new Date().getTime();
            
            displayQuestion();
        }

        function displayQuestion() {
            const quizForm = document.getElementById("quizForm");
            const q = quizQuestions[currentQuestionIndex];
            const questionHtml = `
                <div class="quiz-question">
                    <p>${q.question}</p>
                    <input type="number" id="currentAnswer" placeholder="Jawaban Anda" required>
                </div>
            `;
            quizForm.innerHTML = questionHtml;
            document.getElementById("question-counter").innerText = `Soal ${currentQuestionIndex + 1} dari ${quizQuestions.length}`;

            // Atur status tombol
            const nextButton = document.getElementById("next-button");
            const finishButton = document.getElementById("finish-button");
            
            nextButton.classList.remove("hidden");
            finishButton.classList.add("hidden");
            nextButton.disabled = true;

            const answerInput = document.getElementById("currentAnswer");
            answerInput.addEventListener("input", function() {
                if (this.value.trim() !== '') {
                    if (currentQuestionIndex === quizQuestions.length - 1) {
                        nextButton.classList.add("hidden");
                        finishButton.classList.remove("hidden");
                    } else {
                        nextButton.disabled = false;
                    }
                } else {
                    nextButton.disabled = true;
                    finishButton.classList.add("hidden");
                }
            });
            answerInput.focus();
        }
        
        function nextQuestion() {
            const answerInput = document.getElementById("currentAnswer");
            const answer = parseInt(answerInput.value);
            userAnswers[currentQuestionIndex] = answer;
            
            currentQuestionIndex++;
            if (currentQuestionIndex < quizQuestions.length) {
                displayQuestion();
            }
        }

        function submitQuiz() {
            // Hentikan timer
            const endTime = new Date().getTime();
            const timeTaken = Math.floor((endTime - startTime) / 1000); // Waktu dalam detik

            // Simpan jawaban terakhir
            const answerInput = document.getElementById("currentAnswer");
            const answer = parseInt(answerInput.value);
            userAnswers[currentQuestionIndex] = answer;

            let correctAnswers = 0;
            quizQuestions.forEach((q, index) => {
                if (userAnswers[index] === q.answer) {
                    correctAnswers++;
                }
            });

            const finalScore = correctAnswers * 5;
            let motivationText = "";

            if (finalScore >= 90) {
                motivationText = "Hebat! Pertahankan prestasi luar biasa ini! 🚀";
            } else if (finalScore >= 70) {
                motivationText = "Bagus sekali! Sedikit lagi, kamu pasti bisa jadi yang terbaik! ✨";
            } else if (finalScore >= 50) {
                motivationText = "Terus semangat! Setiap usaha adalah langkah menuju keberhasilan. 💪";
            } else {
                motivationText = "Jangan menyerah! Kegagalan adalah awal dari kesuksesan. Coba lagi, kamu pasti bisa! 💡";
            }
            
            document.getElementById("quizPage").classList.add("hidden");
            document.getElementById("resultsPage").classList.remove("hidden");
            
            document.getElementById("resultName").innerText = `${userName},`;
            document.getElementById("score").innerText = finalScore;
            document.getElementById("time-spent").innerText = `Waktu pengerjaan: ${timeTaken} detik`;
            document.getElementById("motivation").innerText = motivationText;
        }

        function restartQuiz() {
            document.getElementById("nameInput").value = "";
            document.getElementById("classInput").value = "";
            document.getElementById("schoolInput").value = "";

            document.getElementById("resultsPage").classList.add("hidden");
            document.getElementById("loginPage").classList.remove("hidden");
        }

    </script>
</body>
</html>
