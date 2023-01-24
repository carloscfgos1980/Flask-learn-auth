# add the functionability of login into the html

# Steps:
1. Import <Bcrypt>
from flask_bcrypt import Bcrypt

2. Call <Bcrypt>
bcrypt = Bcrypt(app)

3. Write this codes in order to make <Bcrypt> works:
login_manager = LoginManager()
login_manager.init_app(app)
login_manager.login_view = 'login'

@login_manager.user_loader
def load_user(user_id):
    return User.query.get(int(user_id))



4. Create functionability inside the route function for log in
4.1 Add method:
@app.route("/login", methods=['GET', 'POST'])

4.2 condiction to be log in:
def login():

4.3 Condictions to check is the <username is correct>:
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.username.data).first()
        if user:
            if bcrypt.check_password_hash(user.password, form.password.data):

4.4 check is the password is correct:
            if bcrypt.check_password_hash(user.password, form.password.data):
                login_user(user)

4.5 Redirect to dashboard
return redirect(url_for('dashboard'))
* We need to creat a dashboard. html in templates and create a route for this template. 


* The whole login route look like this:

@app.route("/login", methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.username.data).first()
        if user:
            if bcrypt.check_password_hash(user.password, form.password.data):
                login_user(user)
                return redirect(url_for('dashboard'))

    return render_template('login.html', form=form)



5. Create functionability inside the route function to register(line 94 - 105):
5.1 Storage the encrypt password in a variable:
hashed_password = bcrypt.generate_password_hash(form.password.data)

5.2 Create new user:
new_user = User(username=form.username.data, password=hashed_password)

5.3 Add new user to the table in the database:
db.session.add(new_user)

5.4 Commit the changes, just like in github command-line-interface
db.session.commit()

5.5 Redirect to Login
return redirect(url_for('login'))
*Here I could make it to log in directly after register, like this:
return redirect(url_for('dashboard'))
* I guess this way is saver and double check that the user has been correctly created

* The whole register route look like this:

@app.route("/register", methods=['GET', 'POST'])
def register():
    form = RegisterForm()

    if form.validate_on_submit():
        hashed_password = bcrypt.generate_password_hash(form.password.data)
        new_user = User(username=form.username.data, password=hashed_password)
        db.session.add(new_user)
        db.session.commit()
        return redirect(url_for('login'))

    return render_template('register.html', form=form)

