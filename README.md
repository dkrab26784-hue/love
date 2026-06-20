<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>ง้อแฟน 💓</title>
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
  <style>
    body {
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      overflow: hidden;
      height: 100vh;
      margin: 0;
      font-family: "Prompt", sans-serif;
    }
    .falling-text {
      position: absolute;
      font-size: 20px;
      font-weight: bold;
      color: #ff3f6f;
      background: rgba(255,255,255,0.95);
      border-radius: 15px;
      padding: 8px 15px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      animation: fall 6s linear forwards;
      text-align: center;
      min-width: 120px;
    }
    @keyframes fall {
      0% { transform: translateY(-50px); opacity: 1; }
      100% { transform: translateY(100vh); opacity: 0; }
    }
    .buttons {
      position: fixed;
      bottom: 20px;
      width: 100%;
      text-align: center;
    }
    .btn {
      padding: 12px 25px;
      margin: 10px;
      border: none;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
      color: white;
      transition: all 0.3s ease;
    }
    .btn-yes {
      background: #ff6f91;
    }
    .btn-no {
      background: #555;
    }
    /* confetti */
    .confetti {
      position: fixed;
      width: 10px;
      height: 10px;
      background-color: red;
      animation: confetti-fall 2s linear forwards;
    }
    @keyframes confetti-fall {
      0% { transform: translateY(-10px) rotate(0deg); opacity: 1; }
      100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
    }
  </style>
</head>
<body>
  <div class="buttons">
    <button id="yesBtn" class="btn btn-yes" onclick="agree()">คืนดี 💖</button>
    <button id="noBtn" class="btn btn-no" onclick="disagree()">ไม่คืนดี 😢</button>
  </div>

  <script>
    const messages = [
      "เค้าขอโทดดดด 💕",
      "มาง้ออออ 🌹",
      "คืนดีกานนน 💖",
      "เค้ารักอ้วนที่สุดดดด 💘",
      "จะไม่ทำให้เสียใจอีกนะ 🌸",
      "อยู่ด้วยกันตลอดไปนะ 💞",
      "รักเธอที่สุดในโลก 🌎❤️"
    ];

    function createFallingText() {
      const text = document.createElement("div");
      text.className = "falling-text";
      text.innerText = messages[Math.floor(Math.random() * messages.length)];
      text.style.left = Math.random() * (window.innerWidth - 150) + "px";
      document.body.appendChild(text);

      setTimeout(() => {
        text.remove();
      }, 6000);
    }

    // ให้ข้อความตกลงมาต่อเนื่อง
    setInterval(createFallingText, 800);

    // เมื่อกดคืนดี → หน้าต่างดีใจ + confetti รอบๆ
    function agree() {
      Swal.fire({
        title: "🎉 ดีใจที่สุดเลย 💖",
        html: `
          <h2 style="color:#ff3f6f; font-size:26px; margin-bottom:10px;">
            รักเธอที่สุดในโลก 🌎❤️
          </h2>
          <p style="color:#ff6f91; font-size:20px;">
            อยู่ด้วยกันตลอดไปนะ 💞
          </p>
        `,
        background: "linear-gradient(135deg, #ffe0f0, #ffc2d1, #ff9a9e)",
        color: "#333",
        icon: "success",
        confirmButtonText: "รักนะ 💕",
        confirmButtonColor: "#ff3f6f"
      });

      // สร้าง confetti แตกกระจายรอบๆ popup
      for (let i = 0; i < 80; i++) {
        const confetti = document.createElement("div");
        confetti.className = "confetti";
        confetti.style.left = Math.random() * window.innerWidth + "px";
        confetti.style.top = Math.random() * window.innerHeight + "px";
        confetti.style.backgroundColor = randomColor();
        document.body.appendChild(confetti);

        setTimeout(() => confetti.remove(), 2000);
      }
    }

    function randomColor() {
      const colors = ["#ff6f91", "#ff3f6f", "#ffc2d1", "#ffe0f0", "#f9a825", "#4caf50", "#2196f3"];
      return colors[Math.floor(Math.random() * colors.length)];
    }

    // เมื่อกดไม่คืนดี → ปุ่มคืนดีใหญ่ขึ้นเรื่อยๆ
    function disagree() {
      const yesBtn = document.getElementById("yesBtn");
      let currentSize = parseInt(window.getComputedStyle(yesBtn).fontSize);
      let currentPadding = parseInt(window.getComputedStyle(yesBtn).padding);

      // ขยายปุ่มเร็วขึ้น
      yesBtn.style.fontSize = (currentSize + 20) + "px";
      yesBtn.style.padding = (currentPadding + 15) + "px " + (currentPadding + 40) + "px";

      // ถ้าใหญ่จนเต็มจอ → ปุ่มไม่คืนดีจะหายไป
      if (currentSize > 60) {
        document.getElementById("noBtn").style.display = "none";
        yesBtn.style.position = "fixed";
        yesBtn.style.top = "50%";
        yesBtn.style.left = "50%";
        yesBtn.style.transform = "translate(-50%, -50%)";
        yesBtn.style.width = "90%";
        yesBtn.style.height = "50%";
      }
    }
  </script>
</body>
</html>
