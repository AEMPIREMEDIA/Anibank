<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Polaris Transaction Receipt</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f3f4f6;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }
    .receipt {
      background: #fff;
      width: 90%;
      max-width: 500px;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    .receipt h2 {
      margin-top: 0;
    }
    .amount {
      color: #00c28b;
      font-size: 28px;
      font-weight: bold;
    }
    .approved {
      color: #00c28b;
      font-weight: bold;
      margin-bottom: 5px;
    }
    .info {
      text-align: left;
      margin-top: 20px;
    }
    .info div {
      margin: 10px 0;
    }
    .label {
      font-weight: bold;
    }
    .support {
      margin-top: 30px;
      font-size: 14px;
      color: #666;
    }
    .support a {
      color: #00c28b;
      text-decoration: none;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      background: #00c28b;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="receipt" id="receiptContent">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/OPay_logo.svg/512px-OPay_logo.svg.png" alt="Opay Logo" width="80" />
    <h2>Transaction info</h2>
    <div class="amount">NGN 2000.00</div>
    <div class="approved">APPROVED</div>
    <div>06/04/25 14:32:16</div>

    <div class="info">
      <div><span class="label">Transaction Type:</span> Transfer to OPay</div>
      <div><span class="label">Sender:</span> OWUMI BOB MAYOMI</div>
      <div><span class="label">Sender Account:</span> 905 011 0150</div>
      <div><span class="label">Recipient:</span> ANIEFIOK BASSEY ETIM</div>
      <div><span class="label">Recipient Account:</span> 912 776 8874</div>
      <div><span class="label">Remark:</span> FOR DATA</div>
      <div><span class="label">Transaction NO.:</span> 250406010100063646464641</div>
    </div>

    <div class="support">
      SUPPORT<br />
      <a href="mailto:pos-service@opay-inc.com">pos-service@opay-inc.com</a><br />
      07008888329
    </div>

    <button onclick="downloadReceipt()">Download Receipt</button>
  </div>

  <script>
    function downloadReceipt() {
      const element = document.createElement('a');
      const content = document.getElementById('receiptContent').innerText;
      const file = new Blob([content], { type: 'text/plain' });
      element.href = URL.createObjectURL(file);
      element.download = "opay-receipt.txt";
      document.body.appendChild(element);
      element.click();
    }
  </script>
</body>
</html>
