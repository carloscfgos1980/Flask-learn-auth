# Add the functionality to the HTML

1. Add a variable that will pass to tge HTML. app.py:
1.1 Login route function
Inside the login route function, return the variable, like this:
return render_template('login.html', form=form)

1.2 Register route function:
return render_template('register.html', form=form)

2. Create form in login.HTML

    <form method="POST" action="">
        {{ form.hidden_tag() }}
        {{ form.username }}
        {{ form.password }}
        {{ form.submit }}
    </form>

3. Create form in register.HTML:
    <form method="POST" action="">
        {{ form.hidden_tag() }}
        {{ form.username }}
        {{ form.password }}
        {{ form.submit }}
    </form>

* In this case the forms are the same 