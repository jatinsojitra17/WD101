<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration Form</title>
    <style>
        body{
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            /* overflow: hidden; */
        }
        .container{
            width: 400px;
            height: 475px;
            background-color: blue;
            border-radius: 30px;
            font-size: 25px;
        }
        h2{
            text-align: center;
            font-size: 30px;
        }
        label{
            margin-left: 10px;
            font-weight:bold;
        }
        button{
            width: 100px;
            height: 60px;
            background-color: greenyellow;
            color: black;
            font-size: 25px;
            border-radius: 30px;
            margin-left: 10px;
        }
        .name{
            margin-left: 100px;
            width:200px;
            font-size: 25px;
        }
        .email{
            margin-left: 100px;
            width:200px;
            font-size: 25px;
        }
        .password{
            margin-left: 65px;
            width:200px;
            font-size: 25px;
        }
        .date{
            margin-left: 25px;
            width:200px;
            font-size: 25px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Registration Form</h2>
        <form id="user-form">
            <label for="name">Name</label>
            <input type="text" id="name" name="name" class="name" placeholder="Enter Name" required><br><br>

            <label for="email">Email</label>
            <input type="email" id="email" name="email" class="email" placeholder="Enter Email" required><br><br>

            <label for="password">Password</label>
            <input type="password" id="password" name="password" class="password" placeholder="Enter Password" required><br><br>

            <label for="dob">Date Of Birth</label>
            <input type="date" id="date" name="date" class="date" required><br><br>

            <label for="acceptTerms">Accept Terms & Condition</label>
            <input type="checkbox" id="acceptTerms" name="acceptTerms" required><br><br>

            <button type="submit">Submit</button>
        </form>
    </div>
    <div>
        <h2>Entries</h2>
        <div id="user-entries"></div>
    </div>
</body>
<script>
    let userForm = document.getElementById("user-form");

    const retrieveEntries = () => {
        let entries = localStorage.getItem("user-entries");
        if(entries){
            entries = JSON.parse(entry);
        }
        else{
            entries = [];
        }
        return entries;
    }
    let userEntries = retrieveEntries();

    const displayEntries = () => {
        const entries = retrieveEntries();

        const tableEntries = entries.map((entry) => {
            const namecell = '<td class="border px-4 py-2">${entry.name}</td>';
            const emailcell = '<td class="border px-4 py-2">${entry.email}</td>';
            const passwordcell = '<td class="border px-4 py-2">${entry.password}</td>';
            const dobcell = '<td class="border px-4 py-2">${entry.dob}</td>';
            const accepttermscell = '<td class="border px-4 py-2">${entry.acceptedTermsAndconditions}</td>';

            const row = '<tr>${namecell} ${emailcell} ${passwordcell} ${dobcell} ${accepttermscell}</tr>';
            return row;
        }).join("\n");

        const table = '<table class="table-auto w-full"><tr><th class="px-4 py-2">Name</th><th class="px-4 py-2">Email</th> <th class="px-4 py-2">Password</th> <th class="px-4 py-2">Dob</th> <th class="px-4 py-2">Accepted Terms?</th></tr>${tableEntries}</table>';

        let details = document.getElementById("user-entries");
        details.innerHTML = table;
    }
    const saveUserForm = (event) => {
        event.preventDefault();
        const name = document.getElementById("name").value;
        const email = document.getElementById("email").value;
        const password = document.getElementById("password").value;
        const dob = document.getElementById("dob").value;

        const acceptedTermsAndconditions = document.getElementById("acceptTerms").checked;

        const entry = {
            name,email,password,dob,acceptedTermsAndconditions
        };

        userEntries.push(entry);

        localStorage.setItem("user-entries",JSON.stringify(userEntries));
        displayEntries();
    }
    userform.addEventListener("submit",saveUserForm);
    displayEntries();
</script>
</html>
