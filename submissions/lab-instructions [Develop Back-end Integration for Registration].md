::page{title="Develop Back-end Integration for Registration"}

**Estimated duration**: 30 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

---

Welcome to **Develop Back end Integration for Registration**. In this lab, as part of your capstone project, you\'ll develop an API endpoint for the `giftlink-backend` project. This exercise should enhance your skills in Node.js and MongoDB by focusing on building and testing API routes.

## Objectives

- Create an endpoint to register a user in the database (`/register`) in `authRoutes.js`
- Configure the `api/auth` route in the Express application (`app.js`) to use the routes defined in `authRoutes.js`
- Handle errors and structure responses in a server environment
- Push the implemented changes to GitHub

## Prerequisites

- Ensure you have completed the previous modules and pushed all the changes to Github.
- You should have the updated `giftlink-backend` directory in your repository cloned to your local environment, or you will clone the repository that contains all of your pushed code. This will be your working directory for the lab.


::page{title="Step 1: Set up the authRoutes.js file"}

In this exercise, you will create an endpoint to register a user. Use the following template to complete the register endpoint.

### Tasks

1. Create an `authRoutes.js` file inside the `routes` folder
1. Import all the necessary packages
1. Create an instance of the Pino logger
1. Create a JWT authentication using the secret key from the .env file

#### Code Template for authRoutes.js

```js
//Step 1 - Task 2: Import necessary packages

//Step 1 - Task 3: Create a Pino logger instance

dotenv.config();

//Step 1 - Task 4: Create JWT secret

router.post('/register', async (req, res) => {
//Step 2
});

module.exports = router;
```
Task 2: Import all the necessary packages
   <details>
   <summary>Click here for a hint</summary>
```js
const express = require('express');
const app = express();
const bcryptjs = require('bcryptjs');
const jwt = require('jsonwebtoken');
const { body, validationResult } = require('express-validator');
const connectToDatabase = require('../models/db');
const router = express.Router();
const dotenv = require('dotenv');
const pino = require('pino');  // Import Pino logger

```
   </details>

Task 3: Create an instance of the Pino logger
   <details>
   <summary>Click here for a hint</summary>

```js
const logger = pino();  // Create a Pino logger instance
```
</details>

Task 4: Create a JWT authentication using the secret key from the .env file

<details><summary>Click here for hint</summary>

```
const JWT_SECRET = process.env.JWT_SECRET;
```
</details>


::page{title="Step 2: Implement the /register endpoint"}

Now, create the `/register` endpoint using the template provided.
1. Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`.
1. Access the collection
1. Check for existing email ID
1. Save user details in the database
1. Create JWT Authentication

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/routes/authRoutes.js"}

#### Code Template

```javascript
router.post('/register', async (req, res) => {
    try {
        // Task 1: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`
		 // {{insert code here}}

        // Task 2: Access MongoDB collection
		 // {{insert code here}}

		//Task 3: Check for existing email
		 // {{insert code here}}

		const salt = await bcryptjs.genSalt(10);
        const hash = await bcryptjs.hash(req.body.password, salt);
		const email = req.body.email;

		// {{insert code here}} //Task 4: Save user details in database
		 // {{insert code here}} //Task 5: Create JWT authentication with user._id as payload
        logger.info('User registered successfully');
        res.json({authtoken,email});
    } catch (e) {
         return res.status(500).send('Internal server error');
    }
});
```

### Hints


Task 1: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`

<details>
<summary>Click here for a hint</summary>

Use `await connectToDatabase()` to connect to MongoDB
```js
const db = await connectToDatabase();
```
</details>

Task 2: Access the collection

<details>
<summary>Click here for a hint</summary>

Access the collection with `db.collection("users");`
```
const collection = db.collection("users");
```
</details>

Task 3: Check for existing email ID

<details>
 <summary>Click here for a hint</summary>

```
const existingEmail = await collection.findOne({ email: req.body.email });
```
</details>

Task 4: Save user details

<details>
<summary>Click here for a hint</summary>

```
        const newUser = await collection.insertOne({
            email: req.body.email,
            firstName: req.body.firstName,
            lastName: req.body.lastName,
            password: hash,
            createdAt: new Date(),
        });
```
</details>

Task 5: Create JWT authentication

<details>
<summary>Click here for a hint</summary>

```
        const payload = {
            user: {
                id: newUser.insertedId,
            },
        };

        const authtoken = jwt.sign(payload, JWT_SECRET);
```
</details>


::page{title="Step 3: Configure the /api/auth endpoint"}

You should now configure the `/API/auth` endpoint, enabling the `/API/auth/register` endpoint to be routed to `/register`, created in the previous step.

### Your Task

1. Import authRoutes.js in app.js

2. Use `authRoutes` for the `/api/auth` path

3. Run your app from the terminal and connect to the URL the app is running through the tools available in the lab environment. Note the URL and add it to`giftlink-frontend/src/.env`

4. Run the server to test your API endpoint using `curl`

### Hints for middleware in `app.js`

1. Hint for Task 1: Import authRoutes

<details>
<summary>Click here for a hint</summary>

Use `require('./routes/authRoutes');`
```
const authRoutes = require('./routes/authRoutes');
```
</details>

2. Hint for Task 2: Use `authRoutes` for the `/api/auth` path

