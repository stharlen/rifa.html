<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rifa Oficial</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: url('https://images.unsplash.com/photo-1526406915894-7bcd65f60845') no-repeat center center fixed;
    background-size: cover;
    color: #fff;
}

.overlay {
    background: rgba(0,0,0,0.75);
    min-height: 100vh;
    padding-bottom: 40px;
}

header {
    text-align: center;
    padding: 30px 20px 10px;
}

header h1 {
    margin: 0;
    font-size: 32px;
}

header p {
    margin-top: 5px;
    font-size: 18px;
    color: #ccc;
}

/* CARROSSEL */
.carousel {
    width: 90%;
    max-width: 500px;
    margin: 20px auto;
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 0 20px rgba(0,0,0,0.8);
}

.carousel img {
    width: 100%;
    display: none;
}

.carousel img.active {
    display: block;
}

/* NÚMEROS */
.numbers {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    gap: 6px;
    max-width: 500px;
    margin: 20px auto;
}

.number {
    padding: 10px;
    background: #ffffff;
    color: #000;
    text-align: center;
    border-radius: 6px;
    cursor: pointer;
    font-weight: bold;
    transition: 0.3s;
}

.number:hover {
    transform: scale(1.05);
}

.number.selected {
    background: #28a745;
    color: #fff;
}

.number.reserved {
    background: #6c757d;
    color: #fff;
    cursor: not-allowed;
}

/* FORM */
.form {
    max-width: 450px;
    margin: 20px auto;
    background: #ffffff;
    color: #000;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0,0,0,0.5);
}

.form h3 {
    margin-top: 0;
}

input, button {
    width: 100%;
    padding: 12px;
    margin-top: 10px;
    border-radius: 6px;
    border: 1px solid #ccc;
}

button {
    background: #28a745;
    color: #fff;
    border: none;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background: #218838;
}

.pix-box {
    margin-top: 15px;
    padding: 10px;
    background: #e9ecef;
    border-radius: 6px;
}

/* RODAPÉ */
footer {
    text-align: center;
    padding: 20px;
    background: rgba(0,0,0,0.8);
    margin-top: 40px;
    font-size: 14px;
    color: #ccc;
}
</style>
</head>

<body>
<div class="overlay">

<header>
    <h1>🎟️ Rifa Oficial</h1>
    <p>Valor por número: <strong>R$ 10,00</strong></p>
</header>

<!-- CARROSSEL -->
<div class="carousel">
    <img src="https://images.unsplash.com/photo-1606813907291-d86efa9b94db" class="active">
    <img src="https://images.unsplash.com/photo-1599058917765-a780eda07a3e">
    <img src="https://images.unsplash.com/photo-1585386959984-a4155224a1ad">
</div>

<!-- NÚMEROS -->
<div class="numbers" id="numbers"></div>

<!-- FORMULÁRIO -->
<div class="form">
    <h3>Finalizar Compra</h3>
    <input type="text" id="name" placeholder="Nome completo">
    <input type="text" id="whatsapp" placeholder="WhatsApp com DDD">
    <button onclick="finalizarCompra()">Reservar e Pagar</button>
    <div id="resultado"></div>
</div>

<footer>
    © 2026 Rifa Oficial | Pagamento via Pix | 
    Chave Pix: <strong>stharlen1@gmail.com</strong><br>
    Sistema seguro de reserva automática.
</footer>

</div>

<script>
const totalNumbers = 100;
const valorPorNumero = 10;
const pixKey = "stharlen1@gmail.com";

let selectedNumbers = [];
let reservedNumbers = [];

const numbersDiv = document.getElementById("numbers");

for (let i = 1; i <= totalNumbers; i++) {
    const div = document.createElement("div");
    div.className = "number";
    div.innerText = i.toString().padStart(2, '0');
    div.onclick = () => selecionarNumero(div, i);
    numbersDiv.appendChild(div);
}

function selecionarNumero(element, number) {
    if (reservedNumbers.includes(number)) return;

    if (selectedNumbers.includes(number)) {
        selectedNumbers = selectedNumbers.filter(n => n !== number);
        element.classList.remove("selected");
    } else {
        selectedNumbers.push(number);
        element.classList.add("selected");
    }
}

function finalizarCompra() {
    const name = document.getElementById("name").value;
    const whatsapp = document.getElementById("whatsapp").value;

    if (!name || !whatsapp || selectedNumbers.length === 0) {
        alert("Preencha os dados e selecione ao menos um número.");
        return;
    }

    const total = selectedNumbers.length * valorPorNumero;

    selectedNumbers.forEach(num => reservedNumbers.push(num));
    document.querySelectorAll(".number.selected").forEach(el => {
        el.classList.remove("selected");
        el.classList.add("reserved");
    });

    const mensagem = `Olá ${name}! 
Você reservou os números: ${selectedNumbers.join(", ")} 
Valor total: R$ ${total},00 
Chave Pix: ${pixKey}`;

    document.getElementById("resultado").innerHTML = `
        <div class="pix-box">
            <p><strong>Total:</strong> R$ ${total},00</p>
            <p><strong>Chave Pix:</strong> ${pixKey}</p>
            <a href="https://wa.me/55${whatsapp}?text=${encodeURIComponent(mensagem)}" target="_blank">
                <button>Enviar Comprovante no WhatsApp</button>
            </a>
        </div>
    `;

    selectedNumbers = [];
}

/* CARROSSEL AUTOMÁTICO */
let slideIndex = 0;
const slides = document.querySelectorAll(".carousel img");

setInterval(() => {
    slides[slideIndex].classList.remove("active");
    slideIndex = (slideIndex + 1) % slides.length;
    slides[slideIndex].classList.add("active");
}, 3000);
</script>

</body>
</html>
