<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام استعلام درجات الطلاب</title>
    <style>
        /* Your existing CSS styles here */
    </style>
</head>
<body>
    <div class="container">
        <h1>نظام استعلام درجات الطلاب</h1>
        <input type="number" id="number" placeholder="أدخل رقم الطالب">
        <button onclick="lookupGrades()">استعلام عن الدرجات</button>
        <div id="Grades"></div>
    </div>

    <script>
        let studentGrades = {};

        // Load the JSON data when the page loads
        fetch('student_data.json')
            .then(response => response.json())
            .then(data => {
                studentGrades = data;
            })
            .catch(error => console.error('Error loading student data:', error));

        function lookupGrades() {
            const studentNumber = document.getElementById('Number').value;
            const result = document.getElementById('Grades');
            if (studentGrades.hasOwnProperty(Number)) {
                result.textContent = studentGrades[Number];
            } else {
                result.textContent = "لم يتم العثور على درجات لهذا الرقم الطالبي.";
            }
        }
    </script>
</body>
</html>
