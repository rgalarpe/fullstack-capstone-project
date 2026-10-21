::page{title="Implement the Details Page"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

##

Welcome to **Implement the Details Page** for the `giftlink-frontend` project. This lab focuses on developing a detailed view for individual gift items and enhancing the user interface with CSS styling.

## Objectives

- Implement the `DetailsPage.js` component to fetch and display detailed information about a gift.
- Style the Details Page using CSS in `DetailsPage.css`.

## Prerequisite

- Ensure you have completed the previous modules and pushed all the changes to Github.
- You should have the `giftlink-frontend` directory in your repository cloned to your local environment, or you will clone the repository that contains all of your pushed code. This will be your working directory for the lab

::page{title="Step 1: Implement DetailsPage Component"}

Develop `DetailsPage.js` to display detailed information about gifts.

### Tasks

1. Check for authentication and redirect if necessary.
2. Fetch gift details using the gift ID from the URL.
3. Implement scrolling to the top of the page on component mount.
4. Handle user click to navigate back to the previous page.
5. Display the gift details fetched from the API.
6. Dynamically render the comments section for the gift.
7. Ensure error handling for failed fetch operations and display appropriate messages.
8. Add the route to this page in `App.js`.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/DetailsPage/DetailsPage.js"}

You have been provided with the template. Use the hints below to complete the tasks.

### Hints for Implementing DetailsPage Component

1. **Hint for Task 1, Check for Authentication**

<details>
<summary>Click here for a hint</summary>

The code already checks for authentication token. You need to use the `navigate` to redirect to the login page. Note that sessionStorage in React persists data only for the duration set by the server. It is stored on the client side, but you control its duration by the server. Use `navigate('/app/login')` code.
   </details>

2. **Hint for Task 2, Fetch Gift Details**

<details>
<summary>Click here for a hint</summary>

   Use `await` and `fetch` with a template literal to construct the URL `/api/gifts/${productId}` for the GET request. Handle the response and possible errors.
```
const response = await fetch(`${urlConfig.backendUrl}/api/gifts/${productId}`);
```
   </details>

3. **Hint for Task 3, Scroll to Top**

<details>
<summary>Click here for a hint</summary>

Utilize `window.scrollTo(0, 0)` to scroll to the top of the page right after the component mounts. This ensures users are taken to the top of the page for a fresh view of the details.
   </details>

4. **Hint for Task 4, Handle Back Click**

<details>
<summary>Click here for a hint</summary>

Use `navigate(-1)` to take the user back to the previous page they were on.
</details>

5. **Hint for Task 5, Display Gift Image**

<details>
<summary>Click here for a hint</summary>

   The code is checking an image exists for a gift. If the iamge exists, display it using an `<img>` tag. If the image is not avaliable the code shows a placeholder indicating "No Image Available".

```
<img src={gift.image} alt={gift.name} className="product-image-large" />
```
</details>

6. **Hint for Task 6, Display Gift Details**

<details>
<summary>Click here for a hint</summary>

Display the gift's name, category, condition, date added, age, and description using the data fetched. You can get the property for the gift by using the dot opertor. For example; `gift.category`.
   </details>

7. **Hint for Task 7, Render Comments Section**

<details>
<summary>Click here for a hint</summary>

Map through the `comments` array to dynamically create and display each comment in the UI. Use the map function `{comments.map((comment, index) => (`.

</details>

8. **Hint for Task 8, Add the route to this page in `App.js`.**

<details>
<summary>Click here for a hint</summary>

- Add this along with other imports.
```
import DetailsPage from './components/DetailsPage/DetailsPage';
```

- Add this along with the other routes.
```
<Route path="/app/product/:productId" element={<DetailsPage/>} />
```
</details>


::page{title="Step 2: Style DetailsPage Component"}

Style the details page to enhance the visual presentation.

### Tasks

1. Style the image placeholder for a larger display.
2. Ensure the product image fits the container appropriately.
3. Provide styling for when there\'s no image available.
4. Style the card header to match the application\'s theme.
5. Apply additional styles to the `.details-title` for better visibility.
6. Style the comments section for readability.

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/src/components/DetailsPage/DetailsPage.css"}

#### Code Template for `DetailsPage.css`

```css
/* Style for image placeholder */
.image-placeholder-large {
    /* Task 1 styling */
    /* Insert code under this */
}

/* Style for product image */
.product-image-large {
    /* Task 2 styling */
    /* Insert code under this */
}

/* Style for 'no image available' placeholder */
.no-image-available-large {
    /* Task 3 styling */
    /* Insert code under this */
}

/* Style for card header */
.card-header {
    /* Task 4 styling */
    /* Insert code under this */
}

/* Style for details title */
.details-title {
    /* Task 5 styling */
    /* Insert code under this */
}

/* Style for comments section */
.comments-section {
    /* Task 6 styling */
    /* Insert code under this */
}
```

### Hints for Styling DetailsPage Component

1. **Hint for Task 1 - Styling the Image Placeholder**
   <details>
   <summary>Click here for a hint</summary>

	Set the width to 100%, height to 400px, and position to relative. Use `background-color` for the placeholder.
   </details>

2. **Hint for Task 2 - Styling the Product Image**
   <details>
   <summary>Click here for a hint</summary>

	Ensure the image covers the area with `object-fit: cover`. Set width and height to 100%.
   </details>

3. **Hint for Task 3 - Styling 'No Image Available' Placeholder**
   <details>
   <summary>Click here for a hint</summary>
   Use flexbox to center the text inside the placeholder. Set the background color, font size, and color appropriately.
   </details>

4. **Hint for Task 4 - Styling the Card Header**
   <details>
   <summary>Click here for a hint</summary>
   Choose a background color that matches the theme and set the text color to white for contrast.
   </details>

5. **Hint for Task 5 - Styling the Details Title**
   <details>
   <summary>Click here for a hint</summary>
   Apply font size and color to make the title stand out.
   </details>

6. **Hint for Task 6 - Styling the Comments Section**
   <details>
   <summary>Click here for a hint</summary>

	Style the comments section to improve readability. Consider margins, padding, and background colors.
   </details>

::page{title="Step 3: Push Changes to GitHub"}

After implementing the `DetailsPage` component and applying styles with `DetailsPage.css`, push your changes back to GitHub.

### Tasks

1. Stage your changes using Git.
2. Commit your changes with a descriptive message.
3. Push the changes to your GitHub repository.

### Hints for Git Commands

1. **Hint for Staging Changes**
   <details>
   <summary>Click here for a hint</summary>
   Use `git add .` to stage all modified files for committing.
   </details>

2. **Hint for Committing Changes**
   <details>
   <summary>Click here for a hint</summary>
   Use `git commit -m "Your descriptive message"` to commit your staged changes. Replace `"Your descriptive message"` with a summary of what changes were made.
   </details>

3. **Hint for Pushing to GitHub**
   <details>
   <summary>Click here for a hint</summary>
   Use `git push` to upload your local repository changes to the remote repository on GitHub.
   </details>

::page{title="Step 4: Final Solution"}

Ensure your final solution is correctly implemented and ready for submission.Verify that your implementation matches the task requirements and test the page to ensure it displays the gift details correctly and is styled as intended.

### Final Solution

Your `DetailsPage.js` should now fetch and display the details of a gift dynamically from the backend API, and `DetailsPage.css` should style the details page according to the tasks outlined.

<details><summary>Click here for DetailsPage.js</summary>

```
import React, { useEffect, useState } from 'react';
import { useParams, useNavigate } from 'react-router-dom';
import './DetailsPage.css';
import {urlConfig} from '../../config';

function DetailsPage() {
    const navigate = useNavigate();
    const { productId } = useParams();
    const [gift, setGift] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        const authenticationToken = sessionStorage.getItem('auth-token');
        if (!authenticationToken) {
            // Task 1: Check for authentication and redirect
            navigate('/app/login');
        }

        // get the gift to be rendered on the details page
        const fetchGift = async () => {
            try {
                // Task 2: Fetch gift details
                const url = `${urlConfig.backendUrl}/api/gifts/${productId}`;
                const response = await fetch(url);
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                const data = await response.json();
                setGift(data);
            } catch (error) {
                setError(error.message);
            } finally {
                setLoading(false);
            }
        };

        fetchGift();

        // Task 3: Scroll to top on component mount
        window.scrollTo(0, 0);

    }, [productId, navigate]);

    const handleBackClick = () => {
        // Task 4: Handle back click
        navigate(-1);
    };

    //The comments have been hardcoded for this project.
    const comments = [
        {
            author: "John Doe",
            comment: "I would like this!"
        },
        {
            author: "Jane Smith",
            comment: "Just DMed you."
        },
        {
            author: "Alice Johnson",
            comment: "I will take it if it's still available."
        },
        {
            author: "Mike Brown",
            comment: "This is a good one!"
        },
        {
            author: "Sarah Wilson",
            comment: "My family can use one. DM me if it is still available. Thank you!"
        }
    ];

    if (loading) return <div>Loading...</div>;
    if (error) return <div>Error: {error}</div>;
    if (!gift) return <div>Gift not found</div>;

    return (
        <div className="container mt-5">
            <button className="btn btn-secondary mb-3" onClick={handleBackClick}>Back</button>
            <div className="card product-details-card">
                <div className="card-header text-white">
                    <h2 className="details-title">{gift.name}</h2>
                </div>
                <div className="card-body">
                    <div className="image-placeholder-large">
                        {gift.image ? (
                            // Task 5: Display gift image
                            <img src={gift.image} alt={gift.name} className="product-image-large" />
                        ) : (
                            <div className="no-image-available-large">No Image Available</div>
                        )}
                    </div>
                    {/* Task 6: Display gift details */}
                    <p><strong>Category:</strong> 
                        {gift.category}
                    </p>
                    <p><strong>Condition:</strong> 
                        {gift.condition}
                    </p>
                    <p><strong>Date Added:</strong> 
                        {gift.dateAdded}
                    </p>
                    <p><strong>Age (Years):</strong> 
                        {gift.age}
                    </p>
                    <p><strong>Description:</strong> 
                        {gift.description}
                    </p>
                </div>
            </div>
            <div className="comments-section mt-4">
                <h3 className="mb-3">Comments</h3>
                {/* Task 7: Render comments section */}
                {comments.map((comment, index) => (
                    <div key={index} className="card mb-3">
                        <div className="card-body">
                            <p className="comment-author"><strong>{comment.author}:</strong></p>
                            <p className="comment-text">{comment.comment}</p>
                        </div>
                    </div>
                ))}
            </div>
        </div>
    );
}

export default DetailsPage;

```
</details>

<details><summary>Click here for DetailsPage.css</summary>

```
/* Style for image placeholder */
.image-placeholder-large {
    width: 100%; /* Task 1: Set width to 100% */
    height: 400px; /* Task 1: Set height to 400px */
    position: relative; /* Task 1: Set position to relative */
    background-color: #f0f0f0; /* Task 1: Placeholder background color */
    /* Additional styles as needed */
}

/* Style for product image */
.product-image-large {
    width: 100%; /* Task 2: Set width to 100% */
    height: 100%; /* Task 2: Set height to 100% */
    object-fit: cover; /* Task 2: Ensure the image covers the area */
    /* Additional styles as needed */
}

/* Style for 'no image available' placeholder */
.no-image-available-large {
    display: flex; /* Task 3: Use flexbox */
    align-items: center; /* Task 3: Center the text vertically */
    justify-content: center; /* Task 3: Center the text horizontally */
    background-color: #ccc; /* Task 3: Set background color */
    color: #333; /* Task 3: Set text color */
    font-size: 18px; /* Task 3: Set font size */
    /* Additional styles as needed */
}

/* Style for card header */
.card-header {
    background-color: #007bff; /* Task 4: Choose a background color */
    color: #fff; /* Task 4: Set text color to white */
    text-align: center;
    padding: 15px;
    /* Additional styles as needed */
}

/* Style for details title */
.details-title {
    font-size: 28px; /* Task 5: Apply font size */
    color: #333; /* Task 5: Set text color */
    font-weight: bold; /* Task 5: Make the title bold */
    /* Additional styles as needed */
}

/* Style for comments section */
.comments-section {
    /* Task 6: Style the comments section for readability */
    margin-top: 20px; /* Add top margin for spacing */
    /* Additional styles as needed */
}


/* Style for individual comment card */
.comments-section .card {
    margin-bottom: 15px; /* Add bottom margin for spacing between cards */
    /* Additional styles for individual comment card */
}


/* Style for comment author */
.comments-section .comment-author {
    font-weight: bold; /* Make the comment author's name bold */
    /* Additional styles for comment author */
}


/* Style for comment text */
.comments-section .comment-text {
    /* Additional styles for comment text */
    color: #555;
}

```
</details>


## Author(s)

Skills Network

<!---
## Changelog

| Date       | Version | Changed by | Change Description        |
|------------|---------|------------|---------------------------|
| 2024-01-05 | 0.1     | Upkar  | Initial version created   |
|2026-01-30  | 0.1 | Manvi Gupta | Created and updated lab for Mark and PR |-->


## <h3 align="center"> © IBM Corporation. All rights reserved. </h3>
