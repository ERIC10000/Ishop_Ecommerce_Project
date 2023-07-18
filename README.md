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







