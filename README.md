<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Rifa Online</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f4f4;
        padding: 20px;
    }
    h1 {
        text-align: center;
    }
    .numbers {
        display: grid;
        grid-template-columns: repeat(10, 1fr);
        gap: 8px;
        max-width: 500px;
        margin: 20px auto;
    }
    .number {
        padding: 12px;
        background: #fff;
        border: 1px solid #ccc;
        cursor: pointer;
        text-align: center;
        font-weight: bold;
        border-radius: 5px;
    }
    .number.selected {
        background: #4CAF50;
        color: white;
    }
    .number.reserved {
        background: #999;
        color: white;
        cursor: not-allowed;
    }
    .form {
        max-width: 400px;
        margin: 20px auto;
        background: #fff;
        padding: 15px;
        border-radius: 5px;
    }
    input, button {
        width: 100%;
        padding: 10px;
        margin-top: 10px;
    }
    button {
        background: #4CAF50;
        color: white;
        border: none;
        cursor: pointer;
        font-size: 16px;
    }
    .pix {
        background: #e8f5e9;
        padding: 10px;
        margin-top: 10px;
        border-radius: 5px;
        font-weight: bold;
    }
</style>
</head>

<body>

<h1>🎟️ Rifa Online</h1>
<p style="text-align:center;">Valor por número: <strong>R$ 10,00</strong></p>

<div class="numbers" id="numbers"></div>

<div class="form">
    <h3>Dados do Comprador</h3>
    <input type="text" id="name" placeholder="Nome completo" required>
    <input type="text" id="whatsapp" placeholder="WhatsApp (DDD + número)" required>
    <button onclick="finalizarCompra()">Finalizar Compra</button>

    <div id="resultado"></div>
</div>

<script>
const totalNumbers = 100;
const valorPorNumero = 10;
const pixKey = "stharlen1@gmail.com";

let selectedNumbers = [];
let reservedNumbers = [];

const numbersDiv = document.getElementById("numbers");

// Criar números da rifa
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

    // Reservar números
    selectedNumbers.forEach(num => reservedNumbers.push(num));
    document.querySelectorAll(".number.selected").forEach(el => {
        el.classList.remove("selected");
        el.classList.add("reserved");
    });

    const mensagemWhats = `
Olá ${name}!
Você reservou os números: ${selectedNumbers.join(", ")}
Valor total: R$ ${total},00

Chave Pix:
${pixKey}

Após o pagamento, seus números estão confirmados. ✅
`;

    document.getElementById("resultado").innerHTML = `
        <div class="pix">
            <p>💰 Valor total: R$ ${total},00</p>
            <p>🔑 Chave Pix: ${pixKey}</p>
            <p>📲 Envio dos números via WhatsApp</p>
            <a href="https://wa.me/55${whatsapp}?text=${encodeURIComponent(mensagemWhats)}" target="_blank">
                <button>Enviar confirmação no WhatsApp</button>
            </a>
        </div>
    `;

    selectedNumbers = [];
}
</script>

</body>
</html>
