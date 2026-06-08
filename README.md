<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Student Feedback Portal</title>

<style>
    *{
        margin:0;
        padding:0;
        box-sizing:border-box;
        font-family:Times New Roman, sans-serif;
    }

   
    body{
        background: #800000
        
        
    }

    header{
        background:#FFFF00;
        color:black;
        text-align:center;
        padding:20px;
        
    }

    .container{
        width:90%;
        max-width:900px;
        margin:30px auto;
    }

    .card{
        background:white;
        padding:25px;
        border-radius:10px;
        box-shadow:0 3px 10px rgba(0,0,0,0.1);
        margin-bottom:20px;
    }

    h2{
        color:#000000;
        margin-bottom:15px;
    }

    label{
        display:block;
        margin-top:12px;
        font-weight:bold;
    }

    input,
    select,
    textarea{
        width:100%;
        padding:10px;
        margin-top:5px;
        border:1px solid #ccc;
        border-radius:5px;
    }

    textarea{
        resize:vertical;
    }

    button{
        background:#000000;
        color:white;
        border:none;
        padding:12px 20px;
        margin-top:20px;
        border-radius:5px;
        cursor:pointer;
    }

    button:hover{
        background:#002b57;
    }

    .feedback-item{
        border-left:5px solid #004080;
        padding:15px;
        margin-bottom:15px;
        background:#fafafa;
    }

    .feedback-item h3{
        color:#004080;
    }

    .feedback-item small{
        color:gray;
    }

    footer{
        background:#FFFF00;
        color:black;
        text-align:center;
        padding:15px;
        margin-top:30px;
    }
</style>
</head>
<body>

<header>
    <h1>Student Feedback Portal</h1>
    <p>Share your thoughts about your school and staff members.</p>
</header>

<div class="container">

    <div class="card">

        <h2>Submit Feedback</h2>

        <form id="feedbackForm">

            <label>Student Name</label>
            <input type="text" id="studentName" required>

            <label>Student ID</label>
            <input type="text" id="studentID" required>

            <label> Age</label>
            <input type="text" id="age" required>

            <label> Hometown</label>
            <input type="text" id="place" required>

            <label>Grade / Course</label>
            <input type="text" id="course" required>

            <label>Select School</label>
            <select id="school" required>
                <option value="">Choose a School</option>
                <option> Polytechnic University of the Philippines (Unisan Campus) </option>
                <option> Polytechnic University of the Philippines (Lopez Campus)</option>
                <option> Polytechnic University of the Philippines (Sta. Mesa Main Campus)</option>
                <option> Unisan Integrated High School</option>
                <option> Lopez National Comprehensive High School</option> 
                <option> Dulong Bayan Elementary School<option>
                <option> Amontay National High School</option>  
                <option> Pitogo Cental School 1</option>
                <option> Pitogo Central School 2</option>
                <option> Amontay Elementary School <option>
                <option> Pitogo Community High School</option>  
                <option> Caigdal National High School</option>
                <option> Unisan Central Elementary School</option>
                <option> South Luzon State University (Lucban Main Campus)</option>
                <option> South Luzon State University (Gumaca Branch)</option>
                <option> Abuyon National High School </option>
                <option> Cabulihan National High School</option>
                <option> Poctol Elementary School</option>
                <option> Rizalino Elementary School</option>
                <option> Gumaca National High School</option>

            </select>

            <label>Feedback About</label>
            <select id="target" required>
                <option value="">Choose One</option>
                <option>School Administration</option>
                <option>Teacher</option>
                <option>Guidance Office</option>
                <option>Registrar</option>
                <option>Library Staff</option>
                <option>Security Personnel</option>
                <option>Facilities</option>
                <option> Co Students</option>
                <option> Utility Personnel</option>
            </select>

            <label>Staff Name (Optional)</label>
            <input type="text" id="staffName">

            <label>Rating</label>
            <select id="rating" required>
                <option value="">Choose Rating</option>
                <option>⭐⭐⭐⭐⭐ Excellent</option>
                <option>⭐⭐⭐⭐ Good</option>
                <option>⭐⭐⭐ Average</option>
                <option>⭐⭐ Poor</option>
                <option>⭐ Very Poor</option>
            </select>

            <label>Your Feedback</label>
            <textarea id="message" rows="5" required></textarea>

            <button type="submit">Submit Feedback</button>

        </form>

    </div>

    <div class="card">

        <h2>Recent Feedback</h2>

        <div id="feedbackList">
            <p>No feedback submitted yet.</p>
        </div>
 
    </div style="background-image: linear-gradient(to right, #add8e6, #e6e6fa); height; 200px, width; 100%;">
        <!-- Your content goes here -->

</div>

<footer>
<f1> @2026 Student Feedback Portal </f1>
<p>  prepared by: Andrei O. Trinidad</p>
</footer>


<script>

const form = document.getElementById("feedbackForm");
const feedbackList = document.getElementById("feedbackList");

loadFeedback();

form.addEventListener("submit", function(e){

    e.preventDefault();

    const feedback = {
        studentName: document.getElementById("studentName").value,
        studentID: document.getElementById("studentID").value,
        course: document.getElementById("course").value,
        school: document.getElementById("school").value,
        target: document.getElementById("target").value,
        staffName: document.getElementById("staffName").value,
        rating: document.getElementById("rating").value,
        message: document.getElementById("message").value,
        date: new Date().toLocaleString()
    };

    let feedbacks =
        JSON.parse(localStorage.getItem("feedbacks")) || [];

    feedbacks.unshift(feedback);

    localStorage.setItem(
        "feedbacks",
        JSON.stringify(feedbacks)
    );

    form.reset();

    loadFeedback();

    alert("Feedback submitted successfully!");
});

function loadFeedback(){

    const feedbacks =
        JSON.parse(localStorage.getItem("feedbacks")) || [];

    feedbackList.innerHTML = "";

    if(feedbacks.length === 0){
        feedbackList.innerHTML =
        "<p>No feedback submitted yet.</p>";
        return;
    }

    feedbacks.forEach(item => {

        feedbackList.innerHTML += `
        <div class="feedback-item">
            <h3>${item.studentName}</h3>

            <p><strong>School:</strong> ${item.school}</p>

            <p><strong>Grade/Course:</strong> ${item.course}</p>

            <p><strong>Feedback About:</strong> ${item.target}</p>

            <p><strong>Staff Name:</strong> ${item.staffName || "N/A"}</p>

            <p><strong>Rating:</strong> ${item.rating}</p>

            <p>${item.message}</p>

            <small>${item.date}</small>
        </div>
        `;
    });
}

</script>

</body>
</html>
