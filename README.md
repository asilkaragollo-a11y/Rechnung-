# Rechnung-
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Coin Rechner</title>

<style>
    * {
        box-sizing: border-box;
        font-family: Arial, sans-serif;
    }

    body {
        margin: 0;
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #f2f2f7;
        padding: 20px;
    }

    .box {
        width: 100%;
        max-width: 430px;
        background: white;
        padding: 28px;
        border-radius: 24px;
        box-shadow: 0 10px 35px rgba(0,0,0,0.12);
    }

    h1 {
        text-align: center;
        margin: 0;
        font-size: 28px;
    }

    .subtitle {
        text-align: center;
        color: #777;
        margin: 8px 0 25px;
    }

    label {
        display: block;
        font-weight: bold;
        margin-top: 18px;
        margin-bottom: 8px;
    }

    input {
        width: 100%;
        padding: 15px;
        border: 1px solid #d5d5d5;
        border-radius: 12px;
        font-size: 18px;
        outline: none;
    }

    input:focus {
        border-color: #007aff;
    }

    button {
        width: 100%;
        margin-top: 24px;
        padding: 16px;
        border: none;
        border-radius: 14px;
        background: #007aff;
        color: white;
        font-size: 18px;
        font-weight: bold;
        cursor: pointer;
    }

    button:active {
        transform: scale(0.98);
    }

    .error {
        display: none;
        color: #d00000;
        text-align: center;
        margin-top: 15px;
    }

    .result {
        display: none;
        margin-top: 25px;
        background: #f2f2f7;
        border-radius: 18px;
        padding: 20px;
    }

    .result h2 {
        margin-top: 0;
        font-size: 21px;
    }

    .row {
        display: flex;
        justify-content: space-between;
        gap: 15px;
        padding: 9px 0;
        border-bottom: 1px solid #ddd;
    }

    .row:last-of-type {
        border-bottom: none;
    }

    .value {
        font-weight: bold;
        text-align: right;
    }

    .coins {
        font-size: 25px;
        font-weight: bold;
        margin-top: 15px;
    }

    .formula {
        margin-top: 15px;
        padding-top: 15px;
        border-top: 1px solid #ddd;
        color: #555;
        word-break: break-word;
    }
</style>
</head>

<body>

<div class="box">

    <h1>🪙 Coin-Rechner</h1>

    <div class="subtitle">
        Wie viele Coins bekommst du?
    </div>

    <label>Preis pro Coin (€)</label>

    <input
        id="price"
        type="text"
        inputmode="decimal"
        placeholder="z. B. 0,00878"
    >

    <label>Wie viel Geld investierst du? (€)</label>

    <input
        id="money"
        type="text"
        inputmode="decimal"
        placeholder="z. B. 10"
    >

    <button onclick="calculate()">
        Berechnen
    </button>

    <div class="error" id="error">
        Bitte gib gültige Zahlen ein.
    </div>

    <div class="result" id="result">

        <h2>Zusammenfassung</h2>

        <div class="row">
            <span>💰 Preis pro Coin</span>
            <span class="value" id="priceResult"></span>
        </div>

        <div class="row">
            <span>💵 Einsatz</span>
            <span class="value" id="moneyResult"></span>
        </div>

        <div class="coins">
            🪙 Du kaufst: <span id="coinResult"></span> Coins
        </div>

        <div class="formula" id="formula"></div>

    </div>

</div>


<script>

function getNumber(value) {

    // Komma und Punkt werden akzeptiert
    value = value.replace(",", ".");

    return Number(value);
}


function formatEuro(number) {

    return number.toLocaleString("de-DE", {
        minimumFractionDigits: 2,
        maximumFractionDigits: 12
    }) + " €";

}


function formatCoins(number) {

    // Immer genau 2 Nachkommastellen
    return number.toLocaleString("de-DE", {
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
    });

}


function calculate() {

    const priceText =
        document.getElementById("price").value.trim();

    const moneyText =
        document.getElementById("money").value.trim();


    const price = getNumber(priceText);
    const money = getNumber(moneyText);


    const error =
        document.getElementById("error");

    const result =
        document.getElementById("result");


    // Prüfen, ob die Eingaben gültig sind
    if (
        !Number.isFinite(price) ||
        !Number.isFinite(money) ||
        price <= 0 ||
        money <= 0
    ) {

        error.style.display = "block";
        result.style.display = "none";

        return;
    }


    error.style.display = "none";


    // Rechnung
    const coins = money / price;


    // Ergebnisse anzeigen
    document.getElementById("priceResult").textContent =
        formatEuro(price);

    document.getElementById("moneyResult").textContent =
        formatEuro(money);

    document.getElementById("coinResult").textContent =
        formatCoins(coins);


    document.getElementById("formula").textContent =
        `${formatEuro(money)} ÷ ${formatEuro(price)} = ${formatCoins(coins)} Coins`;


    result.style.display = "block";
}

</script>

</body>
</html>
