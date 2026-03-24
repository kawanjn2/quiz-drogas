# quiz-drogas
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz: Drogas e Prevenção</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color: #fff;
    margin: 0;
    padding: 15px;
}

.container {
    max-width: 500px;
    margin: auto;
    background: #1c1c2e;
    padding: 20px;
    border-radius: 18px;
    box-shadow: 0 0 20px rgba(0,0,0,0.6);
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

.question {
    margin-bottom: 20px;
}

.option {
    background: #2f2f4f;
    padding: 12px;
    margin: 6px 0;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.25s;
}

.option:hover {
    background: #50507a;
}

.option.selected {
    background: #00c896;
}

.option.correct {
    background: #00b894;
}

.option.wrong {
    background: #d63031;
}

button {
    width: 100%;
    padding: 14px;
    border: none;
    border-radius: 12px;
    margin-top: 10px;
    font-size: 16px;
    cursor: pointer;
    font-weight: bold;
}

#submit {
    background: #0984e3;
    color: white;
}

#reset {
    background: #e74c3c;
    color: white;
}

#result {
    margin-top: 20px;
    text-align: center;
    font-size: 18px;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="container">
<h1>Quiz: Drogas e Prevenção</h1>

<div id="quiz"></div>

<button id="submit">Finalizar</button>
<button id="reset">Reiniciar</button>

<div id="result"></div>
</div>

<script>
const questions = [
{
q: "Qual combinação de fatores mais contribui para o desenvolvimento de dependência?",
options: [
"Apenas curiosidade momentânea",
"Fatores genéticos, ambiente e saúde mental",
"Uso recreativo raro",
"Acesso financeiro"
],
answer: 1
},
{
q: "Por que drogas ilícitas apresentam maior risco imediato?",
options: [
"Porque são sempre mais fortes",
"Porque não têm controle de qualidade ou composição",
"Porque são usadas só à noite",
"Porque são naturais"
],
answer: 1
},
{
q: "Qual sinal pode indicar início de dependência?",
options: [
"Uso eventual em festas",
"Aumento da tolerância e necessidade de mais consumo",
"Uso por influência de amigos",
"Experimentação única"
],
answer: 1
},
{
q: "Qual impacto psicológico é comum no uso contínuo?",
options: [
"Felicidade constante",
"Maior produtividade",
"Ansiedade e depressão",
"Melhora do sono"
],
answer: 2
},
{
q: "Qual abordagem preventiva é mais eficaz?",
options: [
"Proibir sem diálogo",
"Ignorar o assunto",
"Educação, apoio familiar e informação",
"Ameaças"
],
answer: 2
},
{
q: "Por que a pressão social influencia o uso?",
options: [
"Porque substitui a vontade própria",
"Porque afeta decisões e necessidade de pertencimento",
"Porque não tem impacto real",
"Porque só ocorre com adultos"
],
answer: 1
}
];

let userAnswers = new Array(questions.length).fill(null);

const quizDiv = document.getElementById("quiz");

function loadQuiz() {
    quizDiv.innerHTML = "";

    questions.forEach((q, index) => {
        let div = document.createElement("div");
        div.classList.add("question");

        let title = document.createElement("p");
        title.innerText = (index+1) + ". " + q.q;
        div.appendChild(title);

        q.options.forEach((opt, i) => {
            let optDiv = document.createElement("div");
            optDiv.classList.add("option");
            optDiv.innerText = opt;

            optDiv.onclick = () => {
                let options = div.querySelectorAll(".option");
                options.forEach(o => o.classList.remove("selected"));
                optDiv.classList.add("selected");
                userAnswers[index] = i;
            };

            div.appendChild(optDiv);
        });

        quizDiv.appendChild(div);
    });
}

document.getElementById("submit").onclick = () => {
    let score = 0;

    document.querySelectorAll(".question").forEach((qDiv, index) => {
        let options = qDiv.querySelectorAll(".option");

        options.forEach((opt, i) => {
            if(i === questions[index].answer){
                opt.classList.add("correct");
            }
            if(userAnswers[index] === i && i !== questions[index].answer){
                opt.classList.add("wrong");
            }
        });

        if(userAnswers[index] === questions[index].answer){
            score++;
        }
    });

    document.getElementById("result").innerText =
        "Resultado: " + score + " de " + questions.length + " acertos";
};

document.getElementById("reset").onclick = () => {
    userAnswers = new Array(questions.length).fill(null);
    document.getElementById("result").innerText = "";
    loadQuiz();
};

loadQuiz();
</script>

</body>
</html>