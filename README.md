# PERSONAL-PORTFOLIO
# PROJECT STRUCTURE
portfolio-website/
│
├── index.html
├── style.css
├── script.js
├── images/
│   └── profile.jpg
└── backend/
    ├── app.py
    └── database.db

# FRONTED(index.html)
<!DOCTYPE html>
<html>
<head>
    <title>Braj Kishor Portfolio</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<header>
    <h1>Braj Kishor Das</h1>
    <p>Future Data Scientist | Author | Developer</p>
</header>

<section>
    <h2>About Me</h2>
    <p>I am passionate about Data Science, AI, Writing, and Web Development.</p>
</section>

<section>
    <h2>Projects</h2>

    <div class="project">
        <h3>School Management System</h3>
        <p>Python + MySQL Project</p>
    </div>

    <div class="project">
        <h3>Pharmacy Management System</h3>
        <p>Python + MySQL Project</p>
    </div>
</section>

<section>
    <h2>Contact</h2>

    <form id="contactForm">
        <input type="text" id="name" placeholder="Your Name"><br><br>
        <input type="email" id="email" placeholder="Your Email"><br><br>
        <textarea id="message" placeholder="Message"></textarea><br><br>
        <button type="submit">Send</button>
    </form>
</section>

<script src="script.js"></script>

</body>
</html>

# CSS(style.css)
body{
    font-family: Arial;
    margin:0;
    background:#f4f4f4;
}

header{
    background:#007bff;
    color:white;
    text-align:center;
    padding:30px;
}

section{
    background:white;
    margin:20px;
    padding:20px;
    border-radius:10px;
}

.project{
    border:1px solid #ddd;
    padding:10px;
    margin:10px;
}
button{
    background:#007bff;
    color:white;
    padding:10px 20px;
    border:none;
}

# JavaScript (script.js)
document.getElementById("contactForm").addEventListener("submit", function(e){
    e.preventDefault();

    alert("Message Sent Successfully!");
});

# Backend (Flask)
pip install flask

add.py
from flask import Flask, request, jsonify
import sqlite3

app = Flask(__name__)

@app.route('/contact', methods=['POST'])
def contact():
    data = request.json

    conn = sqlite3.connect('database.db')
    c = conn.cursor()

    c.execute('''
    CREATE TABLE IF NOT EXISTS contacts(
        id INTEGER PRIMARY KEY,
        name TEXT,
        email TEXT,
        message TEXT
    )
    ''')

    c.execute(
        "INSERT INTO contacts(name,email,message) VALUES(?,?,?)",
        (data['name'], data['email'], data['message'])
    )

    conn.commit()
    conn.close()

    return jsonify({"message":"Saved Successfully"})

if __name__ == '__main__':
    app.run(debug=True)


    
