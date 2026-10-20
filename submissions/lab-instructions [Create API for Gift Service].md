::page{title="Create API for Gift Service"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to **Create API for Gift Service**. In this lab, part of your capstone project, you will develop the APIs and endpoints related to gifts for the `giftlink-backend` project.

## Objectives

- Establish a connection to MongoDB in `db.js`.
- Create an endpoint to retrieve all gifts from the database (`/api/gifts`)
- Develop an endpoint to fetch a specific gift by ID (`/api/gifts/:id`)
- Configure the gift routes in the Express application (`app.js`)
- Push the implemented changes to GitHub

## Prerequisite

Ensure the `giftlink-backend` repository is cloned to your local environment, as it will be your working directory for the lab.

::page{title="Step 1: Connect to MongoDB"}

For the first exercise in the lab, you will make edits in `giftlink-backend/models/db.js` to establish a MongoDB connection. You will establish this connection using the template below by completing the `connectToDatabase()` function. The tasks to complete the function are given below and also commented out in the template.

### Tasks

Task 1: Connect to MongoDB
Task 2: Connect to database giftDB and store in variable dbInstance
Task 3: Return the database instance

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/models/db.js"}


### Hints

Task 1: Connect to MongoDB

<details>
<summary>Click here for a hint</summary>

Use `await client.connect()` to connect to MongoDB. No need to store the result anywhere.
</details>

Task 2: Assign dbInstance

<details>
<summary>Click here for a hint</summary>

Assign `dbInstance` with` client.db(dbName)`
   </details>

Task 3: Return dbInstance

<details>
<summary>Click here for a hint</summary>

Return the `dbInstance`
</details>

::page{title="Step 2: Implement the /api/gifts Endpoint"}

Next, you need to implement the `/api/gifts` endpoint to retrieve all gifts stored in the database. Use the template below and complete the `get()` function. This function belongs in the `giftlink-backend/routes/giftRoutes.js` file.

### Tasks

Task 1: Connect to MongoDB and store connection to db constant
Task 2: use the collection() method to retrieve the gift collection
Task 3: Fetch all gifts using the collection.find method. Chain with toArray method to convert to JSON array
Task 4: return the gifts using the res.json method

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/routes/giftRoutes.js"}

### Hints

Task 1: Connect to MongoDB

<details>
<summary>Click here for a hint</summary>

Use `const db = await connectToDatabase();` to get the database connection
</details>

Task 2: use the collection() method to retrieve the gift collection

<details>
<summary>Click here for a hint</summary>

Access the collection using `const collection = db.collection("gifts");`
</details>

Task 3: Fetch all gifts

<details>
<summary>Click here for a hint</summary>

Use `const gifts = await collection.find({}).toArray();` to fetch all gifts
</details>

Task 4: Return gifts

<details>
<summary>Click here for a hint</summary>

Return the `gifts` array in the response with `res.json(gifts)`.
</details>

::page{title="Step 3: Implement the /api/gifts/:id Endpoint"}

In this exercise you will create an endpoint to fetch a specific gift by its ID.  Continue in `routes/giftRoutes.js` to add the `/api/gifts/:id` endpoint.

### Tasks

Task 1: Connect to MongoDB and store connection to db constant
Task 2: use the collection() method to retrieve the gift collection
Task 3: Find a specific gift by ID using the collection.fineOne method and store in constant called gift

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/routes/giftRoutes.js"}

### Hints

Task 1: Connect to MongoDB

<details>
<summary>Click here for a hint</summary>

Similar to the previous, use `const db = await connectToDatabase();` for the DB connection
</details>

Task 2: Access the MongoDB collection

<details>
<summary>Click here for a hint</summary>

Access the collection as before with `const collection = db.collection("gifts");`
</details>

Task 3: Find a specific gift by ID

<details>
<summary>Click here for a hint</summary>

Use `const gift = await collection.findOne({ id: id });` to find the gift.
</details>

::page{title="Step 4: Connect Routes in app.js"}

In this exercise you integrate the gift routes into the main Express application in `app.js` by configuring the middleware to use `giftRoutes` for handling requests to `/api/gifts`.

### Tasks

1. Task1: import the `giftRoutes` and store in a costant called `giftroutes`
2. Task1: add the `giftRoutes` to the server by using the `app.use()` method.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/app.js"}

### Hints for Middleware in `app.js`

1. Hint for Gifts API Task  1: Import giftRoutes

<details>
<summary>Click here for a hint</summary>

Ensure you\'ve imported `giftRoutes` correctly in your `app.js` file.
The correct code is `const giftRoutes = require('./routes/giftRoutes');`
</details>

2. Hint for Gifts API Task 2: Use giftRoutes

<details>
<summary>Click here for a hint</summary>

Attach `giftRoutes` to your Express app to handle routes under `/api/gifts` using the code `app.use('/api/gifts', giftRoutes);`
</details>

::page{title="Step 5: Test the endpoints"}

In this step, you will use the `curl` command to test the API just wrote.

### Tasks
1. Task 1: Start the terminal.
2. Task 2: Test the `/api/gifts` endpoint using the curl command.
3. Task 3: Use the curl command to test the `/api/gifts/:id` endpoint.

### Hints

Task 1: Start the terminal.
<details>
<summary>Click here for a hint</summary>

Use the Terminal menu in the lab to open a new terminal.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CC0100EN-SkillsNetwork/images/new_terminal.jpg" alt="Terminal menu">

</details>

Task 2: Use the `curl` command to test the `/api/gifts/` endpoint.

<details>
<summary>Click here for a hint</summary>

Use the following `curl` command in the terminal to test the `/gifts` API:

```bash
curl --request GET --url http://localhost:3060/api/gifts
```


</details>

### **Assessment:**

**For Option 1: AI-Graded Submission and Evaluation:** Copy and paste the cURL command and its output, and save it in a text file named `mainpage` for the final project submission and evaluation.

**For Option 2: Peer-Graded Submission and Evaluation**: You are required to submit a screenshot after successfully deploying the application. This deployment process is covered in the Module 5 **Hands-on Lab: Containerize and Deploy the Application**.

Task 3: Use the `curl` command to test the `/api/gifts/:id` endpoint.

<details>
<summary>Click here for a hint</summary>

Use the following `curl` command in the terminal to test the `/gifts/:id` API:

```bash
curl --request GET --url http://localhost:3060/api/gifts/424
```
</details>

### **Assessment:**
 
**For Option 1: AI-Graded Submission and Evaluation:** Copy and paste the cURL command and its output, and save it in a text file named `item_detail` for the final project submission and evaluation.

**For Option 2: Peer-Graded Submission and Evaluation**: You are required to submit a screenshot after successfully deploying the application. This deployment process is covered in the Module 5 **Hands-on Lab: Containerize and Deploy the Application**.


::page{title="Step 6: Push Changes to GitHub"}

Finally, configure the git access by running the following commands with your github username and the email id you used to sign in for github, and push your implemented changes back to your GitHub repository using stage, commit, and push  Git commands.

```
git config --global user.name "<Github username>"
```

```
git config --global user.email <Github mail ID>
```

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

::page{title="Step 7: Assessment and Final Solution"}

Your final solution should look similar to the file provided below.

### Final Solution

1. Final solution for `models/db.js`

<details>
<summary>Click here for a hint</summary>

```javascript
// db.js
require('dotenv').config();
const MongoClient = require('mongodb').MongoClient;

// MongoDB connection URL with authentication options
let url = `${process.env.MONGO_URL}`;

let dbInstance = null;
const dbName = "giftdb";

async function connectToDatabase() {
	if (dbInstance){
		return dbInstance
	};

	const client = new MongoClient(url);

	await client.connect();
	dbInstance = client.db(dbName);
	return dbInstance;
}

module.exports = connectToDatabase;

```
</details>


2. Final solution for `giftlink-backend/routes/giftRoutes.js`

<details>
<summary>Click here for a hint</summary>

```javascript
const express = require('express');
const router = express.Router();
const connectToDatabase = require('../models/db');
const logger = require('../logger');

// Get all gifts
router.get('/', async (req, res, next) => {
	logger.info('/ called');
	try {
		const db = await connectToDatabase();

		const collection = db.collection("gifts");
		const gifts = await collection.find({}).toArray();
		res.json(gifts);
	} catch (e) {
		logger.console.error('oops something went wrong', e)
		next(e);
	}
});

// Get a single gift by ID
router.get('/:id', async (req, res, next) => {
	try {
		const db = await connectToDatabase();
		const collection = db.collection("gifts");
		const id = req.params.id;
		const gift = await collection.findOne({ id: id });

		if (!gift) {
			return res.status(404).send("Gift not found");
		}

		res.json(gift);
	} catch (e) {
		next(e);
	}
});


// Add a new gift
router.post('/', async (req, res, next) => {
	try {
		const db = await connectToDatabase();
		const collection = db.collection("gifts");
		const gift = await collection.insertOne(req.body);

		res.status(201).json(gift.ops[0]);
	} catch (e) {
		next(e);
	}
});

module.exports = router;

```
</details>



3. Final solution for `giftlink-backend/app.js`


<details>
<summary>Click here for a hint</summary>

```javascript
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
	// Gift API Task 1: import the giftRoutes and store in a constant called giftroutes
	const giftRoutes = require('./routes/giftRoutes');

	// Search API Task 1: import the searchRoutes and store in a constant called searchRoutes
	//{{insert code here}}


	const pinoHttp = require('pino-http');
	const logger = require('./logger');

	app.use(pinoHttp({ logger }));

	// Use Routes
	// Gift API Task 2: add the giftRoutes to the server by using the app.use() method.
	app.use('/api/gifts', giftRoutes);

	// Search API Task 2: add the searchRoutes to the server by using the app.use() method.
	//{{insert code here}}


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
Copy and paste the the public Github URLs of `app.js`, `giftRoutes.js`and `db.js` and save it in a text file.


## Author

Skills Network

<!--## Changelog

| Date       | Version | Changed by | Change Description        |
|------------|---------|------------|---------------------------|
| 2025-11-17  | 0.2 | Manvi Gupta | Created and updated lab for Mark and PR |
| 2024-01-17  | 0.1  | UL         | Initial version created   |-->

## <h3 align="center"> © IBM Corporation. All rights reserved. </h3>
