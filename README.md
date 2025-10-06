# budget-tracker-nini.glitch.me
Budget Tracker Web App to monitor income and expenses. Built with HTML, CSS, and JavaScript.
let expenses = [];
let total = 0;

// Load from localStorage if available
if(localStorage.getItem("expenses")) {
  expenses = JSON.parse(localStorage.getItem("expenses"));
  expenses.forEach(expense => addExpenseToDOM(expense));
  total = expenses.reduce((sum, exp) => sum + exp.amount, 0);
  document.getElementById("total").textContent = `Total: €${total}`;
}

document.getElementById("add").addEventListener("click", () => {
  const desc = document.getElementById("desc").value;
  const amount = parseFloat(document.getElementById("amount").value);

  if (!desc || !amount) return alert("Please fill in all fields!");

  const expense = { desc, amount };
  expenses.push(expense);
  total += amount;

  addExpenseToDOM(expense);
  document.getElementById("total").textContent = `Total: €${total}`;

  // Save to localStorage
  localStorage.setItem("expenses", JSON.stringify(expenses));

  document.getElementById("desc").value = "";
  document.getElementById("amount").value = "";
});

function addExpenseToDOM(expense) {
  const li = document.createElement("li");
  li.textContent = `${expense.desc}: €${expense.amount}`;
  document.getElementById("list").appendChild(li);
}
