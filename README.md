<!DOCTYPE html>
<html>
<head>
  <title>Sky Dreamers – Live Dashboard</title>

  <!-- Firebase SDK v8 -->
  <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      padding: 20px;
    }
    h1 { color: #2c3e50; }
    pre {
      background: #fff;
      padding: 20px;
      border-radius: 6px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      max-height: 600px;
      overflow: auto;
    }
  </style>
</head>

<body>

<h1>📊 Sky Dreamers – Live Firebase Data</h1>
<p>Status: <span id="status">Connecting…</span></p>

<pre id="output">Waiting for data…</pre>

<script>
  const firebaseConfig = {
    databaseURL: "https://performance-dashboard-c7017-default-rtdb.firebaseio.com"
  };

  firebase.initializeApp(firebaseConfig);
  const db = firebase.database();

  db.ref("dashboard").on("value", snap => {
    const data = snap.val();
    if (!data) {
      document.getElementById("status").textContent = "No data found";
      return;
    }

    document.getElementById("status").textContent =
      "Live – Last updated: " + new Date(data.lastUpdated).toLocaleTimeString();

    document.getElementById("output").textContent =
      JSON.stringify(data, null, 2);
  });
</script>

</body>
</html>
