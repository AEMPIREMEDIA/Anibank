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
    .receipt {
      background: white;
      padding: 1.5rem;
      border: 1px dashed #aaa;
      font-family: monospace;
      width: 100%;
      max-width: 380px;
      margin-top: 1rem;
      display: none;
      text-align: center;
    }
    .receipt h3 {
      margin-bottom: 1rem;
    }
    .receipt img.logo {
      max-width: 80px;
      margin-bottom: 1rem;
    }
    .receipt img.qr {
      max-width: 100px;
      margin-top: 1rem;
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

    <div class="receipt" id="receipt">
      <img src="https://via.placeholder.com/80x40.png?text=Bank+Logo" alt="Bank Logo" class="logo" />
      <h3>Bank Payment Receipt</h3>
      <p><strong>Amount:</strong> ₦<span id="amountDisplay"></span></p>
      <p><strong>To:</strong> <span id="accountNameDisplay"></span> (<span id="accountDisplay"></span>)</p>
      <p><strong>Bank:</strong> <span id="bankDisplay"></span></p>
      <p><strong>From:</strong> <span id="senderNameDisplay"></span></p>
      <p><strong>Date:</strong> <span id="dateTimeDisplay"></span></p>
      <p><strong>Description:</strong> <span id="descDisplay"></span></p>
      <p style="margin-top: 1rem; font-style: italic;">Beneficiary will receive funds within 24 banking hours.</p>
      <img src="https://api.qrserver.com/v1/create-qr-code/?size=100x100&data=Payment%20Confirmed" alt="QR Code" class="qr" />
    </div>

    <button onclick="downloadReceipt()" style="display: none;" id="downloadBtn">Download Receipt</button>
  </div>

  <!-- Include html2canvas -->
  <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>

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

      document.getElementById('receipt').style.display = 'block';
      document.getElementById('downloadBtn').style.display = 'inline-block';
    }

    function downloadReceipt() {
      const receipt = document.getElementById('receipt');
      html2canvas(receipt).then(canvas => {
        const link = document.createElement('a');
        link.href = canvas.toDataURL('image/png');
        link.download = 'payment-receipt.png';
        link.click();
      });
    }
  </script>
</body>
</html>