<details>
<summary>Click here for a hint</summary>

```
app.use('/api/auth', authRoutes);
```
</details>

3. Hint for Task 3: Run your app from the terminal and connect to the URL the app is running through the tools available in the lab environment. Copy the URL and add it to `giftlink-frontend/src/.env`.

<details>
<summary>Click here for a hint</summary>

Paster the url in `.env` file. You should set this up to mirror the following code. Please don't include the / at the end.

```
REACT_APP_BACKEND_URL=http://yourserver_url
```

</details>

4. You should run the server to test your API endpoint using `curl` 

<details><summary>Click here for a hint</summary>


```bash
curl --location 'http://localhost:3060/api/auth/register' \
--header 'Content-Type: application/json' \
--header 'Cookie: jhub-reverse-tool-proxy=s%3Adf8852e8-fe28-47ac-ab62-cb52fc5bbef5.CxZgc7USbJXpxTv4Vs6BH6esBtnhnYv%2FKQ098HtCm5s' \
--data-raw '{
                "firstName": "Lachlan",
                "lastName": "Baker",
                "email": "lachie@gmail.com",
                "password": "lac123"

}'
```
</details>

### **Assessment:**
 
**For Option 1: AI-Graded Submission and Evaluation:** Copy and paste the cURL command and its output, and save it in a text file named `register` for the final project submission and evaluation.
>Note: Please copy and paste only  email address from the response. Avoid copying the authtoken as including it may cause issues during final submission.

**For Option 2: Peer-Graded Submission and Evaluation**: You are required to submit a screenshot after successfully deploying the application. This deployment process is covered in the Module 5 **Hands-on Lab: Containerize and Deploy the Application**.


::page{title="Step 4: Push changes to GitHub"}

After implementing and testing the API endpoints, configure your github username and email through the terminal and push your changes to GitHub.

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

::page{title="Step 5: Assessment and final solution"}

### Final solution

1. Final solution for `routes/authRoutes.js`
> Note : Node.js does not support ES6 modules (import/export) by default. To enable them, update the package.json file with the "type": "module" field. However, since the course\'s solution codes use CommonJS modules, it is recommended to use CommonJS to ensure successful lab execution.

<details>
<summary>Click here for a hint</summary>

```js
const express = require('express');
const app = express();
const bcryptjs = require('bcryptjs');
const jwt = require('jsonwebtoken');
const { body, validationResult } = require('express-validator');
const connectToDatabase = require('../models/db');
const router = express.Router();
const dotenv = require('dotenv');
const pino = require('pino');  // Import Pino logger

const logger = pino();  // Create a Pino logger instance

dotenv.config();

const JWT_SECRET = process.env.JWT_SECRET;

router.post('/register', async (req, res) => {
    try {
        // Task 1: Connect to `giftsdb` in MongoDB through `connectToDatabase` in `db.js`
        const db = await connectToDatabase();

        // Task 2: Access MongoDB collection
        const collection = db.collection("users");

		//Task 3: Check for existing email
        const existingEmail = await collection.findOne({ email: req.body.email });

		const salt = await bcryptjs.genSalt(10);
        const hash = await bcryptjs.hash(req.body.password, salt);
		const email = req.body.email;

		//Task 4: Save user details in database
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
        res.json({authtoken,email});
    } catch (e) {
         return res.status(500).send('Internal server error');
    }
});

module.exports = router;
```
</details>

2. Final solution for `app.js`

<details>
<summary>Click here for a hint</summary>

```js
/*jshint esversion: 8 */
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const pinoLogger = require('./logger');

const connectToDatabase = require('./models/db');
const {loadData} = require("./util/import-mongo/index");


const app = express();
app.use("*",cors());
const port = 3060;

// Connect to MongoDB; we just do this one time
connectToDatabase().then(() => {
    pinoLogger.info('Connected to DB');
})
    .catch((e) => console.error('Failed to connect to DB', e));


app.use(express.json());

// Route files
const giftRoutes = require('./routes/giftRoutes');
const authRoutes = require('./routes/authRoutes');
const searchRoutes = require('./routes/searchRoutes');
const pinoHttp = require('pino-http');
const logger = require('./logger');

app.use(pinoHttp({ logger }));

// Use Routes
app.use('/api/gifts', giftRoutes);
app.use('/api/auth', authRoutes);
app.use('/api/search', searchRoutes);

// Global Error Handler
app.use((err, req, res, next) => {
    console.error(err);
    res.status(500).send('Internal Server Error');
});

app.get("/",(req,res)=>{
    res.send("Inside the server")
})

app.listen(port, () => {
    console.log(`Server running on port ${port}`);
});

```
</details>

### **Assessment**: 
For both **Option 1: AI-Graded Submission and Evaluation** and **Option 2: Peer-Graded Submission and Evaluation:**
Copy and paste the the public Github URL of `authRoutes.js` and save it in a text file.

You may use the `curl` command or Postman to ensure your backend works as expected.

<!---
## Changelog


| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2025-11-18 | 0.3 | Manvi Gupta | Created and updated lab for Mark and PR |
| 2024-02-14 | 0.2 | MS | QA review   |
| 2024-01-17 | 0.1 | UL | Initial version created |
--->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
