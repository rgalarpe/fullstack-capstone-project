---

::page{title="Finish Populating MongoDB "}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

Welcome to the **Finish Populating MongoDB** lab. In this lab, you will apply the skills you have already acquired in managing MongoDB databases and handling data within a Node.js environment. Using a GitHub repository, you will clone, set up, and populate a MongoDB database with gifts data, leveraging your existing knowledge in database operations and Node.js scripting. This lab is an opportunity to test your learning and showcase your ability to handle data management tasks in a full-stack development context.

## Objectives

- Clone a GitHub repository template containing the necessary files and data
- Initialize and configure MongoDB in the lab environment
- Employ command-line skills to navigate and execute database operations
- Apply best practices in managing secure database connections using environment variables
- Import data into MongoDB

::page{title="Prerequisite"}

## Important security information
Welcome to the Cloud IDE for the lab. This lab environment is where all of your development will take place. It has all the tools you will need, including a MongoDB database.

Your lab environment is temporary. You will not see the same lab environment twice. So, you must push all changes to your own GitHub repository to recreate it in a new lab environment, whenever required.

Also, note that this environment is shared and, therefore, not secure. You should not store personal information, usernames, passwords, or access tokens in this environment for any purpose.

## Your task
1. If you still need to generate a **GitHub Personal Access Token**, you should do so now. You can follow the instructions in [this](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0131EN-SkillsNetwork/labs/create-personal-token/instructions.md.html "this") lab to generate a personal token. You will need it to push code back to your repository. Your repo should have `repo` and `write` permissions and set to expire in `60` days. When Git prompts you for a password in the Cloud IDE environment, use your Personal Access Token instead.

1. You can recreate this environment by **Initializing the Development Environment** each time.

::page{title="Step 1: Clone your repository"}

You can skip this step if you have already cloned the repository as part of the previous [lab](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m1/user_stories.md.html "lab"). If the repository is not available in this lab environment, take the following steps to clone the repository.

## Your task
1. Access your GitHub account and locate the repository you created from the template provided. It should be named `fullstack-capstone-project`.
1. Use Git commands to clone the repository to your local environment.
1. Confirm that the repository contents, including the gifts data, are correctly downloaded.

### Hint

<details>
<summary>Click here for a hint.</summary>

Utilize the `git clone <repository-url>` command.
</details>

::page{title="Step 2: Initialize MongoDB"}


Next, you will initialize an instance of MongoDB.

**IMPORTANT!** You must take a screenshot of the terminal output as directed in the last task of this step, Initialize MongoDB. Save it in an easy to fine location. You will need this screenshot for your final project.

## Tasks
1. Open the `Skills Network Toolbox`
2. Open the `Databases` category and select `MongoDB`. Click `Create` to initialize the database service.

![momgo_create.jpg](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/iNRowlWXTxx0HHVS4s32DA/momgo-create.jpg)


3. You should see the database starting. This process can take a couple of minutes.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/m1l2-mongodb-starting.png" alt="MongoDB starting database" style="width:90%;margin:1cm;border: 1px grey solid;display: block;margin-left: auto;margin-right: auto;">

4.  Copy the **MONGO_HOST**,**MONGO_PORT** ,**MONGO_PASSWORD** which is generated under connection information tab.You will need this information in the next step of this lab. Since the lab environment is temporary, the password and Host Id might be different the next time you start MongoDB database service.

![connection_information.jpg](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/BdvOTXaJOpgRoegD7O2Zug/connection-information.jpg)

::page{title="Step 3: Import gifts data"}

The next step is to import the gifts data provided to you in the `giftlink-backend/util/import-mongo/gifts.json` file. MongoDB is a document-based NoSQL database where data is organized into collections and documents, providing a flexible schema. Each document can store varied data structures, making MongoDB particularly well-suited for handling large volumes of unstructured or semi-structured data. In this capstone project, you will work with `gifts` that have the following attributes.
- id
- name
- category
- condition
- posted_by
- zipcode
- date_added
- age_days
- age_years
- description
- image

A sample gift document is given below.

```
{
_id: ObjectId('65c166b57361698a5cdd82cc'),
    id: '875',
    name: 'Lamp',
    category: 'Kitchen',
    condition: 'New',
    posted_by: '26872',
    zipcode: '94805',
    date_added: 1667520000,
    age_days: 400,
    age_years: 1.1,
    description: "A charming lamp that's been lighting up my reading nook. It casts a soft, inviting glow, perfect for those who love to curl up with a good book. It's seen some of my favorite chapters and is ready to illuminate yours!",
    image: '/images/lamp.jpeg'
}
```
Open the `gifts.json` file and look at the sample data provided to you. You don\'t need to make any changes to this file.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-backend/util/import-mongo/gifts.json"}

