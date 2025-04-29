# The-billion-dollar-game
It is a game where you can spend a billion dollar
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How Many Things You Can Buy With a Billion Dollars</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
      color: #333;
    }
    h1 {
      text-align: center;
    }
    .balance {
      font-size: 1.5em;
      text-align: center;
      margin-bottom: 20px;
    }
    .item {
      display: flex;
      align-items: center;
      background: white;
      padding: 10px;
      margin: 10px 0;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }
    .item img {
      width: 100px;
      margin-right: 20px;
    }
    .item input {
      width: 60px;
      margin-left: 10px;
    }
    .summary {
      text-align: center;
      margin-top: 30px;
      font-size: 1.2em;
    }
    button {
      padding: 10px 20px;
      font-size: 1em;
      margin-top: 20px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>How Many Things You Can Buy With a Billion Dollars</h1>
  <div class="balance">Remaining Balance: $<span id="balance">1,000,000,000</span></div>

  <div id="items"></div>

  <div class="summary" id="summary"></div>
  <div style="text-align:center">
    <button onclick="resetGame()">Reset</button>
  </div>

  <script>
    const billion = 1000000000;
    let itemsData = [
      { name: "Big Mac", price: 5, image: "https://via.placeholder.com/100?text=Big+Mac" },
      { name: "iPhone 15", price: 999, image: "https://via.placeholder.com/100?text=iPhone" },
      { name: "Tesla Model 3", price: 40000, image: "https://via.placeholder.com/100?text=Tesla" },
      { name: "Private Jet", price: 20000000, image: "https://via.placeholder.com/100?text=Jet" },
      { name: "Yacht", price: 7500000, image: "https://via.placeholder.com/100?text=Yacht" },
      { name: "NBA Team", price: 2500000000, image: "https://via.placeholder.com/100?text=NBA" }
    ];

    function formatNumber(num) {
      return num.toLocaleString("en-US");
    }

    function createItems() {
      const container = document.getElementById("items");
      container.innerHTML = "";
      itemsData.forEach((item, index) => {
        const div = document.createElement("div");
        div.className = "item";
        div.innerHTML = `
          <img src="${item.image}" alt="${item.name}">
          <div>
            <strong>${item.name}</strong><br>
            Price: $${formatNumber(item.price)}<br>
            Quantity: <input type="number" min="0" value="0" onchange="updateBalance()" data-index="${index}">
          </div>
        `;
        container.appendChild(div);
      });
    }

    function updateBalance() {
      let total = 0;
      document.querySelectorAll("input[type='number']").forEach(input => {
        const index = parseInt(input.dataset.index);
        const quantity = parseInt(input.value) || 0;
        total += itemsData[index].price * quantity;
      });
      const remaining = billion - total;
      document.getElementById("balance").textContent = formatNumber(Math.max(0, remaining));

      const summary = document.getElementById("summary");
      if (remaining === 0) {
        summary.textContent = "Perfect! You spent exactly $1 billion!";
      } else if (remaining < 0) {
        summary.textContent = "Oops! You went over budget.";
      } else {
        summary.textContent = "You still have money left to spend!";
      }
    }

    function resetGame() {
      document.querySelectorAll("input[type='number']").forEach(input => input.value = 0);
      updateBalance();
    }

    createItems();
    updateBalance();
  </script>
</body>
</html>


The interactive browser game is ready! It includes a fun interface where users can pick quantities of real-world items to try and spend exactly $1 billion.

Would you like me to help you publish it online (e.g., on GitHub Pages or another platform)?

