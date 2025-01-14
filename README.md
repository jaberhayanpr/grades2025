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
        label, input, button {
            font-size: 16px;
            margin: 10px 0;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 20px;
        }
        table {
            border-collapse: collapse;
            width: 100%;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>Student Grades Lookup</h1>
    <label for="studentNumber">Enter Student Number:</label>
    <input type="text" id="studentNumber">
    <button onclick="showGrades()">Show Grades</button>
    <div id="result"></div>

<script>
        const studentData = {
            "150805039": {
                "name": "احمد حسين محمد جميل يوسف",
                "class": "4ب1",
                "grades": {
                    "التربية الإسلامية": "-",
                    "اللغة العربية": "17",
                    "اللغة الانجليزية": "11",
                    "الرياضيات": "18",
                    "العلوم": "17.5",
                    "الاجتماعيات": "19",
                    "التربية للمواطنة": "17"
                }
            },
            "150910568": {
                "name": "احمد صالح محمد شهاب",
                "class": "4ب1",
                "grades": {
                    "التربية الإسلامية": "-",
                    "اللغة العربية": "19",
                    "اللغة الانجليزية": "19",
                    "الرياضيات": "18",
                    "العلوم": "20",
                    "الاجتماعيات": "20",
                    "التربية للمواطنة": "20"
                }
            }
        };

        function showGrades() {
            const studentNumber = document.getElementById('studentNumber').value;
            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = '';

            if (studentData[studentNumber]) {
                const student = studentData[studentNumber];
                let gradesHtml = `<h2>Student: ${student.name}</h2>`;
                gradesHtml += `<p>Class: ${student.class}</p>`;
                gradesHtml += '<table><tr><th>Subject</th><th>Grade</th></tr>';
                for (const [subject, grade] of Object.entries(student.grades)) {
                    gradesHtml += `<tr><td>${subject}</td><td>${grade}</td></tr>`;
                }
                gradesHtml += '</table>';
                resultDiv.innerHTML = gradesHtml;
            } else {
                resultDiv.innerHTML = '<p>Student not found.</p>';
            }
        }
    </script>
</body>
</html>
