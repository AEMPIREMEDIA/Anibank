<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
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
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      max-width: 400px;
      width: 100%;
    }
    input, button, select, textarea {
      width: 100%;
      padding: 1rem;
      margin: 0.5rem 0;
      border-radius: 0.5rem;
      border: 1px solid #ccc;
      box-sizing: border-box;
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
    <input type="text" id="senderName" placeholder="Enter Sender's Name">
    <input type="text" id="bankName" placeholder="Enter Bank Name">
    <input type="text" id="accountNumber" placeholder="Enter Nigerian Account Number" maxlength="10">
    <input type="text" id="accountName" placeholder="Enter Beneficiary Account Name">
    <input type="number" id="amount" placeholder="Enter Amount (₦)">
    <textarea id="description" placeholder="Enter Transfer Description"></textarea>
    <button onclick="sendAlert()">Send Alert</button>
    <div class="alert" id="alertBox">
      Payment alert of ₦<span id="amountDisplay"></span> sent to <span id="accountNameDisplay"></span> 
      (<span id="accountDisplay"></span>) at <span id="bankDisplay"></span> by <span id="senderNameDisplay"></span> on 
      <span id="dateTimeDisplay"></span>. <br>
      Description: <span id="descDisplay"></span><br>
      The beneficiary will receive the fund within 24 banking hours.
    </div>
    <button onclick="downloadReceipt()" style="display: none;" id="downloadBtn">Download Receipt</button>
  </div>

  <script>
    function sendAlert() {
      const sender = document.getElementById('senderName').value.trim();
      const bank = document.getElementById('bankName').value.trim();
      const account = document.getElementById('accountNumber').value.trim();
      const accountName = document.getElementById('accountName').value.trim();
      const amount = document.getElementById('amount').value.trim();
      const description = document.getElementById('description').value.trim();

      if (!sender || !bank || !account || !accountName) {
        alert('Please fill in all required fields.');
        return;
      }

      if (account.length !== 10 || isNaN(account)) {
        alert('Please enter a valid 10-digit account number.');
        return;
      }

      if (!amount || isNaN(amount) || amount <= 0) {
        alert('Please enter a valid amount.');
        return;
      }

      const now = new Date();
      const dateTime = now.toLocaleString();

      document.getElementById('senderNameDisplay').textContent = sender;
      document.getElementById('bankDisplay').textContent = bank;
      document.getElementById('accountDisplay').textContent = account;
      document.getElementById('accountNameDisplay').textContent = accountName;
      document.getElementById('amountDisplay').textContent = parseFloat(amount).toLocaleString();
      document.getElementById('descDisplay').textContent = description || "N/A";
      document.getElementById('dateTimeDisplay').textContent = dateTime;

      document.getElementById('alertBox').style.display = 'block';
      document.getElementById('downloadBtn').style.display = 'inline-block';
    }

    function downloadReceipt() {
      const text = document.getElementById('alertBox').innerText;
      const blob = new Blob([text], { type: 'text/plain' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = 'payment-receipt.txt';
      link.click();
    }
  </script>
</body>
</html>
