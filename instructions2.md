# Create database

Everything in appp.py:
1. Import the modules I need:
1.1 SQLAlchemy
from flask_sqlalchemy import SQLAlchemy

1.2 UserMixin
from flask_login import UserMixin
* This is one is used to create tables inside the database


2. Call the function SQLAlchemy:
db = SQLAlchemy()

3. Create a link with the app and the database:
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///database.db"

4. Create a key
app.config['SECRET_KEY'] = 'thisisasecretkey'

5. Initialize the database
db.init_app(app)

6. Create the tables:
class User(db.Model, UserMixin):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(20), nullable=False,
                         unique=True)  # "unique=True means that user name has to be unique"
    # "nullable=False" means that this field can not be empty
    password = db.Column(db.String(80), nullable=False)

7. Create the database with the User table
    with app.app_context():
    db.create_all()