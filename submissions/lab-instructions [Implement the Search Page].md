::page{title="Implement the Search Page"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to **Implement the Search Page** for the `giftlink-frontend` project. This lab focuses on developing a search functionality that allows users to find gifts based on various criteria such as category, condition, and age.

## Objectives

- Implement the `SearchPage.js` component to enable searching for gifts.
- Style the search page using CSS in `SearchPage.css`.
- Add `/app/search` route to `App.js`.
- Add `Search` link to the navigation bar, in `NavBar.js`.

## Prerequisite

Ensure the `giftlink-frontend` project is set up in your local environment, as it will be your working directory for the lab.

::page{title="Step 1: Implement SearchPage Component"}

Develop `SearchPage.js` to enable search functionality.

### Tasks

1. Define state variables for the search query, age range, and search results.
2. Fetch search results from the API based on user inputs.
3. Dynamically generate category and condition dropdown options.
4. Implement an age range slider and display the selected value.
5. Display search results and handle empty results with a message.
6. Enable navigation to the details page of a selected gift.
7. Add text input field for search criteria.
8. Implement the search button to trigger the search operation.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/SearchPage/SearchPage.js"}

You have been provided with the template. Use the following hints to complete the implementation of the component.

### Hints for Implementing SearchPage Component

1. **Initialize state variables for search criteria and results:**

<details>
	<summary>Click here for the answer</summary>

- Use `const [<state>,<setter>] = useState(<initial value>);` to store the searchQuery, ageRange and the searchResults.

```js
	const [searchQuery, setSearchQuery] = useState('');
    const [ageRange, setAgeRange] = useState(6); // Initialize with minimum value
    const [searchResults, setSearchResults] = useState([]);
```
</details>

2. **Fetch search results based on user inputs:**

<details>
	<summary>Click here for the answer</summary>

- Construct the search URL with `const queryParams = new URLSearchParams({ name: searchQuery, age_years: ageRange, ... }).toString();`

- Fetch the search results using ```await fetch(`${baseUrl}${queryParams}`);```

- Update the search results state with `setSearchResults(data);` upon successful fetch.

```js
	const handleSearch = async () => {
        // Construct the search URL based on user input
        const baseUrl = `${urlConfig.backendUrl}/api/search?`;
        const queryParams = new URLSearchParams({
            name: searchQuery,
            age_years: ageRange,
            category: document.getElementById('categorySelect').value,
            condition: document.getElementById('conditionSelect').value,
        }).toString();

        try {
            const response = await fetch(`${baseUrl}${queryParams}`);
            if (!response.ok) {
                throw new Error('Search failed');
            }
            const data = await response.json();
            setSearchResults(data);
        } catch (error) {
            console.error('Failed to fetch search results:', error);
        }
    };
```
</details>

3. **Dynamically generate category and condition dropdown options:**

<details>
	<summary>Click here for the answer</summary>

- Map through the `categories` array to render `<option>` elements for each category within the select dropdown.

- Similar to categories, map through the `conditions` array for the condition select dropdown.

```js
	{/* Category Dropdown */}
	<label htmlFor="categorySelect">Category</label>
	<select id="categorySelect" className="form-control my-1">
		<option value="">All</option>
		{categories.map(category => (
		<option key={category} value={category}>{category}</option>
		))}
	</select>

	{/* Condition Dropdown */}
	<label htmlFor="conditionSelect">Condition</label>
	<select id="conditionSelect" className="form-control my-1">
		<option value="">All</option>
		{conditions.map(condition => (
		<option key={condition} value={condition}>{condition}</option>
		))}
	</select>
```

</details>

4. **Implement age range slider:**

<details>
	<summary>Click here for the answer</summary>

- Use an `<input type="range">` element for the age slider, binding its value to `ageRange` and updating it on change.

```js
	{/* Age Range Slider */}
	<label htmlFor="ageRange">Less than {ageRange} years</label>
	<input
		   type="range"
		   className="form-control-range"
		   id="ageRange"
		   min="1"
		   max="10"
		   value={ageRange}
		   onChange={e => setAgeRange(e.target.value)}
	/>
```
</details>

5. **Display fetched search results:**

<details>
	<summary>Click here for the answer</summary>

```js
	<div className="search-results mt-4">
		{searchResults.length > 0 ? (
		searchResults.map(product => (
		<div key={product.id} className="card mb-3">
			{/* Check if product has an image and display it */}
			<img src={product.image} alt={product.name} className="card-img-top" />
			<div className="card-body">
				<h5 className="card-title">{product.name}</h5>
				<p className="card-text">{product.description.slice(0, 100)}...</p>
			</div>
			<div className="card-footer">
				<button onClick={() => goToDetailsPage(product.id)} className="btn btn-primary">
					View More
				</button>
			</div>
		</div>
		))
		) : (
		<div className="alert alert-info" role="alert">
			No products found. Please revise your filters.
		</div>
		)}
	</div>

```
</details>

6. **Navigate to the details page when a result is clicked:**

<details>
	<summary>Click here for the answer</summary>

- Use `navigate(path_to_prodid);` to redirect the user to the detailed page of the clicked product.

```js
navigate(`/app/product/${productId}`);
```
</details>


7. **Add text input field for search criteria**

<details>
	<summary>Click here for the answer</summary>

- Implement an input field for users to type their search query, updating the `searchQuery` state as the input changes.
</details>

8. **Implement search button with onClick event to trigger search:**

<details>
	<summary>Click here for the answer</summary>

- Add a search button and set its `onClick` event to call the `handleSearch` function.
</details>

::page{title="Step 2: Style SearchPage Component"}

Style the search page to enhance the visual presentation and user experience.

### Tasks for `SearchPage.css`

1. Style the search input field.
2. Style the search button.
3. Customize dropdown filters for category and condition.
4. Style the age range slider.
5. Enhance search results cards appearance.
6. Style the "No products found" alert message.
7. Apply a hover effect to the search results cards.
8. Ensure images in search results are displayed appropriately.
9. Create a responsive layout for search results on various devices.
10. Overall page styling for a cohesive and user-friendly design.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/SearchPage/SearchPage.css"}

You have been provided with the code template. Use the hints below to complete the tasks.

### Hints for Styling SearchPage Component

1. **Hint for Task 1 - Style the search input field:**
   <details>
   <summary>Click here for a hint</summary>
   - `width`: `75%`<br>
   - `margin-right`: `1rem`
   </details>

2. **Hint for Task 2 - Style the search button:**
   <details>
   <summary>Click here for a hint</summary>
   - `width`: `20%`<br>
   - `background-color`: `#007bff`<br>
   - `color`: `#ffffff`
   </details>

3. **Hint for Task 3 - Customize dropdown filters:**
   <details>
   <summary>Click here for a hint</summary>
   - `margin-bottom`: `1rem`<br>
   - `border`: `1px solid #ced4da`
   </details>

4. **Hint for Task 4 - Style the age range slider:**
   <details>
   <summary>Click here for a hint</summary>
   - `width`: `100%`
   </details>

5. **Hint for Task 5 - Enhance search results cards appearance:**
   <details>
   <summary>Click here for a hint</summary>
   - `box-shadow`: `0 2px 5px rgba(0,0,0,0.2)`<br>
   - `border-radius`: `10px`
   </details>

6. **Hint for Task 6 - Style the "No products found" alert message:**
   <details>
   <summary>Click here for a hint</summary>
   - `background-color`: `#f8d7da`<br>
   - `color`: `#721c24`<br>
   - `padding`: `0.75rem 1.25rem`<br>
   - `margin-top`: `1rem`<br>
   - `border`: `1px solid transparent`<br>
   - `border-radius`: `0.25rem`
   </details>

7. **Hint for Task 7 - Apply a hover effect to search results cards:**
   <details>
   <summary>Click here for a hint</summary>
   - `transition`: `box-shadow 0.3s ease-in-out`<br>
   - `&:hover`: <br>
     - `box-shadow`: `0 4px 8px rgba(0,0,0,0.2)`
   </details>

8. **Hint for Task 8 - Ensure images in search results are displayed appropriately:**
   <details>
   <summary>Click here for a hint</summary>
   - `.card-img-top`: <br>
     - `width`: `100%`<br>
     - `height`: `200px`<br>
     - `object-fit`: `cover`
   </details>

9. **Hint for Task 9 - Create a responsive layout for search results on various devices:**
   <details>
   <summary>Click here for a hint</summary>
   - Use media queries to adjust layout styles for smaller screens:<br>
     - `@media (max-width: 768px)`: <br>
       - Adjust card layout, image sizes, and text sizing for optimal readability.
   </details>

10. **Hint for Task 10 - Overall page styling for a cohesive and user-friendly design:**
    <details>
    <summary>Click here for a hint</summary>
    - Consider using a consistent color scheme throughout the page.<br>
    - Utilize spacing and padding to create a visually appealing layout.<br>
    - Ensure text is readable against background colors.<br>
    - Style interactive elements (buttons, inputs) for clear visibility and usability.
    </details>


It is a good idea to test your code at this point in time. Follow the same process suggested in the earlier lab. Start the backend, configure the backend URL in the front end and check if the SearchPage renders and functions as desired. Below is the sample SearchPage.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/labs/v1/m3/images/searchpage.png" style="padding:1cm; border: bold 1pt grey">

::page{title="Step 3: Add routes and navigation links"}

### Tasks
1. Add Routes for this in App.js

2. Add the Nav links also for this in NavBar.js, to click and access `SearchPage from the app

### Hints

1. **Hint for Task 1 - Add Routes for this in App.js**

<details><summary>Click here for a hint</summary>

- Add this along with other imports.
```
import SearchPage from './components/SearchPage/SearchPage';
```

- Add this along with the other routes.
```
<Route path="/app/search" element={<SearchPage/>} />
```
</details>

2. **Hint for Task 2 - Add the Nav links also for this in NavBar.js, to click and access `SearchPage from the app**

<details><summary>Click here for a hint</summary>

Add this link after the Gifts link in `Navrbar.js`.
```
<li className="nav-item">
	<Link className="nav-link" to="/app/search">Search</Link>
</li>
```
</details>


::page{title="Step 4: Push Changes to GitHub"}

After completing the implementation and styling, commit and push your changes to GitHub.

### Tasks

1. Stage your changes using Git.
2. Commit your changes with a descriptive message.
3. Push the changes to your GitHub repository.

### Hints for Git Commands

1. **Stage Changes:** Use `git add .` to add all changes.
2. **Commit Changes:** Use `git commit -m "Implement search functionality and style SearchPage."`.
3. **Push Changes:** Use `git push` to update your repository on GitHub.


::page{title="Step 5: Final Solution"}

Showcase your completed Search Page implementation.

### Final Solution

Your `SearchPage.js` should now enable users to effectively search for gifts with various filters, and `SearchPage.css` should provide a polished and responsive UI.

1. Final solution for `giftlink-frontend/src/components/SearchPage/SearchPage.js`

<details>
<summary>Click here for a hint</summary>

```js
import React, { useEffect, useState } from 'react';
import { useNavigate } from 'react-router-dom';
import 'bootstrap/dist/css/bootstrap.min.css';
import {urlConfig} from '../../config';

function SearchPage() {
    const [searchQuery, setSearchQuery] = useState('');
    const [ageRange, setAgeRange] = useState(6); // Initialize with minimum value
    const [searchResults, setSearchResults] = useState([]);
    const categories = ['Living', 'Bedroom', 'Bathroom', 'Kitchen', 'Office'];
    const conditions = ['New', 'Like New', 'Older'];

    useEffect(() => {
        // fetch all products
        const fetchProducts = async () => {
            try {
                let url = `${urlConfig.backendUrl}/api/gifts`
                console.log(url)
                const response = await fetch(url);
                if (!response.ok) {
                    //something went wrong
                    throw new Error(`HTTP error; ${response.status}`)
                }
                const data = await response.json();
                setSearchResults(data);
            } catch (error) {
                console.log('Fetch error: ' + error.message);
            }
        };

        fetchProducts();
    }, []);


    const handleSearch = async () => {
        // Construct the search URL based on user input
        const baseUrl = `${urlConfig.backendUrl}/api/search?`;
        const queryParams = new URLSearchParams({
            name: searchQuery,
            age_years: ageRange,
            category: document.getElementById('categorySelect').value,
            condition: document.getElementById('conditionSelect').value,
        }).toString();

        try {
            const response = await fetch(`${baseUrl}${queryParams}`);
            if (!response.ok) {
                throw new Error('Search failed');
            }
            const data = await response.json();
            setSearchResults(data);
        } catch (error) {
            console.error('Failed to fetch search results:', error);
        }
    };

    const navigate = useNavigate();

    const goToDetailsPage = (productId) => {
        navigate(`/app/product/${productId}`);
    };

    return (
        <div className="container mt-5">
            <div className="row justify-content-center">
                <div className="col-md-6">
                    <div className="filter-section mb-3 p-3 border rounded">
                        <h5>Filters</h5>
                        <div className="d-flex flex-column">
                            {/* Category Dropdown */}
                            <label htmlFor="categorySelect">Category</label>
                            <select id="categorySelect" className="form-control my-1">
                                <option value="">All</option>
                                {categories.map(category => (
                                    <option key={category} value={category}>{category}</option>
                                ))}
                            </select>

                            {/* Condition Dropdown */}
                            <label htmlFor="conditionSelect">Condition</label>
                            <select id="conditionSelect" className="form-control my-1">
                                <option value="">All</option>
                                {conditions.map(condition => (
                                    <option key={condition} value={condition}>{condition}</option>
                                ))}
                            </select>

                            {/* Age Range Slider */}
                            <label htmlFor="ageRange">Less than {ageRange} years</label>
                            <input
                                type="range"
                                className="form-control-range"
                                id="ageRange"
                                min="1"
                                max="10"
                                value={ageRange}
                                onChange={e => setAgeRange(e.target.value)}
                            />
                        </div>
                    </div>

                    <input
                        type="text"
                        className="form-control mb-2"
                        placeholder="Search for items..."
                        value={searchQuery}
                        onChange={e => setSearchQuery(e.target.value)}
                    />
                    <button className="btn btn-primary" onClick={handleSearch}>Search</button>
                    <div className="search-results mt-4">
                        {searchResults.length > 0 ? (
                            searchResults.map(product => (
                                <div key={product.id} className="card mb-3">
                                    {/* Check if product has an image and display it */}
                                    <img src={product.image} alt={product.name} className="card-img-top" />
                                    <div className="card-body">
                                        <h5 className="card-title">{product.name}</h5>
                                        <p className="card-text">{product.description.slice(0, 100)}...</p>
                                    </div>
                                    <div className="card-footer">
                                        <button onClick={() => goToDetailsPage(product.id)} className="btn btn-primary">
                                            View More
                                        </button>
                                    </div>
                                </div>
                            ))
                        ) : (
                            <div className="alert alert-info" role="alert">
                                No products found. Please revise your filters.
                            </div>
                        )}
                    </div>
                </div>
            </div>
        </div>
    );
}

export default SearchPage;

```
   </details>

1. Final solution for `giftlink-frontend/src/components/SearchPage/SearchPage.css`

<details>
   <summary>Click here for a hint</summary>

```css
	.search-bar {
		display: flex;
		justify-content: space-between;
		margin-bottom: 1rem;
	}

	.search-bar .form-control {
		width: 75%; /* Adjust based on your design preference */
		margin-right: 1rem;
	}

	.search-bar .btn {
		width: 20%; /* Adjust based on your design preference */
	}

	.card {
		/* Use similar styles as in MainPage.css */
		box-shadow: 0 2px 5px rgba(0,0,0,0.2);
		border-radius: 10px;
	}

	.card-body {
		padding: 1rem;
	}

	.card-footer {
		text-align: right;
		padding: 0.5rem 1rem;
		border-top: 1px solid #ddd;
	}

	.card-title {
		font-size: 1.2rem;
		color: #0056b3;
	}

	.card-text {
		color: #333;
		margin-bottom: 0.5rem;
	}

	.btn-info {
		color: #fff;
		background-color: #17a2b8;
		border-color: #17a2b8;
	}

	.btn-info:hover {
		background-color: #138496;
		border-color: #117a8b;
	}

	.fas.fa-arrow-right {
		margin-left: 5px;
	}

	.card-img-top {
		width: 100%; /* Full width */
		height: 180px; /* Fixed height */
		object-fit: cover; /* Cover the entire area without stretching */
	}

	.card {
		transition: box-shadow 0.3s ease-in-out;
	}

	.card:hover {
		box-shadow: 0 4px 10px rgba(0,0,0,0.3);
	}

	.card-body {
		padding: 1rem;
	}

	.card-footer {
		text-align: center;
		padding: 1rem;
		border-top: none;
	}

	.card-title {
		font-size: 1.2rem;
		color: #0056b3;
		margin-bottom: 0.5rem;
	}

	.card-text {
		color: #333;
	}

	.btn-primary {
		background-color: #009688; /* A shade of teal for a modern look */
		border: none;
	}

	.btn-primary:hover {
		background-color: #00796b; /* A darker shade of teal for hover state */
	}

	/* Responsive design for smaller screens */
	@media (max-width: 768px) {
		.search-bar .form-control,
		.search-bar .btn {
			width: 100%; /* Full width for small screens */
			margin-right: 0;
			margin-bottom: 0.5rem;
		}

		.search-bar .btn {
			width: auto; /* Auto width for button to fit content */
		}
	}
```
</details>


## Author(s)

Skills Networks

<!--## Changelog

| Date       | Version | Changed by | Change Description        |
|------------|---------|------------|---------------------------|
| 2024-01-29 | 0.1     | UL  | Initial version created   |
|2026-01-30  | 0.1 | Manvi Gupta | Created and updated lab for Mark and PR |-->

## <h3 align="center"> © IBM Corporation. All rights reserved. </h3>
