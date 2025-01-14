<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نتائج الطلاب</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            margin: auto;
            background: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .student {
            background: #f9f9f9;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 5px;
        }
        .student h2 {
            color: #444;
            margin-top: 0;
        }
        .grades {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
        }
        .grade {
            background: #eee;
            padding: 10px;
            border-radius: 3px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>نتائج الطلاب</h1>
        <div id="students"></div>
    </div>
<script>
        // Function to fetch and display student data
        async function displayStudentData() {
            try {
                const response = await fetch('student_data.json');
                const data = await response.json();
                const studentsContainer = document.getElementById('students');
                data.forEach(entry => {
                    for (const [key, value] of Object.entries(entry)) {
                        if (typeof value === 'string' && value.includes('درجات الطالب')) {
                            const studentDiv = document.createElement('div');
                            studentDiv.className = 'student'; 
                            const nameMatch = value.match(/درجات الطالب: (.+?) المقيد/);
                            const name = nameMatch ? nameMatch[1] : 'اسم غير معروف';                    
                            studentDiv.innerHTML = `
                                <h2>${name}</h2>
                                <div class="grades">
                                    ${parseGrades(value)}
                                </div>
                            `;
                            studentsContainer.appendChild(studentDiv);
                        }
                    }
                });
            } catch (error) {
                console.error('Error fetching or parsing data:', error);
            }
        }
        // Function to parse and format grades
        function parseGrades(gradeString) {
            const gradeMatches = gradeString.match(/[^،]+: \([^)]+\)/g);
            return gradeMatches ? gradeMatches.map(grade => {
                const [subject, score] = grade.split(': ');
                return `<div class="grade"><strong>${subject}:</strong> ${score}</div>`;
            }).join('') : 'لا توجد درجات متاحة';
        }
        // Call the function to display data when the page loads
        window.onload = displayStudentData;
    </script>
</body>
</html>
