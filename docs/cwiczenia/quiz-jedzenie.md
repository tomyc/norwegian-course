# Quiz słownictwa - Lekcja 11: Jedzenie

Test swoją wiedzę z słownictwa norweskiego!

<div id="quiz-container">
    <div id="question-container">
        <h3 id="question">Ładowanie...</h3>
        <div id="options"></div>
        <div id="feedback"></div>
        <button id="next-btn" onclick="nextQuestion()" style="display: none;">Następne pytanie</button>
    </div>
    
    <div id="results" style="display: none;">
        <h3>🎉 Quiz zakończony!</h3>
        <p>Twój wynik: <span id="final-score"></span></p>
        <button onclick="restartQuiz()">Zagraj ponownie</button>
    </div>
    
    <div id="progress">
        Pytanie: <span id="current">1</span> / <span id="total">10</span>
    </div>
</div>

<style>
#quiz-container {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px;
    border-radius: 15px;
    margin: 20px 0;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

#question {
    font-size: 1.5em;
    margin-bottom: 20px;
    text-align: center;
}

.option {
    background: rgba(255,255,255,0.2);
    border: 2px solid rgba(255,255,255,0.3);
    color: white;
    padding: 15px 20px;
    margin: 10px 0;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 1.1em;
    display: block;
    width: 100%;
    text-align: left;
}

.option:hover {
    background: rgba(255,255,255,0.3);
    transform: translateY(-2px);
}

.option.correct {
    background: #2ECC71;
    border-color: #27AE60;
}

.option.wrong {
    background: #E74C3C;
    border-color: #C0392B;
}

.option.disabled {
    cursor: not-allowed;
    opacity: 0.6;
}

#feedback {
    margin: 20px 0;
    font-weight: bold;
    text-align: center;
    font-size: 1.2em;
}

#next-btn, button {
    background: #4ECDC4;
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 25px;
    cursor: pointer;
    font-size: 1em;
    margin: 10px auto;
    display: block;
    transition: all 0.3s ease;
}

#next-btn:hover, button:hover {
    background: #44A08D;
    transform: translateY(-2px);
}

#progress {
    text-align: center;
    margin-top: 20px;
    font-size: 1.1em;
    opacity: 0.9;
}

#results {
    text-align: center;
}
</style>

<script>
const questions = [
    {
        question: "Jak się mówi 'chleb' po norwesku?",
        options: ["brød", "ost", "melk", "smør"],
        correct: 0,
        explanation: "Brød [brø] to chleb po norwesku"
    },
    {
        question: "Co oznacza słowo 'sulten'?",
        options: ["spragniony", "zmęczony", "głodny", "szczęśliwy"],
        correct: 2,
        explanation: "Sulten oznacza 'głodny'. Er du sulten? - Czy jesteś głodny?"
    },
    {
        question: "Które słowo oznacza 'ser'?",
        options: ["egg", "ost", "fisk", "kjøtt"],
        correct: 1,
        explanation: "Ost to ser po norwesku"
    },
    {
        question: "Jak powiedzieć 'Mam ochotę na pizzę'?",
        options: ["Jeg vil pizza", "Jeg har lyst på pizza", "Jeg spiser pizza", "Jeg liker pizza"],
        correct: 1,
        explanation: "'Å ha lyst på' używamy z jedzeniem i piciem"
    },
    {
        question: "Co oznacza 'pålegg'?",
        options: ["obiad", "śniadanie", "dodatki do kanapek", "deser"],
        correct: 2,
        explanation: "Pålegg to wszystko co kładziemy na chleb"
    },
    {
        question: "Jak się mówi 'masło' po norwesku?",
        options: ["smør", "melk", "egg", "ris"],
        correct: 0,
        explanation: "Smør [smør] oznacza masło"
    },
    {
        question: "Które zdanie jest poprawne?",
        options: ["Jeg liker også ikke", "Jeg heller ikke liker", "Jeg liker heller ikke", "Jeg ikke også liker"],
        correct: 2,
        explanation: "'Heller ikke' używamy w negacji dla 'też nie'"
    },
    {
        question: "Co to jest 'rundstykke'?",
        options: ["kromka chleba", "bułka", "ciasto", "kanapka"],
        correct: 1,
        explanation: "Rundstykke to bułka po norwesku"
    },
    {
        question: "Jak powiedzieć 'Poprosiłbym kawę' w sklepie?",
        options: ["Jeg vil ha kaffe", "Jeg vil gjerne ha kaffe", "Jeg har lyst på kaffe", "Jeg drikker kaffe"],
        correct: 1,
        explanation: "'Jeg vil gjerne ha...' to grzecznościowy zwrot w sklepie"
    },
    {
        question: "Co oznacza 'Jeg vet ikke'?",
        options: ["Nie lubię", "Nie wiem", "Nie mam", "Nie chcę"],
        correct: 1,
        explanation: "'Jeg vet ikke' oznacza 'Nie wiem'"
    }
];

