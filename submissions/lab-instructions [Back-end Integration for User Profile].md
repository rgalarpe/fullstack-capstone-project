::page{title="Develop Back-end Integration for User Profile"}

**Estimated duration**: 30 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

Welcome to the **Develop the Back-end Integration for User Profile** lab. In this lab you\'ll develop an API endpoint for the `giftlink-backend` project. This exercise is designed to enhance your skills in Node.js and MongoDB by focusing on building and testing APIs routes.

## Objectives

- Create an endpoint to update user credenitals in the database (`/update`) in `authRoutes.js`
- Configure the `api/auth` route in the Express application (`app.js`) to use the routes defined in `authRoutes.js`
- Handle errors and structure responses in a server environment
- Push the implemented changes to GitHub

## Prerequisites

- Ensure you have completed the previous modules and pushed all the changes to Github.
- You should have the updated `giftlink-backend` directory in your repository cloned to your local environment, or you will clone the repository that contains all of your pushed code. This will be your working directory for the lab


::page{title="Step 1: Implement the /update Endpoint"}

Add the code to the `/update` endpoint in `authRoutes.js` file so it can act as middleware. This should create an authentication route to update the profile. You can find the `authRoutes.js` file in the `routes` folder.

### Tasks

1. Use the `body`,`validationResult` from `express-validator` for input validation
2. Validate the input using `validationResult` and return approiate message if there is an error.
3. Check if `email` is present in the header and throw an appropriate error message if not present.
4. Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js` and access `users` collection.
5. Find user credentials in database
6. Update user credentials in database
7. Create JWT authentication with user._id as payload using secret key from .env file

#### Code Template

```javascript
// {Insert it along with other imports} Task 1: Use the `body`,`validationResult` from `express-validator` for input validation

router.put('/update', async (req, res) => {
        // Task 2: Validate the input using `validationResult` and return approiate message if there is an error.
    try {
        // Task 3: Check if `email` is present in the header and throw an appropriate error message if not present.
        // Task 4: Connect to MongoDB
		// Task 5: find user credentials in database

		existingUser.updatedAt = new Date();

		// Task 6: update user credentials in database
		// Task 7: create JWT authentication using secret key from .env file
        res.json({authtoken});
    } catch (e) {
         return res.status(500).send('Internal server error');

    }
});
```

### Hints

Task 1: Use the `body`,`validationResult` from `express-validator` for input validation

<details>
<summary>Click here for a hint</summary>

```
const { body, validationResult } = require('express-validator');
````

</details>

Task 2: Validate the input using `validationResult` and return approiate message if there is an error.

<details>
<summary>Click here for a hint</summary>

```
const errors = validationResult(req);
if (!errors.isEmpty()) {
  logger.error('Validation errors in update request', errors.array());
  return res.status(400).json({ errors: errors.array() });
}
```
</details>

Task 3: Check if `email` is present in the header and throw an appropriate error message if not present.

<details>
<summary>Click here for a hint</summary>

```
 const email = req.headers.email;

  if (!email) {
      logger.error('Email not found in the request headers');
      return res.status(400).json({ error: "Email not found in the request headers" });
  }
```
</details>


Task 4: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js` and access `users` collection.

<details>
<summary>Click here for a hint</summary>

```
const db = await connectToDatabase();
const collection = db.collection("users");
```
</details>

Task 5: Access the user details

<details>
<summary>Click here for a hint</summary>

```
const existingUser = await collection.findOne({ email });
```
</details>

Task 6: Update user credentials

<details>
 <summary>Click here for a hint</summary>

```
const updatedUser = await collection.findOneAndUpdate(
            { email },
            { $set: existingUser },
            { returnDocument: 'after' }
        );
```
</details>


Task 7: Create JWT authentication with user._id as payload using secret key from `.env` file

<details>
<summary>Click here for a hint</summary>

```
		const payload = {
					user: {
						id: updatedUser._id.toString(),
					},
				};

        const authtoken = jwt.sign(payload, JWT_SECRET);
```
</details>


::page{title="Step 2: Push changes to GitHub"}

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

::page{title="Step 3: Final Solution"}

### Solution

<details><summary>Your authRoutes.js file should look similar to the code provided below.</summary>

```javascript
const express = require('express');
const bcryptjs = require('bcryptjs');
const jwt = require('jsonwebtoken');
const connectToDatabase = require('../models/db');
const router = express.Router();
const dotenv = require('dotenv');
const pino = require('pino');  // Import Pino logger

//Task 1: Use the `body`,`validationResult` from `express-validator` for input validation
const { body, validationResult } = require('express-validator');


const logger = pino();  // Create a Pino logger instance

dotenv.config();
const JWT_SECRET = process.env.JWT_SECRET;

router.post('/register', async (req, res) => {
    try {
      //Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.
	  const db = await connectToDatabase();
      const collection = db.collection("users");
      const existingEmail = await collection.findOne({ email: req.body.email });

        if (existingEmail) {
            logger.error('Email id already exists');
            return res.status(400).json({ error: 'Email id already exists' });
        }

        const salt = await bcryptjs.genSalt(10);
        const hash = await bcryptjs.hash(req.body.password, salt);
        const email=req.body.email;
        console.log('email is',email);
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

        const authtoken = jwt.sign(payload, JWT_SECRET);
        logger.info('User registered successfully');
        res.json({ authtoken,email });
    } catch (e) {
        logger.error(e);
        return res.status(500).send('Internal server error');
    }
});

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

// update API
router.put('/update', async (req, res) => {
	// Task 2: Validate the input using `validationResult` and return approiate message if there is an error.

    const errors = validationResult(req);

	// Task 3: Check if `email` is present in the header and throw an appropriate error message if not present.
	if (!errors.isEmpty()) {
        logger.error('Validation errors in update request', errors.array());
        return res.status(400).json({ errors: errors.array() });
    }

    try {
        const email = req.headers.email;

        if (!email) {
            logger.error('Email not found in the request headers');
            return res.status(400).json({ error: "Email not found in the request headers" });
		}

		//Task 4: Connect to MongoDB
		const db = await connectToDatabase();
        const collection = db.collection("users");

		//Task 5: Find user credentials
        const existingUser = await collection.findOne({ email });

        if (!existingUser) {
            logger.error('User not found');
            return res.status(404).json({ error: "User not found" });
        }

        existingUser.firstName = req.body.name;
        existingUser.updatedAt = new Date();

		//Task 6: Update user credentials in DB
        const updatedUser = await collection.findOneAndUpdate(
            { email },
            { $set: existingUser },
            { returnDocument: 'after' }
        );

		//Task 7: Create JWT authentication with user._id as payload using secret key from .env file
        const payload = {
            user: {
                id: updatedUser._id.toString(),
            },
        };

        const authtoken = jwt.sign(payload, JWT_SECRET);
        logger.info('User updated successfully');

        res.json({ authtoken });
    } catch (error) {
        logger.error(error);
        return res.status(500).send("Internal Server Error");
    }
});
module.exports = router;
```
</details>


<!---
## Changelog


| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2024-01-17 | 0.1 | UL | Initial version created |
|2026-01-30  | 0.2 | Manvi Gupta | Created and updated lab for Mark and PR |
--->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
