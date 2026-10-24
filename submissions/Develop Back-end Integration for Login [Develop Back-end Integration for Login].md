::page{title="Develop Back-end Integration for Login"}

**Estimated duration**: 30 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

Welcome to **Develop Backend Integration for Login**. In this lab, part of your capstone project, you\'ll develop an API endpoints for the `giftlink-backend` project. This exercise is designed to enhance your skills in Node.js and MongoDB by focusing on building and testing APIs routes.

## Objectives
- Create an endpoint to login a user `/login` in `authRoutes.js`
- Configure the `api/auth` route in the Express application (`app.js`) to use the routes defined in authRoutes.js.
- Handle errors and structure responses in a server environment
- Push the implemented changes to GitHub

## Prerequisite

- Ensure you have completed the previous modules and pushed all the changes to Github.
- You should have the updated `giftlink-backend` directory in your repository cloned to your local environment, or you will clone the repository that contains all of your pushed code. This will be your working directory for the lab

::page{title="Step 1: Implement the /login Endpoint"}

In this step, you implement the `/login` endpoint in **authRoutes.js** file to act as middleware. It should create an authentication route to POST details using the login API route.

### Tasks

1. Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.
2. Access MongoDB `users` collection
3. Check for user credentials in database
4. Check if the user entered password matches the stored encrypyted password and send appropriate message on mismatch
5. Fetch user details from database
6. Create JWT authentication if passwords match with user._id as payload
7. Send appropriate message if user not found
8. Run the server and test your API endpoint at this point using `curl`

#### Code Template

```javascript
router.post('/login', async (req, res) => {
    try {
        // Task 1: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.
        // Task 2: Access MongoDB `users` collection
		// Task 3: Check for user credentials in database
		// Task 4: Task 4: Check if the password matches the encrypyted password and send appropriate message on mismatch
        // Task 5: Fetch user details from database
		// Task 6: Create JWT authentication if passwords match with user._id as payload
        res.json({authtoken, userName, userEmail });
		// Task 7: Send appropriate message if user not found
    } catch (e) {
         return res.status(500).send('Internal server error');

    }
});
```

### Hints
Task 1: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.

<details>
<summary>Click here for a hint</summary>

Use `await connectToDatabase()` to connect to MongoDB
```
const db = await connectToDatabase();
```
</details>

Task 2: Access the `users` collection

<details>
<summary>Click here for a hint</summary>

Access the collection with `db.collection("users")`

```
const collection = db.collection("users");
```
</details>

Task 3: Check user credentials

<details>
<summary>Click here for a hint</summary>

```
const theUser = await collection.findOne({ email: req.body.email });
```
</details>

Task 4: Check if the password matches the encrypyted password and send appropriate message on mismatch

<details>
<summary>Click here for a hint</summary>

```
if (theUser) {
	let result = await bcryptjs.compare(req.body.password, theUser.password)
  if(!result) {
		logger.error('Passwords do not match');
		return res.status(404).json({ error: 'Wrong pasword' });
	}
	//continue other tasks
}
```
</details>

Task 5: Fetch user details in database

<details>
<summary>Click here for a hint</summary>

```
	const userName = theUser.firstName;
	const userEmail = theUser.email;
```
</details>

Task 6: Create JWT authentication if passwords match with user._id as payload

<details>
<summary>Click here for a hint</summary>

```js
		let payload = {
                user: {
                    id: theUser._id.toString(),
                },
            };
		jwt.sign(user._id, JWT_SECRET)
```
</details>

Task 7: Send appropriate message if user not found

<details><summary>Click here for a hint</summary>

```
	if (theUser) {
	// Tasks 1-6 as done previously
	} else {
		logger.error('User not found');
		return res.status(404).json({ error: 'User not found' });
	}
```
</details>

Task 8: You should run the server and test your API endpoint at this point using `curl`

<details><summary>Click here for a hint</summary>

```bash
curl --location 'http://localhost:3060/api/auth/login' \
--header 'Content-Type: application/json' \
--header 'Cookie: jhub-reverse-tool-proxy=s%3Adf8852e8-fe28-47ac-ab62-cb52fc5bbef5.CxZgc7USbJXpxTv4Vs6BH6esBtnhnYv%2FKQ098HtCm5s' \
--data-raw '{
    "email": "lachie@gmail.com",
    "password": "lac123"
}'
```
</details>