let currentQuestion = 0;
let score = 0;
let answered = false;

function loadQuestion() {
    const q = questions[currentQuestion];
    document.getElementById('question').textContent = q.question;
    document.getElementById('current').textContent = currentQuestion + 1;
    document.getElementById('total').textContent = questions.length;
    
    const optionsContainer = document.getElementById('options');
    optionsContainer.innerHTML = '';
    
    q.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.className = 'option';
        button.textContent = option;
        button.onclick = () => selectAnswer(index);
        optionsContainer.appendChild(button);
    });
    
    document.getElementById('feedback').textContent = '';
    document.getElementById('next-btn').style.display = 'none';
    answered = false;
}

function selectAnswer(selectedIndex) {
    if (answered) return;
    
    answered = true;
    const q = questions[currentQuestion];
    const options = document.querySelectorAll('.option');
    
    options.forEach((option, index) => {
        option.classList.add('disabled');
        if (index === q.correct) {
            option.classList.add('correct');
        } else if (index === selectedIndex && index !== q.correct) {
            option.classList.add('wrong');
        }
    });
    
    const feedback = document.getElementById('feedback');
    if (selectedIndex === q.correct) {
        score++;
        feedback.textContent = `✅ Poprawnie! ${q.explanation}`;
        feedback.style.color = '#2ECC71';
    } else {
        feedback.textContent = `❌ Niepoprawnie. ${q.explanation}`;
        feedback.style.color = '#E74C3C';
    }
    
    document.getElementById('next-btn').style.display = 'block';
}

function nextQuestion() {
    currentQuestion++;
    
    if (currentQuestion >= questions.length) {
        showResults();
    } else {
        loadQuestion();
    }
}

function showResults() {
    document.getElementById('question-container').style.display = 'none';
    document.getElementById('results').style.display = 'block';
    
    const percentage = Math.round((score / questions.length) * 100);
    let message = '';
    
    if (percentage >= 90) {
        message = `${score}/${questions.length} (${percentage}%) - Doskonały wynik! 🏆`;
    } else if (percentage >= 70) {
        message = `${score}/${questions.length} (${percentage}%) - Bardzo dobry wynik! 🎉`;
    } else if (percentage >= 50) {
        message = `${score}/${questions.length} (${percentage}%) - Niezły wynik! 👍`;
    } else {
        message = `${score}/${questions.length} (${percentage}%) - Więcej ćwiczeń potrzeba! 📚`;
    }
    
    document.getElementById('final-score').textContent = message;
}

function restartQuiz() {
    currentQuestion = 0;
    score = 0;
    answered = false;
    
    document.getElementById('question-container').style.display = 'block';
    document.getElementById('results').style.display = 'none';
    
    loadQuestion();
}

// Inicjalizacja quizu
document.addEventListener('DOMContentLoaded', function() {
    loadQuestion();
});
</script>

---

## 🎯 Co przetestowałeś?

Ten quiz sprawdził Twoją znajomość:
- Podstawowego słownictwa kulinarnego
- Wyrażeń "å ha lyst på/til"
- Negacji z "heller ikke"
- Zwrotów grzecznościowych w sklepie
- Gramatyki z Lekcji 11

## 📚 Jeśli chcesz poćwiczyć więcej:

- **[Wróć do Lekcji 11](../lekcje-srednie/lekcja-11.md)** - powtórz materiał
- **[Słownictwo: Jedzenie](../slownictwo/jedzenie.md)** - pełna lista słów
- **[Memory Game - Jedzenie](../games/memory-game.html?category=food)** - interaktywna gra
- **[Dialogi praktyczne](../cwiczenia/dialogi.md)** - rozmowy w restauracji

---

**💡 Wskazówka:** Aby lepiej zapamiętać słownictwo, spróbuj opisać swoje ostatnie posiłki po norwesku!
