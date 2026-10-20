::page{title="Create the Landing Page"}

**Estimated duration**: 60 mins

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMSkillsNetwork-JS0322EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to **Create the Landing Page**. In this lab, you will develop the landing page for the project by implementing specific design elements and functionality in HTML and CSS. This exercise aims to enhance your skills in front-end development, focusing on building a responsive and visually appealing landing page.

## Objectives

- Structure the landing page content by modifying `home.html`.
- Apply CSS styles to the landing page by editing `home.css`.
- Ensure the landing page is responsive and visually appealing on all devices.

## Prerequisite

Ensure your repository that is cloned to your local environment, has `giftlink-frontend`, as it will be your working directory for the lab.

::page{title="Step 1: Structure the Landing Page"}

Modify `giftlink-frontend/public/home.html` to structure the content of your landing page.

Each of these tasks will help familiarize you with structuring web content using HTML and applying Bootstrap classes for styling. Ensure each element is correctly placed within the provided &#60;div&#62; container to maintain the layout\'s integrity.

In `giftlink-frontend/public/home.html`, fill in the missing HTML elements to structure the landing page.

### Tasks

1. Add the main heading
1. Add the subheading
1. Add an inspirational quote
1. Add a **Get Started** button

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/public/home.html"}

You have been provided with the template. Use the following hints to complete the implementation of the landing page.

### Hints

Task 1: Add the main heading
<details>
<summary>Click here for a hint</summary>

Use the `<h1>` element for the main heading of the page. Apply Bootstrap's class `display-4` for styling and `mb-3` for margin-bottom spacing. Your HTML should look like this:

```
<h1 class="display-4 mb-3"> GiftLink</h1>
```

</details>


Task 2: Add the subheading
<details>
<summary>Click here for a hint</summary>

For the subheading, utilize the `<h2>` element. Include Bootstrap classes for styling, such as `mb-4` to add some bottom margin. Example:

```
<h2 class="mb-4">Share Gifts and Joy!</h2>
```

</details>

Task 3: Add the inspirational quote
<details>
<summary>Click here for a hint</summary>

Place your quote within a `<p>` element. To make it stand out, use the `lead` class provided by Bootstrap, which will style the paragraph as a leading introductory text.
Example:

```
<p class="lead">"Sharing is the essence of community. It is through giving that we enrich and perpetuate both our lives and the lives of others."</p>
```

</details>

Task 4: Add the **Get Started** button
<details>
<summary>Click here for a hint</summary>

To create a button that links to another page or section, use the `<a>` element styled as a button with Bootstrap classes. For a primary button style, use `btn btn-primary`. You should also include the destination where the button will lead when clicked, set in the `href` attribute. Example:

```
<a href="/app" class="btn btn-primary">Get Started</a>
```

</details>

::page{title="Step 2: Style the Landing Page"}

Apply CSS styling to the landing page by editing `giftlink-frontend/public/static/home.css` Complete the CSS rules in the template provided to style the landing page.

### Tasks

1. Style the body
1. Create a pseudo-element for the background and blur
1. Style the content area
1. Add styles for headings, paragraphs, and buttons

::openFile{path="/home/project/fullstack-capstone-project/giftlink-frontend/public/static/home.css"}

#### Code Template for `home.css`

```css
/* Task 1: Style the body */
body {
    /* insert code here */
}

/* Task 2: Create a pseudo-element for the background and blur */
body::before {
    /* insert code here */
}

/* Task 3: Style the content area */
.content {
    /* insert code here */
}

/* Task 4: Add styles for headings, paragraphs, and buttons */
h1, h2, .lead, .btn-primary {
    /* insert code here */
}
```

### Hints

Task 1: Styling the body

<details>
<summary>Click here for a hint</summary>

- Use font-family `'Montserrat', sans-serif;`
- Set margin as `0`
- Set padding as `0`
- Set height to `100vh`
- Set display to `flex`
- Align the items and justify the contents to `center`
- Set overflow to `hidden`
- Set the background colour to `#f4f4f4;`

</details>

Task 2: Background and blur

<details>
<summary>Click here for a hint</summary>


- Use `position: fixed`.
- Cover the entire viewport with `top: 0`, `left: 0`, `width: 100%`, and `height: 100%`.
- Set `background` with the desired image and styling.
- Apply `filter: blur(8px)` for the blur effect.


</details>

