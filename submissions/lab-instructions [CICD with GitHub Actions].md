::page{title="CI/CD with GitHub Actions"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

**Estimated time needed:** 60 minutes

Your team is growing! Management has decided to hire front-end and back-end engineers to ensure features on the roadmap are developed in time for future releases. However, this means that multiple engineers will need to work in parallel on the repository. You must ensure the code pushed to the main branch meets the team coding style and is free of syntax errors.

So far, you have created the back end, created the front end, integrated the front end and back end, and pushed all the code to your GitHub repository. Go to your GitHub repository to ensure all your code is present.

The code in your repository should be error-free, follow the standardized coding norms, and adhere to best practices. You may have noticed some suggestions that come up with colored squiggly lines while using the Cloud IDE. These are the IDE\'s built-in `linters` in action. 

**Linting** automates the code review process by providing feedback on code quality and adherence to coding standards before being merged into the codebase.

Overall, linting is an essential tool for improving code quality, maintaining consistency, and preventing common coding errors and security vulnerabilities in software development projects.

In this lab, you will add linting to your repository using a GitHub workflow containing GitHub Actions. Your linting will automatically check for errors whenever a developer creates a pull request or whenever a branch is merged into the default main branch. 

::page{title="GitHub Workflow"}

Examine the workflow template provided below. 

```
name: 'CI/CD'

on:
  push:
    branches: [master, main]
  pull_request:
    branches: [master, main]

jobs:
  lint_js:
      name: Lint JavaScript Files
      runs-on: ubuntu-latest

      steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 14

      - name: Install JSHint
        run: npm install jshint --global

      - name: Run Linter
        run: |
          # This command finds all JavaScript files recursively and runs JSHint on them
          find ./giftlink-backend -name app.js -exec jshint {} +
          find ./giftlink-backend -name auth.js -exec jshint {} +
          find ./giftlink-backend -name giftRoutes.js -exec jshint {} +
          find ./giftlink-backend -name searchRoutes.js -exec jshint {} +
          echo "Linted all the js files successfully"

  client_build:
      name: Build client
      runs-on: ubuntu-latest

      steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 14

      - name: Run build
        run: |
          cd giftlink-frontend
          npm install
          npm run build
          echo "Client-side build successfully"
```

1. Line 1 contains the name of the workflow.
2. The lines after **on** define when this workflow will run. The workflow should run when developers *push* a change to the main branch or create a *pull_request*. These two ways are captured as follows:
   - run on push to the main branch (main or master):
      ```
      push:
        branches: [master, main]
      ```
   - run when PR is created on main branches (main or master):
      ```
      pull_request:
        branches: [master, main]
      ```
3. Next, the workflow defines 2 jobs:
   - lint_js: Lint specified JavaScript files
   - client_build: Ensure there are no errors when building the React client 

::page{title="GitHub Jobs"}

Let\'s look at each of these jobs:
1. lint_js
   - Set up the Node.js runtime for the action to run using the `actions/setup-node@v3` action.
   - Install all JSHint linter `npm install jshint`.
   - Run the linting command on the .js files specified.
   - Print a message saying the linting was completed successfully.

1. client_build
   - Set up the Node.js runtime for the action to run using the `actions/setup-node@v3` action.
   - Change to the front-end directory `giftlink-frontend`
   - Install all the packages.
   - Run the `npm run build` to build the client side and copy it to the server side.
   - Print a message saying the linting was completed successfully.

# Enable GitHub Actions

1. To enable GitHub actions, log into GitHub and open your forked repo. Next, go to the `Actions` tab and click `Set up a workflow yourself`.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m5/images/github_action_create.png" style="margin-bottom:20px;margin-top:10x;border:solid grey 1px">

2. Paste the lint code given above inside `main.yml` and commit it.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m5/images/edit_workflow.png" style="margin-bottom:20px;margin-top:10x;border:solid grey 1px">


3. Open the `Actions` tab again, and you will see that the commit has automatically started the lint workflow.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m5/images/workflow_WIP.png" style="margin-bottom:20px;margin-top:10x;border:solid grey 1px">


4. You can click the workflow run to see the individual jobs and the logs for each job. When the workflow successfully completes, you will see the green tick indicating it went well. A red cross means it found errors in the code while linting.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m5/images/workflow_success.png" style="margin-bottom:20px;margin-top:10x;border:solid grey 1px"> <br>

##### 5. Check these hints to resolve usual Linting errors you could come across.

<details>

<summary> Click here </summary>

### JS Hint (JavaScript) linting errors:

##### 1.  If you receive one or more errors as listed below:
```
'const' is available in ES6 (use 'esversion: 6') or Mozilla JS extensions (use moz).

'arrow function syntax (=>)' is only available in ES6 (use 'esversion: 6').

'async functions' is only available in ES8 (use 'esversion: 8').

'let' is available in ES6 (use 'esversion: 6') or Mozilla JS extensions (use moz).

'template literal syntax' is only available in ES6 (use 'esversion: 6').
```

##### Resolution:
Add the line below at the start of the file(s) where this error is reported:

```
/*jshint esversion: 8 */
```
<br>

</details>

::page{title="Assessment:"}

 
<h4>For Option 1: AI-Graded Submission and Evaluation:</h4>  Follow the steps given below

1. Start by installing the GitHub CLI (`gh`) using the commands below:

```bash
sudo apt update
```
```bash
sudo apt install gh
```

2. Authenticate GitHub CLI using command `gh auth login`

Run the following command in your terminal:

```shell
gh auth login
```

When prompted, choose the options shown below:
1. What account do you want to log into?
   Select **GitHub.com**

2. What is your preferred protocol for Git operations?
   Select **HTTPS**

3. Authenticate Git with your GitHub credentials?
   Type **Y**

4. How would you like to authenticate GitHub CLI?
   Select **Paste an authentication token**

   > If you haven\'t already you can generate a Personal Access Token (PAT) by following the instructions given in the [Hands-on Lab: Generate GitHub personal access token](https://author-ide.skills.network/render?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJtZF9pbnN0cnVjdGlvbnNfdXJsIjoiaHR0cHM6Ly9jZi1jb3Vyc2VzLWRhdGEuczMudXMuY2xvdWQtb2JqZWN0LXN0b3JhZ2UuYXBwZG9tYWluLmNsb3VkL0lCTS1DRDAxMzFFTi1Ta2lsbHNOZXR3b3JrL2xhYnMvY3JlYXRlLXBlcnNvbmFsLXRva2VuL2luc3RydWN0aW9ucy5tZCIsInRvb2xfdHlwZSI6Imluc3RydWN0aW9uYWwtbGFiIiwiYWRtaW4iOmZhbHNlLCJpYXQiOjE2OTMyMDM0NzZ9.trhrHYxgdMIc-UW_NwcM9WeUOGzIfaIJMAcENksvrHg) and be sure to include these scopes: `repo`, `read:org` and `workflow`

5. Paste your authentication token
   Paste your PAT into the terminal
   > Note: If you see an `error validating token: missing required scope` error after entering your PAT, generate a new token and be sure to include these scopes: `repo`, `read:org` and `workflow`

Once done, you should see messages confirming:

* Git protocol configured
* Logged in with your GitHub username


3. Next, clone your GitHub repository and move into the project\'s root directory in the terminal.

<details>
<summary>Click here for a hint.</summary>

Use the following commands to clone the repository and change directories:

```shell
git clone <your-github-repository-link>
cd xrwvm-fullstack_capstone_project
```

</details>


4. To get the list of workflow runs for your GitHub repository run the following command from your project directory in the terminal:

```bash
gh run list
```

After the list of workflow runs is displayed, pick the top most `run-id` from the output and view its details using command below:

```bash
gh run view <run-id> --verbose
```
> Replace `<run-id>` with the ID shown in the list.

This will give you detailed information about that workflow run.

> Note: Ensure you are inside the correct repository directory and have successfully authenticated using ```gh auth login``` before running these commands.

Your output should appear similar to the image below:

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/ZnXVQT-0vwpMyfOVeAIcAA/image%20-83-%20-2-.png">


5. Copy and paste the terminal output that shows your GitHub Actions workflow running successfully and save it in a text file named `CI/CD` for the final project submission and evaluation. The output should clearly display the steps executed in the workflow.

#### For Option 2: Peer-Graded Submission and Evaluation:
Take a screenshot of the action workflow succeeding and save it as `CI/CD.png` or `CI/CD.jpeg`.

# Summary
In this lab, you added a linting service to your application. As a result, all new code will automatically get checked for syntax errors, and this will ensure all developers are following the team coding guidelines.

<!--
## Author(s)
<h4> Upkar Lidder <h4/>
<h4> Lavanya T S <h4/>
### Other Contributor(s)
Yan Luo
Priya
## Changelog
| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2024-01-25 | 1.0 | Lavanya | Initial version created |
| 2024-02-13 | 1.1 | Mercedes Schneider | QA pass with edits |
| 2025-11-19 | 1.2 | Manvi Gupta | Created and updated lab for Mark and PR |
-->

## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>