## Tasks
1. Open a terminal with `Terminal` -> `New Terminal` if one isn\'t open already.
2. Change to the `import-mongo` directory.

```bash
cd /home/project/fullstack-capstone-project/giftlink-backend/util/import-mongo
```

3. Duplicate the `.env.sample` file, naming the new file `.env`. This file contains the username and password for MongoDB. Fill out the password and Host Id from the previous step where you started the database service. The username should remain `root`.

```
MONGO_URL=mongodb://root:password_of_mongodb_instance@localhost:27017
```

4. Install the required npm packages by executing the `npm install` command in the terminal.

```bash
npm install
```

5. Run the Node program by executing the `npm start` command in the terminal.

```bash
npm start
```

6. If all goes well, you should see the following message in the terminal:

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/db_populated.png)

The line, `Inserted documents: 16` confirms you inserted 16 gifts into the database.

### **Assessment:**
 
**For Option 1: AI-Graded Submission and Evaluation:** Copy and paste the terminal output showing that you imported 16 documents into MongoDB and save it in a text file named `inserted_items` for the final project submission and evaluation.
 
**For Option 2: Peer-Graded Submission and Evaluation:** Take a screenshot of the terminal output and save it as `inserted_items.png` or `inserted_items.jpeg`for the Peer Assignment.

::page{title="Step 4: Validate gifts data import"}

Having successfully imported your sample gifts data into MongoDB, next you will validate your database contains the correct data. In this task, you\'ll use *mongosh*, the official MongoDB shell, an interactive JavaScript interface to MongoDB.

Mongosh will query and update data as well as perform administrative operations. With its user-friendly interface and powerful capabilities, mongosh is an essential tool for developers working with MongoDB databases.

## Tasks
1. Open the mongosh terminal by using the MongoDB tab. You can open it again if you closed it.

![mongo_cli.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/7ALRYRhtOyylqhriPiaRbg/mongo-cli.png)

2. This will automatically open a terminal and start `Mongosh` for you.

![mongo_sh.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/aAEuAQP2pnBtjWtFcpuxug/mongo-sh.png)


Try the `show databases` command to see all the databases in the system. You should see several databases, including `giftdb`. Use the `use giftdb` command to switch to that database, and then execute `show collections` to display the gifts collection created by the Node program.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/m1l2-mongodb-commands-1.png" alt="Mongodb shell commands" style="width:90%;margin:1cm;border: 1px grey solid;display: block;margin-left: auto;margin-right: auto;">


3. Your turn now. Count the number of documents in the `gifts` collection. The result should be 16.

4. Execute a second command to get the two documents from the `gifts` collection. 

5. Find the gift with the id `429`. The output should look as follows:
```
[
	{
    _id: ObjectId('65c166b57361698a5cdd82da'),
    id: '429',
    name: 'Side Table',
    category: 'Living Room',
    condition: 'Older',
    posted_by: '23789',
    zipcode: '94102',
    date_added: 1664928900,
    age_days: 1100,
    age_years: 3.01,
    description: "This side table has been a convenient spot for lamps and books. It's still functional but has some scratches. Selling it as part of a living room makeover.",
    image: '/images/side-table.jpeg'
  }
]
```

### Hints

Count the number of gifts in the collection:

<details>
<summary>Click here for the answer</summary>

Use the `countDocuments()` method.
</details>

Retrieve the first two gifts from the collection:

<details>
<summary>Click here for the answer</summary>

Use the `find()` method with the `limit()` method.
</details>

Find a specific gift in the collection:

<details>
<summary>Click here for the answer</summary>

Use the `find()` method and pass in the query `{ "id": "429" }` as a parameter.
</details>

::page{title="Conclusion"}

Congratulations on completing the `Populate MongoDB` lab. By completing this lab, you effectively utilized your existing knowledge in database management and Node.js to perform a full-stack development task. This exercise reinforced your ability to integrate back-end technologies and handle data operations, solidifying your skills in building dynamic and efficient web applications.

## Next steps

You should spend some more time trying other commands you remember from the course on MongoDB. This environment is a good place to practice your skills.

<!--## Author(s)

Skills Network

## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
|2025-11-17  | 0.4 | Manvi Gupta | Created and updated lab for Mark and PR |
|2024-09-05  | 0.3 | Ritika | Changed screenshot and instructions as per new mongo db interface |
|2024-02-01  | 0.2 | MS | QA review |
| 2023-12-08 | 0.1 | UL | Initial version created |-->


## <h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>