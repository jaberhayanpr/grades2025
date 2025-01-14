<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام استعلام درجات الطلاب</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 20px;
            white-space: pre-wrap;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>نظام استعلام درجات الطلاب</h1>
        <input type="number" id="studentNumber" placeholder="أدخل رقم الطالب">
        <button onclick="lookupGrades()">استعلام عن الدرجات</button>
        <div id="result"></div>
    </div>

    <script>
        let studentGrades = {};

        fetch('student_data.json')
            .then(response => response.json())
            .then(data => {
                studentGrades = data;
            })
            .catch(error => console.error('Error loading student data:', error));

        function lookupGrades() {
            const studentNumber = document.getElementById('studentNumber').value;
            const result = document.getElementById('result');
            if (studentGrades[studentNumber]) {
                result.textContent = studentGrades[studentNumber].Grades;
            } else {
                result.textContent = "لم يتم العثور على درجات لهذا الرقم الطالبي.";
            }
        }
    </script>
</body>
</html>
