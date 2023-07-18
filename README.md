# Ishop_Ecommerce_Project
Ecommerce Application using Flask Python Framework
##This project will be using Flask Framework to create an ecommeerce Application with the following features
#### Vendor Registration, Vendor Login, Sessions, Access and Roles Control, Vendor Profile Page, Vendor Product Upload
#### Products Display, Buyer Purchase, Payment Integration, and Deployment

# Step1: Database and Table Creation
### Create Database Named IshopDB
### Create Tables: products and vendors

# Step2:
## Create the Flask Application File Structure: 
### app.py file to run backend application
### templates folder to house all the front end html files
### static folder to hold all the resources: css, js, images, products

# Step3: Vendor Registration
### Inside the templates folder, create a files named vendor_register.html and paste the code below
### It contaion sthe form for registering a new vwndor to the ecommerce application
### Code:
```  <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        * {
            border: 0;
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        :root {
            --hue: 223;
            --bg: hsl(0, 0%, 100%);
            --fg: hsl(var(--hue), 10%, 10%);
            --primary: hsl(var(--hue), 90%, 50%);
            --trans-dur: 0.3s;
            font-size: calc(16px + (24 - 16) * (100vw - 320px) / (2560 - 320));
        }

        a {
            color: hsl(var(--hue), 90%, 50%);
            transition: color var(--trans-dur);
        }

        a:focus-visible,
        a:hover {
            text-decoration: none;
        }

        body,
        button,
        input {
            color: var(--fg);
            font: 1em/1.5 Nunito, sans-serif;
        }

        body {
            background-color: var(--bg);
            display: flex;
            height: 100vh;
            overflow: hidden;
            transition:
                background-color var(--trans-dur),
                color var(--trans-dur);
        }

        h1 {
            font-size: 2em;
            margin: 0 0 0.75rem;
        }

        p {
            color: hsl(var(--hue), 10%, 30%);
            margin: 0 0 1.5em;
            transition: color var(--trans-dur);
        }

        .login,
        .login__bg-img,
        .login__col {
            display: flex;
        }

        .login,
        .login__col {
            width: 100%;
            height: 100%;
        }

        .login__bg-img {
            background: url(https://assets.codepen.io/416221/woman_at_computer.jpg) center / cover no-repeat;
            border-radius: 1.5em;
            margin: 0.75em 0.75em 0.75em 0;
            height: 100%;
            min-height: 20em;
        }

        .login__brand,
        .login__copyright {
            padding: 1.5em;
        }

        .login__brand {
            display: flex;
            align-items: center;
            font-weight: bold;
        }

        .login__brand:before {
            background-color: var(--fg);
            border-radius: 50%;
            content: "";
            display: block;
            margin-right: 0.5em;
            width: 0.75em;
            height: 0.75em;
            transition: background-color var(--trans-dur);
        }

        .login__btn {
            background-color: hsl(var(--hue), 90%, 50%);
            border-radius: 0.2em;
            color: hsl(0, 0%, 100%);
            cursor: pointer;
            display: block;
            margin-bottom: 1.5em;
            outline: transparent;
            padding: 0.5em 1.5em;
            position: relative;
            width: 100%;
            transition:
                background-color var(--trans-dur),
                opacity var(--trans-dur);
            -webkit-appearance: none;
            appearance: none;
        }

        .login__btn:disabled {
            cursor: not-allowed;
            opacity: 0.5;
        }

        .login__btn:not(:disabled):focus-visible,
        .login__btn:not(:disabled):hover {
            background-color: hsl(var(--hue), 90%, 30%);
        }

        .login__btn-spinner,
        .login__btn-spinner:before,
        .login__btn-spinner:after {
            animation: spinner 1s ease-in-out infinite;
            background-color: hsl(0, 0%, 100%);
            border-radius: 50%;
            position: absolute;
        }

        .login__btn-spinner {
            animation-delay: -0.2s;
            display: none;
            top: 50%;
            left: 50%;
            width: 0.375em;
            height: 0.375em;
            transform: translate(-50%, -50%);
        }

        .login__btn-spinner:before,
        .login__btn-spinner:after {
            content: "";
            display: block;
            width: 100%;
            height: 100%;
        }

        .login__btn-spinner:before {
            animation-delay: -0.4s;
            left: -0.75em;
        }

        .login__btn-spinner:after {
            right: -0.75em;
        }

        .login__btn[data-login="true"] .login__btn-label {
            visibility: hidden;
        }

        .login__btn[data-login="true"] .login__btn-spinner {
            display: block;
        }

        .login__checkbox,
        .login__field {
            background-color: hsla(var(--hue), 90%, 50%, 0);
            border-radius: 0.2em;
            box-shadow: 0 0 0 1px hsl(var(--hue), 10%, 70%) inset;
            outline: transparent;
            transition:
                background-color var(--trans-dur),
                box-shadow var(--trans-dur);
            -webkit-appearance: none;
            appearance: none;
        }

        .login__checkbox {
            margin-right: 0.5em;
            width: 1em;
            height: 1em;
        }

        .login__checkbox:before {
            color: hsla(0, 0%, 100%, 0);
            content: "\2713";
            display: block;
            line-height: 1.333;
            text-align: center;
        }

        .login__checkbox:checked {
            background-color: hsla(var(--hue), 90%, 50%, 1);
            box-shadow: 0 0 0 1px var(--primary) inset;
        }

        .login__checkbox:checked:before {
            color: hsla(0, 0%, 100%, 1);
        }

        .login__checkbox:focus-visible,
        .login__checkbox:hover,
        .login__field:focus-visible,
        .login__field:hover {
            box-shadow: 0 0 0 1px var(--primary) inset;
        }

        .login__col {
            flex-direction: column;
            overflow-y: auto;
        }

        .login__copyright p {
            font-size: 0.75em;
            line-height: 2;
            margin: 0;
        }

        .login__field {
            padding: 0.5em 0.75em;
            width: 100%;
            height: 2.5em;
        }

        .login__field-group {
            margin-bottom: 0.75em;
        }

        .login__field-group--horz {
            display: flex;
            justify-content: space-between;
        }

        .login__form,
        .login__form-wrapper {
            margin: auto;
        }

        .login__form {
            padding: 0 1.5em;
            width: 100%;
        }

        .login__form-wrapper {
            max-width: 18em;
        }

        .login__label {
            display: block;
            font-weight: 500;
        }

        .login__label--horz {
            font-weight: normal;
            display: flex;
            align-items: center;
        }

        .login__label,
        .login__label+a,
        .login__sign-up {
            font-size: 0.75em;
            line-height: 2;
        }

        .login__sign-up {
            margin: 0;
            text-align: center;
        }

        .login__testimonial {
            background-image: linear-gradient(hsla(0, 0%, 0%, 0), hsla(0, 0%, 0%, 0.6));
            border-radius: 0 0 1.5em 1.5em;
            margin-top: auto;
            padding: 1.5em;
            width: 100%;
        }

        .login__testimonial p {
            color: hsl(0, 0%, 100%);
            font-size: 1.5em;
            text-wrap: balance;
        }

        .login__testimonial p+p {
            margin-bottom: 0;
        }

        .login__testimonial small {
            font-size: 1rem;
        }

        /* Dark theme */
        @media (prefers-color-scheme: dark) {
            :root {
                --bg: hsl(var(--hue), 10%, 10%);
                --fg: hsl(var(--hue), 10%, 90%);
            }

            a {
                color: hsl(var(--hue), 90%, 70%);
            }

            p {
                color: hsl(var(--hue), 10%, 70%);
            }

            .login__checkbox,
            .login__field {
                box-shadow: 0 0 0 1px hsl(var(--hue), 10%, 30%) inset;
            }

            .login__checkbox:focus-visible,
            .login__checkbox:hover,
            .login__field:focus-visible,
            .login__field:hover {
                box-shadow: 0 0 0 1px hsl(var(--hue), 90%, 70%) inset;
            }

            .login__checkbox:checked:focus-visible,
            .login__checkbox:checked:hover,
            .login__field:checked:focus-visible,
            .login__field:checked:hover {
                box-shadow: 0 0 0 1px hsl(var(--hue), 90%, 50%) inset;
            }
        }

        /* Mobile */
        @media (max-width: 767px) {
            .login__col+.login__col {
                display: none;
            }
        }

        /* Animations */
        @keyframes spinner {

            from,
            to {
                background-color: hsla(0, 0%, 100%, 1);
            }

            50% {
                background-color: hsla(0, 0%, 100%, 0);
            }
        }
    </style>

    <script>
        // for mock login and copyright year only
        window.addEventListener("DOMContentLoaded", () => {
            const loginForm = new LoginForm(".login");
        });

        class LoginForm {
            isLoggingIn = false;
            timer = null;

            constructor(el) {
                this.el = document.querySelector(el);

                this.init();
            }
            init() {
                this.copyright();

                this.form = this.el?.querySelector("form");
                this.form?.addEventListener("submit", this.login.bind(this));

                this.loginBtn = this.el?.querySelector("[data-login]");
                this.loginBtn?.addEventListener("click", this.login.bind(this));
            }
            copyright() {
                const year = this.el?.querySelector("[data-year]");
                if (year) year.innerHTML = new Date().getFullYear();
            }
            login() {
                if (this.isLoggingIn) return;

                this.isLoggingIn = true;
                this.loginStateToggle();

                clearTimeout(this.timer);
                this.timer = setTimeout(this.reset.bind(this), 1500);
            }
            loginStateToggle() {
                this.loginBtn.disabled = this.isLoggingIn;
                this.loginBtn.setAttribute("data-login", this.isLoggingIn);
            }
            reset() {
                this.isLoggingIn = false;
                this.loginStateToggle();
                this.form.reset();
            }
        }

    </script>
</head>

<body>
    <main class="login">
        <div class="login__col">
            <header class="login__brand">Ishop Ecommerce</header>
            <form class="login__form" method="post" action="/vendor_registration" enctype="multipart/form-data">
                <div class="login__form-wrapper">
                    <h1>Register Here...</h1>
                    <p>{{message}}</p>
                    <div class="login__field-group">
                        <label class="login__label" for="vendor_name">Vendor name</label>
                        <input class="login__field" id="vendor_name" type="text" name="name" />
                    </div>

                    <div class="login__field-group">
                        <label class="login__label" for="contact">Vendors Contact</label>
                        <input class="login__field" id="contact" type="tel" name="contact" />
                    </div>



                    <div class="login__field-group">
                        <label class="login__label" for="email">Vendors Email</label>
                        <input class="login__field" id="email" type="email" name="email" />
                    </div>

                    <div class="login__field-group">
                        <label class="login__label" for="location">Vendors Location</label>
                        <input class="login__field" id="location" type="text" name="location" />
                    </div>

                    <div class="login__field-group">
                        <label class="login__label" for="password">Vendors Password</label>
                        <input class="login__field" id="password" type="password" name="password" />
                    </div>

                    <div class="login__field-group">
                        <label class="login__label" for="photo">Vendors Profile Photo</label>
                        <input class="login__field" id="photo" type="file" name="photo" />
                    </div>

                    <div class="login__field-group">
                        <label class="login__label" for="desc">Vendor Description</label>
                        <textarea name="desc" id="desc" cols="30" rows="10"></textarea>
                    </div>

                    <div class="login__field-group login__field-group--horz">
                        <label class="login__label login__label--horz">
                            <input class="login__checkbox" type="checkbox" name="remember_me">
                            <span>Remember me</span>
                        </label>
                        <a href="#">Forgot password</a>

                    </div>
                    <input class="login__btn" type="submit" value="SIGN UP">

                    <p class="login__sign-up">Don’t have an account? <a href="#">Sign up</a></p>
                </div>
            </form>

            <footer class="login__copyright">
                <p>© <span data-year>2023</span> Ishop Ecommerce. All rights reserved.</p>
            </footer>
        </div>
        <div class="login__col">
            <div class="login__bg-img">
                <div class="login__testimonial">
                    <p><q>Assduff Jekyll has helped us kick-start projects in a bang and save thousands of hours of
                            work.</q></p>
                    <p>Ann Thrax
                    <p>
                    <p><small>Senior UX Designer, X.Y. Zee</small></p>
                </div>
            </div>
        </div>
    </main>

</body>

</html>

```
# Step4: app.py
### Now proceed to app.py file and implement backend for vendor registration
### Use the code below
 ```
from flask import *
import pymysql

# start
app = Flask(__name__)
# SESSIONS
# step 1: Provide secret key to your application
# Avoid session hijacking, cross -site scripting
app.secret_key = "1234#$fuhutguhiknknnnnk6568gghcghhvufuy"

# 1. Vendor Registration


@app.route('/vendor_registration', methods=['POST', 'GET'])
def register_vendor():
    if request.method == 'POST':
        vendor_name = request.form['name']
        vendor_contact = request.form['contact']
        vendor_email = request.form['email']
        vendor_location = request.form['location']
        vendor_password = request.form['password']

        vendor_photo = request.files['photo']
        vendor_photo.save('static/images/' + vendor_photo.filename)

        vendor_desc = request.form['desc']

        connection = pymysql.connect(
            host='localhost', user='root', password='', database='IshopDB')

        cursor = connection.cursor()

        data = (vendor_name, vendor_contact, vendor_email,
                vendor_location, vendor_password, vendor_photo.filename, vendor_desc)

        sql = "insert into vendors (vendor_name, vendor_contact, vendor_email, vendor_location,vendor_password, vendor_profilephoto, vendor_desc) values (%s, %s, %s, %s, %s, %s, %s)"

        cursor.execute(sql, data)
        connection.commit()

        return render_template('vendor_register.html', message='Vendor Registred Successful')

    else:
        return render_template('vendor_register.html', message='Please Register Here')

app.run(debug=True)

```

