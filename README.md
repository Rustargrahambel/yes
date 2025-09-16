
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>To Lily, With All My Heart</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Roboto:wght@300;400&display=swap" rel="stylesheet" />
  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
  <style>
    body {
      margin: 0;
      height: 100vh;
      background: linear-gradient(135deg, #ffe6f0, #cceeff);
      font-family: 'Roboto', sans-serif;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
    }

    h1 {
      font-family: 'Great Vibes', cursive;
      font-size: 4em;
      color: #ff3366;
      margin-bottom: 10px;
      text-shadow: 2px 2px #fff;
    }

    .typewriter {
      font-size: 1.5em;
      color: #333;
      margin-bottom: 40px;
      height: 80px;
    }

    .heart-wrapper {
      width: 200px;
      height: 200px;
      transform-style: preserve-3d;
      perspective: 1000px;
      cursor: pointer;
      margin-bottom: 20px;
    }

    .heart-svg {
      width: 100%;
      height: 100%;
      transition: transform 0.2s ease;
      filter: drop-shadow(0 0 10px #ff3366);
    }

    .label {
      font-size: 1.2em;
      color: #333;
      margin-top: 10px;
    }

    .btn-love {
      background: linear-gradient(to right, #ff3366, #ff6f91);
      color: white;
      border: none;
      padding: 14px 32px;
      font-size: 1.2em;
      border-radius: 40px;
      box-shadow: 0 8px 16px rgba(255, 51, 102, 0.4);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      font-weight: bold;
      letter-spacing: 1px;
    }

    .btn-love:hover {
      transform: scale(1.08);
      box-shadow: 0 12px 24px rgba(255, 51, 102, 0.6);
    }
  </style>
</head>
<body>

  <h1>To Lily 💖</h1>
  <div class="typewriter" id="typewriter"></div>

  <div class="heart-wrapper" onclick="openModal()">
    <svg class="heart-svg" viewBox="0 0 32 29.6">
      <path fill="#ff3366" d="M23.6,0c-3.4,0-6.4,2.1-7.6,5.1C14.8,2.1,11.8,0,8.4,0C3.8,0,0,3.8,0,8.4c0,4.5,3.4,8.2,8.5,13.1
        c2.4,2.2,5.1,4.5,7.5,6.5c2.4-2,5.1-4.3,7.5-6.5C28.6,16.6,32,13,32,8.4C32,3.8,28.2,0,23.6,0z"/>
    </svg>
    <div class="label btn text-light " style="background-color: #ff3366;">Your answer click here please 💌</div>
  </div>

  <!-- Modal for Love Response -->
  <div class="modal fade" id="loveResponseModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content" style="background-color: #fff0f5;">
        <div class="modal-header">
          <h5 class="modal-title">Your Answer, Lily 💌</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
        </div>
        <div class="modal-body text-center">
          <p>Will you be mine forever?</p>
          <button class="btn-love" onclick="sendEmail('Yes 💘')">Yes 💘</button>
          <button class="btn-love" style="background-color:#999;" onclick="askWhy()">No 💔</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal for Rejection Reason -->
  <div class="modal fade" id="whyModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content" style="background-color: #ffe4e1;">
        <div class="modal-header">
          <h5 class="modal-title">Oh no... 😢</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
        </div>
        <div class="modal-body">
          <p>Please share why you rejected Ruster:</p>
          <textarea id="rejectionReason" class="form-control" rows="3"></textarea>
        </div>
        <div class="modal-footer">
          <button class="btn-love" onclick="sendEmail('No 💔')">Send</button>
        </div>
      </div>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

  <script>
    const text = "Every heartbeat whispers your name... Every moment longs for you...";
    let i = 0;
    function typeWriter() {
      if (i < text.length) {
        document.getElementById("typewriter").innerHTML += text.charAt(i);
        i++;
        setTimeout(typeWriter, 100);
      }
    }
    typeWriter();

    document.addEventListener('mousemove', (e) => {
      const x = e.clientX / window.innerWidth - 0.5;
      const y = e.clientY / window.innerHeight - 0.5;
      document.querySelector('.heart-svg').style.transform = `rotateX(${y * 30}deg) rotateY(${x * 30}deg)`;
    });

    document.addEventListener('touchmove', (e) => {
      const touch = e.touches[0];
      const x = touch.clientX / window.innerWidth - 0.5;
      const y = touch.clientY / window.innerHeight - 0.5;
      document.querySelector('.heart-svg').style.transform = `rotateX(${y * 30}deg) rotateY(${x * 30}deg)`;
    });

    function openModal() {
      new bootstrap.Modal(document.getElementById('loveResponseModal')).show();
    }

    function askWhy() {
      bootstrap.Modal.getInstance(document.getElementById('loveResponseModal')).hide();
      new bootstrap.Modal(document.getElementById('whyModal')).show();
    }

    function sendEmail(answer) {
      const reason = document.getElementById('rejectionReason')?.value || '';
      const message = answer === 'Yes 💘'
        ? 'Lily said YES! 💖'
        : `Lily said NO 💔. Reason: ${reason}`;

      emailjs.init("6v_L71Drr1lGRW9TF");

      emailjs.send("service_0gdkdll", "template_qbal6di", {
        name: "Lily",
        email: "no-reply@love.com",
        message: message
      }).then(() => {
        alert("✅ Message sent to Ruster's Gmail!");
      }, (error) => {
        alert("❌ Error: " + error.text);
      });

      bootstrap.Modal.getInstance(document.getElementById('whyModal'))?.hide();
      bootstrap.Modal.getInstance(document.getElementById('loveResponseModal'))?.hide();
    }
  </script>

</body>
