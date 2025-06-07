<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simple Currency Converter</title>
  <style>
    
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body, html {
      margin: 0;
      height: 100%;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
      background: #ffffff;
      color: #6b7280;
      font-size: 16px;
      line-height: 1.5;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 2rem;
      min-height: 100vh;
    }
    .converter-card {
      background: white;
      border-radius: 0.75rem;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.07);
      max-width: 400px;
      width: 100%;
      padding: 2.5rem 2rem 3rem;
      text-align: center;
    }
    h1 {
      font-weight: 700;
      font-size: 48px;
      margin-bottom: 1.5rem;
      color: #111827;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1.25rem;
      max-width: 320px;
      margin: 0 auto;
      text-align: left;
    }
    label {
      font-weight: 600;
      margin-bottom: 0.5rem;
      color: #374151;
      font-size: 1rem;
      display: block;
    }
    input[type="number"],
    select {
      font-size: 1rem;
      border: 1px solid #d1d5db;
      border-radius: 0.5rem;
      padding: 0.6rem 1rem;
      color: #111827;
      background-color: white;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
      width: 100%;
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
    }
    input[type="number"]:focus,
    select:focus {
      border-color: #2563eb;
      outline: none;
      box-shadow: 0 0 8px rgba(37, 99, 235, 0.4);
    }
    button {
      margin-top: 1.5rem;
      background-color: #111827;
      color: white;
      font-weight: 700;
      font-size: 1.125rem;
      padding: 0.85rem 0;
      border: none;
      border-radius: 0.75rem;
      cursor: pointer;
      transition: background-color 0.3s ease;
      width: 100%;
    }
    button:hover,
    button:focus {
      background-color: #2563eb;
      outline: none;
    }
    .result {
      margin-top: 1.5rem;
      font-size: 1.25rem;
      font-weight: 600;
      color: #2563eb;
      min-height: 1.5em;
      text-align: center;
    }
    .error-message {
      color: #dc2626;
      font-size: 0.875rem;
      min-height: 1em;
      margin-top: 0.25rem;
      text-align: left;
    }
  </style>
</head>
<body>
  <section class="converter-card" role="region" aria-labelledby="title">
    <h1 id="title">Currency Converter</h1>
    <form id="form" novalidate>
      <label for="amount">Amount</label>
      <input type="number" id="amount" name="amount" placeholder="Enter amount" min="0" step="any" required aria-describedby="amount-error" />
      <div id="amount-error" class="error-message" aria-live="assertive"></div>

      <label for="from-currency">From</label>
      <select id="from-currency" name="from-currency" required>
        <option value="USD">United States Dollar (USD)</option>
        <option value="EUR">Euro (EUR)</option>
        <option value="INR">Indian Rupee (INR)</option>
        <option value="GBP">British Pound (GBP)</option>
        <option value="JPY">Japanese Yen (JPY)</option>
      </select>

      <label for="to-currency">To</label>
      <select id="to-currency" name="to-currency" required>
        <option value="USD">United States Dollar (USD)</option>
        <option value="EUR">Euro (EUR)</option>
        <option value="INR">Indian Rupee (INR)</option>
        <option value="GBP">British Pound (GBP)</option>
        <option value="JPY">Japanese Yen (JPY)</option>
      </select>

      <button type="submit">Convert</button>
    </form>
    <div id="result" class="result" aria-live="polite" aria-atomic="true"></div>
  </section>

  <script>
    
    const rates = {
      USD: 1,
      EUR: 0.92,
      INR: 82,
      GBP: 0.82,
      JPY: 136,
    };

    const form = document.getElementById('form');
    const amountInput = document.getElementById('amount');
    const fromSelect = document.getElementById('from-currency');
    const toSelect = document.getElementById('to-currency');
    const resultDiv = document.getElementById('result');
    const amountError = document.getElementById('amount-error');

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      amountError.textContent = '';
      resultDiv.textContent = '';

      const amount = parseFloat(amountInput.value);
      if (isNaN(amount) || amount <= 0) {
        amountError.textContent = 'Please enter a valid positive number.';
        return;
      }

      const from = fromSelect.value;
      const to = toSelect.value;

      if (from === to) {
        resultDiv.textContent = 'Please select different currencies.';
        return;
      }

      
      const amountInUSD = amount / rates[from];
      const convertedAmount = amountInUSD * rates[to];

      resultDiv.textContent = `${amount.toFixed(2)} ${from} = ${convertedAmount.toFixed(2)} ${to}`;
    });
  </script>
</body>
</html>

