# Event-Countdown-Timer
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Event Countdown Timer</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      padding: 20px;
      text-align: center;
    }

    h1 {
      margin-bottom: 20px;
    }

    input, button {
      padding: 10px;
      font-size: 16px;
      margin: 5px;
    }

    #countdown {
      font-size: 2rem;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Event Countdown Timer</h1>
  
  <input type="text" id="eventName" placeholder="Event Name" />
  <input type="datetime-local" id="eventDate" />
  <button onclick="startCountdown()">Start Countdown</button>

  <div id="output" style="margin-top: 20px; font-size: 1.2rem;"></div>
  <div id="countdown"></div>

  <script>
    let countdownInterval;

    function startCountdown() {
      clearInterval(countdownInterval); // Clear previous countdown if any

      const eventName = document.getElementById("eventName").value;
      const eventDate = new Date(document.getElementById("eventDate").value);
      const output = document.getElementById("output");
      const countdown = document.getElementById("countdown");

      if (!eventName || isNaN(eventDate)) {
        output.textContent = "Please enter a valid event name and date.";
        countdown.textContent = "";
        return;
      }

      output.textContent = `Countdown to ${eventName}:`;

      countdownInterval = setInterval(() => {
        const now = new Date();
        const diff = eventDate - now;

        if (diff <= 0) {
          clearInterval(countdownInterval);
          countdown.textContent = "🎉 The event has started!";
          return;
        }

        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
        const minutes = Math.floor((diff / (1000 * 60)) % 60);
        const seconds = Math.floor((diff / 1000) % 60);

        countdown.textContent = `${days}d ${hours}h ${minutes}m ${seconds}s`;
      }, 1000);
    }
  </script>
</body>
</html>
