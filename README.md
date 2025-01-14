<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Grades Lookup</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        #result {
            white-space: pre-wrap;
            background-color: #f0f0f0;
            padding: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>Student Grades Lookup</h1>
    <input type="file" id="jsonFile" accept=".json">
    <br><br>
    <input type="text" id="studentNumber" placeholder="Enter student number">
    <button onclick="lookupGrades()">Look up grades</button>
    <div id="result"></div>

<script>
        let studentData = {};

        document.getElementById('jsonFile').addEventListener('change', function(e) {
            const file = e.target.files[0];
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    studentData = JSON.parse(e.target.result);
                    alert('JSON file loaded successfully');
                } catch (error) {
                    alert('Error parsing JSON file');
                }
            };
            reader.readAsText(file);
        });

        function lookupGrades() {
            const studentNumber = document.getElementById('studentNumber').value;
            const resultDiv = document.getElementById('result');
            
            if (studentData[studentNumber]) {
                resultDiv.textContent = studentData[studentNumber].Grades;
            } else {
                resultDiv.textContent = 'Student not found';
            }
        }
    </script>
</body>
</html>
