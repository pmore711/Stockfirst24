<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>StockFirst24 - Indian Stock Market Info</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      margin: 0;
      padding: 0;
    }
    header {
      background: #002060;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    section {
      max-width: 1200px;
      margin: 2rem auto;
      padding: 1rem;
      background: white;
      border-radius: 8px;
      box-shadow: 0 0 10px #ccc;
      overflow-x: auto;
    }
    input[type="text"], input[type="number"], input[type="password"], input[type="email"] {
      width: 100%;
      padding: 0.5rem;
      margin: 0.5rem 0 1rem 0;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      background-color: #002060;
      color: white;
      padding: 0.7rem 1.2rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0044cc;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 1rem;
    }
    th, td {
      padding: 0.6rem;
      border: 1px solid #ddd;
      text-align: left;
      font-size: 0.9rem;
    }
    th {
      background-color: #002060;
      color: white;
      position: relative;
      white-space: nowrap;
    }
    th input.filter {
      width: 80%;
      margin: 0.3rem 0;
      font-size: 0.8rem;
      border-radius: 3px;
      border: none;
      padding: 3px;
    }
    .range-inputs {
      display: flex;
      gap: 4px;
      justify-content: center;
    }
    .range-inputs input {
      width: 40%;
      padding: 3px;
      font-size: 0.8rem;
      border: none;
      border-radius: 3px;
    }
    .error-message { color: red; }
    .success-message { color: green; }
    .pagination {
      margin-top: 1rem;
      text-align: center;
    }
    .pagination button {
      margin: 0 4px;
      padding: 6px 12px;
      background-color: #002060;
      color: white;
      border-radius: 4px;
      border: none;
      cursor: pointer;
    }
    .pagination button.disabled {
      background-color: #999;
      cursor: not-allowed;
    }
    #csv-controls button {
      margin-right: 8px;
    }
  </style>
