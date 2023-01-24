# Flask App by Arpan Neupane

https://www.youtube.com/watch?v=71EU8gnZqZQ&t=66s

* run the app, type in the terminal
python3 app.py

or simple go the app.py file and run from VSCode

# Steps
1. Create the app.py
1.1 Import Flask and render-templates, like this:
from flask import Flask, render_template

1.2
app = Flask(__name__)

1.3 
if __name__ == '__main__':
    app.run(debug=True)

1.4 Set the routes

2. Create the html files in templates folder
3. Create the <href> so we can access the login and register. home.html:
    <a href="{{ url_for('login') }}">Login Page</a><br>
    <a href="{{ url_for('register') }}">Register Page</a><br>

4. Create the <href> to create account. login.html:
<a href="{{ url_for('register') }}">Don't have an account? Sign Up</a>

5. Create the <href> to create sign up. register.html:
<a href="{{ url_for('login') }}">Already have an account? Log In</a>


