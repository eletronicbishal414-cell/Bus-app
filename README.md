<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bus Service App</title>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: #f4f4f4;
}

header {
  background: #007bff;
  color: white;
  padding: 15px;
  text-align: center;
  font-size: 20px;
}

.container {
  padding: 20px;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  font-size: 16px;
}

.bus-card {
  background: white;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
}

.loading, .no-data {
  text-align: center;
  font-size: 18px;
}
</style>

</head>
<body>

<header>🚌 Bus Service App</header>

<div class="container">
  <input type="text" id="search" placeholder="Search bus or route...">

  <div id="loading" class="loading">Loading...</div>
  <div id="busList"></div>
</div>

<script>
// Fake JSON Data (future এ আলাদা file করতে পারবে)
const buses = [
  { name: "Kandra Express", route: "Kandra to Siliguri", time: "6:00 AM", fare: "₹150" },
  { name: "North Bengal Bus", route: "Siliguri to Kolkata", time: "8:00 AM", fare: "₹500" },
  { name: "City Rider", route: "Kandra to Durgapur", time: "10:00 AM", fare: "₹200" }
];

const busList = document.getElementById("busList");
const searchInput = document.getElementById("search");
const loading = document.getElementById("loading");

function displayBuses(data) {
  busList.innerHTML = "";

  if (data.length === 0) {
    busList.innerHTML = "<div class='no-data'>No bus found</div>";
    return;
  }

  data.forEach(bus => {
    busList.innerHTML += `
      <div class="bus-card">
        <h3>${bus.name}</h3>
        <p><strong>Route:</strong> ${bus.route}</p>
        <p><strong>Time:</strong> ${bus.time}</p>
        <p><strong>Fare:</strong> ${bus.fare}</p>
      </div>
    `;
  });
}

// Simulate loading
setTimeout(() => {
  loading.style.display = "none";
  displayBuses(buses);
}, 1000);

// Search
searchInput.addEventListener("input", () => {
  const value = searchInput.value.toLowerCase();
  const filtered = buses.filter(bus =>
    bus.name.toLowerCase().includes(value) ||
    bus.route.toLowerCase().includes(value)
  );
  displayBuses(filtered);
});
</script>

</body>
</html>
