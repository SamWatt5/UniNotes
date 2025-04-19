
## What is JSON?
- **JSON** stands for JavaScript Object Notation
- A lightweight data format for exchanging structured information
- Text-based, human-readable, and easy for computers to parse and generate
- Widely used in:
	- Web APIs
	- Configuration files
	- Data storage

## Why use JSON?
- **Advantages of JSON:**
	- Lightweight and efficient
	- Language-independent but easily used with most programming languages
	- Easy to read and write for developers
	- Perfect for structured data (e.g. objects arrays)
- **Common Use Cases:**
	- Sending and receiving data in web application
	- Storing data locally in web browsers
	- Interacting with third-party APIs

## JSON Structure
- **Key Components:**
	- **Objects:** key value pairs enclosed in curly braces **{ }**
	- **Arrays:** Ordered collections of values enclosed in square brackets **[ ]**
```json
{
	"name": "Alice",
	"score": 150,
	"isActive": true,
	"skills": ["JavaScript", "HTML", "CSS"]
}
```
- Data types in JSON:
	- Strings, Numbers, Booleans, Arrays, Objects, Null

## Parsing JSON in JavaScript
**Converting JSON to JavaScript Objects:**
```js
const jsonData = '{"name":"Alice","Score":150}';
const player = JSON.parse(jsonData);
console.log(player.name); // Output: Alice
```
**Converting JavaScript Objects into JSON:**
```js
const player = {name: "Alice", score: 150};
const jsonString = JSON.stringify(player);
console.log(jsonString); // Output: {"name":"Alice","score":150}
```

## Accessing JSON Data
**Accessing Nested Data:**
```js
const data = {
	players: [
		{name: "Alice", Score: 150},
		{name: "Bob", Score: 200}
	]
};
console.log(data.players[0].name) // Output: Alice
```
**Looping Through JSON Arrays:**
```js
data.players.forEach(player => {
console.log(`${player.name}: ${player.score});
}); // Output:  Alice: 150
				Bob: 200
```

## Dynamic HTML Updates with JSON
Now that we have the ability to access individual bits of JSON data, we can use JavaScript DOM manipulation
```js
const table = document.getElementByID('leaderboard');
data.players.forEach(player => {
	const row = document.createElement('tr');
	row.innerHTML = `<td>${player.name}</td><td>${player.score}</td>`;
	table.appendChild(row);
});
```

## Best Practice for JSON

**1. Keep JSON Well-Formatted:**
- Use online tools or editor plugins for validation
**2. Error Handling:**
```js
try{
	const data = JSON.parse(jsonString);
}catch (error) {
	console.error("Invalid JSON data");
}
```
**3. Validate Input:**
- Prevent invalid data from entering the JSON structure