<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OTC Signal Sender</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f2f5;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 500px;
            margin: 60px auto;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            margin-bottom: 30px;
        }
        label {
            display: block;
            margin-bottom: 10px;
        }
        select, input, button {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 8px;
        }
        button {
            background: #28a745;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }
        button:hover {
            background: #218838;
        }
        .status {
            text-align: center;
            margin-top: 15px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>OTC Signal Sender</h2>
        <label for="pair">Select Pair:</label>
        <select id="pair">
            <option>EUR/USD (OTC)</option>
            <option>GBP/USD (OTC)</option>
            <option>USD/JPY (OTC)</option>
            <option>EUR/JPY (OTC)</option>
            <option>GBP/JPY (OTC)</option>
            <option>EUR/CAD (OTC)</option>
            <option>AUD/USD (OTC)</option>
        </select>

        <label for="duration">Duration (minutes):</label>
        <input type="number" id="duration" value="1" min="1" max="5">

        <button onclick="sendSignal()">Send Signal</button>

        <div class="status" id="status"></div>
    </div>

    <script>
        function autoDirection() {
            // Dummy logic for auto direction (Up or Down)
            return Math.random() > 0.5 ? "Call (Up)" : "Put (Down)";
        }

        function sendSignal() {
            const pair = document.getElementById("pair").value;
            const duration = document.getElementById("duration").value;
            const direction = autoDirection();

            const message = OTC Trade Signal:\nPair: ${pair}\nDirection: ${direction}\nDuration: ${duration} minute(s);

            const botToken = "7775024284:AAHl_MFURKlIrpyiG42rnemz13U3pHk8o8s";
            const chatId = "6382500535";
            const url = https://api.telegram.org/bot${botToken}/sendMessage;

            fetch(url, {
                method: 'POST',
                headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                body: chat_id=${chatId}&text=${encodeURIComponent(message)}
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById("status").innerText = data.ok ? "Signal sent successfully!" : "Failed to send signal.";
            })
            .catch(error => {
                document.getElementById("status").innerText = "Error sending signal.";
            });
        }
    </script>
</body>
</html>
