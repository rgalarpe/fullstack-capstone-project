::page{title="Create the MainPage and Navbar"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to **Create the Main Page and Navbar** for the `giftlink-frontend` project. This lab focuses on enhancing the main page to display gifts and streamlining the user interface by adjusting the NavBar component.

## Objectives

- Fetch and display gifts on the `MainPage.js` component.
- Provide navigation to `Home` and `Gifts` from the `Navbar.js`.

## Prerequisite

- Ensure you have completed the previous modules and pushed all the changes to Github.
- You should have the `giftlink-frontend` and `giftlink-backend` directories in your repository cloned to your local environment, or you will clone the repository that contains all of your pushed code. The  `giftlink-frontend` will be your working directory for the lab.

::page{title="Step 1: Implement MainPage Component"}

Modify `MainPage.js` to fetch and display gifts.

### Tasks

1. In `MainPage.js`, complete the implementation to fetch gifts and display them on the page
2. Navigate to the details page
3. Format the timestamp
4. Display gift image or placeholder
5. Display gift name
6. Display the formatted date


::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/MainPage/MainPage.js"}

You have been provided with the template. Use the following hints to complete the implementation of the component.

### Hints for Implementing MainPage Component

Task 1: Fetching gifts

<details>
<summary>Click here for a hint</summary>

Use `fetch(url)` to initiate a GET request to your API. Handle the response by checking if it\'s ok, then converting it to JSON and setting the gifts state with the received data.

```javascript
		// fetch all gifts
        const fetchGifts = async () => {
            try {
                let url = `${urlConfig.backendUrl}/api/gifts`
                const response = await fetch(url);
                if (!response.ok) {
                    //something went wrong
                    throw new Error(`HTTP error; ${response.status}`)
                }
                const data = await response.json();
                setGifts(data);
            } catch (error) {
                console.log('Fetch error: ' + error.message);
            }
        };

        fetchGifts();
```
</details>

Task 2: Navigate to details page

<details>
<summary>Click here for a hint</summary>

Use the `navigate` function to redirect the user. Pass the path to the product\'s details page using template literals.

```javascript
   navigate(`/app/product/${productId}`);
```
</details>

Task 3: Format timestamp

<details>
<summary>Click here for a hint</summary>

To format the timestamp, convert it to a Date object and use `toLocaleDateString` for a readable format. Assume the timestamp is in seconds and needs to be converted to milliseconds by multiplying by 1000.

```javascript
const date = new Date(timestamp * 1000);
return date.toLocaleDateString('default', { month: 'long', day: 'numeric', year: 'numeric' });
```
</details>

Task 4: Display gift image or placeholder

<details>
<summary>Click here for a hint</summary>

Use conditional rendering to display the image if it exists. If there\'s no image, show a placeholder text or element. Remember to use the `gift.image` property to check for an image URL.

```javascript

<div className="image-placeholder">
   {gift.image ? (
       <img src={gift.image} alt={gift.name} className="card-img-top" />
   ) : (
       <div className="no-image-available">No Image Available</div>
   )}
</div>
```
</details>

Task 5: Display gift name

<details>
<summary>Click here for a hint</summary>

   Display the gift\'s name using the `gift.name` property. Wrap the name in an `<h5>` tag to ensure it uses the appropriate styling for a card title.

   ```javascript
   <h5 className="card-title">{gift.name}</h5>
   ```
</details>

Task 6: Display formatted date

<details>
<summary>Click here for a hint</summary>

Call the `formatDate` function, passing in the `gift.date_added` property to display the formatted date. Ensure the `gift.date_added` property is correctly passed to the `formatDate` function and rendered within a paragraph tag.

```javascript
<p className="card-text">{formatDate(gift.date_added)}</p>
```
</details>


::page{title="Step 2: Modify Navbar Component"}

Modify `Navbar.js` to provide navigation to `Home` and `Gifts`.

### Tasks:

1. Add links to Home and Gifts in the space provided in the `NavBar.js` to link to home page and the MainPage respectively.



::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/Navbar/Navbar.js"}

You have been provided with the template. Use the following hints to complete the implementation of the component.

### Hints for Modifying Navbar Component

Task 1: Add links to Home and Gifts in the space provided in the `NavBar.js` to link to home page and the MainPage respectively.

<details>
<summary>Click here for a hint</summary>

Add direct links to Home and Gifts pages.

```html
                    <li className="nav-item">
                    <a className="nav-link" href="/home.html">Home</a> {/* Link to home.html */}
                    </li>
                    <li className="nav-item">
                        <a className="nav-link" href="/app">Gifts</a> {/* Updated Link */}
                    </li>
```
</details>

::page{title="Step 3: Test Your Code"}

You should test your code to ensure it runs properly.

1. If the MongoDB is not running, start MongoDB and copy the password and paste it in the `.env` file in the `giftlink-backend` folder.

2. Open a new terminal.

3. Go to `giftlink-backend` directory.

4. `npm install` and run the server.

> The server should be able to serve the end points that you created as part of the previous modules.

5. Launch the application in port `3060`.

6. Copy the URL in the browser.

7. Rename `.env.sample` inside the `giftlink-frontend` to `.env`.

8. Paste the URL you had copied in step 6, as the backend URL to the `.env` file without the `/` at the end.

9. Open a new terminal and go to `giftlink-frontend` directory.

10. Run `npm install` and `npm run build`.

11. Run `npm start` to start the front end application.

12. Launch the application in port `3000`. You should be able to see the following output on the browser, if everything is done correctly.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m3/images/sample%20mainpage.png" style="margin:1cm;border:solid grey 1pt">

13. Click on the `Home` button to see if it takes you to the home.html you created in the previous lab.

14. Clicking `Get Started` on the Home page should take you back to the Main page.

::page{title="Step 3: Push Changes to GitHub"}

After implementing the MainPage component and adjusting the Navbar, it\'s time to push your changes to GitHub.

>Remember to congifure git with username and email before you proceed with the task

### Tasks

1. Stage your changes for commit.
2. Commit your changes with a meaningful message.
3. Push the changes to your GitHub repository.

### Hints for Git Commands

1. **Hint for staging changes:**
   <details>
   <summary>Click here for a hint</summary>
   ```plaintext
   git add .
   ```
   Use `git add .` to stage all modified files for commit.
   </details>

2. **Hint for committing changes:**
   <details>
   <summary>Click here for a hint</summary>
   ```plaintext
   git commit -m "Updated MainPage and Navbar components for better user experience."
   ```
   Replace the message with a brief description of the changes you made.
   </details>

3. **Hint for pushing to GitHub:**
   <details>
   <summary>Click here for a hint</summary>
   ```plaintext
   git push
   ```
   Use `git push` to upload your committed changes to your GitHub repository.
   </details>

::page{title="Step 4: Final Solution"}

Ensure your final solution is correctly implemented and ready for submission.

### Final Solution

Confirm that your `MainPage.js` component correctly fetches and displays the list of gifts.

Final solution for `giftlink-frontend/src/components/MainPage/MainPage.js`
   <details>
   <summary>Click here for a hint</summary>

```js
	import React, { useState, useEffect } from 'react';
	import { useNavigate } from 'react-router-dom';
	import {urlConfig} from '../../config';

	function MainPage() {
		const [gifts, setGifts] = useState([])
		const navigate = useNavigate();

		useEffect(() => {
			// fetch all gifts
			const fetchGifts = async () => {
				try {
					let url = `${urlConfig.backendUrl}/api/gifts`
					const response = await fetch(url);
					if (!response.ok) {
						//something went wrong
						throw new Error(`HTTP error; ${response.status}`)
					}
					const data = await response.json();
					setGifts(data);
				} catch (error) {
					console.log('Fetch error: ' + error.message);
				}
			};

			fetchGifts();
		}, []);

		const goToDetailsPage = (productId) => {
			navigate(`/app/product/${productId}`);
		};

		const formatDate = (timestamp) => {
			const date = new Date(timestamp * 1000);
			return date.toLocaleString('default', { month: 'long', day: 'numeric', year: 'numeric' });
		};

		const getConditionClass = (condition) => {
			return condition === "New" ? "list-group-item-success" : "list-group-item-warning";
		};

		return (
			<div className="container mt-5">
				<div className="row">
					{gifts.map((gift) => (
						<div key={gift.id} className="col-md-4 mb-4">
							<div className="card product-card">
								<div className="image-placeholder">
									{gift.image ? (
										<img src={gift.image} alt={gift.name} />
									) : (
										<div className="no-image-available">No Image Available</div>
									)}
								</div>
								<div className="card-body">
									<h5 className="card-title">{gift.name}</h5>
									<p className={`card-text ${getConditionClass(gift.condition)}`}>
										{gift.condition}
									</p>
									<p className="card-text date-added">
										{formatDate(gift.date_added)}
									</p>
								</div>
								<div className="card-footer">
									<button onClick={() => goToDetailsPage(gift.id)} className="btn btn-primary w-100">
										View Details
									</button>
								</div>
							</div>
						</div>
					))}
				</div>
			</div>
		);
	}
	export default MainPage;
```
</details>

Ensure your `Navbar.js` component is properly adjusted to reflect the simplified user interface without authentication.

Final solution for `giftlink-frontend/src/components/Navbar/Navbar.js`
<details>
<summary>Click here for a hint</summary>

```js
import React from 'react';

export default function Navbar() {
    return (
        <nav className="navbar navbar-expand-lg navbar-light bg-light">
            <a className="navbar-brand" href="/">GiftLink</a>
            <div className="collapse navbar-collapse" id="navbarNav">
                <ul className="navbar-nav">

                    <li className="nav-item">
                    <a className="nav-link" href="/home.html">Home</a> {/* Link to home.html */}
                    </li>
                    <li className="nav-item">
                        <a className="nav-link" href="/app">Gifts</a> {/* Updated Link */}
                    </li>
                </ul>
            </div>
        </nav>
    );
}
```
</details>



## Author

Skills Network

<!--
## Changelog

| Date       | Version | Changed by | Change Description        |
|------------|---------|------------|---------------------------|
| 2024-01-20 | 0.1     | UL         | Initial version created   |
| 2024-02-22 | 0.2     | MS         | QA pass with edits        |
|2026-01-30  | 0.1 | Manvi Gupta | Created and updated lab for Mark and PR |
-->

## <h3 align="center"> © IBM Corporation. All rights reserved. </h3>
