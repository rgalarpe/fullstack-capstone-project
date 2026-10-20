::page{title="Add a Sentiment Analysis Service"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to the lab **Add a Sentiment Analysis Service**. In this lab, you will develop an Express server that performs sentiment analysis by using the `natural` npm package. The **Natural** library is a general natural language facility for Node.js that offers sentiment analysis.

## Objectives

- Use the `natural` library to perform sentiment analysis on English sentences.
- Implement an Express server with a `/sentiment` endpoint.

## Prerequisite

Ensure you cloned the GitHub repository you worked on in the previous labs.

::page{title="Step 1: Install the required packages"}

You are provided with skeleton code for the Express server but you will need to install the `natural` package. You will use the Node Package Manager or `npm` to install this package in the first step. Go to `fullstack-capstone-project/sentiment` directory on the terminal. This will be your working directory for this lab.

## Tasks
Install the `natural` package using the npm command.


<details>
<summary>Click here for a hint</summary>

```
npm install natural
```
</details>


## Evidence
Running the install command will put the `natural` package in the dependencies array of the package.json file that is present in the `sentiment` folder.
```
"dependencies": {
"axios": "^1.6.7",
"dotenv": "^16.4.1",
"express": "^4.18.2",
"express-pino-logger": "^7.0.0",
"natural": "^6.10.4",
"nodemon": "^3.0.3",
"pino": "^8.17.2",
"pino-pretty": "^10.3.1"
 }
 ```

::page{title="Step 2: Implement the Sentiment Analysis Server"}

Now that you have installed the npm package, you will write the server logic that uses the `Natural` library to perform sentiment analysis. You will first create a server, write the endpoint route, process the input from the caller, handle any errors that might occur and finally start the server on a pre-defined port.

### Tasks

You need to complete the tasks in the `sentiment/index.js` file.

::openFile{path="/home/project/fullstack-capstone-project/sentiment/index.js"}

Task 1: Import the **Natural** library.
Task 2: Initialize the Express server.
Task 3: Create a `POST /sentiment` endpoint.
Task 4: Extract the `sentence` parameter from the request body.
Task 5: Process the response from *Natural* by adding a sentiment of \'positive\', \'negative\' or \'neutral\' based on the scores returned.
- If score is < 0, the sentiment should be `negative`.
- If the score is between 0 and 0.33, it should `neutral`.
- Otherwise, the sentiment should be `positive`.

Task 6: Implement success return state.
Task 7: Implement error return state.

You have been provided with the code template. Use the hints below to complete the task.

### Hints for Implementing the Sentiment Analysis Server

Task 1: Import the library

<details>
<summary>Click here for a hint</summary>

Use the import statement `const natural = require("natural");`
</details>

Task 2: Initialize the server

<details>
<summary>Click here for a hint</summary>

Simply call the express method to initialize the server:
```
const app = express();
```
</details>

Task 3: Create the endpoint

<details>
<summary>Click here for a hint</summary>

Use `POST` for the method and `/sentiment` for the route.
</details>

Task 4: Extract the parameter

<details>
<summary>Click here for a hint</summary>

 Use the query object of the request to obtain the sentence. The `req.query` object contains a set of key-value pairs representing the query parameters of the URL. The `req.query` code will get the query object. Use the destructuring assignment to get the value directly.
</details>

Task 5: Process the response

<details>
<summary>Click here for a hint</summary>

The code already sets the default value of sentiment to `neutral`. Use if/else loops to set the value to `negative` or `positive` based on the score.
</details>

Task 6: Implement success return state
<details>
<summary>Click here for a hint</summary>

Use the status method on res to set the status and chain the json method to send the result back.

```
	res.status(200).json({ sentimentScore: analysisResult, sentiment: sentiment });
```
</details>


Task 7: Implement error return state (missing)
<details>
<summary>Click here for a hint</summary>

Use the status method again to set 500 and return the json using the `json()` method.
</details>


::page{title="Step 3: Push Changes to GitHub"}

Finally, push your implemented changes back to your GitHub repository using stage, commit, and push  Git commands.

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

::page{title="Step 4: Assessment and Final Solution"}

Your final solution should look similar to the file provided below.

### Final Solution

Final solution for `sentiment/package.json`

<details>
<summary>Click here for a hint</summary>

While your package.json file will not look exactly like this, you should have the `natural` package listed in dependencies. Do not fill this out manually. It will automatically get populated when you run the `npm install` command.

```
"dependencies": {
"axios": "^1.6.7",
"dotenv": "^16.4.1",
"express": "^4.18.2",
"express-pino-logger": "^7.0.0",
"natural": "^6.10.4",
"nodemon": "^3.0.3",
"pino": "^8.17.2",
"pino-pretty": "^10.3.1"
}
```
</details>


Final solution for `sentiment/index.js`
<details>
<summary>Click here for a hint</summary>

```javascript
require('dotenv').config();
const express = require('express');
const axios = require('axios');
const logger = require('./logger');
const expressPino = require('express-pino-logger')({ logger });
const natural = require("natural");

const app = express();
const port = process.env.PORT || 3000;

app.use(express.json());
app.use(expressPino);

// Define the sentiment analysis route
app.post('/sentiment', async (req, res) => {
	const { sentence } = req.query;


	if (!sentence) {
		logger.error('No sentence provided');
		return res.status(400).json({ error: 'No sentence provided' });
	}

	// Initialize the sentiment analyzer with the Natural's PorterStemmer and "English" language
	const Analyzer = natural.SentimentAnalyzer;
	const stemmer = natural.PorterStemmer;
	const analyzer = new Analyzer("English", stemmer, "afinn");

	// Perform sentiment analysis
	try {
		const analysisResult = analyzer.getSentiment(sentence.split(' '));

		let sentiment = "neutral";

		if (analysisResult < 0) {
			sentiment = "negative";
		} else if (analysisResult > 0.33) {
			sentiment = "positive";
		}

		// Logging the result
		logger.info(`Sentiment analysis result: ${analysisResult}`);
		// Responding with the sentiment analysis result
		res.status(200).json({ sentimentScore: analysisResult, sentiment: sentiment });
	} catch (error) {
		logger.error(`Error performing sentiment analysis: ${error}`);
		res.status(500).json({ message: 'Error performing sentiment analysis' });
	}
});

// Start the server
app.listen(port, () => {
	logger.info(`Server running on port ${port}`);
});

```
</details>

To demonstrate you have successfully completed the lab, provide the URL to your GitHub repository containing the sentiment analysis service code.
	
### **Assessment**: 
For both **Option 1: AI-Graded Submission and Evaluation** and **Option 2: Peer-Graded Submission and Evaluation:**  
Copy and paste the the public Github URL of `index.js` file and save it in a text file.

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

## <h3 align="center">© IBM Corporation. All rights reserved.</h3>