Task 3: Content area styling

<details>
<summary>Click here for a hint</summary>

- Use `position: relative`
- Set `z-index` to ensure it's above the background
- Apply text alignment and color
- Use `max-width` for maximum width
- Apply padding and background for readability


</details>

Task 4: Headings, paragraphs, and buttons

<details>
<summary>Click here for a hint</summary>

- Customize font size, weight, and color for `max-width`, `h2`
- Style `.lead` for the quote
- Adjust `.btn-primary` for the button's visual design

</details>


::page{title="Step 3: Push Changes to GitHub"}

Finally, configure your git username and email, as done in the previous lab and push your implemented changes back to your GitHub repository using stage, commit, and push  Git commands.

```
git config --global user.name "<Github username>"
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

::page{title="Step 4: Final Solution"}

Ensure your final solution is correctly implemented and ready for submission.

### Final Solution

Verify that your modifications to `home.html` and `home.css` reflect the desired layout and styling for the landing page.


<details>
<summary>Sample solution for giftlink-frontend/public/home.html</summary>

```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>GiftLink Home</title>
		<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
		<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
		<link rel="stylesheet" href="/static/home.css">
	</head>
	<body>
		<div class="container my-5">
			<div class="text-center">
				<h1 class="display-4 mb-3">GiftLink</h1>
				<h2 class="mb-4">Share Gifts and Joy!</h2>
				<p class="lead">"Sharing is the essence of community. It is through giving that we enrich and perpetuate both our lives and the lives of others."</p>
				<a href="/app" class="btn btn-primary">Get Started</a>
			</div>
		</div>
	</body>
	</html>

```
   </details>

   <details>
   <summary>Sample solution for giftlink-frontend/public/static/home.css</summary>

```css
	body {
		font-family: 'Montserrat', sans-serif;
		margin: 0;
		padding: 0;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
		background-color: #f4f4f4; /* Updated background color */
	}

	/* Create a pseudo-element for the background and blur */
	body::before {
		content: '';
		position: fixed; /* Fixed position to cover the entire viewport */
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: url('/static/background-colors.jpg') no-repeat center center;
		background-size: cover;
		filter: blur(8px); /* Slightly reduced blur effect */
		z-index: -1; /* Place it behind the content */
	}

	.content {
		position: relative;
		font-weight: 600;
		z-index: 2; /* Higher z-index to ensure content is above the blurred background */
		text-align: center;
		color: #1a1a1a; /* Updated text color for better readability */
		max-width: 1200px;
		margin: 0 auto;
		padding: 20px;
		background: rgba(255, 255, 255, 0.7); /* Semi-transparent white background */
		border-radius: 10px; /* Rounded corners for the content area */
	}

	h1, h2 {
		font-size: 4rem; /* Large font size for main heading */
		color: #333; /* Darker text color for headings */
		margin-bottom: 0.5em;

		font-weight: 700;
	}

	.lead {
		font-size: 1.5rem; /* Large font size for the quote */
		color: #333; /* Dark text color for better readability */
		margin-bottom: 2rem;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* Text shadow for legibility */
	}

	.btn-primary {
		background-color: #1E90FF; /* Vibrant color for the button */
		color: #FFFFFF; /* White text for contrast */
		border: none;
		padding: 1rem 2.5rem; /* Generous padding for a larger button */
		border-radius: 30px; /* Rounded, but not fully pill-shaped */
		font-size: 1.2rem; /* Larger font size for readability */
		font-weight: 700; /* Bold font for the button text */
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Subtle shadow for depth */
		transition: background-color 0.3s, transform 0.1s;
	}

	.btn-primary:hover,
	.btn-primary:focus {
		background-color: #f50057; /* A lighter shade for interaction feedback */
		transform: scale(1.05); /* Slightly enlarge button on hover/focus */
	}

	@media (max-width: 768px) {
		h1 {
			font-size: 3rem; /* Smaller font size for headings on mobile */
		}
		h2 {
			font-size: 2.5rem; /* Smaller font size for subheadings on mobile */
		}
		.lead {
			font-size: 1.25rem; /* Smaller font size for text on mobile */
		}
	}

```
   </details>
	
	
## Author(s)

Skills Network


<!--## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
|2026-01-30  | 0.1 | Manvi Gupta | Created and updated lab for Mark and PR |-->

##### © IBM Corporation. All rights reserved.
