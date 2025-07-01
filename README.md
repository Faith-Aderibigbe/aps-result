<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aderibigbe Private School Result Checker</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      min-height: 100vh;
      background: linear-gradient(135deg, #667eea, #764ba2);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #fff;
      animation: fadeIn 2s ease;
    }

    .container {
      background: rgba(255, 255, 255, 0.1);
      padding: 30px 20px;
      border-radius: 40px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
      text-align: center;
      backdrop-filter: blur(10px);
      animation: slideIn 1.5s ease;
      position: relative;
      width: 90%;
      max-width: 400px;
    }

    .container::before {
      content: "";
      position: absolute;
      top: -5px;
      left: -5px;
      right: -5px;
      bottom: -5px;
      z-index: -1;
      background: linear-gradient(45deg, lightblue, darkblue, navy, royalblue, white, #d63384, lightblue);
      background-size: 400% 400%;
      border-radius: 45px;
      animation: borderAnimation 12s ease infinite;
    }

    @keyframes borderAnimation {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    h2 {
      margin-bottom: 20px;
      font-size: 22px;
    }

    input {
      padding: 12px 16px;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      width: 90%;
      max-width: 250px;
      margin-bottom: 20px;
      outline: none;
    }

    button {
      padding: 12px 24px;
      background-color: #4fd1c5;
      color: white;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    button:hover {
      background-color: #38b2ac;
    }

    .modal, .alert-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.8);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal-content {
      width: 95%;
      height: 95%;
      background-color: #fff;
      border-radius: 15px;
      overflow: hidden;
      position: relative;
    }

    .alert-content {
      width: 90%;
      max-width: 500px;
      background-color: #fff;
      border-radius: 15px;
      overflow: hidden;
      position: relative;
      padding: 20px;
      color: #000;
    }

    .modal iframe {
      width: 100%;
      height: 100%;
      border: none;
    }

    .close-btn {
      position: absolute;
      top: 10px;
      right: 20px;
      font-size: 24px;
      color: #000;
      cursor: pointer;
    }

    #loader {
      display: none;
      border: 6px solid #f3f3f3;
      border-top: 6px solid #4fd1c5;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    footer {
      margin-top: 30px;
      text-align: center;
      font-size: 14px;
      color: #ccc;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    @keyframes slideIn {
      from { transform: translateY(-50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    @media (max-width: 480px) {
      h2 {
        font-size: 20px;
      }
      input, button {
        font-size: 14px;
      }
      .modal-content {
        width: 100%;
        height: 100%;
        border-radius: 0;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Aderibigbe Private School Result Checker</h2>
    <input type="text" id="recordId" placeholder="e.g. recAbc1234">
    <br>
    <button onclick="goToResult()">View Result</button>
    <div id="loader"></div>
  </div>

  <div class="modal" id="resultModal">
    <div class="modal-content">
      <span class="close-btn" onclick="closeModal()">&times;</span>
      <iframe id="resultFrame"></iframe>
    </div>
  </div>

  <div class="alert-modal" id="alertModal">
    <div class="alert-content">
      <span class="close-btn" onclick="closeAlert()">&times;</span>
      <p><strong>Note:</strong> You are about to view results for 2nd Term, 2024/2025 Academic Session.</p>
      <br>
      <button onclick="proceedToResult()">Proceed</button>
    </div>
  </div>

  <footer>
    &copy; 2025 Aderibigbe Private School. All rights reserved.<br>
    Contact: 08147090653 | aderibigbeprivateschoolbot@gmail.com
  </footer>

  <script>
    function goToResult() {
      const id = document.getElementById("recordId").value.trim();
      if (id !== "") {
        sessionStorage.setItem('recordId', id);
        document.getElementById("alertModal").style.display = "flex";
      } else {
        alert("Please enter a valid Record ID.");
      }
    }

    function proceedToResult() {
      const id = sessionStorage.getItem('recordId');
      if (!id) return;

      document.getElementById("alertModal").style.display = "none";
      document.getElementById("loader").style.display = "block";

      setTimeout(() => {
        const url = "https://aps-result-portal.softr.app/student/result/request?recordId=" + encodeURIComponent(id);
        document.getElementById("resultFrame").src = url;
        document.getElementById("resultModal").style.display = "flex";
        document.getElementById("loader").style.display = "none";
      }, 1500);
    }

    function closeModal() {
      document.getElementById("resultModal").style.display = "none";
      document.getElementById("resultFrame").src = "";
    }

    function closeAlert() {
      document.getElementById("alertModal").style.display = "none";
    }
  </script>
</body>
</html>
