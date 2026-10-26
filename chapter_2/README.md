# Chapter 2 — Building Your First Express Server

This chapter covers creating a basic backend server using Node.js and Express, adding website and API endpoints, and testing HTTP requests.

**Original tutorial:** [Smoljames — Backend Full Course, Chapter 2](https://www.youtube.com/watch?v=9BD9eK9VqXA&t=1063s)

**Project files:**

- [`server.js`](server.js) — Express application
- [`package.json`](package.json) — Project dependencies and scripts
- [`test.rest`](test.rest) — HTTP request examples

## 1. Initialize a Node.js Project

Verify that Node.js and npm are installed.

```bash
node -v
npm -v
```

Create a project directory and initialize npm.

```bash
mkdir chapter_2
cd chapter_2
npm init -y
```

The `-y` flag accepts the default values and creates a `package.json` file.

**Concept: `package.json`**

This file describes the project, its dependencies, and scripts used to execute commands.

## 2. Install Express

Install Express using npm.

```bash
npm install express
```

Express is a framework for Node.js that simplifies creating servers and handling HTTP requests.

Create a file named `server.js`.

## 3. Create an Express Server

Add the following code to `server.js`.

```javascript
const express = require("express");
const app = express();
const PORT = 8383;

app.listen(PORT, () => {
	console.log(`Server has started on: ${PORT}`);
});
```

**Explanation:**

- `require("express")` imports Express.
- `express()` creates an Express application.
- `PORT` identifies the port on which the server listens.
- `app.listen()` starts the server and listens for incoming connections.

Start the server.

```bash
node server.js
```

Expected output:

```text
Server has started on: 8383
```

**Concept: Localhost and ports**

The local server can be accessed at:

```text
http://localhost:8383
```

The equivalent loopback address is:

```text
http://127.0.0.1:8383
```

`localhost` refers to your own computer. The port identifies the network service handling the connection.

At this point, the server is running but has no defined routes.

## 4. Install nodemon

Install nodemon as a development dependency.

```bash
npm install --save-dev nodemon
```

nodemon automatically restarts the server when changes are saved.

Add a development script to the `scripts` section of `package.json`.

```json
"scripts": {
    "dev": "nodemon server.js"
}
```

Start the server using npm.

```bash
npm run dev
```

Use `Ctrl + C` to stop the server.

## 5. HTTP Methods, Routes, and Endpoints

**Concept: HTTP methods (verbs)**

HTTP methods describe the intended action of a request.

A route or path identifies the location within an application where the request should be handled.

The combination of an HTTP method and path identifies an endpoint.

For example:

```text
GET /dashboard
```

- `GET` is the HTTP method.
- `/dashboard` is the path.
- The combination identifies the endpoint handled by the server.

In Express, we define a route using:

```javascript
app.get("/", (req, res) => {
	res.send("Hello World");
});
```

**Important concepts:**

- `app.get()` handles GET requests for the specified path.
- `req` represents the incoming request.
- `res` represents the response sent to the client.
- `res.send()` sends a response.

Source: [Smoljames — HTTP Methods and Routes (~45:00)](https://www.youtube.com/watch?v=9BD9eK9VqXA&t=2700s)

## 6. Create Website Endpoints

Website endpoints commonly respond with HTML that can be displayed in a browser.

### Home page

Add this route above `app.listen()`.

```javascript
app.get("/", (req, res) => {
	res.send(`
        <body>
            <h1>Home Page</h1>
            <a href="/dashboard">Dashboard</a>
        </body>
    `);
});
```

### Dashboard page

```javascript
app.get("/dashboard", (req, res) => {
	res.send(`
        <body>
            <h1>Dashboard</h1>
            <a href="/">Home</a>
        </body>
    `);
});
```

**Test in the browser:**

```text
http://localhost:8383
http://localhost:8383/dashboard
```

Each URL triggers a different Express route.

**Concept: Website endpoints**

As noted in my original code, website endpoints return content intended for display in a browser.

In these examples, the server responds directly with HTML strings.

## 7. Create an API Endpoint

API endpoints commonly return data rather than complete HTML pages.

Create an array near the top of `server.js`.

```javascript
let data = ["Heidi"];
```

Create an endpoint for retrieving the array.

```javascript
app.get("/api/data", (req, res) => {
	console.log("this one is for data.");
	res.json(data);
});
```

Open:

```text
http://localhost:8383/api/data
```

Expected response:

```json
["Heidi"]
```

**Concept: Website vs. API endpoints**

Website endpoints commonly serve HTML, while API endpoints commonly return JSON or other data for consumption by a client application.

Both are HTTP endpoints. The primary difference in these examples is the content returned.

`res.json()` explicitly sends a JSON response.

## 8. Understand CRUD Operations

**Concept: CRUD**

CRUD represents four common operations used when working with data.

| Operation | HTTP method | Purpose                |
| --------- | ----------- | ---------------------- |
| Create    | POST        | Add new data           |
| Read      | GET         | Retrieve existing data |
| Update    | PUT / PATCH | Modify existing data   |
| Delete    | DELETE      | Remove data            |

These methods commonly correspond to database operations, although the Chapter 2 application uses an array instead of a database.

Source: [Smoljames — CRUD and HTTP Methods (~1:13:00)](https://www.youtube.com/watch?v=9BD9eK9VqXA&t=4380s)

## 9. Add Middleware to Handle JSON

Add the following after initializing the Express application, before defining the routes.

```javascript
app.use(express.json());
```

**Concept: Middleware**

Middleware executes during the request-response cycle.

`express.json()` parses incoming requests containing JSON and makes the parsed data available through `req.body`.

This is particularly useful when a client submits data using POST, PUT, or PATCH.

## 10. Create a POST Endpoint

A POST request is commonly used to create a new resource.

```javascript
app.post("/api/data", (req, res) => {
	const newEntry = req.body;

	console.log(newEntry);

	data.push(newEntry.name);

	res.sendStatus(201);
});
```

**Concept: How a POST request works**

An example from my notes:

A user enters information into a signup form and clicks the signup button.

The frontend sends a network request containing the information to the backend.

The server receives the request and executes the corresponding route handler.

In this simplified project:

1. `req.body` retrieves the submitted JSON.
2. `data.push()` adds the submitted name to the array.
3. `res.sendStatus(201)` responds with HTTP status `201 Created`.

This example does not implement an actual signup process or database.

### Optional improvement: Validate incoming data

A real application should not assume that `req.body.name` always exists.

```javascript
app.post("/api/data", (req, res) => {
	const newEntry = req.body;

	if (typeof newEntry?.name !== "string" || !newEntry.name.trim()) {
		return res.status(400).json({
			error: "A name is required.",
		});
	}

	data.push(newEntry.name);
	res.sendStatus(201);
});
```

This returns `400 Bad Request` when the name is missing or invalid.

## 11. Create a DELETE Endpoint

A DELETE request is used to remove a resource.

My original Chapter 2 implementation removes the last item from the array.

```javascript
app.delete("/api/data", (req, res) => {
	data.pop();

	console.log("We deleted the last item.");

	res.sendStatus(204);
});
```

**Explanation:**

- `data.pop()` removes the last element of the array.
- `204 No Content` indicates successful processing with no response body.

**Correction from my original code:**

The original implementation used HTTP status `203`, which means _Non-Authoritative Information_.

For this example, `204 No Content` is a more appropriate response.

In a real application, the DELETE endpoint would typically identify a specific resource rather than automatically removing the last array item.

## 12. Test Requests Using REST Client

Install the **REST Client** extension by Huachao Mao in Visual Studio Code.

This extension allows HTTP requests to be sent directly from a `.rest` file.

Create:

```text
test.rest
```

Requests can be separated using `###`.

### Test the home page

```http
### HOME PAGE
GET http://localhost:8383/
```

### Test the dashboard

```http
### DASHBOARD
GET http://localhost:8383/dashboard
```

### Test the GET API endpoint

```http
### GET DATA
GET http://localhost:8383/api/data
```

Expected response:

```json
["Heidi"]
```

### Test the POST API endpoint

```http
### ADD DATA
POST http://localhost:8383/api/data
Content-Type: application/json

{
    "name": "angela"
}
```

Expected response status:

```text
201 Created
```

Run the GET request again to verify that the new entry was added.

Expected response:

```json
["Heidi", "angela"]
```

### Test the DELETE API endpoint

```http
### DELETE DATA
DELETE http://localhost:8383/api/data
```

Expected response status after applying the correction in Step 11:

```text
204 No Content
```

Run the GET request again.

Expected response:

```json
["Heidi"]
```

**Important:** The array is stored in memory. Restarting the server resets it to its original value.

Source: [Smoljames — REST Client Demonstration (~1:08:30)](https://www.youtube.com/watch?v=9BD9eK9VqXA&t=4110s)

## 13. Review the Completed Application

The completed introductory Express application includes:

| Endpoint     | Method | Description                |
| ------------ | ------ | -------------------------- |
| `/`          | GET    | Returns an HTML home page  |
| `/dashboard` | GET    | Returns an HTML dashboard  |
| `/api/data`  | GET    | Returns the data array     |
| `/api/data`  | POST   | Adds an entry to the array |
| `/api/data`  | DELETE | Removes the last entry     |

### Important Reminders

- Define middleware before routes that depend on it.
- HTTP methods describe the intended action of a request.
- A method and path together identify an endpoint.
- `req` contains incoming request information.
- `res` is used to send responses.
- `req.body` contains parsed request data when the appropriate middleware is configured.
- `res.json()` sends JSON responses.
- HTTP status codes communicate the result of a request.
- The REST Client extension provides a convenient way to test endpoints without building a frontend.
- Data stored in an in-memory array does not survive a server restart.

## Attribution

This chapter was developed while following [Backend Full Course by Smoljames](https://www.youtube.com/watch?v=9BD9eK9VqXA).

The steps and notes reflect my implementation of the Chapter 2 project and include concepts I recorded while learning.

The documentation includes additional examples, clarifications, and corrections where appropriate.

For the full explanations and demonstrations, please watch the original tutorial.

**Original course:** [Smoljames — Backend Full Course](https://www.youtube.com/watch?v=9BD9eK9VqXA)
