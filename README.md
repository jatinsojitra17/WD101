<!DOCTYPE html>
<html>

<head>
    <title>Registration Form</title>
    <!-- <link rel="stylesheet" href="style.css"> -->
    <style>
        body {
            font-family: Arial, sans-serif;
        }

        h1,
        h2 {
            text-align: center;
        }

        form {
            margin: 0 auto;
            width: 50%;
            border: 1px solid #ccc;
            padding: 10px;
            border-radius: 5px;
        }

        label {
            display: inline-block;
            width: 30%;
            text-align: right;
            margin-right: 5px;
        }

        input[type="text"],
        input[type="email"],
        input[type="password"],
        input[type="date"] {
            width: 60%;
            padding: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        input[type="checkbox"] {
            margin-left: 35%;
        }

        button[type="submit"] {
            margin-left: 30%;
            margin-top: 10px;
            padding: 5px 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #user-table {
            margin-top: 20px;
            border-collapse: collapse;
        }

        #user-table th,
        #user-table td {
            padding: 5px;
            border: 1px solid #ccc;
        }
    </style>
</head>

<body>
    <h1>Registration Form</h1>
    <form id="registration-form">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br>

        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br>

        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" name="dob" required><br>

        <label for="terms">I accept the terms and conditions:</label>
        <input type="checkbox" id="terms" name="terms" required><br>

        <button type="submit">Submit</button>
    </form>

    <h2>Registered Users</h2>
    <table id="user-table">
        <thead>
            <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Password</th>
                <th>Dob</th>
                <th>Accepted terms?</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

    <!-- <script src="script.js"></script> -->

</body>
<script>
    const form = document.getElementById('registration-form');
    const userTable = document.getElementById('user-table');
    const nameInput = document.getElementById('name');
    const emailInput = document.getElementById('email');
    const passwordInput = document.getElementById('password');
    const dobInput = document.getElementById('dob');
    const termsInput = document.getElementById('terms');

    // Load data from localStorage on page load
    window.addEventListener('load', () => {
        const users = JSON.parse(localStorage.getItem('users')) || [];
        users.forEach(user => {
            const row = userTable.insertRow();
            row.insertCell().textContent = user.name;
            row.insertCell().textContent = user.email;
            row.insertCell().textContent = user.password;
            row.insertCell().textContent = user.dob;
            row.insertCell().textContent = user.terms ? 'Yes' : 'No';
        });
    });

    // Add additional validation to date of birth input field
    dobInput.addEventListener('input', () => {
        const dob = new Date(dobInput.value);
        const age = (Date.now() - dob.getTime()) / (1000 * 60 * 60 * 24 * 365.25);
        if (age < 18 || age > 55) {
            dobInput.setCustomValidity('You must be between 18 and 55 years old to register');
        } else {
            dobInput.setCustomValidity('');
        }
    });

    // Handle form submission
    form.addEventListener('submit', (event) => {
        event.preventDefault();

        const user = {
            name: nameInput.value,
            email: emailInput.value,
            password: passwordInput.value,
            dob: dobInput.value,
            terms: termsInput.checked
        };

        const row = userTable.insertRow();
        row.insertCell().textContent = user.name;
        row.insertCell().textContent = user.email;
        row.insertCell().textContent = user.password;
        row.insertCell().textContent = user.dob;
        row.insertCell().textContent = user.terms ? 'Yes' : 'No';

        const users = JSON.parse(localStorage.getItem('users')) || [];
        users.push(user);
        localStorage.setItem('users', JSON.stringify(users));

        form.reset();
    });
    ``

</script>

</html>
