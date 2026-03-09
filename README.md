# Flask-Based Student Registration Web Application

## Project Overview

This project is a **Flask-based Student Registration Web Application** that allows users to submit student details through a web form and store the data in a **MySQL database**. The application also provides functionality to retrieve and display registered students.

The application demonstrates basic **full-stack development** using **HTML/CSS for frontend**, **Python Flask for backend**, and **MySQL for persistent data storage**. The project also integrates **GitHub for version control** and can be deployed using **Jenkins CI/CD pipeline** and optionally hosted on **AWS EC2**.

---

# Technology Stack

Frontend  
- HTML  
- CSS  

Backend  
- Python Flask  

Database  
- MySQL  

DevOps Tools  
- Git  
- GitHub  
- Jenkins  

Deployment (Optional)  
- AWS EC2

---

# Repository

Original Repository

```
https://github.com/swati-zampal/stud-reg-flask-app.git
```

Forked / Student Repository

```
https://github.com/vaishnavikadam1918
```

---

# Project Structure

```
stud-reg-flask-app
│
├── app.py
├── database.py
│
├── templates
│   ├── register.html
│   └── students.html
│
├── static
│   └── style.css
│
├── requirements.txt
└── README.md
```

---

# Application Workflow

1. User opens the **student registration form**
2. User fills details and submits the form
3. Flask backend processes the request
4. Data is stored in **MySQL database**
5. Users can view all registered students on a separate page

---

# Functional Requirements

## Registration Form

Fields included:

- Name
- Email
- Phone Number
- Course
- Address

The form includes:

- Client-side validation
- Server-side validation

---

# Flask Application Code

## app.py

```python
from flask import Flask, render_template, request, redirect
import mysql.connector

app = Flask(__name__)

db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="studentdb"
)

cursor = db.cursor()

@app.route('/')
def index():
    return render_template('register.html')

@app.route('/register', methods=['POST'])
def register():

    name = request.form['name']
    email = request.form['email']
    phone = request.form['phone']
    course = request.form['course']
    address = request.form['address']

    query = "INSERT INTO students (name,email,phone,course,address) VALUES (%s,%s,%s,%s,%s)"
    values = (name,email,phone,course,address)

    cursor.execute(query,values)
    db.commit()

    return "Student Registered Successfully"

@app.route('/students')
def students():

    cursor.execute("SELECT * FROM students")
    data = cursor.fetchall()

    return render_template('students.html', students=data)

if __name__ == '__main__':
    app.run(debug=True)
```

---

# HTML Registration Form

## templates/register.html

```html
<!DOCTYPE html>
<html>
<head>
<title>Student Registration</title>
</head>

<body>

<h2>Student Registration Form</h2>

<form action="/register" method="POST">

Name
<input type="text" name="name" required>

<br><br>

Email
<input type="email" name="email" required>

<br><br>

Phone Number
<input type="text" name="phone" required>

<br><br>

Course
<input type="text" name="course" required>

<br><br>

Address
<textarea name="address"></textarea>

<br><br>

<button type="submit">Register</button>

</form>

</body>
</html>
```

---

# Display Students Page

## templates/students.html

```html
<!DOCTYPE html>
<html>

<head>
<title>Registered Students</title>
</head>

<body>

<h2>Registered Students</h2>

<table border="1">

<tr>
<th>ID</th>
<th>Name</th>
<th>Email</th>
<th>Phone</th>
<th>Course</th>
<th>Address</th>
</tr>

{% for student in students %}

<tr>
<td>{{student[0]}}</td>
<td>{{student[1]}}</td>
<td>{{student[2]}}</td>
<td>{{student[3]}}</td>
<td>{{student[4]}}</td>
<td>{{student[5]}}</td>
</tr>

{% endfor %}

</table>

</body>

</html>
```

---

# MySQL Database Setup

Create database

```
CREATE DATABASE studentdb;
```

Create table

```
CREATE TABLE students (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(100),
email VARCHAR(100),
phone VARCHAR(20),
course VARCHAR(100),
address TEXT
);
```

---

# Requirements File

## requirements.txt

```
Flask
mysql-connector-python
```

Install dependencies

```
pip install -r requirements.txt
```

---

# Running the Application

Run Flask app

```
python app.py
```

Open browser

```
http://127.0.0.1:5000
```

---

# Jenkins Pipeline (Optional Deployment)

Example Jenkins pipeline:

```
pipeline {

    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/swati-zampal/stud-reg-flask-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Flask App') {
            steps {
                sh 'python app.py'
            }
        }
    }
}
```

---

# Screenshots

Include screenshots in documentation.

Example:

```
screenshots/register-form.png
screenshots/student-table.png
screenshots/mysql-data.png
screenshots/jenkins-build.png
```

---

# Optional Enhancements

Future improvements can include:

- Edit student records
- Delete student records
- Add login authentication
- Improve UI with Bootstrap
- Deploy on AWS EC2

---

# Deployment on AWS EC2 (Optional)

Steps:

1. Launch EC2 instance
2. Install Python and MySQL
3. Clone repository

```
git clone https://github.com/swati-zampal/stud-reg-flask-app.git
```

4. Install dependencies

```
pip install -r requirements.txt
```

5. Run application

```
python app.py
```

---

# Learning Outcomes

After completing this project you will understand:

- Flask web development
- HTML form handling
- MySQL database integration
- Backend API routes
- GitHub version control
- Jenkins CI/CD pipeline basics

---

# Author

Vaishnavi Kadam

LinkedIn  
https://www.linkedin.com/in/vaishnavi-kadam-206207311

GitHub  
https://github.com/vaishnavikadam1918

Email  
vaishnavikadam8153@gmail.com

---
