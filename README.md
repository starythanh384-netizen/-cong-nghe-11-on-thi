<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <title>Luyện thi Công nghệ 11</title>
  <style>
    body { font-family: Arial, sans-serif; background:#f4f6f8; }
    .container { max-width: 800px; margin: 20px auto; background:#fff; padding:20px; border-radius:8px; box-shadow:0 2px 8px rgba(0,0,0,0.1);}    
    h1, h2 { text-align:center; }
    .question { margin-bottom: 15px; }
    button { padding:10px 20px; font-size:16px; cursor:pointer; margin-top:10px }
    .result { margin-top:20px; font-weight:bold; }
    #timer { font-weight:bold; color:#d9534f; text-align:center; margin-bottom:15px }
  </style>
</head>
<body>
  <div class="container">
    <h1>Luyện thi Công nghệ 11</h1>

    <label><b>Chọn chuyên đề:</b></label>
    <select id="topic" onchange="loadQuiz()">
      <option value="789">Bài 7–8–9</option>
      <option value="11">Bài 11</option>
      <option value="12">Bài 12</option>
      <option value="13">Bài 13</option>
    </select>

    <div id="timer">⏱ Thời gian: 10:00</div>

    <form id="quiz"></form>

    <button onclick="submitQuiz()">Nộp bài</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    let time = 600; // 10 phút
    let timer;

    const quizzes = {
      "789": [
        {q:"Phương pháp thuộc nhóm chế tạo phôi là?", a:["Phay","Đúc","Lắp ráp","Đóng gói"], correct:1},
        {q:"Đặc điểm dây chuyền tự động mềm là?", a:["Độ linh hoạt cao","Độ ổn định thấp","Chi phí thấp","Năng suất thấp"], correct:0}
      ],
      "11": [
        {q:"Bước đầu của sản xuất cơ khí là?", a:["Gia công","Chế tạo phôi","Nghiên cứu bản vẽ","Đóng gói"], correct:2}
      ],
      "12": [
        {q:"Vai trò của robot công nghiệp là?", a:["Tăng năng suất","Giảm an toàn","Tăng lao động tay chân","Không linh hoạt"], correct:0}
      ],
      "13": [
        {q:"Công nghệ giúp ra quyết định thông minh là?", a:["IoT","Big Data","AI","In 3D"], correct:2}
      ]
    };

    function startTimer() {
      clearInterval(timer);
      time = 600;
      timer = setInterval(() => {
        let min = Math.floor(time / 60);
        let sec = time % 60;
        document.getElementById('timer').innerText = `⏱ Thời gian: ${min}:${sec.toString().padStart(2,'0')}`;
        time--;
        if (time < 0) {
          clearInterval(timer);
          submitQuiz();
        }
      }, 1000);
    }

    function loadQuiz() {
      startTimer();
      const topic = document.getElementById('topic').value;
      const quizDiv = document.getElementById('quiz');
      quizDiv.innerHTML = '';

      quizzes[topic].forEach((item, index) => {
        let html = `<div class='question'><p><b>Câu ${index+1}:</b> ${item.q}</p>`;
        item.a.forEach((opt, i) => {
          html += `<label><input type='radio' name='q${index}' value='${i}'> ${opt}</label><br>`;
        });
        html += '</div>';
        quizDiv.innerHTML += html;
      });
    }

    function submitQuiz() {
      clearInterval(timer);
      const topic = document.getElementById('topic').value;
      let score = 0;
      quizzes[topic].forEach((item, index) => {
        const checked = document.querySelector(`input[name='q${index}']:checked`);
        if (checked && parseInt(checked.value) === item.correct) score++;
      });
      document.getElementById('result').innerText = `✔ Kết quả: ${score}/${quizzes[topic].length} câu đúng`;
    }

    loadQuiz();
  </script>
</body>
</html>
