::page{title="Implement Back-end in Register Component"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

<hr>

**Estimated duration**: 40 mins

Welcome to **Implement Backend in Register Component**. In a previous lab, you developed the user interface for registration containing form fields to intake user details, which includes state management for input values.

In this lab, you will call an API in the `RegisterPage` component to register the user on form click of the `Register` button. Upon successful registration you will store the authentication token in session storage and redirect to `/app`. You will also display registration errors from the backend, below the email input.

## Objectives

- Enhance client-side form handling by using the states to obtain user input for first name, last name, email, and password in the `handleRegister` function that you defined earlier with just a console log inside `RegisterPage`.

- Integrate the call to the backend API in `handleRegister`.

- Handle asynchronous API responses, specifically interpreting and processing the JSON data returned from the registration endpoint.

- Handle authorization by extracting the Bearer token in the API response and storing it in the session for enhancing security.

- Provide appropriate error messages for registration failure.


## Prerequisite

Ensure that you have completed the previous tasks and pushed all the changes to GitHub. You should have already updated `giftlink-backend` and `giftlink-frontend` directories in your repository from the previous lab.

Clone the repository to this local environment that contains all the code that you pushed as a part of the previous lab before starting this lab, as these will be your working directories for the lab.

::page{title="Registration Tasks"}

In this lab, you will complete two steps to complete the asynchronous `handleRegiser()` function. The stucture of these tasks should look like the template below where each task will be developed in each step of this lab.


```javascript
const handleRegister = async () => {
	try{
		//Step 1: Implement API call
		//Step 2: Access data, login, set the AuthContext and set user details
}
```
You will also update the `navbar.js` file so rather than display the login and register buttons, it will display a logout button and the username.

This code will be provided to you in Step 3.

::page{title="Step 1: Implement API call for handleRegister()"}

In this step you will access the `giftlink-frontend/src/config.js` in the `RegisterPage.js` to obtain the URL for the backend API.

You will also need the `useAppContext` from `giftlink-frontend/context/AuthContext.js` to maintain the login status globally for the application.

Call the API to implement the `handleRegister()` functionality. You need to set its method, headers, and body.

### Tasks
1. Import urlConfig from `giftlink-frontend/src/config.js`
2. Import useAppContext `giftlink-frontend/context/AuthContext.js`
3. Import useNavigate from `react-router-dom` to handle navigation after successful registration.
4. Include a state for error message.
5. Create a local variable for `navigate` and `setIsLoggedIn`.
6. Set the POST method
7. Set the headers section
8. Set the body section to send user details


#### Code Template

```javascript
//{{Insert code here}} //Task 1: Import urlConfig from `giftlink-frontend/src/config.js`
//{{Insert code here}} //Task 2: Import useAppContext `giftlink-frontend/context/AuthContext.js`
//{{Insert code here}} //Task 3: Import useNavigate from `react-router-dom` to handle navigation after successful registration.
.
.
.
//Do these tasks inside the RegisterPage function, after the useStates definition
//{{Insert code here}} //Task 4: Include a state for error message.
//{{Insert code here}} //Task 5: Create a local variable for `navigate`   and `setIsLoggedIn`.
.
.
.
const handleRegister = async () => {
	try{
      const response = await fetch(`${urlConfig.backendUrl}/api/auth/register`, {
		   //{{Insert code here}} //Task 6: Set method
           //{{Insert code here}} //Task 7: Set headers
           //{{Insert code here}} //Task 8: Set body to send user details
	 })
	  }catch (e) {
        console.log("Error fetching details: " + e.message);
    }
}
```

### Hints

Task 1: Import urlConfig from `giftlink-frontend/src/config.js`

<details><summary>Click here for hint</summary>

```
import {urlConfig} from '../../config';
```
</details>

Task 2: Import useAppContext `giftlink-frontend/context/AuthContext.js`

<details><summary>Click here for hint</summary>

```
import { useAppContext } from '../../context/AuthContext';
```
</details>

Task 3: Import useNavigate from `react-router-dom` to handle navigation after successful registration.

<details><summary>Click here for hint</summary>

```
import { useNavigate } from 'react-router-dom';
```
</details>

Task 4: Include a state for error message.

<details><summary>Click here for hint</summary>

```
const [showerr, setShowerr] = useState('');
```
</details>

Task 5: Create a local variable for `navigate`   and `setIsLoggedIn`.

<details>
<summary>Click here for hint</summary>
	
```js
const navigate = useNavigate();
const { setIsLoggedIn } = useAppContext();
```
</details>


Task 6: Set POST method

<details>
<summary>Click here for a hint</summary>

Use `method: 'POST'` to post user details
</details>

Task 7: Set headers

<details>
<summary>Click here for a hint</summary>

```
	headers: {
	    'content-type': 'application/json',
	},
```
</details>

Task 8: Set the body section to send user details

<details>
<summary>Click here for a hint</summary>

Use `body: JSON.stringify` to set body variables that send user details to the backend.
```
body: JSON.stringify({
                firstName: firstName,
                lastName: lastName,
                email: email,
                password: password
            })
```
</details>

::page{title="Step 2: Access data and set user details coming from backend"}

Next, you need to access the data sent from the backend in JSON format and also set the user details.

### Tasks

1. Access data in JSON format as a response from the back end
2. Set user details in session storage
3. Set the state of user to logged in using the `useAppContext`.
4. Navigate to the MainPage after logging in.
5. Set an error message if the registration fails.
6. Display error message to end user.

#### Code Template

```javascript
const handleRegister = async () => {
	try{
		//{code from Step 1}
		// Task 1: Access data coming from fetch API
		// Task 2: Set user details
		// Task 3: Set the state of user to logged in using the `useAppContext`.
		// Task 4: Navigate to the MainPage after logging in.
		// Task 5: Set an error message if the registration fails.
		// Task 6: Display error message to enduser.
}
```
### Hints
Task 1: Access data coming from fetch API

<details>
<summary>Click here for a hint</summary>

```
const json = await response.json();
```
</details>

Task 2: Set user details

<details>
<summary>Click here for a hint</summary>

Use `sessionStorage.setItem('<attr>','<val>')`

```
if (json.authtoken) {
            sessionStorage.setItem('auth-token', json.authtoken);
            sessionStorage.setItem('name', firstName);
            sessionStorage.setItem('email', json.email);
			//insert code for setting logged in state
			//insert code for navigating to MainPAge
}
```
</details>

Task 3: Set the state of user to logged in using the `useAppContext`

<details>
<summary>Click here for a hint</summary>

Use `setIsLoggedIn(true);`
</details>

Task 4: Navigate to the MainPage after logging in

<details>
<summary>Click here for a hint</summary>

Use `navigate('/app')`
</details>

Task 5: Set an error message if the registration fails.

<details>
<summary>Click here for a hint</summary>

```
if (json.error) {
setShowerr(json.error);
}
```
</details>

Task 6: Display error message to end user

<details>
<summary>Click here for a hint</summary>

In the placeholder provided to include the error message inside the return function add the code given below.

```
<div className="text-danger">{showerr}</div>
```
</details>


::page{title="Step 3: Update the navbar.js file"}

When the user registers, the user is logged in. Once the user has logged in to the website, rather than display the login and register buttons, the navbar needs to display a logout button and the username. You can use the code below to do so.

```javascript
import React, { useEffect } from 'react'
import { Link, useNavigate } from 'react-router-dom'
import {urlConfig} from '../../config';
import { useAppContext } from '../../context/AuthContext';

export default function Navbar() {
    const { isLoggedIn, setIsLoggedIn, userName, setUserName } = useAppContext();

  const navigate=useNavigate();
    useEffect(() => {
        const authTokenFromSession = sessionStorage.getItem('auth-token');
        const nameFromSession = sessionStorage.getItem('name');
        if (authTokenFromSession) {
            if(isLoggedIn && nameFromSession) {
              setUserName(nameFromSession);
            } else {
              sessionStorage.removeItem('auth-token');
              sessionStorage.removeItem('name');
              sessionStorage.removeItem('email');
              setIsLoggedIn(false);
            }
        }
    },[isLoggedIn, setIsLoggedIn, setUserName])
    const handleLogout=()=>{
        sessionStorage.removeItem('auth-token');
        sessionStorage.removeItem('name');
        sessionStorage.removeItem('email');
        setIsLoggedIn(false);
        navigate(`/app`);

    }
    const profileSecton=()=>{
      navigate(`/app/profile`);
    }
    return (
        <>
            <nav className="navbar navbar-expand-lg navbar-light bg-light" id='navbar_container'>
        <a className="navbar-brand" href={`${urlConfig.backendUrl}/app`}>GiftLink</a>

        <button className="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span className="navbar-toggler-icon"></span>
        </button>

        <div className="collapse navbar-collapse justify-content-end" id="navbarNav">
          <ul className="navbar-nav">
            <li className="nav-item">
              <a className="nav-link" href="/home.html">Home</a> {/* Link to home.html */}
            </li>
            <li className="nav-item">
              <Link className="nav-link" to="/app">Gifts</Link> {/* Updated Link */}
            </li>
            <li className="nav-item">
              <Link className="nav-link" to="/app/search">Search</Link>
            </li>
            <ul className="navbar-nav ml-auto">
            {isLoggedIn ? (
                                    <>
                                    <li className="nav-item"> <span className="nav-link" style={{color: "black", cursor:"pointer"}} onClick={profileSecton}>Welcome, {userName}</span> </li>
                                    <li className="nav-item"><button className="nav-link login-btn" onClick={handleLogout}>Logout</button></li>
                                    </>
                                    )  : (
                                    <>
                                        <li className="nav-item">

                                        <Link className="nav-link login-btn" to="/app/login">Login</Link>
                                        </li>
                                        <li className="nav-item">
                                        <Link className="nav-link register-btn" to="/app/register">Register</Link>
                                        </li>
                                    </>
                                )

                                }
            </ul>
          </ul>
        </div>
      </nav>
        </>
    )
}
```

::page{title="Step 4: Push changes to GitHub"}

It is highly recommended that you test your project at this point before you proceed to the next step. You should be able to see:
1. The main page listing all the gift items.
2. The search page where you can search the gifts.
3. You should be able to register a user.

### Tasks

Task 1: Stage changes
Task 2: Commit changes
Task 3: Push changes

### Hints for Git Commands

1. Hint for staging changes

<details>
<summary>Click here for a hint</summary>

Use `git add .` to stage all your changes for commit
</details>

2. Hint for committing changes

<details>
<summary>Click here for a hint</summary>

Commit your staged changes with `git commit -m "Your message here"`
</details>

3. Hint for pushing to GitHub

<details>
<summary>Click here for a hint</summary>

Finally, push your commits to GitHub with `git push`
</details>

::page{title="Step 5: Final Solution"}

## Solution

<details><summary>Click here for the sample solution</summary>

```javascript
	import React, { useState } from 'react';
	//Step 1 - Task 1
	import {urlConfig} from '../../config';

	//Step 1 - Task 2
	import { useAppContext } from '../../context/AuthContext';

	//Step 1 - Task 3
	import { useNavigate } from 'react-router-dom';

	import './RegisterPage.css';

	function RegisterPage() {
		const [firstName, setFirstName] = useState('');
		const [lastName, setLastName] = useState('');
		const [email, setEmail] = useState('');
		const [password, setPassword] = useState('');

		//Step 1 - Task 4
 		const [showerr, setShowerr] = useState('');

		//Step 1 - Task 5
		const navigate = useNavigate();
		const { setIsLoggedIn } = useAppContext();

		const handleRegister = async () => {
			const response = await fetch(`${urlConfig.backendUrl}/api/auth/register`, {
				//Step 1 - Task 6
				method: 'POST',
				//Step 1 - Task 7
				headers: {
					'content-type': 'application/json',
				},
				//Step 1 - Task 8
				body: JSON.stringify({
					firstName: firstName,
					lastName: lastName,
					email: email,
					password: password
				})
			});

			//Step 2 - Task 1
			const json = await response.json();
			console.log('json data', json);
			console.log('er', json.error);

			//Step 2 - Task 2
			if (json.authtoken) {
				sessionStorage.setItem('auth-token', json.authtoken);
				sessionStorage.setItem('name', firstName);
				sessionStorage.setItem('email', json.email);
			//Step 2 - Task 3
				setIsLoggedIn(true);
			//Step 2 - Task 4
				navigate('/app');
			}
			if (json.error) {
			//Step 2 - Task 5
				setShowerr(json.error);
			}
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
							{/* Step 2 - Task 6*/}

									<div className="text-danger">{showerr}</div>
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



## Author:

Skills Network
<!--
## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2024-01-17 | 0.1 | UL | Initial version created |
| 2024-02-01 | 0.2 | Mercedes Schneider | QA pass with edits |
|2026-01-30  | 0.1 | Manvi Gupta | Created and updated lab for Mark and PR |
-->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
