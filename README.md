# TPO’s Virtual Assistant

A Flask-based web application that helps students and visitors schedule appointments with the Training and Placement Officer (TPO), provides institute information, and allows the TPO (admin) to view and manage appointments. The application uses Bootstrap for styling, SQLAlchemy for database interaction, and Flask-Mail for sending confirmation emails.

## Table of Contents

1. [Features](#features)
2. [Project Structure](#project-structure)
3. [Getting Started](#getting-started)
4. [Configuration](#configuration)
5. [Usage](#usage)
6. [Routes](#routes)
7. [Contact](#contact)

---

## Features

- **User Registration and Login**  
  Secure password storage using `werkzeug.security` (passwords are hashed and salted).
- **Appointment Scheduling**  
  Users can schedule appointments with the TPO and receive confirmation emails upon booking.
- **Admin Dashboard**  
  Admin (TPO) can log in with separate credentials to view and manage all appointments.
- **Feedback System**  
  Users can leave feedback or messages.
- **Responsive UI**  
  Uses [Bootstrap](https://getbootstrap.com/) for a clean, mobile-friendly interface.

---

## Project Structure

TPO-s-Virtual-Assistant/
├─ project/
│  ├─ static/
│  │  ├─ css/
│  │  ├─ js/
│  │  └─ images/
│  ├─ templates/
│  │  ├─ admin-login.html
│  │  ├─ admindata.html
│  │  ├─ adminfunctions.html
│  │  ├─ adminappointments.html
│  │  ├─ user-login.html
│  │  ├─ user.html
│  │  ├─ appointment.html
│  │  ├─ others.html
│  │  ├─ thanks.html
│  │  └─ ...
│  ├─ main.py
│  ├─ config.json        # Configuration file (ignored by Git)
│  ├─ .gitignore         # Contains config.json, .env, etc.
│  └─ requirements.txt


- **`main.py`** – The primary Flask application file containing routes, models, and configuration.
- **`config.json`** – Contains sensitive configuration parameters (database credentials, email credentials, admin login, etc.).  
  *Ensure this file is added to your `.gitignore` so it’s not pushed publicly.*
- **`templates/`** – Jinja2 templates for HTML pages.
- **`static/`** – Static files such as CSS, JavaScript, and images.
- **`.gitignore`** – Specifies files and directories Git should ignore.

---

## Getting Started

### Prerequisites

- **Python 3.7+**
- **pip** (Python package installer)
- **MySQL** or a compatible database server
- A working email account (e.g., Gmail) for sending appointment confirmations

### Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/<your-username>/TPO-s-Virtual-Assistant.git
   cd TPO-s-Virtual-Assistant/project

2. Create a Virtual Environment (Recommended)
python -m venv venv
# On Linux/Mac:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

3. Install Dependencies
pip install -r requirements.txt

### Configuration

config.json
Create a config.json file in the project root (if not already created) with the following content:

{
  "DEBUG": true,
  "SECRET_KEY": "your-secret-key",
  "SQLALCHEMY_DATABASE_URI": "mysql+pymysql://username:password@localhost/db_name",
  "MAIL_SERVER": "smtp.gmail.com",
  "MAIL_PORT": 587,
  "MAIL_USERNAME": "your-email@example.com",
  "MAIL_PASSWORD": "your-email-password",
  "MAIL_USE_TLS": true,
  "MAIL_USE_SSL": false
}

secret_key: Used by Flask to secure sessions.
userpass, basedir, dbname: Combined to build the SQLAlchemy database URI.
username, password: Admin credentials for TPO login.
gmail-user, gmail-password: Email credentials for sending appointment confirmations.

### Usage
Set Up the Database

Ensure MySQL is running.
Create a database named placement (or update the name in config.json).
Ensure your MySQL user has the appropriate privileges.

Run the Application
python main.py

The Flask server will run on http://127.0.0.1:5000 by default.

Access the Application

User Login/Signup:
Navigate to /login for logging in or /signup for creating a new user account.
Admin Login:
Navigate to /admin and use the credentials specified in config.json.
Appointment Booking:
After logging in, visit /appointment to schedule an appointment.
Feedback:
Submit feedback via /feedback.
Admin Dashboard:
Admin can view all appointments via /adminappointment.

### Routes
Here are some key routes defined in the application:

- / : Renders the homepage (index.html)
  
- /signup (GET, POST) : User registration endpoint; creates a new user record in the database
  
- /login (GET, POST) : User login endpoint; verifies email and password using secure hash functions
  
- /logout : Logs out the current user
  
- /admin (GET, POST) : Admin login endpoint; verifies admin credentials as stored in config.json

- /adminlogout : Logs out the admin (ensure session key consistency)

- /appointment (GET, POST) : Allows users to schedule an appointment; sends a confirmation email upon booking
  
- /adminappointment : Displays all appointments to the admin
  
- /feedback (GET, POST) : Submits user feedback to the database
  
- /others (GET, POST) : Stores additional trainer data in the tr table
  
- /test : A test route to check database connectivity

### Contact
For any issues, suggestions, or contributions, please feel free to open an issue or contact the author directly.