# Step5: Vendor Login and Sessions : vendor_login.html
### Inside the templates folder create a file vendor_login.html
### Paste the code below to implemnt vendor login login form:
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        * {
            border: 0;
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        :root {
            --hue: 223;
            --bg: hsl(0, 0%, 100%);
            --fg: hsl(var(--hue), 10%, 10%);
            --primary: hsl(var(--hue), 90%, 50%);
            --trans-dur: 0.3s;
            font-size: calc(16px + (24 - 16) * (100vw - 320px) / (2560 - 320));
        }

        a {
            color: hsl(var(--hue), 90%, 50%);
            transition: color var(--trans-dur);
        }

        a:focus-visible,
        a:hover {
            text-decoration: none;
        }

        body,
        button,
        input {
            color: var(--fg);
            font: 1em/1.5 Nunito, sans-serif;
        }

        body {
            background-color: var(--bg);
            display: flex;
            height: 100vh;
            overflow: hidden;
            transition:
                background-color var(--trans-dur),
                color var(--trans-dur);
        }

        h1 {
            font-size: 2em;
            margin: 0 0 0.75rem;
        }

        p {
            color: hsl(var(--hue), 10%, 30%);
            margin: 0 0 1.5em;
            transition: color var(--trans-dur);
        }

        .login,
        .login__bg-img,
        .login__col {
            display: flex;
        }

        .login,
        .login__col {
            width: 100%;
            height: 100%;
        }

        .login__bg-img {
            background: url(https://assets.codepen.io/416221/woman_at_computer.jpg) center / cover no-repeat;
            border-radius: 1.5em;
            margin: 0.75em 0.75em 0.75em 0;
            height: 100%;
            min-height: 20em;
        }

        .login__brand,
        .login__copyright {
            padding: 1.5em;
        }

        .login__brand {
            display: flex;
            align-items: center;
            font-weight: bold;
        }

        .login__brand:before {
            background-color: var(--fg);
            border-radius: 50%;
            content: "";
            display: block;
            margin-right: 0.5em;
            width: 0.75em;
            height: 0.75em;
            transition: background-color var(--trans-dur);
        }

        .login__btn {
            background-color: hsl(var(--hue), 90%, 50%);
            border-radius: 0.2em;
            color: hsl(0, 0%, 100%);
            cursor: pointer;
            display: block;
            margin-bottom: 1.5em;
            outline: transparent;
            padding: 0.5em 1.5em;
            position: relative;
            width: 100%;
            transition:
                background-color var(--trans-dur),
                opacity var(--trans-dur);
            -webkit-appearance: none;
            appearance: none;
        }

        .login__btn:disabled {
            cursor: not-allowed;
            opacity: 0.5;
        }

        .login__btn:not(:disabled):focus-visible,
        .login__btn:not(:disabled):hover {
            background-color: hsl(var(--hue), 90%, 30%);
        }

        .login__btn-spinner,
        .login__btn-spinner:before,
        .login__btn-spinner:after {
            animation: spinner 1s ease-in-out infinite;
            background-color: hsl(0, 0%, 100%);
            border-radius: 50%;
            position: absolute;
        }

        .login__btn-spinner {
            animation-delay: -0.2s;
            display: none;
            top: 50%;
            left: 50%;
            width: 0.375em;
            height: 0.375em;
            transform: translate(-50%, -50%);
        }

        .login__btn-spinner:before,
        .login__btn-spinner:after {
            content: "";
            display: block;
            width: 100%;
            height: 100%;
        }

        .login__btn-spinner:before {
            animation-delay: -0.4s;
            left: -0.75em;
        }

        .login__btn-spinner:after {
            right: -0.75em;
        }

        .login__btn[data-login="true"] .login__btn-label {
            visibility: hidden;
        }

        .login__btn[data-login="true"] .login__btn-spinner {
            display: block;
        }

        .login__checkbox,
        .login__field {
            background-color: hsla(var(--hue), 90%, 50%, 0);
            border-radius: 0.2em;
            box-shadow: 0 0 0 1px hsl(var(--hue), 10%, 70%) inset;
            outline: transparent;
            transition:
                background-color var(--trans-dur),
                box-shadow var(--trans-dur);
            -webkit-appearance: none;
            appearance: none;
        }

        .login__checkbox {
            margin-right: 0.5em;
            width: 1em;
            height: 1em;
        }

        .login__checkbox:before {
            color: hsla(0, 0%, 100%, 0);
            content: "\2713";
            display: block;
            line-height: 1.333;
            text-align: center;
        }

        .login__checkbox:checked {
            background-color: hsla(var(--hue), 90%, 50%, 1);
            box-shadow: 0 0 0 1px var(--primary) inset;
        }

        .login__checkbox:checked:before {
            color: hsla(0, 0%, 100%, 1);
        }

        .login__checkbox:focus-visible,
        .login__checkbox:hover,
        .login__field:focus-visible,
        .login__field:hover {
            box-shadow: 0 0 0 1px var(--primary) inset;
        }

        .login__col {
            flex-direction: column;
            overflow-y: auto;
        }

        .login__copyright p {
            font-size: 0.75em;
            line-height: 2;
            margin: 0;
        }

        .login__field {
            padding: 0.5em 0.75em;
            width: 100%;
            height: 2.5em;
        }

        .login__field-group {
            margin-bottom: 0.75em;
        }

        .login__field-group--horz {
            display: flex;
            justify-content: space-between;
        }

        .login__form,
        .login__form-wrapper {
            margin: auto;
        }

        .login__form {
            padding: 0 1.5em;
            width: 100%;
        }

        .login__form-wrapper {
            max-width: 18em;
        }

        .login__label {
            display: block;
            font-weight: 500;
        }

        .login__label--horz {
            font-weight: normal;
            display: flex;
            align-items: center;
        }

        .login__label,
        .login__label+a,
        .login__sign-up {
            font-size: 0.75em;
            line-height: 2;
        }

        .login__sign-up {
            margin: 0;
            text-align: center;
        }

        .login__testimonial {
            background-image: linear-gradient(hsla(0, 0%, 0%, 0), hsla(0, 0%, 0%, 0.6));
            border-radius: 0 0 1.5em 1.5em;
            margin-top: auto;
            padding: 1.5em;
            width: 100%;
        }

        .login__testimonial p {
            color: hsl(0, 0%, 100%);
            font-size: 1.5em;
            text-wrap: balance;
        }

        .login__testimonial p+p {
            margin-bottom: 0;
        }

        .login__testimonial small {
            font-size: 1rem;
        }

        /* Dark theme */
        @media (prefers-color-scheme: dark) {
            :root {
                --bg: hsl(var(--hue), 10%, 10%);
                --fg: hsl(var(--hue), 10%, 90%);
            }

            a {
                color: hsl(var(--hue), 90%, 70%);
            }

            p {
                color: hsl(var(--hue), 10%, 70%);
            }

            .login__checkbox,
            .login__field {
                box-shadow: 0 0 0 1px hsl(var(--hue), 10%, 30%) inset;
            }

            .login__checkbox:focus-visible,
            .login__checkbox:hover,
            .login__field:focus-visible,
            .login__field:hover {
                box-shadow: 0 0 0 1px hsl(var(--hue), 90%, 70%) inset;
            }

            .login__checkbox:checked:focus-visible,
            .login__checkbox:checked:hover,
            .login__field:checked:focus-visible,
            .login__field:checked:hover {
                box-shadow: 0 0 0 1px hsl(var(--hue), 90%, 50%) inset;
            }
        }

        /* Mobile */
        @media (max-width: 767px) {
            .login__col+.login__col {
                display: none;
            }
        }

        /* Animations */
        @keyframes spinner {

            from,
            to {
                background-color: hsla(0, 0%, 100%, 1);
            }

            50% {
                background-color: hsla(0, 0%, 100%, 0);
            }
        }
    </style>

    <script>
        // for mock login and copyright year only
        window.addEventListener("DOMContentLoaded", () => {
            const loginForm = new LoginForm(".login");
        });

        class LoginForm {
            isLoggingIn = false;
            timer = null;

            constructor(el) {
                this.el = document.querySelector(el);

                this.init();
            }
            init() {
                this.copyright();

                this.form = this.el?.querySelector("form");
                this.form?.addEventListener("submit", this.login.bind(this));

                this.loginBtn = this.el?.querySelector("[data-login]");
                this.loginBtn?.addEventListener("click", this.login.bind(this));
            }
            copyright() {
                const year = this.el?.querySelector("[data-year]");
                if (year) year.innerHTML = new Date().getFullYear();
            }
            login() {
                if (this.isLoggingIn) return;

                this.isLoggingIn = true;
                this.loginStateToggle();

                clearTimeout(this.timer);
                this.timer = setTimeout(this.reset.bind(this), 1500);
            }
            loginStateToggle() {
                this.loginBtn.disabled = this.isLoggingIn;
                this.loginBtn.setAttribute("data-login", this.isLoggingIn);
            }
            reset() {
                this.isLoggingIn = false;
                this.loginStateToggle();
                this.form.reset();
            }
        }

    </script>
</head>

<body>
    <main class="login">
        <div class="login__col">
            <header class="login__brand">Ishop Ecommerce</header>
            <form class="login__form" method="post" action="/vendor_login">
                <div class="login__form-wrapper">
                    <h1>Login Here..</h1>
                    <p>{{message}}</p>

                    <div class="login__field-group">
                        <label class="login__label" for="vendor_name">Enter Username</label>
                        <input class="login__field" id="vendor_name" type="text" name="name" />
                    </div>


                    <div class="login__field-group">
                        <label class="login__label" for="password"> Enter Password</label>
                        <input class="login__field" id="password" type="password" name="password" />
                    </div>

                    <div class="login__field-group login__field-group--horz">
                        <label class="login__label login__label--horz">
                            <input class="login__checkbox" type="checkbox" name="remember_me">
                            <span>Remember me</span>
                        </label>
                        <a href="#">Forgot password</a>

                    </div>

                    <input class="login__btn" type="submit" value="SIGN IN">

                    <p class="login__sign-up">Don’t have an account? <a href="#">Sign up</a></p>
                </div>
            </form>

            <footer class="login__copyright">
                <p>© <span data-year>2023</span> Ishop Ecommerce. All rights reserved.</p>
            </footer>
        </div>
        <div class="login__col">
            <div class="login__bg-img">
                <div class="login__testimonial">
                    <p><q>Assduff Jekyll has helped us kick-start projects in a bang and save thousands of hours of
                            work.</q></p>
                    <p>Ann Thrax
                    <p>
                    <p><small>Senior UX Designer, X.Y. Zee</small></p>
                </div>
            </div>
        </div>
    </main>

</body>

</html>

```

# Step 6: app.py: Vendor login Backend
# Add a new route: /vendor_login
### Use the code below

```
@app.route('/vendor_login', methods=['POST', 'GET'])
def vendor_login():
    if request.method == 'POST':
        username = request.form['name']
        password = request.form['password']

        connection = pymysql.connect(
            host='localhost', user='root', password='', database='IshopDB')

        cursor = connection.cursor()

        sql = 'select * from vendors where vendor_name = %s and vendor_password = %s'
        data = (username, password)
        cursor.execute(sql, data)

        count = cursor.rowcount
        if count == 0:
            return render_template('vendor_login.html', message='Invalid Credentials')
        else:
            # session: Store Information About a specific user
            user_record = cursor.fetchone()
            session['key'] = user_record[1]
            session['vendor_id'] = user_record[0]
            session['contact'] = user_record[2]
            session['location'] = user_record[4]
            session['image'] = user_record[5]
            session['desc'] = user_record[7]

            return redirect('/vendor_profile')
    else:
        return render_template('vendor_login.html', message='Please Login Here')

```

# Step 7: Vendor profile
### Before Executing the Code Above : Create a vendor profile, where a vendor will be redirected after a successful login
### vendor_profile.html: code

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> User </title>

    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.6.1/css/all.css"
        integrity="sha384-gfdkjb5BdAXd+lj+gudLWI+BXq4IuLW5IT+brZEZsLFm++aCMlF1V92rMkPaX4PP" crossorigin="anonymous">

    <link rel="stylesheet" href="../static/css/bootstrap.css">
    <script src="../static/js/bootstrap.js"></script>

    <style>
        @import u rl("https://fonts.googleapis.com/css?family=Montserrat:600");
        @import u rl("https://fonts.googleapis.com/css?family=Montserrat:800");
        @import u rl("https://fonts.googleapis.com/css?family=Montserrat");

        body {
            font-family: "Montserrat", sans-serif;
            background: linear-gradient(270deg, #ffead1, #ffb6bd, #e0b5ff);

            background-size: 150% 150%;
            animation: backgroundAnimation 10s ease infinite;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100vw;
            height: 100vh;
            margin: 0;
        }

        .profile {
            animation: loadProfile 0.6s ease-in-out;
            animation-fill-mode: both;
            font-size: 0.9rem;
            display: flex;
            flex-direction: column;
            position: relative;
            max-height: 750px;
            max-width: 900px;
        }

        .profile-bg {
            position: absolute;
            bottom: 0;
            right: 0;
            border-radius: 10px;
            background: white;
            box-shadow: 0 30px 50px -20px rgba(14, 0, 47, 0.21);
            width: calc(100% - 75px);
            height: calc(100% - 110px);
            z-index: -1;
        }

        .container {
            display: flex;
            flex-direction: row;
            align-items: stretch;
            width: 100%;
        }

        .profile-image {
            animation: loadProfileImage 1s ease-in-out 0.5s;
            animation-fill-mode: both;
            position: relative;
            border-radius: 10px;
            box-shadow: 0 25px 45px -20px rgba(255, 0, 47, 0.3),
                inset 0 0px 120px rgba(255, 0, 47, 0.2);
            width: 45%;
            flex: none;
            background-image: url("../static/images/{{session['image']}}");
            background-size: cover;
            background-position: center;
        }

        .profile-image::before {
            content: "";
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 10px;
            background-color: #000;
            opacity: 0.2;
            mix-blend-mode: screen;
        }

        .camera {
            color: #FFFF;
            position: absolute;
            bottom: 28px;
            left: 28px;
            font-size: 1.3rem;
        }

        .profile-info {
            margin-top: 120px;
            padding: 8% 8% 2% 8%;
            position: relative;
        }

        .profile-info h1 {
            font-size: 3rem;
            font-weight: 800;
            margin: 0.7rem;
            position: absolute;
            animation-fill-mode: both;
        }

        h1.first-name {
            animation: titleEffect 1s cubic-bezier(0, 0.2, 0.4, 1);
            top: -115px;
            left: -85px;
        }

        h1.second-name {
            animation: titleEffect 1s cubic-bezier(0, 0, 0.3, 1);
            /* top: -50px;
left: -45px; */
        }

        .profile-info h2 {
            font-size: 1rem;
            font-weight: 600;
            letter-spacing: 0.2rem;
            margin-top: 0;
            margin-bottom: 5%;
        }

        .social-media-icons a,
        .profile-info h2 {
            color: #f63d47;
        }

        .profile-info p {
            line-height: 1.5rem;
        }

        .social-media-icons {
            display: flex;
        }

        .social-media-icons a {
            margin-top: 7%;
            font-size: 1.2rem;
            flex: auto;
            text-align: center;
        }

        .camera,
        .social-media-icons a {
            transition: text-shadow 0.5s ease;
        }

        .camera:hover,
        .social-media-icons a:hover {
            text-shadow: 0px 5px 15px rgba(255, 0, 47, 0.45);
        }

        .statistics {
            margin-right: 10px;
            margin-left: 10px;
            line-height: 2rem;
            display: flex;
            flex-direction: row;
            align-items: center;
        }

        .statistics p {
            margin: 3%;
            flex: auto;
            color: #f63d47;
        }

        .statistics p strong {
            font-size: 1.4rem;
            color: #000;
            font-weight: 200;
            margin-right: 0.3rem;
        }

        .icon {
            background: transparent no-repeat center;
            background-size: contain;
            background-origin: content-box;
            width: 60px;
            height: 60px;
            padding: 15px;
            border: none;
            transition: transform 0.5s ease;
        }

        .icon:hover {
            transform: scale(0.9);
        }

        .arrow {
            flex: 0 1 75px;
            background-image: u rl("https://zephyo.github.io/22Days/code/3/graphics/arrow.svg");
        }

        .right {
            transform: rotate(180deg);
        }

        .right:hover {
            transform: scale(0.9) rotate(180deg);
        }

        .close {
            background-image: u rl("https://zephyo.github.io/22Days/code/3/graphics/close.svg");
            position: absolute;
            top: 5px;
            right: 10px;
        }

        @media only screen and (max-aspect-ratio: 4/7) and (max-width: 600px) {
            .profile {
                margin: 3%;
                height: 97%;
            }

            .container {
                height: 86%;
                flex-direction: column;
            }

            .profile-image {
                height: 40%;
                width: calc(100% - 90px);
            }

            .profile-bg {
                width: 100%;
            }

            h1.first-name {
                left: 10px;
            }

            h1.second-name {
                left: 60px;
            }
        }

        @media screen and (min-aspect-ratio: 4/7) {
            .profile {
                margin-left: 10%;
                margin-right: 10%;
            }
        }

        @keyframes backgroundAnimation {
            0% {
                background-position: 0% 50%;
            }

            50% {
                background-position: 100% 50%;
            }

            100% {
                background-position: 0% 50%;
            }
        }

        @keyframes loadProfile {
            from {
                transform: translateY(100px);
                opacity: 0;
            }

            to {
                transform: translateY(0px);
                opacity: 1;
            }
        }

        @keyframes loadProfileImage {
            from {
                transform: translateY(50px);
                opacity: 0;
            }

            to {
                transform: translateY(0px);
                opacity: 1;
            }
        }

        @keyframes titleEffect {
            from {
                opacity: 0;
                transform: translateX(-75px);
            }

            to {
                transform: translateX(0px);
                opacity: 1;
            }
        }
    </style>
</head>

<body>
    <main class="profile">
        <div class="profile-bg"></div>
        <section class="container">
            <aside class="profile-image">
                <a class="camera" href="#">
                    <i class="fas fa-camera"></i>
                </a>
            </aside>
            <section class="profile-info">
                <h1 class="first-name text-white">{{session['key']}} <span class="second-name text-danger">Stores
                    </span> </h1>

                <h2>ABOUT</h2>
                <p>
                    {{session['desc']}}
                </p>

                <p>Location: {{session['location']}}</p>
                <p>Contact: {{session['contact']}}</p>

                <aside class="social-media-icons">
                    <a href="https://twitter.com/zephybite" target="_blank">
                        <i class="fab fa-twitter"></i>
                    </a>
                    <a href="https://codepen.io/zephyo" target="_blank">
                        <i class="fab fa-codepen"></i>
                    </a>
                    <a href="https://github.com/zephyo" target="_blank">
                        <i class="fab fa-github"></i>
                    </a>
                    </a>
                    <a href="https://medium.com/@zephyo" target="_blank">
                        <i class="fab fa-medium"></i>
                    </a>
                </aside>
            </section>
        </section>
        <section class="statistics">
            <button class="icon arrow left"></button>
            <button class="icon arrow right"></button>

            <p><button type="button" data-bs-toggle="modal" data-bs-target="#add" class="btn btn-outline-dark">Add
                    Product</button></p>

            <p><a href="#" class="btn btn-outline-dark">View Products</a></p>
            <p><a href="/vendor_logout" class="btn btn-outline-danger">Log Out</a></p>

        </section>
        <button class="icon close"></button>
    </main>

    <!-- add product modal -->
    <div class="modal fade" id="add">
        <div class="modal-dialog modal-dialog-scrollable modal-lg">
            <div class="modal-content">
                <!-- header -->
                <div class="modal-header">
                    <h5 class="modal-title">Ishop Ecommerce</h5>
                    <button type="button" class="btn btn-close" data-bs-dismiss="modal"></button>
                </div>

                <!-- body -->
                <div class="modal-body">

                    <div class="card shadow mt-3 mb-3">
                        <h5 class="m-2">{{message}}</h5>
                        <form action="/add_product" method="post" enctype="multipart/form-data">

                            <label for="name" class="form-label"> Product Name </label>
                            <input type="text" name="name" id="name" class="form-control">

                            <label for="desc" class="form-label"> Product Description </label>
                            <textarea name="desc" id="desc" cols="30" rows="10" class="form-control"></textarea>

                            <label for="cost" class="form-label"> Product Cost </label>
                            <input type="number" name="cost" id="cost" class="form-control">


                            <label for="discount" class="form-label"> Product Discount </label>
                            <input type="number" name="discount" id="discount" class="form-control">


                            <label for="category" class="form-label"> Product Category </label>
                            <input type="text" name="category" id="category" class="form-control">

                            <label for="brand" class="form-label"> Product Brand </label>
                            <input type="text" name="brand" id="brand" class="form-control">

                            <label for="image" class="form-label"> Product Image </label>
                            <input type="file" name="image" id="image" class="form-control"><br>

                            <input type="number" name="vendor" id="vendor" placeholder="Vendor Id" class="form-control"><br>

                            <input type="submit" value="Add Product" class="btn btn-success"><br>

                        </form>

                    </div>

                </div>

                <!-- footer -->
                <div class="modal-footer">

                    <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Cancel</button>

                </div>

            </div>

        </div>

    </div>


</body>

</html>

```

## On app.py file implement /vendor_profile route
### Use the code below

```
@app.route('/vendor_profile')
def vendor_profile():
    return render_template('vendor_profile.html')
```

# Step 8: Vendor Logout Feature:
### Add the route below to Logout a vendor

```
@app.route('/vendor_logout')
def vendor_logout():
    if 'key' in session:
        session.clear()
    return redirect('/vendor_login')

```

# Step 9: Vendor Add product Feature:
### Implement the route below to add product to the shop as a vendor

```
@app.route('/add_product', methods=['POST', 'GET'])
def add_product():
    if request.method == 'POST':
        product_name = request.form['name']
        product_desc = request.form['desc']
        product_cost = request.form['cost']
        product_discount = request.form['discount']
        product_category = request.form['category']
        product_brand = request.form['brand']
        image_url = request.files['image']
        image_url.save('static/products/' + image_url.filename)

        vendor_id = request.form['vendor']

        connection = pymysql.connect(
            host='localhost', user='root', password='', database='IshopDB')

        cursor = connection.cursor()

        data = (product_name, product_desc, product_cost, product_discount,
                product_category, product_brand, image_url.filename, vendor_id)

        sql = "insert into products (product_name, product_desc, product_cost, product_discount, product_category, product_brand, image_url, vendor_id) values (%s, %s, %s, %s, %s, %s, %s, %s)"

        cursor.execute(sql, data)
        connection.commit()
        return render_template('vendor_profile.html', message='Product Added Successfully')

    else:
        return render_template('vendor_profile.html', message='Please Add Product Details')

```

# Step 10: Home Page
## This will be implement on '/' route
### On Your templates, create a file index.html
### Paste the code Below:

```
<!DOCTYPE html>
<html>
    <head>
        <title>Home Page</title>
        <link href='https://unpkg.com/boxicons@2.0.7/css/boxicons.min.css'
            rel='stylesheet'>
        <link rel="stylesheet" href="../static/index.css">
        <script src="../static/index.js"></script>
        <style>
            .btn{
                background-color: aqua;
                padding: 20px;
                border-radius: 20px;
                margin-right: 10px;
                text-decoration: none;
                
                align-items: center;
            }
        </style>
    </head>


    <body>
        <header>
            <div class="company-logo">D</div>
            <nav class="navbar">
                <ul class="nav-items">
                    <li class="nav-item"><a href="#" class="nav-link">HOME</a></li>
                    <li class="nav-item"><a href="#" class="nav-link">OFFER</a></li>
                    <li class="nav-item"><a href="#" class="nav-link">SHOP</a></li>
                    <li class="nav-item"><a href="#" class="nav-link">CONTACT</a></li>
                </ul>
            </nav>
            <div class="menu-toggle">
                <i class="bx bx-menu"></i>
                <i class="bx bx-x"></i>
            </div>
        </header>
        <main>
            <!-- HOME SECTION -->
            <section class="container section-1">
                <div class="slogan">
                    <h1 class="company-title">Alpha Online Shop</h1>
                    <h2 class="company-slogan">
                        A website where vendors upload products and buyers
                        purchase goods or services from.
                    </h2>
                    <br>
                    <a href="/save_vendor" class="btn ">Sell Products</a>
                    <a href="#" class="btn ">Buy Products</a>
                </div>
                <div class="home-computer-container">
                    <img class="home-computer"
                        src="../static/images/home_img.png"
                        alt="a computer in dark with shadow" class="home-img">
                </div>
            </section>


            <!-- SPONSOR SECTION -->
            <section class="container section-4">
                <!-- SPONSOR group 1 -->
                <div class="sponsor sponsor-1"><img
                        src="../static/images/microsoft.svg"
                        alt=""></div>
                <div class="sponsor sponsor-2"><img
                        src="../static/images/apple.svg"
                        alt=""></div>

                <!-- SPONSOR group 2 -->
                <div class="sponsor sponsor-3"><img
                        src="../static/images/dell.svg"
                        alt=""></div>
                <div class="sponsor sponsor-4"><img
                        src="../static/images/ibm.svg"
                        alt=""></div>
            </section>

            <!-- SUBSCRIBE SECTION-->
            <section class="container section-5">
                <h2 class="subscribe-input-label">NEWSLETTER</h2>
                <div class="subscribe-container">
                    <input type="text" id="email-subscribe" placeholder="Email
                        address...">
                    <input type="submit" value="SUBSCRIBE">
                </div>
            </section>
        </main>

    </body>
</html>
```

## index.css
```
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@100;200;300;400");

*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

/* ================= VARIABLE ================ */
:root {
  --primary-color: hsl(9, 94%, 61%);
  --primary-color-alt: hsl(28, 72%, 83%);
  --second-color: #3e537c;
  --second-color-alt: hsla(220, 33%, 36%, 65%);
  --third-color: hsl(220, 36%, 28%);
  --white-color: #fbfbfb;
  --white-color-alt: hsl(12, 14%, 93%);
  --dark-color: hsl(300, 100%, 0%);
}

/* ================= BASE ==================== */
li {
  list-style: none;
}
a {
  text-decoration: none;
}
img {
  width: 100%;
  height: auto;
}
.bx {
  font-size: 2.5rem;
}
.container {
  padding: 0 2rem;
}

/* -- BODY -- */
body {
  font-family: "Raleway", sans-serif;
  font-size: 1rem;
  background-color: var(--white-color);
}

/* ================= HEADER ================ */
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: var(--dark-color);
  padding: 1rem 2rem;
}
.company-logo {
  font-size: 2.5rem;
  background: -webkit-linear-gradient(
    120deg,
    var(--primary-color-alt),
    var(--primary-color)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.nav-items {
  display: flex;
}
.nav-item {
  margin: 0 2rem;
}
.nav-link {
  font-size: 1.1rem;
  letter-spacing: 0.05rem;
  position: relative;
  background: -webkit-linear-gradient(
    var(--primary-color-alt),
    var(--primary-color)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.nav-link::before {
  content: "";
  background: linear-gradient(var(--primary-color), var(--primary-color-alt));
  width: 100%;
  height: 0.05rem;
  position: absolute;
  left: 0;
  bottom: 0;
  transform: scaleX(0);
  transform-origin: bottom right;
  transition: transform 150ms;
}
.nav-link:hover::before {
  transform: scaleX(1);
  transform-origin: bottom left;
}
.menu-toggle {
  display: none;
}
.bx-menu,
.bx-x {
  cursor: pointer;
  background: -webkit-linear-gradient(
    120deg,
    var(--primary-color-alt),
    var(--primary-color)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  display: none !important;
}

/* ================= MAIN ================ */

/* -------- HOME SECTION -------------- */
.section-1 {
  background-color: var(--dark-color);
  display: grid;
}
/* .home-computer-container {} */

.slogan .company-title {
  background: -webkit-linear-gradient(
    120deg,
    var(--primary-color-alt),
    var(--primary-color)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-top: 2rem;
  font-size: 1.5rem;
  font-weight: 600;
}
.slogan .company-slogan {
  background: -webkit-linear-gradient(
    120deg,
    var(--primary-color-alt),
    var(--primary-color)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-top: 1rem;
  font-size: 1.2rem;
  font-weight: 400;
  line-height: 1.8rem;
}

/* -------- OFFER SECTION ------------- */
.section-2 {
  margin: 2rem 0;
}
.offer {
  background-color: var(--dark-color);
  margin: 1rem 0;
  display: grid;
}
.offer img {
  background-color: var(--dark-color);
  padding: 2rem 0;
}
.offer-1 img {
  background-color: var(--dark-color);
  padding: 3rem 0;
}
.offer-description {
  background-color: var(--white-color-alt);
  padding: 0 1rem;
}
.offer-description .offer-title {
  color: var(--second-color);
  font-size: 1.8rem;
  font-weight: 400;
  padding: 1.5rem 0 0.5rem 0;
}
.offer-description .offer-hook {
  color: var(--second-color-alt);
  font-size: 1.2rem;
}
.offer-description .cart-btn {
  cursor: pointer;
  color: var(--second-color-alt);
  font-size: 1.1rem;
  display: grid;
  place-items: center;
  margin: 2rem 0 1rem 0;
  width: 10rem;
  height: 3rem;
  background-image: linear-gradient(
    to top,
    var(--primary-color-alt),
    var(--primary-color)
  );
}
.offer-description .cart-btn:hover {
  background-image: linear-gradient(
    to bottom,
    var(--primary-color-alt),
    var(--primary-color)
  );
}

/* -------- PRODUCT SECTION ----------- */
.section-3 {
  display: grid;
  place-items: center;
  justify-content: space-around;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 400px));
}
.product {
  cursor: pointer;
  background-color: var(--white-color-alt);
  position: relative;
}
.product::before {
  content: "";
  background-image: linear-gradient(
    to bottom,
    hsla(29, 72%, 83%, 0.438),
    hsla(9, 94%, 61%, 0.507)
  );
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
.product_add_cart {
  color: var(--white-color-alt);
  font-size: 1.2rem;
  background-color: hsl(9, 94%, 65%);
  padding: 1rem 0.4rem;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: transform 300ms, color 300ms, box-shadow 300ms;
}
.product_add_cart:hover {
  color: var(--white-color);
  box-shadow: 0 1rem 0 -0.5rem hsl(17, 79%, 65%, 0.7),
    0 2rem 0 -1rem hsla(17, 79%, 65%, 0.65);
}

/* -------- SPONSOR SECTION ----------- */
.section-4 {
  margin: 4rem 0;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
}
.sponsor img {
  cursor: pointer;
  width: 40px;
  height: 40px;
  filter: grayscale(100%);
  opacity: 0.8;
  transition: opacity 300ms;
}
.sponsor img:hover {
  /* filter: grayscale(0); */
  opacity: 1;
}

/* ========= SUBSCRIBE SECTION ========== */
.section-5 {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 2rem 0;
}
.subscribe-input-label {
  margin-bottom: 1rem;
  font-size: 1.5rem;
  font-weight: 400;
  letter-spacing: 0.05rem;
  color: var(--second-color);
}
input[type="text"] {
  padding: 0 0.5rem;
  font-size: 1.1rem;
  width: 100%;
  height: 3rem;
  border: none;
  background-color: hsl(220, 33%, 90%);
  color: var(--second-color-alt);
  transition: background-color 300ms;
}
input[type="text"]:focus {
  outline: none;
  background-color: hsl(220, 33%, 95%);
}
input[type="text"]::placeholder {
  color: var(--second-color-alt);
}
input[type="submit"] {
  cursor: pointer;
  background-image: linear-gradient(
    to top,
    var(--primary-color-alt),
    var(--primary-color)
  );
  color: var(--white-color-alt);
  margin: 1rem 0;
  border: none;
  width: 100%;
  height: 3rem;
  font-size: 1.2rem;
  transition: color 300ms;
}
input[type="submit"]:hover {
  background-image: linear-gradient(
    to bottom,
    var(--primary-color-alt),
    var(--primary-color)
  );
  color: var(--white-color);
}
/* =============== FOOTER =============== */
.top-footer {
  background-color: var(--second-color);
  display: flex;
  flex-direction: column;
}
.footer-title {
  font-weight: 500;
  font-size: 1.2rem;
  padding: 1rem 0;
  background-image: -webkit-linear-gradient(
    120deg,
    var(--primary-color-alt),
    var(--primary-color)
  );
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.footer-items h3 {
  cursor: pointer;
  font-weight: 300;
  font-size: 1.1rem;
  padding: 0.1rem 0;
  color: var(--white-color-alt);
}
.footer-items h3:hover {
  text-decoration: underline;
}
.footer-items h3:last-child {
  padding-bottom: 2rem;
}

.end-footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: var(--third-color);
}
.copyright {
  color: var(--white-color-alt);
  padding: 1rem 0;
  font-size: 0.9rem;
}
.copyright b {
  font-weight: inherit;
  font-size: 0.9rem;
}
.designer {
  color: hsla(0, 0%, 98%, 0.541);
  padding-bottom: 0.5rem;
  font-size: 0.9rem;
}
.designer:hover {
  text-decoration: underline;
}

/* =============== MEDIA QUERIES ======= */

@media screen and (max-width: 768px) {
  .container {
    padding: 0 1rem;
  }
  /* ================= HEADER ================ */
  header {
    padding: 0.5rem 1rem;
  }
  .navbar {
    background-color: var(--dark-color);
    position: absolute;
    top: 3.5rem;
    right: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    transform: scaleY(0);
    transform-origin: bottom;
    transition: transform 500ms;
  }
  .show-navbar {
    display: flex;
    transform: scaleY(1);
    transform-origin: top;
    transition: transform 300ms;
  }
  .nav-items {
    display: flex;
    flex-direction: column;
  }
  .nav-item {
    margin: 0.5rem 0;
  }
  .menu-toggle {
    display: block;
  }
  .bx-menu {
    display: block !important;
  }
  .show-bx {
    display: block !important;
  }
  .hide-bx {
    display: none !important;
  }
}
@media (min-width: 769px) {
  header {
    padding: 1rem 5rem;
  }
  /* ================= MAIN ================ */

  /* -------- HOME SECTION -------------- */
  .section-1 {
    justify-content: space-between;
    grid-template-columns: 1fr 1fr;
    padding: 10rem 5rem 0 5rem;
  }
  .slogan .company-title {
    max-width: 30rem;
    font-size: 1.8rem;
    letter-spacing: 0.5rem;
  }
  .slogan .company-slogan {
    max-width: 20rem;
    font-size: 1.3rem;
  }
  /* -------- OFFER SECTION ------------- */
  .section-2 {
    margin: 2rem 5rem;
  }
  .offer {
    margin: 5rem 0;
    align-items: center;
    justify-content: space-between;
    grid-template-rows: auto auto;
  }
  .offer-1 {
    grid-template-areas: "offer-1-img offer-desc-1";
  }
  .offer-1 img {
    background-color: var(--dark-color);
    padding: 2rem 0;
  }
  .offer-2 {
    grid-template-areas: "offer-desc-2 offer-2-img";
  }
  .offer-1-img {
    grid-area: offer-1-img;
  }
  .offer-2-img {
    grid-area: offer-2-img;
  }
  .offer-desc-1 {
    grid-area: offer-desc-1;
  }
  .offer-desc-2 {
    grid-area: offer-desc-2;
  }
  .offer-description .offer-title {
    font-size: 1.9rem;
    padding: 1.5rem 0 0.5rem 0;
  }
  .offer-description .offer-hook {
    max-width: 30rem;
  }
  .offer-description {
    background-color: var(--white-color-alt);
    padding: 2rem 1rem;
  }
  .offer-description .offer-title {
    padding: 0.5rem 0 1rem 0;
  }
  .offer-description .cart-btn {
    margin: 2rem 0 0.5rem 0;
  }
  /* -------- PRODUCT SECTION ----------- */
  .section-3 {
    gap: 5rem;
  }
  .product::before {
    transform: scaleY(0);
    transform-origin: bottom;
    transition: transform 300ms;
  }
  .product:hover::before {
    transform: scaleY(1);
    transform-origin: top;
    transition: transform 300ms;
  }
  .product_add_cart {
    transform: scaleY(0);
    transform-origin: bottom;
  }
  .product:hover .product_add_cart {
    transform: translate(-50%, -50%) scaleY(1);
    transform-origin: top;
  }
  /* -------- SPONSOR SECTION ----------- */
  .section-4 {
    margin: 5rem 0;
  }
  /* ========= SUBSCRIBE SECTION ========== */
  .section-5 {
    padding: 1rem 0;
  }
  .section-5 .subscribe-container {
    display: flex;
    align-items: center;
  }
  input[type="text"] {
    padding: 0 1rem;
    width: 15rem;
  }
  input[type="submit"] {
    width: 10rem;
  }
  /* =============== FOOTER =============== */
  .top-footer {
    flex-direction: row;
    justify-content: space-around;
    padding-bottom: 8rem;
    padding-top: 2rem;
  }
  .footer-title {
    font-size: 1rem;
    padding: 1rem 0;
  }
  .footer-items h3 {
    font-size: 0.9rem;
  }

  .end-footer {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: var(--third-color);
  }
  .copyright {
    color: hsla(0, 0%, 98%, 0.747);
    padding: 1rem 0;
    font-size: 0.8rem;
  }
  .copyright b {
    font-size: 0.7rem;
  }
  .designer {
    color: hsla(0, 0%, 98%, 0.322);
    font-size: 0.8rem;
  }
}

```
### index.js
```

'use strict'

const menuToggle = document.querySelector('.menu-toggle');
const bxMenu = document.querySelector('.bx-menu');
const bxX = document.querySelector('.bx-x');

const navBar = document.querySelector('.navbar');

// --- open menu ---

bxMenu.addEventListener('click', (e)=> {
    if(e.target.classList.contains('bx-menu')){
        navBar.classList.add('show-navbar');
        bxMenu.classList.add('hide-bx');
        bxX.classList.add('show-bx');
    }
})

// --- close menu ---

bxX.addEventListener('click', (e)=> {
    if(e.target.classList.contains('bx-x')){
        navBar.classList.remove('show-navbar');
        bxMenu.classList.remove('hide-bx');
        bxX.classList.remove('show-bx');
    }
})
```

# Step 11: Flask Include Statements
# Include repetitive sections(navbars, footer) on diffrent pages
# Syntax : {% include 'document.html' %}

### Footer Page Code:
```
 <div class="footer">
    <div class="container">
        <div class="row">
            <div class="col-lg-4 col-sm-4 col-xs-12">
                <div class="single_footer">
                    <h4>Services</h4>
                    <ul>
                        <li><a href="#">Lorem Ipsum</a></li>
                        <li><a href="#">Simply dummy text</a></li>
                        <li><a href="#">The printing and typesetting </a></li>
                        <li><a href="#">Standard dummy text</a></li>
                        <li><a href="#">Type specimen book</a></li>
                    </ul>
                </div>
            </div><!--- END COL -->
            <div class="col-md-4 col-sm-4 col-xs-12">
                <div class="single_footer single_footer_address">
                    <h4>Page Link</h4>
                    <ul>
                        <li><a href="#">Lorem Ipsum</a></li>
                        <li><a href="#">Simply dummy text</a></li>
                        <li><a href="#">The printing and typesetting </a></li>
                        <li><a href="#">Standard dummy text</a></li>
                        <li><a href="#">Type specimen book</a></li>
                    </ul>
                </div>
            </div><!--- END COL -->
            <div class="col-md-4 col-sm-4 col-xs-12">
                <div class="single_footer single_footer_address">
                    <h4>Subscribe today</h4>
                    <div class="signup_form">
                        <form action="#" class="subscribe">
                            <input type="text" class="subscribe__input" placeholder="Enter Email Address">
                            <button type="button" class="subscribe__btn"><i class="fas fa-paper-plane"></i></button>
                        </form>
                    </div>
                </div>
                <div class="social_profile">
                    <ul>
                        <li><a href="#"><i class="fab fa-facebook-f"></i></a></li>
                        <li><a href="#"><i class="fab fa-twitter"></i></a></li>
                        <li><a href="#"><i class="fab fa-google-plus-g"></i></a></li>
                        <li><a href="#"><i class="fab fa-instagram"></i></a></li>
                    </ul>
                </div>
            </div><!--- END COL -->
        </div><!--- END ROW -->
        <div class="row">
            <div class="col-lg-12 col-sm-12 col-xs-12">
                <p class="copyright">Copyright © 2019 <a href="#">Akdesign</a>.</p>
            </div><!--- END COL -->
        </div><!--- END ROW -->
    </div><!--- END CONTAINER -->
</div>
```

### On the static, create footer.css
### Paste the code Below:
```
h1,
h2,
h3,
h4,
h5,
h6 {}
a,
a:hover,
a:focus,
a:active {
    text-decoration: none;
    outline: none;
}

a,
a:active,
a:focus {
    color: #333;
    text-decoration: none;
    transition-timing-function: ease-in-out;
    -ms-transition-timing-function: ease-in-out;
    -moz-transition-timing-function: ease-in-out;
    -webkit-transition-timing-function: ease-in-out;
    -o-transition-timing-function: ease-in-out;
    transition-duration: .2s;
    -ms-transition-duration: .2s;
    -moz-transition-duration: .2s;
    -webkit-transition-duration: .2s;
    -o-transition-duration: .2s;
}

ul {
    margin: 0;
    padding: 0;
    list-style: none;
}
img {
max-width: 100%;
height: auto;
}
section {
    padding: 60px 0;
   /* min-height: 100vh;*/
}
.footer {
background: linear-gradient(105deg,#6e99e6 ,#093c94);
padding-top: 80px;
padding-bottom: 40px;
}
/*END FOOTER SOCIAL DESIGN*/
.single_footer{}
@media only screen and (max-width:768px) { 
.single_footer{margin-bottom:30px;}
}
.single_footer h4 {
color: #fff;
margin-top: 0;
margin-bottom: 25px;
font-weight: 700;
text-transform: uppercase;
font-size: 20px;
}
.single_footer h4::after {
content: "";
display: block;
height: 2px;
width: 40px;
background: #fff;
margin-top: 20px;
}
.single_footer p{color:#fff;}
.single_footer ul {
margin: 0;
padding: 0;
list-style: none;
}
.single_footer ul li{}
.single_footer ul li a {
color: #fff;
-webkit-transition: all 0.3s ease 0s;
transition: all 0.3s ease 0s;
line-height: 36px;
font-size: 15px;
text-transform: capitalize;
}
.single_footer ul li a:hover { color: #ff3666; }

.single_footer_address{}
.single_footer_address ul{}
.single_footer_address ul li{color:#fff;}
.single_footer_address ul li span {
font-weight: 400;
color: #fff;
line-height: 28px;
}
.contact_social ul {
list-style: outside none none;
margin: 0;
padding: 0;
}

/*START NEWSLETTER CSS*/
.subscribe {
display: block;
position: relative;
margin-top: 15px;
width: 100%;
}
.subscribe__input {
background-color: #fff;
border: medium none;
border-radius: 5px;
color: #333;
display: block;
font-size: 15px;
font-weight: 500;
height: 60px;
letter-spacing: 0.4px;
margin: 0;
padding: 0 150px 0 20px;
text-align: center;
text-transform: capitalize;
width: 100%;
}
@media only screen and (max-width:768px) { 
.subscribe__input{padding: 0 50px 0 20px;}
}

.subscribe__btn {
background-color: transparent;
border-radius: 0 25px 25px 0;
color: #01c7e9;
cursor: pointer;
display: block;
font-size: 20px;
height: 60px;
position: absolute;
right: 0;
top: 0;
width: 60px;
}
.subscribe__btn i{transition: all 0.3s ease 0s;}
@media only screen and (max-width:768px) { 
.subscribe__btn{right:0px;}
}

.subscribe__btn:hover i{
color:#ff3666;
}
button {
padding: 0;
border: none;
background-color: transparent;
-webkit-border-radius: 0;
border-radius: 0;
}
/*END NEWSLETTER CSS*/

/*START SOCIAL PROFILE CSS*/
.social_profile {margin-top:40px;}
.social_profile ul{
list-style: outside none none;
margin: 0;
padding: 0;
}
.social_profile ul li{float:left;}
.social_profile ul li a {
text-align: center;
border: 0px;
text-transform: uppercase;
transition: all 0.3s ease 0s;
margin: 0px 5px;
font-size: 18px;
color: #fff;
border-radius: 30px;
width: 50px;
height: 50px;
line-height: 50px;
display: block;
border: 1px solid rgba(255,255,255,0.2);
}
@media only screen and (max-width:768px) { 
.social_profile ul li a{margin-right:10px;margin-bottom:10px;}
}
@media only screen and (max-width:480px) { 
.social_profile ul li a{
width:40px;
height:40px;
line-height:40px;
}
}
.social_profile ul li a:hover{
background:#ff3666;
border: 1px solid #ff3666;
color:#fff;
border:0px;
}
/*END SOCIAL PROFILE CSS*/
.copyright {
margin-top: 70px;
padding-top: 40px;
color:#fff;
font-size: 15px;
border-top: 1px solid rgba(255,255,255,0.4);
text-align: center;
}
.copyright a{color:#01c7e9;transition: all 0.2s ease 0s;}
.copyright a:hover{color:#ff3666;}

```








