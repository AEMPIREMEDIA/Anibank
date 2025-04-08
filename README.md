<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Mock Payment Gateway</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f3f4f6;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background: white;
      padding: 2rem;
      border-radius: 1rem;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      max-width: 400px;
      width: 100%;
    }
    input, button {
      width: 100%;
      padding: 1rem;
      margin: 0.5rem 0;
      border-radius: 0.5rem;
      border: 1px solid #ccc;
    }
    .alert {
      display: none;
      padding: 1rem;
      background-color: #d1fae5;
      color: #065f46;
      border: 1px solid #10b981;
      border-radius: 0.5rem;
      margin-top: 1rem;
      text-align: center;
      animation: flash 0.5s alternate infinite;
    }
    @keyframes flash {
      0% { opacity: 1; }
      100% { opacity: 0.4; }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Send Payment Alert</h2>
    <input type="text" id="accountNumber" placeholder="Enter Nigerian Account Number" maxlength="10">
    <input type="number" id="amount" placeholder="Enter Amount (₦)">
    <button onclick="sendAlert()">Send Alert</button>
    <div class="alert" id="alertBox">
      Payment alert of ₦<span id="amountDisplay"></span> sent to account <span id="accountDisplay"></span>.
    </div>
  </div>

  <script>
    function sendAlert() {
      const account = document.getElementById('accountNumber').value.trim();
      const amount = document.getElementById('amount').value.trim();
      const alertBox = document.getElementById('alertBox');
      const accountDisplay = document.getElementById('accountDisplay');
      const amountDisplay = document.getElementById('amountDisplay');

      if (account.length !== 10 || isNaN(account)) {
        alert('Please enter a valid 10-digit Nigerian account number.');
        return;
      }
      if (!amount || isNaN(amount) || amount <= 0) {
        alert('Please enter a valid amount.');
        return;
      }

      accountDisplay.textContent = account;
      amountDisplay.textContent = parseFloat(amount).toLocaleString();

      alertBox.style.display = 'block';
    }
  </script>
</body>
</html>
