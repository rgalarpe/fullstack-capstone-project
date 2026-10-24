::page{title="Implement Back-end in Login Component"}

**Estimated duration**: 40 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

Welcome to **Implement Backend in Login Component**. In a previous lab, you created a front-end login page containing form fields for users to log in with their credentials.

In this lab, you will call an API to obtain the login information upon form submission. On a successful login, you will store the authentication token in session storage and redirect to \'/app\'.

## Objectives

-  Develop and implement the `/api/auth/login` endpoint to handle user login requests.

- Integrate and handle authorization by including a bearer token in the API request headers, enhancing security during user login.

- Handle asynchronous API responses, specifically interpreting and processing the JSON data returned from the login endpoint.

- Enhance client-side form handling using a react state to manage user input for the user\'s email and password.

## Prerequisite

Ensure you have completed the previous tasks and pushed all the changes to GitHub. You should have already updated the `giftlink-backend` and `giftlink-frontend` directories in your repository from the previous lab.

Clone the repository to this local environment containing all the code you pushed as a part of the previous lab before starting this lab, as these will be your working directories for the lab.

::page{title="Login tasks"}

In this lab, you will complete two steps to write the asynchronous `handleLogin()` function. The structure of these tasks should look like the following template. You need to develop each task in each step of the lab.


```javascript
const handleLogin = async () => {
	try{
		//Step 1: Implement API call
		//Step 2: Access data and set user details
}
```

::page{title="Step 1: Implement API call for handleLogin()"}

Your first task is to call the API to implement the `handleLogin` functionality to set its method, headers, and body.

To begin, you will need to open the `LoginPage.js` file in your project under the `giftlink-frontend` folder.

### Tasks

1. Import urlConfig from `giftlink-frontend/src/config.js`
2. Import useAppContext `giftlink-frontend/context/AuthContext.js`
3. Import useNavigate from `react-router-dom` to handle navigation after successful registration.
4. Include a state for incorrect password.
5. Create a local variable for `navigate`, `bearerToken` and `setIsLoggedIn`.
6. If the bearerToken has a value (user already logged in), navigate to MainPage
7. Set the POST method
8. Set the headers section
9. Set the body section to send user details

#### Code template

```javascript
//{{Insert code here}} //Task 1: Import urlConfig from `giftlink-frontend/src/config.js`
//{{Insert code here}} //Task 2: Import useAppContext `giftlink-frontend/context/AuthContext.js`
//{{Insert code here}} //Task 3: Import useNavigate from `react-router-dom` to handle navigation after successful registration.
.
.
.
//Do these tasks inside the RegisterPage function after the useStates definition
//{{Insert code here}} //Task 4: Include a state for incorrect password.
//{{Insert code here}} //Task 5: Create a local variable for `navigate`,`bearerToken`   and `setIsLoggedIn`.

//{{Insert code here}} //Task 6. If the bearerToken has a value (user already logged in), navigate to MainPage
.
.

const handleLogin = async () => {
	try{
		//first task
      const response = await fetch(`/api/auth/login`, {
		   //{{Insert code here}} //Task 7: Set method
           //{{Insert code here}} //Task 8: Set headers
           //{{Insert code here}} //Task 9: Set body to send user details

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

Task 4: Include a state for the error message.

<details><summary>Click here for hint</summary>

```
const [incorrect, setIncorrect] = useState('');
```
</details>

Task 5: Create a local variable for `navigate`, `bearerToken`   and `setIsLoggedIn`.

<details>
<summary>Click here for hint</summary>

```js
const navigate = useNavigate();
const bearerToken = sessionStorage.getItem('bearer-token');
const { setIsLoggedIn } = useAppContext();
```
</details>

Task 6. If the bearerToken has a value (user already logged in), navigate to MainPage

<details>
<summary>Click here for a hint</summary>

```
useEffect(() => {
  if (sessionStorage.getItem('auth-token')) {
    navigate('/app')
  }
}, [navigate])
```
</details>

Task 7: Set the POST method

<details>
<summary>Click here for a hint</summary>

Use `method: 'POST'` to post user details
</details>

Task 8: Set headers
<details>
<summary>Click here for a hint</summary>
Remember to set the bearerToken also inside the headers.

```
        headers: {
          'content-type': 'application/json',
          'Authorization': bearerToken ? `Bearer ${bearerToken}` : '', // Include Bearer token if available
        },
```
</details>

Task 9: Set the body section to send user details

<details>
<summary>Click here for a hint</summary>

```
        body: JSON.stringify({    
          email: email,
          password: password,
        })
