# Forms
# Steps:
1. Install packages to mages forms: 
pip install -U Flask-WTF

pip install flask-bcrypt

2. Import all this packages. app.py::
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import InputRequired, Length, ValidationError
from flask_bcrypt import Bcrypt

3. Create a class for the register form. app.py:

class RegisterForm(FlaskForm):
    username = StringField(validators=[
                           InputRequired(), Length(min=4, max=20)], render_kw={"placeholder": "Username"})

    password = PasswordField(validators=[
                             InputRequired(), Length(min=8, max=20)], render_kw={"placeholder": "Password"})

    submit = SubmitField('Register')

    def validate_username(self, username):
        existing_user_username = User.query.filter_by(
            username=username.data).first()
        if existing_user_username:
            raise ValidationError(
                'That username already exists. Please choose a different one.')

* <render_kw> is used to encript the password
* <Length(min=8, max=20)> in this case the max extension of the password is 20 characters, despite we defined in the used that the User class in dabtabase.db could be 80 characters, because with the hash encription, it could gain some length.
* <def validate_username(self, username):> Checks is this user doesn't exist before create a new one.
It queries the database (username.data)
In case that it already exists then it raises a messager error.

4. Create a class for the login form. app.py:
* It is almost the same as creating the class for Register. Only with the checking if there is already that user. 
And in the submit field, 'login' instead of 'register
submit = SubmitField('login')

it looks like this:

class LoginForm(FlaskForm):
    username = StringField(validators=[
                           InputRequired(), Length(min=4, max=20)], render_kw={"placeholder": "Username"})

    password = PasswordField(validators=[
                             InputRequired(), Length(min=8, max=20)], render_kw={"placeholder": "Password"})

    submit = SubmitField('Login')