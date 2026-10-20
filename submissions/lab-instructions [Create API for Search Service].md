::page{title="Create API for Search Service"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to **Create API for Search Service**. In this lab, as part of your capstone project, you will develop the API and endpoint related to the search functionality with various filters for the `giftlink-backend` project.

## Objectives

- Develop a search endpoint in `searchRoutes.js` to filter gifts based on different criteria.
- Integrate the search routes into the Express application (`app.js`).
- Push the implemented changes to GitHub and prepare your code for review.

## Prerequisite

Ensure the `giftlink-backend` repository is cloned to your local environment, as it will be your working directory for the lab.

::page{title="Step 1: Implement the search endpoint"}

Create a search endpoint to filter gifts by name, category, condition, and age. Next, you need to implement the /api/gifts endpoint to retrieve all gifts stored in the database. Use the template below and complete the get() function. This function belongs in the `giftlink-backend/routes/searchRoutes.js` file.

### Tasks

**Task 1:** Connect to MongoDB
**Task 2:** Check if the name exists and is not empty
**Task 3:** Add the other three filters to the query.
- category
- condition
- age_years

**Task 4:** Fetch filtered gifts

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/routes/searchRoutes.js"}

### Hints for the search endpoint

Task 1: Connect to MongoDB

<details>
<summary>Click here for a hint</summary>

Connect to MongoDB using connectToDatabase database. Remember to use the await keyword and store the connection in `db`. Your code should look as follows:

```
const db = await connectToDatabase();
```
</details>

Task 2: Add the name filter

<details>
<summary>Click here for a hint</summary>

Use the following inside the if condition:

```
req.query.name>req.query.name && req.query.name.trim() !== ''
```
</details>

Task 3: Add other filters
<details>
<summary>Click here for a hint</summary>

For each filter, use this code:
```
query.category = req.query.category;
query.condition = req.query.condition;
query.age_years = { $lte: parseInt(req.query.age_years) };
```
</details>

Task 4: Fetch filtered gifts
<details>
<summary>Click here for a hint</summary>

Use `await collection.find(query).toArray()` to fetch the filtered gifts and assign them to `gifts` constant.
</details>

::page{title="Step 2: Integrate search routes in app.js"}

Ensure the search functionality is accessible through the Express application.

### Tasks
1. Search API Task 1: import the `searchRoutes` and store in a costant called `searchRoutes`
2. Search API Task 2: add the `searchRoutes` to the server by using the `app.use()` method.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/app.js"}

### Hints
Task 1: Import searchRoutes

<details>
<summary>Click here for a hint</summary>

Ensure you've imported `searchRoutes` correctly in your `app.js` file.

```
const searchRoutes = require('./routes/searchRoutes');
```
</details>

Task 2: Use searchRoutes

<details>
<summary>Click here for a hint</summary>

Attach `searchRoutes` to your Express app to handle routes under `/api/search` using the code `app.use('/api/search', searchRoutes);`
</details>

::page{title="Step 3: Test the API"}

Now that you have finished coding the API, you should test the endpoint. You will open a terminal, as in the previous lab, and type the following curl command to test the endpoint:

```bash
curl "http://localhost:3060/api/search?name=&age_years=6&category=Office&condition=Older"

```

This command sends a GET request to the `/api/search` endpoint with the `category` parameter set to `Office` and the `condition` parameter is  set to `Older`. If the service works properly, the code will return an array containing the items. There are three item in the database that satisfies these constraints.


### Assessment:
**For Option 1 - AI Graded Submission and Evaluation**: Copy and paste the cURL command and its output, and save it in a text file named `search_item` for the final project submission and evaluation.

**For Option 2: Peer-Graded Submission and Evaluation**: You are required to submit a screenshot after successfully deploying the application. This deployment process is covered in the Module 5 **Hands-on Lab: Containerize and Deploy the Application**.

::page{title="Step 4: Push changes to GitHub"}

Configure you git username and email in a terminal and perform the following tasks.

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

::page{title="Step 5: Assessment and final solution"}

Ensure you have correctly implemented your final solution and it is ready for submission.

### Final solution
Ensure your final solution looks like the files listed below.

1. Solution for `giftlink-backend/app.js`

<details><summary>Click here for a hint</summary>

```javascript
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
const searchRoutes = require('./routes/searchRoutes');
const pinoHttp = require('pino-http');
const logger = require('./logger');

app.use(pinoHttp({ logger }));

// Use Routes
app.use('/api/gifts', giftRoutes);
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

2. Solution for `giftlink-backend/routes/searchRoutes.js`

<details>
<summary>Click here for a hint</summary>

```javascript
	const express = require('express');
	const router = express.Router();
	const connectToDatabase = require('../models/db');

	// Search for gifts
	router.get('/', async (req, res, next) => {
		try {

	        // Task 1: Connect to MongoDB
			const db = await connectToDatabase();
			const collection = db.collection("gifts");
			// Initialize the query object
			let query = {};

			// Task 2: check if the name exists and is not empty
			if (req.query.name && req.query.name.trim() !== '') {
				query.name = { $regex: req.query.name, $options: "i" }; // Using regex for partial match, case-insensitive
			}

            // Task 3: Add other filters to the query
			if (req.query.category) {
				query.category = req.query.category;
			}
			if (req.query.condition) {
				query.condition = req.query.condition;
			}
			if (req.query.age_years) {
				query.age_years = { $lte: parseInt(req.query.age_years) };
			}

            // Task 4: Fetch filtered gifts
			const gifts = await collection.find(query).toArray();
			res.json(gifts);
		} catch (e) {
			next(e);
		}
	});

	module.exports = router;
```
</details>

### **Assessment**: 
For both **Option 1: AI-Graded Submission and Evaluation** and **Option 2: Peer-Graded Submission and Evaluation:**  
Copy and paste the the public Github URL of `searchRoutes.js` file and save it in a text file.

## Author

Skills Network

<!--
## Changelog

| Date       | Version | Changed by | Change Description        |
|------------|---------|------------|---------------------------|
| 2025-11-18 | 0.3 	   | Manvi Gupta| Created and updated lab for Mark and PR |
| 2024-02-12 | 0.2     | MS         | QA pass                   |
| 2024-01-18 | 0.1     | UL         | Initial version created   |
-->

## <h3 align="center"> © IBM Corporation. All rights reserved. </h3>
