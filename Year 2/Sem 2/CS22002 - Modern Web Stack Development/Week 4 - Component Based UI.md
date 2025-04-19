## **Client Side Data Handling**
### The problem with Multiple API Calls
- Fetching data from an API on every user action (e.g. typing in a search box) is inefficient
- This leads to slow response times, increased server load, and unnecessary bandwidth usage
- **EXAMPLE:** Imagine an e-commerce site fetching product data every time a user searches instead of using cached data
- As an alternative, we want to store APIU data once and search within the stored dataset
	- Remember the principles we talked about last week...

### What Happens When you fetch() Too Often?
- **It is bad practice to make** an API request **on every keystroke** in a search box.
- This causes **network congestion** and slows down the user experience
- Every keypress triggers a new fetch request... wasteful and unnecessary!
	- Every time the user types a character, a new API request is fired
	- The API gets spammed, which can lead to rate-limiting or bans
	- The UI may become sluggish due to excessive fetch calls
	- This approach does **not** debounce requests, making it highly inefficient

### Efficient API Calls using Caching
- Instead of fetching data repeatedly, **fetch it once and store it**
- Use **LocalStorage** to save API responses for quick retrieval
- **This has many benefits:**
	- Faster user experience
	- Rescues API requests
	- Works even when offline

### How to save API data locally
- Fetch and store the API response
```js
async function fetchUsers() {
	const response = await fetch("https://randomuser.me/api/?results=20");
	const data = await response.json();
	localStorage.setItem("users", JSON.stringify(data.results));
}
```
- Retrieve the stored data when needed
```js
const users = JSON.parse(localStorage.getItem("users"));
console.log(users);
```

### Check if data exists before fetching
- Before making an API request, check if the data you need is already in localStorage
```js
let cachedUsers = localStorage.getItem("users");

if (!cachedUsers) {
fetchUsers(); // Fetch only if needed
} else {
	cachedUsers = JSON.parse(cachedUsers);
	console.log("Using cached data:", cachedUsers);
}
```
- Doing this means that we don't need to do another fetch if data is already available locally.

### How do we filter JSON data?
- Instead of re-fething API data, we can use the `Array.filter()` method:
```js
const filteredUsers = users.filter(user => user.name.first.includes("John"));
```
- This works instantly because we are searching within stored data

### Handling large datasets without lag
- When we are searching through large datasets, every keypress can cause UI lag
	- This is called bouncing
- We want to use **debouncing** to prevent excessive function calls
	- In this, we can set a search to happen only after a given amount of time (300ms in this case....)
```js
let debounceTimer;
document.getElementByID("searchInput").addEventListener("input", (e) => {
	clearTimeout(debounceTimer);
	debounceTimer = setTimeout(() ={
		searchUsers(e.target.value);
	}, 300);
});
```

## **Component-Based UI**

### Why use components?
- In **modern web development**, UI elements should be **modular and reusable**
- **Instead of writing repeated HTML, we use JavaScript functions to create UI components dynamically**
```js
function createUserCard(user){
	return `<div class="card">${user.name.first}</div>`
}
```
- While we're not using React and Vue in this module... this mirrors how these libraries handle UI generation and usage

### Why should we use components...CRUMB!
- **C**onsistency - UI components look and behave the same across the app
- **R**eusability - Create once, use everywhere
- **U**pgradability - Makes adding new features simpler
- **M**odularity - Easier to debug and maintain
- **B**etter organisation - Helps avoid spaghetti code

### Understanding Component Based UI
- What is a UI Component?
	- A **self-contained unit** of UI that can be reused in multiple places
	- Typically **takes input (data) and produces output (HTML)**
- Why do we like this?
	- It reduces code duplication
	- Easier to debug as all of the logic is in one place
	- More maintainable for larger applications
```js
function createButton(label, action) {
	const button = document.createElement("button");
	button.innerText = label;
	button.className = "btn btn-success";
	button.onclick = action;
	return button;
}
```

### Making UI Components Dynamic
- Instead of hardcoding data inside a function, **pass data as parameters**
- Example: Passing user details into a dynamic card generator
```js
function createUserCard(user) {
	const card = document.createElement("div");
	card.className = "card shadow-sm";
	card.innerHTML = `
		<div class="card-body">
			<h5 class="Card-title">${user.name.first} ${user.name.last}</h5>
			<p class="card-text">Email: ${user.email}</p>
		</div>
	`;
	return card;
}
```

### Building Dynamic UI with JS functions
- Instead of us manually writing div elements in HTML, we generate UI components dynamically in Javascript
- This helps us to separate logic from structire, making our code easy to maintain and extend
- We can reuse this function any time we need a new card
- Instead of manually adding elements, JS will handle the UI updates for us

## **Multi page navigation**
### How do we navigate between pages
- When we are creating web applications, we may want to pass data dynamically between pages
- We can use URL parameters to store and retrieve information
```js
const userID = "xyz123";
const profileLink = `profile.html?userID=${userID}`;
```

### Reading URL parameters in JavaScript
- JavaScript provides **URLSearchParams** to retrieve parameters from a URL
- Example: Extracting userID from profile.html?userID=xyz123
```js
const params = new URLSearchParams(window.location.search);
const userID = params.get("userID");
console.log(userID); // Output: xyz123
```
- Now we can use the **userID** to fetch details and update a profile page dynamically

## **Real world applications of component-based UI**
### How modern web apps use component based UI
- The principles of component-based UI apply to modern frameworks like
	- **React** - Functional & Class Components
	- **Vue.js** - Single-File Components
	- **Angular** - Modular Components with TypeScript
- Key benefits of using components:
	- **Separation of concerns** - UI logic stays organised
	- **Reusability** - The same components works in multiple places
	- **Scalability** - Easily add new features without rewriting everything