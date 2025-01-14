<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام استعلام درجات الطلاب</title>
</head>
<body>
    <div class="container">
        <h1>نظام استعلام درجات الطلاب</h1>
        <input type="number" id="studentNumber" placeholder="أدخل رقم الطالب">
        <button onclick="lookupGrades()">استعلام عن الدرجات</button>
        <div id="Grades"></div>
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
            const studentNumber = document.getElementById('number').value;
            const Grades = document.getElementById('Grades');
            if (studentGrades[number]) {
                Grades.textContent = studentGrades[number].Grades;
            } else {
                Grades.textContent = "لم يتم العثور على درجات لهذا الرقم الطالبي.";
            }
        }
    </script>
</body>
</html>
