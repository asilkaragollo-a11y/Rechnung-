# Rechnung-
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Coin & Aktien Rechner</title>

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

    .calculator {
      width: 100%;
      max-width: 420px;
      background: white;
      padding: 30px;
      border-radius: 25px;
      box-shadow: 0 10px 35px rgba(0,0,0,0.12);
    }

    h1 {
      text-align: center;
      margin-bottom: 8px;
    }

    .subtitle {
      text-align: center;
      color: #777;
      margin-bottom: 30px;
    }

    label {
      display: block;
      font-weight: bold;
      margin: 18px 0 8px;
    }

    input {
      width: 100%;
      padding: 15px;
      border: 1px solid #ddd;
      border-radius: 12px;
      font-size: 18px;
      outline: none;
    }

    input:focus {
      border-color: #007aff;
    }

    button {
      width: 100%;
      margin-top: 25px;
      padding: 16px;
      border: none;
      border-radius: 14px;
      background: #007aff;
      color: white;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      opacity: 0.9;
    }

    .result {
      margin-top: 25px;
      padding: 20px;
      background: #f2f2f7;
      border-radius: 16px;
      display: none;
    }

    .result-title {
      font-weight: bold;
      margin-bottom: 12px;
    }

    .calculation {
      font-size: 18px;
      line-height: 1.6;
      word-break: break-word;
    }

    .amount {
      font-size: 28px;
      font-weight: bold;
      margin-top: 12px;
    }

    .error {
      color: #d00;
      margin-top: 15px;
      display: none;
      text-align: center;
    }
  </style>
</head>

<body>

  <div class="calculator">

    <h1>💰 Rechner</h1>
    <div class="subtitle">Coins oder Aktien berechnen</div>

    <label for="price">Preis pro Coin / Aktie (€)</label>
    <input
      id="price"
      type="text"
      inputmode="decimal"
      placeholder="z. B. 0,008"
    >

    <label for="investment">Wie viel Geld möchtest du investieren? (€)</label>
    <input
      id="investment"
      type="text"
      inputmode="decimal"
      placeholder="z. B. 10"
    >

    <button onclick="calculate()">Berechnen</button>

    <div class="error" id="error">
      Bitte gib gültige Zahlen ein.
    </div>

    <div class="result" id="result">
      <div class="result-title">Deine Rechnung:</div>

      <div class="calculation" id="calculation"></div>

      <div class="amount" id="amount"></div>
    </div>

  </div>

  <script>
    function toNumber(value) {
      // Komma in Punkt umwandeln
      return parseFloat(value.replace(",", "."));
    }

    function formatNumber(number) {
      return new Intl.NumberFormat("de-DE", {
        maximumFractionDigits: 12
      }).format(number);
    }

    function calculate() {

      const priceInput = document.getElementById("price").value.trim();
      const investmentInput = document.getElementById("investment").value.trim();

      const price = toNumber(priceInput);
      const investment = toNumber(investmentInput);

      const error = document.getElementById("error");
      const result = document.getElementById("result");

      if (
        !isFinite(price) ||
        !isFinite(investment) ||
        price <= 0 ||
        investment <= 0
      ) {
        error.style.display = "block";
        result.style.display = "none";
        return;
      }

      error.style.display = "none";

      const quantity = investment / price;

      document.getElementById("calculation").innerHTML =
        `${formatNumber(investment)} € ÷ ${formatNumber(price)} €`;

      document.getElementById("amount").innerHTML =
        `${formatNumber(quantity)} Stück`;

      result.style.display = "block";
    }
  </script>

</body>
</html>
