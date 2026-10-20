::page{title="Create the Register and Login Pages"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

**Estimated duration**: 50 mins

Welcome to **Create the Register and Login Pages**. In a previous lab, you developed `MainPage.js` and `Navbar.js`.

You will create two React components in this lab: RegistrationPage and LoginPage. You will facilitate user registration and login functionalities using the `useState` hook.

Both components manage form input states for user details like first name, last name, email, and password. You will render input fields and buttons for users to enter their credentials and handle the form submission functionality, handled by handleRegister() and handleLogin() functions.

## Objectives

- Create React components, `RegisterPage` and `LoginPage`, to facilitate user registration and login functionalities.

- Manage form input states by utilizing the `useState` hook to dynamically manage the state of form inputs, ensuring real-time updates as users interact with the forms.

- Implement handleRegister() and handleLogin() functions within the components to manage form submission events, enabling users to register and log in securely.

- Utilize react-router-dom to enable navigation between the registration and login pages to facilitate smooth transitions within the application.

## Prerequisite

Ensure you have completed the previous modules and pushed all the changes to GitHub. You should already have either:
- the updated `giftlink-frontend` directory in your repository cloned to your local environment
OR
- you will clone the repository, which contains all the code you pushed as a part of the previous lab before starting this lab.

This will be your working directory for this lab.



::page{title="Step 1: Develop the RegisterPage component"}

In this step, you will work with two files, RegisterPage.js and RegisterPage.css, to implement its style.


`RegisterPage.css` will be used to style the RegisterPage component.
### Task

1. Create a **RegisterPage** folder within the **components** folder.
2. Create a `RegisterPage.js` and a `RegisterPage.css` files.

3. Add styling for the `RegisterPage` in `RegisterPage.css`.

<details>
<summary>Click here for a sample style page</summary>

	.register-card {
		background-color: #fff;
		box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
	}

	.register-card .form-label {
		font-weight: 600;
	}

	.register-card input {
		border-radius: 0.25rem;
	}

	.register-card .btn {
		padding: 0.5rem 1rem;
		border-radius: 0.25rem;
	}

	.register-card .btn-primary {
		background-color: #0056b3;
		border: none;
	}

	.register-card .btn-secondary {
		background-color: #dc3545;
		border: none;
	}

	.register-card .text-primary {
		color: #0056b3;
	}

	.register-card .text-secondary {
		color: #6c757d;
	}

	/* Additional styles */
	a.text-primary:hover {
		text-decoration: underline;
	}

	a.text-secondary:hover {
		text-decoration: underline;
	}

</details>

4. Store all of these attributes firstName, lastName, email and password as states.

5. Define a method `handleRegister` to be invoked when the user clicks the `Register` button. At this point, you should just print a message to the console in its place.

6. Create input elements for registration with the following user information in the labeled text boxes in the `RegisterPage.js`.
- firstName
- lastName
- email
- password

7. Add a `Register` button which on click invokes the `handleRegister` function.

#### Code template

```js
import React, { useState } from 'react';

import './RegisterPage.css';

function RegisterPage() {

    //insert code here to create useState hook variables for firstName, lastName, email, password

    // insert code here to create handleRegister function and include console.log

         return (
            <div className="container mt-5">
                <div className="row justify-content-center">
                    <div className="col-md-6 col-lg-4">
                        <div className="register-card p-4 border rounded">
                            <h2 className="text-center mb-4 font-weight-bold">Register</h2>

                    {/* insert code here to create input elements for all the variables - firstName, lastName, email, password */}

					{/* insert code here to create a button that performs the `handleRegister` function on click */}
						<p className="mt-4 text-center">
							Already a member? <a href="/app/login" className="text-primary">Login</a>
						</p>

             			</div>
                    </div>
                </div>
            </div>

         )//end of return
}

export default RegisterPage;

```

### Hints

Create useState hook variables

<details>
<summary>Click here for a hint</summary>

Use `const [firstName, setFirstName] = useState('');`.

```js
    const [firstName, setFirstName] = useState('');
    const [lastName, setLastName] = useState('');
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
```

</details>

Create handleRegister function

<details>
<summary>Click here for a hint</summary>

Use `const handleRegister = async () => {...}`

```js
    const handleRegister = async () => {
		console.log("Register invoked")
	}
```
</details>


Create a form for these variables
<details>
<summary>Click here for a hint</summary>

```html

	<div className="mb-4">

		<label htmlFor="firstName" className="form label"> FirstName</label><br>
		<input
		id="firstName"
		type="text"
		className="form-control"
		placeholder="Enter your firstName"
		value={firstName}
		onChange={(e) => setFirstName(e.target.value)}
		/>
	</div>

```
   </details>

Create a button
   <details>
	   <summary>Click here for a hint</summary>

```
	<button className="btn btn-primary w-100 mb-3" onClick={handleRegister}>Register</button>
````
   </details>

::page{title="Step 2: Develop the login page component"}

### Tasks

1. Create the **LoginPage** folder under the **components** folder and then create `LoginPage.js` and `LoginPage.css`.
`LoginPage.css` will be used to style the LoginPage component.

2. Create the Login form component inside `LoginPage.js`.

3. Add styling for the `LoginPage` in `LoginPage.css`.

<details><summary>Click here for sample</summary>

```css
.login-card {
    background-color: #fff;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.login-card .form-label {
    font-weight: 600;
}

.login-card input {
    border-radius: 0.25rem;
}

.login-card .btn {
    padding: 0.5rem 1rem;
    border-radius: 0.25rem;
}

.login-card .btn-primary {
    background-color: #0056b3;
    border: none;
}

.login-card .btn-secondary {
    background-color: #dc3545;
    border: none;
}

.login-card .text-primary {
    color: #0056b3;
}

.login-card .text-secondary {
    color: #6c757d;
}

/* Additional styles */
a.text-primary:hover {
    text-decoration: underline;
}

a.text-secondary:hover {
    text-decoration: underline;
}

```
</details>
4. Store the email and password as states.


5. Define a method `handleLogin` to be invoked when the user clicks the `Login` button. At this point, you should just print a message to the console in its place.

6. Create input elements for login using email and password, with labeled text boxes in the `LoginPage.js`.

7. Add a `Login` button which on click invokes the `handleLogin` function.



#### Code template

```javascript

import React, { useState } from 'react';
import './LoginPage.css';

function LoginPage() {

    //insert code here to create useState hook variables for email, password

    // insert code here to create handleLogin function and include console.log

		return (
      <div className="container mt-5">
        <div className="row justify-content-center">
          <div className="col-md-6 col-lg-4">
            <div className="login-card p-4 border rounded">
              <h2 className="text-center mb-4 font-weight-bold">Login</h2>

  		{/* insert code here to create input elements for the variables email and  password */}

  		{/* insert code here to create a button that performs the `handleLogin` function on click */}
				<p className="mt-4 text-center">
					New here? <a href="/app/register" className="text-primary">Register Here</a>
				</p>

            </div>
          </div>
        </div>
      </div>
    )
}

export default LoginPage;
```

### Hints

Create useState hook variables
<details>
<summary>Click here for a hint</summary>

Use `const [email, setEmail] = useState('');`.

```js
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
```
</details>

Create handleLogin function
<details>
<summary>Click here for a hint</summary>

Use `const handleLogin = async (e) => {...}`

```js
    const handleLogin = async () => {
        console.log("Inside handleLogin");
	}

```
</details>


Create input elements for the email and password variables.
   <details>
	   <summary>Click here for a hint</summary>

```html
<div className="mb-3">
	<label htmlFor="email" className="form-label">Email</label>
	<input
		id="email"
		type="text"
		className="form-control"
		placeholder="Enter your email"
		value={email}
		onChange={(e) => setEmail(e.target.value)}
	/>
</div>
```
</details>

Create button
<details>
<summary>Click here for a hint</summary>

```
<button className="btn btn-primary w-100 mb-3" onClick={handleLogin}>Login</button>
```
 </details>

::page{title="Step 3: Create routes in App.js"}

The App.js file contains the main Express application.

### Tasks

1. Go to `App.js` and import `RegisterPagee.js` `LoginPage.js`.
2. Create routes for both RegisterPage and LoginPage components under `<Routes></Routes>`

```javascript
import React from 'react';
import { Routes, Route, useNavigate } from 'react-router-dom';
import MainPage from './components/MainPage/MainPage';
import LoginPage from './components/LoginPage/LoginPage';
import RegisterPage from './components/RegisterPage/RegisterPage';
import 'bootstrap/dist/css/bootstrap.min.css';
import './App.css';
import Navbar from './components/Navbar/Navbar';
function App() {
  const navigate = useNavigate();
  return (
		<>
        <Navbar/>
        <Routes>
          <Route path="/" element={<MainPage />} />
          <Route path="/app" element={<MainPage />} />
          <Route path="/app/login" element={<LoginPage/>} />
          <Route path="/app/register" element={<RegisterPage />} />
        </Routes>
        </>
  );
}
export default App;
```


::page{title="Step 4: Push changes to GitHub"}

After implementing and testing the API endpoints, push your changes to GitHub.

### Task

1. Use Git commands to add, commit, and push your changes.
2. Use your prsonal Access Token for authentication when prompted.

### Hints
1. Hint for staging changes
   <details>
	   <summary>Click here for a hint</summary>
	   Stage all changes with `git add .`
   </details>

2. Hint for committing changes
   <details>
	   <summary>Click here for a hint</summary>
	   Commit your changes with a message using `git commit -m "Implemented API endpoints"`
   </details>

3. Hint for pushing to GitHub
<details>
	   <summary>Click here for a hint</summary>
	   Push the changes to the remote repository using `git push`
</details>

### Solution for RegisterPage.js

<details><summary>Click here to see the solution.</summary>


```js
import React, { useState } from 'react';

import './RegisterPage.css';

function RegisterPage() {
    const [firstName, setFirstName] = useState('');
    const [lastName, setLastName] = useState('');
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

    const handleRegister = async () => {
        console.log("Register invoked")
    }

return (
    <div className="container mt-5">
        <div className="row justify-content-center">
            <div className="col-md-6 col-lg-4">
                <div className="register-card p-4 border rounded">
                    <h2 className="text-center mb-4 font-weight-bold">Register</h2>
                    <div className="mb-3">
                        <label htmlFor="firstName" className="form-label">FirstName</label>
                        <input
                            id="firstName"
                            type="text"
                            className="form-control"
                            placeholder="Enter your firstName"
                            value={firstName}
                            onChange={(e) => setFirstName(e.target.value)}
                        />
                    </div>

                    {/* last name */}

                    <div className="mb-3">
                        <label htmlFor="lastName" className="form-label">LastName</label>
                        <input
                            id="lastName"
                            type="text"
                            className="form-control"
                            placeholder="Enter your lastName"
                            value={lastName}
                            onChange={(e) => setLastName(e.target.value)}
                        />
                    </div>

                    {/* email  */}
                    <div className="mb-3">
                        <label htmlFor="email" className="form-label">Email</label>
                        <input
                            id="email"
                            type="text"
                            className="form-control"
                            placeholder="Enter your email"
                            value={email}
                            onChange={(e) => setEmail(e.target.value)}
                        />
                    </div>

                    <div className="mb-4">
                        <label htmlFor="password" className="form-label">Password</label>
                        <input
                            id="password"
                            type="password"
                            className="form-control"
                            placeholder="Enter your password"
                            value={password}
                            onChange={(e) => setPassword(e.target.value)}
                        />
                    </div>
                    <button className="btn btn-primary w-100 mb-3" onClick={handleRegister}>Register</button>
                    <p className="mt-4 text-center">
                        Already a member? <a href="/app/login" className="text-primary">Login</a>
                    </p>
                </div>
            </div>
        </div>
    </div>
);
}

export default RegisterPage;
```

</details>

### Solution for LoginPage.js

<details><summary>Click here to see the solution</summary>

	import React, { useState,useEffect } from 'react';

	import './LoginPage.css';

	function LoginPage() {
		const [email, setEmail] = useState('');
		const [password, setPassword] = useState('');

		const handleLogin = async (e) => {
			e.preventDefault();
	}


		return (
			<div className="container mt-5">
				<div className="row justify-content-center">
					<div className="col-md-6 col-lg-4">
						<div className="login-card p-4 border rounded">
							<h2 className="text-center mb-4 font-weight-bold">Login</h2>
							<div className="mb-3">
								<label htmlFor="email" className="form-label">Email</label>
								<input
									id="email"
									type="text"
									className="form-control"
									placeholder="Enter your email"
									value={email}
									onChange={(e) => setEmail(e.target.value)}
								/>
							</div>
							<div className="mb-4">
								<label htmlFor="password" className="form-label">Password</label>
								<input
									id="password"
									type="password"
									className="form-control"
									placeholder="Enter your password"
									value={password}
									onChange={(e) => setPassword(e.target.value)}
								/>
							</div>
							{/* Include appropriate error message if login is incorrect*/}
							<button className="btn btn-primary w-100 mb-3" onClick={handleLogin}>Login</button>
							<p className="mt-4 text-center">
								New here? <a href="/app/register" className="text-primary">Register Here</a>
							</p>
						</div>
					</div>
				</div>
			</div>
		);
	}

	export default LoginPage;
</details>


### **Assessment**: 
For both **Option 1: AI-Graded Submission and Evaluation** and **Option 2: Peer-Graded Submission and Evaluation:**
Copy and paste the the public Github URLs of `RegisterPage.js`and `LoginPage.js` and save it in a text file.

## Author

Skills Network
<!--
## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2025-11-18 | 0.3 | Manvi Gupta | Created and updated lab for Mark and PR |
| 2024-02-21 | 0.2 | Mary Stenberg | QA review    |
| 2024-01-17 | 0.1 | UL | Initial version created |
-->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