### **Assessment:**
 
**For Option 1: AI-Graded Submission and Evaluation:** Copy and paste the cURL command and its output, and save it in a text file named `login` for the final project submission and evaluation.
>Note: Please copy and paste only userName and userEmail from the response. Avoid copying the authtoken, as including it may cause issues during final submission

**For Option 2: Peer-Graded Submission and Evaluation**: You are required to submit a screenshot after successfully deploying the application. This deployment process is covered in the Module 5 **Hands-on Lab: Containerize and Deploy the Application**.

::page{title="Step 2: Push changes to GitHub"}

After implementing and testing the API endpoints, configure your git username and email through the terminal and push your changes to GitHub.

### Tasks

Task 1: Stage changes
Task 2: Commit changes
Task 3: Push changes

### Hints
1. Hint for staging changes

<details>
<summary>Click here for a hint</summary>

Stage all changes with `git add.`
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

::page{title="Step 3: Assessment and Final Solution"}

Your final solution should look similar to the file provided below.

### Final Solution

Solution for `routes/authRoutes.js` including both `/register` and `/login` APIs

<details>
<summary>Click here for a hint</summary>

```js
const express = require('express');
const bcryptjs = require('bcryptjs');
const jwt = require('jsonwebtoken');
const connectToDatabase = require('../models/db');
const router = express.Router();
const dotenv = require('dotenv');
const pino = require('pino');  // Import Pino logger
dotenv.config();

const logger = pino();  // Create a Pino logger instance

//Create JWT secret
dotenv.config();
const JWT_SECRET = process.env.JWT_SECRET;

router.post('/register', async (req, res) => {
    try {
      //Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.
	  const db = await connectToDatabase();

	  //Access the `users` collection
      const collection = db.collection("users");

	  //Check for existing email in DB
      const existingEmail = await collection.findOne({ email: req.body.email });

        if (existingEmail) {
            logger.error('Email id already exists');
            return res.status(400).json({ error: 'Email id already exists' });
        }

        const salt = await bcryptjs.genSalt(10);
        const hash = await bcryptjs.hash(req.body.password, salt);
        const email=req.body.email;

		//Save user details
        const newUser = await collection.insertOne({
            email: req.body.email,
            firstName: req.body.firstName,
            lastName: req.body.lastName,
            password: hash,
            createdAt: new Date(),
        });

        const payload = {
            user: {
                id: newUser.insertedId,
            },
        };

		//Create JWT
        const authtoken = jwt.sign(payload, JWT_SECRET);
        logger.info('User registered successfully');
        res.json({ authtoken,email });
    } catch (e) {
        logger.error(e);
        return res.status(500).send('Internal server error');
    }
});

	//Login Endpoint
router.post('/login', async (req, res) => {
    console.log("\n\n Inside login")

    try {
        // const collection = await connectToDatabase();
        const db = await connectToDatabase();
        const collection = db.collection("users");
        const theUser = await collection.findOne({ email: req.body.email });

        if (theUser) {
            let result = await bcryptjs.compare(req.body.password, theUser.password)
            if(!result) {
                logger.error('Passwords do not match');
                return res.status(404).json({ error: 'Wrong pasword' });
            }
            let payload = {
                user: {
                    id: theUser._id.toString(),
                },
            };

            const userName = theUser.firstName;
            const userEmail = theUser.email;

            const authtoken = jwt.sign(payload, JWT_SECRET);
            logger.info('User logged in successfully');
            return res.status(200).json({ authtoken, userName, userEmail });
        } else {
            logger.error('User not found');
            return res.status(404).json({ error: 'User not found' });
        }
    } catch (e) {
        logger.error(e);
        return res.status(500).json({ error: 'Internal server error', details: e.message });
      }
});

module.exports = router;

```
</details>

### **Assessment:**
For both **Option 1: AI-Graded Submission and Evaluation** and **Option 2: Peer-Graded Submission and Evaluation**:
Push `authRoutes.js` and all code to GitHub and note the repository link for evaluation.


<!---
## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2024-01-17 | 0.1 | UL | Initial version created |
| 2024-02-14 | 1.x | BH | Changes to make parallel to Register lab |
| 2024-02-20 | 1.1 | MS | QA pass with edits |
| 2025-11-20 | 1.2 | Manvi Gupta | Created and updated lab for Mark and PR |
--->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
