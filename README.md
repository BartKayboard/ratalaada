const quizData = [
    {
        question: "What does a liar do when he is dead?",
        a: "He stays silent",
        b: "He becomes truthful",
        c: "He pretends he is dead",
        d: "He lies Still",
        correct: "d",
    },
    {
        question: "What does 'You are El Ratalada' meant in the movie?",
        a: "The Penguin",
        b: " Use url to open Ratalada.com",
        c: "Batman",
        d: "Riddler was passing time so that we can see the action scene with Penguin, XD",
        correct: "b",
    },
    {
        question: "Who was the last victim of Riddler?",
        a: "The Batman",
        b: "Gotham",
        c: "Jim Gordon",
        d: "His followers",
        correct: "a",
    },
    {
        question: "Does Riddler know that Bruce Wayne is Batman?",
        a: "Yes",
        b: "No",
        c: "Maybe",
        d: "none of the above",
        correct: "b",
    },
];

const quiz = document.getElementById("quiz");
const answerEls = document.querySelectorAll(".answer");
const questionEl = document.getElementById("question");
const a_text = document.getElementById("a_text");
const b_text = document.getElementById("b_text");
const c_text = document.getElementById("c_text");
const d_text = document.getElementById("d_text");
const submitBtn = document.getElementById("submit");

let currentQuiz = 0;
let score = 0;

loadQuiz();

function loadQuiz() {
    deselectAnswers();

    const currentQuizData = quizData[currentQuiz];

    questionEl.innerText = currentQuizData.question;
    a_text.innerText = currentQuizData.a;
    b_text.innerText = currentQuizData.b;
    c_text.innerText = currentQuizData.c;
    d_text.innerText = currentQuizData.d;
}

function getSelected() {
    let answer = undefined;

    answerEls.forEach((answerEl) => {
        if (answerEl.checked) {
            answer = answerEl.id;
        }
    });

    return answer;
}

function deselectAnswers() {
    answerEls.forEach((answerEl) => {
        answerEl.checked = false;
    });
}

submitBtn.addEventListener("click", () => {
    // check to see the answer
    const answer = getSelected();

    if (answer) {
        if (answer === quizData[currentQuiz].correct) {
            score++;
        }

        currentQuiz++;
        if (currentQuiz < quizData.length) {
            loadQuiz();
        } else {
            quiz.innerHTML = `
                <h2>You answered correctly at ${score}/${quizData.length} questions.</h2>
                
                <button onclick="location.reload()">Reload</button>
            `;
        }
    }
});