```
</details>

::page{title="Step 2: Access data and set user details coming from backend"}

Your second task is to access the data from the backend in JSON format and set the user details.

### Tasks

1. Access data in JSON format as a response from the back end
2. Set user details in session storage
3. Set the user\'s state to log in using the `useAppContext`
4. Navigate to the MainPage after logging in.
5. Clear input and set an error message if the password is incorrect
6. Display an error message to the user.

#### Code template

```javascript
const handleLogin = async () => {
	try{
		//{code from Step 1}
		// Task 1: Access data coming from fetch API
		// Task 2: Set user details
		// Task 3: Set the user's state to log in using the `useAppContext`.
		// Task 4: Navigate to the MainPage after logging in.
		// Task 5: Clear input and set an error message if the password is incorrect
		// Task 6: Display an error message to the user.
}
```

### Hints
Task 1: Access data coming from fetch API
<details>
<summary>Click here for a hint</summary>

```
const json = await res.json();
```
</details>

Task 2: Set user details

<details>
<summary>Click here for a hint</summary>

Use `sessionStorage.setItem('<attr>','<val>')`

```
          sessionStorage.setItem('auth-token', json.authtoken);
          sessionStorage.setItem('name', json.userName);
          sessionStorage.setItem('email', json.userEmail);
```
</details>

Task 3: Set the state of the user to logged in using the `useAppContext`
<details>
<summary>Click here for a hint</summary>

Use `setIsLoggedIn(true);`
</details>

Task 4: Navigate to the MainPage after logging in

<details>
<summary>Click here for a hint</summary>

Use `navigate('/app')`
</details>

Task 5: Set an error message if the password is incorrect

<details>
<summary>Click here for a hint</summary>

```
if (json.authtoken) {
	// Tasks 1-4 done previously
      } else {
        document.getElementById("email").value="";
        document.getElementById("password").value="";
        setIncorrect("Wrong password. Try again.");
	//Below is optional, but recommended - Clear out error message after 2 seconds
        setTimeout(() => {
          setIncorrect("");
        }, 2000);
      }
```

</details>


Task 6: Display an error message to the user

<details>
<summary>Click here for a hint</summary>
Add the following code in the placeholder to include the error message inside the return function.

```
<span style={{color:'red',height:'.5cm',display:'block',fontStyle:'italic',fontSize:'12px'}}>{incorrect}</span>
```
</details>


::page{title="Step 3: Push changes to GitHub"}

### Tasks

Task 1: Stage changes
Task 2: Commit changes
Task 3: Push changes

### Hints for Git commands

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


::page{title="Step 5: Final solution"}

## Solution

<details>

<summary>Click here for the sample solution</summary>

```javascript

import React, { useState,useEffect } from 'react';
//Step 1 - Task 1
import {urlConfig} from '../../config';
//Step 1 - Task 2
import { useAppContext } from '../../context/AuthContext';
//Step 1 - Task 3
import { useNavigate } from 'react-router-dom';

import './LoginPage.css';

function LoginPage() {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
	//Step 1 - Task 4
	const [incorrect, setIncorrect] = useState('');
	//Step 1 - Task 5
	const navigate = useNavigate();
    const bearerToken = sessionStorage.getItem('bearer-token');
    const { setIsLoggedIn } = useAppContext();

	//Step 1 - Task 6
    useEffect(() => {
        if (sessionStorage.getItem('auth-token')) {
          navigate('/app')
        }
      }, [navigate])

    const handleLogin = async (e) => {
        e.preventDefault();
        //api call
        const res = await fetch(`${urlConfig.backendUrl}/api/auth/login`, {
			//Step 1 - Task 7
			method: 'POST',
			//Step 1 - Task 8
          headers: {
            'content-type': 'application/json',
            'Authorization': bearerToken ? `Bearer ${bearerToken}` : '', // Include Bearer token if available
          },
		//Step 1 - Task 9
          body: JSON.stringify({
            email: email,
            password: password,
          })
        });

		//Step 2: Task 1
		const json = await res.json();
        console.log('Json',json);
        if (json.authtoken) {
			//Step 2: Task 2
          sessionStorage.setItem('auth-token', json.authtoken);
          sessionStorage.setItem('name', json.userName);
          sessionStorage.setItem('email', json.userEmail);
			//Step 2: Task 3
          setIsLoggedIn(true);
			//Step 2: Task 4
	      navigate('/app');
        } else {
			//Step 2: Task 5
          document.getElementById("email").value="";
          document.getElementById("password").value="";
          setIncorrect("Wrong password. Try again.");
          setTimeout(() => {
            setIncorrect("");
          }, 2000);
        }

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
                                onChange={(e) => {setEmail(e.target.value); setIncorrect("")}}
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
                                onChange={(e) => {setPassword(e.target.value);setIncorrect("")}}
                            />

							{/*Step 2: Task 6*/}
                            <span style={{color:'red',height:'.5cm',display:'block',fontStyle:'italic',fontSize:'12px'}}>{incorrect}</span>
                        </div>
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

```

</details>

You may want to check the front-end backend integration to see if it works as expected.



## Author
Skills Network

<!--
## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
|2026-02-02  | 0.3 | Manvi Gupta | Created and updated lab for Mark and PR |
|2024-02-20  | 0.2 | MS | QA Review |
| 2024-01-17 | 0.1 | UL | Initial version created |
-->


## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