</head>
<body>
    <header>
    <h1>StockFirst24</h1>
    <p>Indian Listed Companies - 20 Fundamental Parameters</p>
  </header>

  <section id="signup-section">
    <h2>Sign Up</h2>
    <form id="signup-form" onsubmit="return handleSignup(event)">
      <label>Email:</label>
      <input type="email" id="signup-email" required />
      <label>Password:</label>
      <input type="password" id="signup-password" required minlength="6" />
      <button type="submit">Create Account</button>
      <p id="signup-message"></p>
      <p>Already have an account? <a href="#" onclick="showLogin()">Login</a></p>
    </form>
  </section>

  <section id="login-section" style="display:none;">
    <h2>Login</h2>
    <form id="login-form" onsubmit="return handleLogin(event)">
      <label>Email:</label>
      <input type="email" id="email" required />
      <label>Password:</label>
      <input type="password" id="password" required />
      <button type="submit">Login</button>
      <p><a href="#" onclick="showResetPassword()">Forgot Password?</a></p>
      <p id="login-error" class="error-message"></p>
      <p>Don't have an account? <a href="#" onclick="showSignup()">Sign up</a></p>
    </form>
  </section>

  <section id="password-reset-section" style="display:none;">
    <h2>Reset Password</h2>
    <form id="reset-form" onsubmit="return handleResetPassword(event)">
      <label>Enter your Email:</label>
      <input type="email" id="reset-email" required />
      <button type="submit">Send Reset Link</button>
      <p id="reset-message"></p>
    </form>
    <p><a href="#" onclick="showLogin()">Back to Login</a></p>
  </section>
  <section id="subscription-section" style="display:none;">
    <h2>Subscription</h2>
    <p id="subscription-status"></p>
    <button id="purchase-btn" onclick="initiatePayment()">Purchase / Renew Subscription</button>
    <button onclick="logout()" style="margin-left:10px; background:#900;">Logout</button>
  </section>
  <section id="stock-table-section" style="display:none;">
    <h2>Stock Fundamentals (Top 20 Parameters)</h2>

    <!-- CSV Controls (Shown only for authorized email) -->
    <div id="csv-controls" style="margin: 10px 0; display:none;">
      <button onclick="exportCSV()">Export CSV</button>
      <input type="file" id="import-file" accept=".csv" style="display:none;" onchange="importCSV(event)" />
      <button onclick="document.getElementById('import-file').click()">Import CSV</button>
    </div>

    <table id="stock-table">
      <thead>
        <tr>
          <th>Company<br /><input class="filter" data-column="company" placeholder="Filter" /></th>
          <th>Symbol<br /><input class="filter" data-column="symbol" placeholder="Filter" /></th>
          <th>Market Cap (₹Cr)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="marketCap" placeholder="Min">
              <input type="number" class="max" data-column="marketCap" placeholder="Max">
            </div>
          </th>
          <th>P/E Ratio<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="peRatio" placeholder="Min">
              <input type="number" class="max" data-column="peRatio" placeholder="Max">
            </div>
          </th>
          <th>EPS<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="eps" placeholder="Min">
              <input type="number" class="max" data-column="eps" placeholder="Max">
            </div>
          </th>
          <th>Dividend Yield (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="dividendYield" placeholder="Min">
              <input type="number" class="max" data-column="dividendYield" placeholder="Max">
            </div>
          </th>
          <th>Book Value<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="bookValue" placeholder="Min">
              <input type="number" class="max" data-column="bookValue" placeholder="Max">
            </div>
          </th>
          <th>P/B Ratio<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="pbRatio" placeholder="Min">
              <input type="number" class="max" data-column="pbRatio" placeholder="Max">
            </div>
          </th>
          <th>Face Value<br /><input class="filter" data-column="faceValue" placeholder="Filter" /></th>
          <th>Debt/Equity<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="deRatio" placeholder="Min">
              <input type="number" class="max" data-column="deRatio" placeholder="Max">
            </div>
          </th>
          <th>ROE (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="roe" placeholder="Min">
              <input type="number" class="max" data-column="roe" placeholder="Max">
            </div>
          </th>
          <th>ROCE (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="roce" placeholder="Min">
              <input type="number" class="max" data-column="roce" placeholder="Max">
            </div>
          </th>
          <th>Current Ratio<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="currentRatio" placeholder="Min">
              <input type="number" class="max" data-column="currentRatio" placeholder="Max">
            </div>
          </th>
          <th>Quick Ratio<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="quickRatio" placeholder="Min">
              <input type="number" class="max" data-column="quickRatio" placeholder="Max">
            </div>
          </th>
          <th>PEG Ratio<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="pegRatio" placeholder="Min">
              <input type="number" class="max" data-column="pegRatio" placeholder="Max">
            </div>
          </th>
          <th>Promoter Holding (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="promoterHolding" placeholder="Min">
              <input type="number" class="max" data-column="promoterHolding" placeholder="Max">
            </div>
          </th>
          <th>FII Holding (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="fiiHolding" placeholder="Min">
              <input type="number" class="max" data-column="fiiHolding" placeholder="Max">
            </div>
          </th>
          <th>DII Holding (%)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="diiHolding" placeholder="Min">
              <input type="number" class="max" data-column="diiHolding" placeholder="Max">
            </div>
          </th>
          <th>Profit Growth (3Y %)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="profitGrowth" placeholder="Min">
              <input type="number" class="max" data-column="profitGrowth" placeholder="Max">
            </div>
          </th>
          <th>Sales Growth (3Y %)<br />
            <div class="range-inputs">
              <input type="number" class="min" data-column="salesGrowth" placeholder="Min">
              <input type="number" class="max" data-column="salesGrowth" placeholder="Max">
            </div>
          </th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
    <div class="pagination" id="pagination-controls"></div>
  </section>
  <script>
  // === Mock Database ===
  const usersDB = {
    "demo@example.com": { password: "123456", subscriptionExpiry: new Date(Date.now() + 7*24*60*60*1000) }
  };

  // === Sample Stock Data ===
  const stockData = [];
  for (let i = 1; i <= 100; i++) {
    stockData.push({
      company: `Company ${i}`,
      symbol: `SYM${i}`,
      marketCap: (1000 + Math.random() * 500000).toFixed(0),
      peRatio: (10 + Math.random() * 40).toFixed(2),
      eps: (1 + Math.random() * 100).toFixed(2),
      dividendYield: (Math.random() * 5).toFixed(2),
      bookValue: (50 + Math.random() * 500).toFixed(2),
      pbRatio: (1 + Math.random() * 10).toFixed(2),
      faceValue: 10,
      deRatio: (Math.random() * 2).toFixed(2),
      roe: (5 + Math.random() * 30).toFixed(2),
      roce: (5 + Math.random() * 30).toFixed(2),
      currentRatio: (1 + Math.random() * 2).toFixed(2),
      quickRatio: (0.5 + Math.random() * 1.5).toFixed(2),
      pegRatio: (0.5 + Math.random() * 2).toFixed(2),
      promoterHolding: (30 + Math.random() * 40).toFixed(2),
      fiiHolding: (5 + Math.random() * 30).toFixed(2),
      diiHolding: (5 + Math.random() * 20).toFixed(2),
      profitGrowth: (5 + Math.random() * 25).toFixed(2),
      salesGrowth: (5 + Math.random() * 25).toFixed(2)
    });
  }

  let loggedInUserEmail = null;
  let currentPage = 1;
  const rowsPerPage = 10;
  let filteredData = stockData.slice();

  // === User Functions ===
  function handleSignup(e) {
    e.preventDefault();
    const email = document.getElementById("signup-email").value.trim();
    const password = document.getElementById("signup-password").value.trim();
    const msg = document.getElementById("signup-message");
    if (usersDB[email]) return msg.textContent = "Email already exists!";
    usersDB[email] = { password, subscriptionExpiry: null };
    msg.textContent = "Account created successfully!";
    setTimeout(showLogin, 1000);
  }

  function handleLogin(e) {
    e.preventDefault();
    const email = document.getElementById("email").value.trim();
    const password = document.getElementById("password").value.trim();
    const err = document.getElementById("login-error");
    err.textContent = "";
    if (!usersDB[email]) return err.textContent = "User not found.";
    if (usersDB[email].password !== password) return err.textContent = "Wrong password.";
    loggedInUserEmail = email;
    hideAllSections();
    document.getElementById("subscription-section").style.display = "block";
    showSubscriptionStatus();
    if (checkSubscriptionActive()) showStockTable();
  }

  function handleResetPassword(e) {
    e.preventDefault();
    const email = document.getElementById("reset-email").value.trim();
    const msg = document.getElementById("reset-message");
    msg.textContent = usersDB[email] ? `Reset link sent to ${email}` : "Email not found.";
  }

  // === UI Navigation ===
  function hideAllSections() {
    ["signup-section","login-section","password-reset-section","subscription-section","stock-table-section"]
      .forEach(id => document.getElementById(id).style.display = "none");
  }
  function showSignup() { hideAllSections(); document.getElementById("signup-section").style.display = "block"; }
  function showLogin() { hideAllSections(); document.getElementById("login-section").style.display = "block"; }
  function showResetPassword() { hideAllSections(); document.getElementById("password-reset-section").style.display = "block"; }

  // === Subscription Logic ===
  function checkSubscriptionActive() {
    const exp = usersDB[loggedInUserEmail]?.subscriptionExpiry;
    return exp && new Date() < exp;
  }

  function showSubscriptionStatus() {
    const s = document.getElementById("subscription-status");
    if (checkSubscriptionActive()) {
      const exp = new Date(usersDB[loggedInUserEmail].subscriptionExpiry);
      s.textContent = `Active until ${exp.toDateString()}`;
      s.className = "success-message";
    } else {
      s.textContent = "Subscription expired. Please renew.";
      s.className = "error-message";
    }
  }

  function initiatePayment() {
    if (!loggedInUserEmail) return alert("Login first!");
    if (confirm("Pay ₹499 for 30-day subscription?")) {
      usersDB[loggedInUserEmail].subscriptionExpiry = new Date(Date.now() + 30*24*60*60*1000);
      alert("Payment successful!");
      showSubscriptionStatus();
      showStockTable();
    }
  }

  function logout() { loggedInUserEmail = null; showLogin(); }

  // === Stock Table Display ===
  function showStockTable() {
    hideAllSections();
    document.getElementById("subscription-section").style.display = "block";
    document.getElementById("stock-table-section").style.display = "block";

    // Show CSV buttons only for authorized email
    document.getElementById("csv-controls").style.display =
      loggedInUserEmail === "pmore711@gmail.com" ? "block" : "none";

    displayStockData();
  }

  function displayStockData() {
    const tbody = document.querySelector("#stock-table tbody");
    tbody
    tbody.innerHTML = "";
    const start = (currentPage - 1) * rowsPerPage;
    const pageData = filteredData.slice(start, start + rowsPerPage);
    pageData.forEach(stock => {
      const tr = document.createElement("tr");
      Object.keys(stock).forEach(k => {
        const td = document.createElement("td");
        td.textContent = stock[k];
        tr.appendChild(td);
      });
      tbody.appendChild(tr);
    });
    renderPagination();
  }

  function renderPagination() {
    const div = document.getElementById("pagination-controls");
    div.innerHTML = "";
    const totalPages = Math.ceil(filteredData.length / rowsPerPage);
    for (let i = 1; i <= totalPages; i++) {
      const btn = document.createElement("button");
      btn.textContent = i;
      btn.disabled = i === currentPage;
      btn.onclick = () => { currentPage = i; displayStockData(); };
      div.appendChild(btn);
    }
  }

  // === Filtering Logic ===
  function applyFilters() {
    const textFilters = {};
    const rangeFilters = {};

    document.querySelectorAll("input.filter").forEach(inp => {
      if (inp.value.trim()) textFilters[inp.dataset.column] = inp.value.trim().toLowerCase();
    });

    document.querySelectorAll(".range-inputs").forEach(div => {
      const min = div.querySelector(".min");
      const max = div.querySelector(".max");
      const col = min.dataset.column;
      const minVal = min.value ? parseFloat(min.value) : -Infinity;
      const maxVal = max.value ? parseFloat(max.value) : Infinity;
      rangeFilters[col] = { minVal, maxVal };
    });

    filteredData = stockData.filter(item => {
      for (let key in textFilters) {
        if (!item[key].toString().toLowerCase().includes(textFilters[key])) return false;
      }
      for (let key in rangeFilters) {
        const num = parseFloat(item[key]);
        const { minVal, maxVal } = rangeFilters[key];
        if (num < minVal || num > maxVal) return false;
      }
      return true;
    });

    currentPage = 1;
    displayStockData();
  }

  // === CSV Export / Import ===
  function exportCSV() {
    if (loggedInUserEmail !== "pmore711@gmail.com") return alert("Access denied!");
    let csv = [];
    const headers = Object.keys(stockData[0]);
    csv.push(headers.join(","));
    filteredData.forEach(row => {
      csv.push(headers.map(h => row[h]).join(","));
    });
    const csvContent = "data:text/csv;charset=utf-8," + csv.join("\n");
    const encodedUri = encodeURI(csvContent);
    const link = document.createElement("a");
    link.setAttribute("href", encodedUri);
    link.setAttribute("download", "stock_data.csv");
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  }

  function importCSV(event) {
    if (loggedInUserEmail !== "pmore711@gmail.com") return alert("Access denied!");
    const file = event.target.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = function(e) {
      const text = e.target.result;
      const lines = text.split("\n").filter(l => l.trim() !== "");
      const headers = lines[0].split(",");
      const newData = lines.slice(1).map(line => {
        const values = line.split(",");
        let obj = {};
        headers.forEach((h, i) => {
          obj[h] = isNaN(values[i]) ? values[i] : parseFloat(values[i]);
        });
        return obj;
      });
      stockData.length = 0;
      stockData.push(...newData);
      filteredData = stockData.slice();
      currentPage = 1;
      displayStockData();
      alert("CSV Imported successfully!");
    };
    reader.readAsText(file);
  }

  // === Initialize Filters and Show Signup by Default ===
  window.onload = () => {
    document.querySelectorAll("input.filter, .range-inputs input").forEach(inp => inp.addEventListener("input", applyFilters));
    showSignup();
  };
  </script>
</body>
</html>
