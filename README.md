# BURME-LAN-HOK-TOKEN-SHOP
const packages = [
  { tokens: "80 Tokens", price: "2,500 MMK" },
  { tokens: "240 Tokens", price: "7,000 MMK" },
  { tokens: "500 Tokens", price: "14,000 MMK" },
  { tokens: "1,000 Tokens", price: "27,000 MMK" },
  { tokens: "2,500 Tokens", price: "65,000 MMK" },
  { tokens: "5,000 Tokens", price: "125,000 MMK" }
];

let selectedPackage = null;
let payment = null;

const box = document.getElementById("packages");

packages.forEach((p, i) => {
  box.innerHTML += `
    <div class="pkg">
      <strong>${p.tokens}</strong>
      <small>${p.price}</small>
      <button onclick="choosePackage(${i})">Select</button>
    </div>
  `;
});

function choosePackage(i) {
  selectedPackage = packages[i];

  document.getElementById("selected").textContent =
    `${selectedPackage.tokens} — ${selectedPackage.price}`;

  document.querySelector(".order-card").scrollIntoView({
    behavior: "smooth"
  });
}

function selectPayment(el) {
  document.querySelectorAll(".pay").forEach(x => {
    x.classList.remove("active");
  });

  el.classList.add("active");
  payment = el.dataset.method;
}

function placeOrder() {
  const id = document.getElementById("gameId").value.trim();
  const msg = document.getElementById("message");

  if (!id) {
    msg.textContent = "Please enter your HoK Game ID.";
    return;
  }

  if (!selectedPackage) {
    msg.textContent = "Please select a token package.";
    return;
  }

  if (!payment) {
    msg.textContent = "Please select a payment method.";
    return;
  }

  msg.textContent =
    `Order ready: ${selectedPackage.tokens} via ${payment}.`;
}

function openChat() {
  document.getElementById("chat").classList.remove("hidden");
}

function closeChat() {
  document.getElementById("chat").classList.add("hidden");
}

function sendMessage() {
  const input = document.getElementById("chatText");
  const text = input.value.trim();

  if (!text) return;

  const body = document.getElementById("chatBody");

  body.innerHTML += `
    <div class="bubble me">${text.replace(/</g, "&lt;")}</div>
  `;

  input.value = "";
  body.scrollTop = body.scrollHeight;
}
