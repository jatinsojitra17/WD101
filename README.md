// localStorage.clear();
        let date_picker = document.getElementById('dob');
        let now = new Date();
        let day = now.getDate().toString().padStart(2, '0');
        let month = (now.getMonth() + 1).toString().padStart(2, '0');
        let year = now.getFullYear();

        date_picker.min = (year - 55) + "-" + month + "-" + day;
        date_picker.max = (year - 18) + "-" + month + "-" + day;

        const retriveEntries = () => {
            let entries = localStorage.getItem("user-entries");

            if (entries) {
                entries = JSON.parse(entries);
            }
            else {
                entries = [];
            }

            return entries;
        }

        let userForm = document.getElementById("user-form");
        let userEntries = retriveEntries();

        const displayEntries = () => {
            const entries = retriveEntries();
            const tableEntries = entries.map(entry => {
                const nameCell = `<td class='border px-4 py-2'>${entry.name}</td>`;
                const emailCell = `<td class='border px-4 py-2'>${entry.email}</td>`;
                const passwordCell = `<td class='border px-4 py-2'>${entry.password}</td>`;
                const dobCell = `<td class='border px-4 py-2'>${entry.dob}</td>`;
                const acceptTermsCell = `<td class='border px-4 py-2'>${entry.acceptedTermsAndconditions}</td>`;

                const row = `<tr> ${nameCell} ${emailCell} ${passwordCell} ${dobCell} ${acceptTermsCell} </tr>`;
                return row;
            }).join('\n');

            const table = `
                <table class="table-auto w-full">
                    <tr>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Email</th>
                        <th class="px-4 py-2">Password</th>
                        <th class="px-4 py-2">Dob</th>
                        <th class="px-4 py-2">Accepted terms?</th>
                    </tr>
                    ${tableEntries}
                </table>`;

            let details = document.getElementById('user-entries');
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
                name,
                email,
                password,
                dob,
                acceptedTermsAndconditions
            };

            userEntries.push(entry);

            localStorage.setItem("user-entries", JSON.stringify(userEntries));

            displayEntries();
        }

        userForm.addEventListener("submit", saveUserForm);

        displayEntries();
