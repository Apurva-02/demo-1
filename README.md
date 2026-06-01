# demo-1
This is my first repositary
Author - Apurva


# Procedure: Create a RESTful Web Application Using Express.js with Routing, Middleware, and Error Handling

### Step 1: Install Node.js

1. Download and install Node.js from the official website:

   * [Node.js Official Website](https://nodejs.org?utm_source=chatgpt.com)
2. Verify installation by opening Command Prompt and running:

```bash
node -v
npm -v
```

Both commands should display version numbers.

---

### Step 2: Create a New Project Folder

Create a folder for the experiment and open it in VS Code.

```bash
mkdir ExpressRESTAPI
cd ExpressRESTAPI
```

---

### Step 3: Initialize Node.js Project

Run the following command:

```bash
npm init -y
```

This creates a `package.json` file containing project information.

---

### Step 4: Install Express.js

Install Express framework using npm:

```bash
npm install express
```

After installation, a `node_modules` folder and `package-lock.json` file will be created.

---

### Step 5: Create Application File

Create a file named:

```text
app.js
```

Project structure:

```text
ExpressRESTAPI
│
├── node_modules
├── package.json
├── package-lock.json
└── app.js
```

---

### Step 6: Write the Program

Copy and paste the given code into `app.js`.

```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.use((req, res, next) => {
    console.log(`${req.method} request for ${req.url}`);
    next();
});

let users = [
    { id: 1, name: 'Rahul' },
    { id: 2, name: 'Priya' }
];

app.get('/users', (req, res) => {
    res.json(users);
});

app.get('/users/:id', (req, res) => {
    const user = users.find(u => u.id == req.params.id);
    if (user) {
        res.json(user);
    } else {
        res.status(404).send('User not found');
    }
});

app.post('/users', (req, res) => {
    const newUser = { id: users.length + 1, name: req.body.name };
    users.push(newUser);
    res.status(201).json(newUser);
});

app.put('/users/:id', (req, res) => {
    const user = users.find(u => u.id == req.params.id);
    if (user) {
        user.name = req.body.name;
        res.json(user);
    } else {
        res.status(404).send('User not found');
    }
});

app.delete('/users/:id', (req, res) => {
    const index = users.findIndex(u => u.id == req.params.id);
    if (index !== -1) {
        const deletedUser = users.splice(index, 1);
        res.json(deletedUser);
    } else {
        res.status(404).send('User not found');
    }
});

app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
});

const port = 3000;

app.listen(port, () => {
    console.log(`Server running on http://localhost:${port}`);
});
```

Save the file.

---

### Step 7: Run the Application

Open terminal and execute:

```bash
node app.js
```

Output:

```text
Server running on http://localhost:3000
```

The server is now running.

---

### Step 8: Test GET Request (Read All Users)

Open browser and visit:

```text
http://localhost:3000/users
```

Output:

```json
[
  {
    "id": 1,
    "name": "Rahul"
  },
  {
    "id": 2,
    "name": "Priya"
  }
]
```

---

### Step 9: Test GET Request (Read Single User)

Open:

```text
http://localhost:3000/users/1
```

Output:

```json
{
  "id": 1,
  "name": "Rahul"
}
```

---

### Step 10: Test POST Request Using Postman

1. Open Postman.
2. Select **POST** method.
3. Enter URL:

```text
http://localhost:3000/users
```

4. Go to **Body → raw → JSON**.
5. Enter:

```json
{
  "name": "Amit"
}
```

6. Click **Send**.

Output:

```json
{
  "id": 3,
  "name": "Amit"
}
```

---

### Step 11: Test PUT Request Using Postman

1. Select **PUT** method.
2. URL:

```text
http://localhost:3000/users/2
```

3. Body:

```json
{
  "name": "Priya Sharma"
}
```

4. Click **Send**.

Output:

```json
{
  "id": 2,
  "name": "Priya Sharma"
}
```

---

### Step 12: Test DELETE Request Using Postman

1. Select **DELETE** method.
2. URL:

```text
http://localhost:3000/users/1
```

3. Click **Send**.

Output:

```json
[
  {
    "id": 1,
    "name": "Rahul"
  }
]
```

---

### Step 13: Observe Middleware Execution

In the terminal, request logs will appear:

```text
GET request for /users
GET request for /users/1
POST request for /users
PUT request for /users/2
DELETE request for /users/1
```

This confirms that the middleware is executing before every request.

---

### Step 14: Test Error Handling

Try accessing a non-existing user:

```text
http://localhost:3000/users/100
```

Output:

```text
User not found
```

Status Code:

```text
404 Not Found
```

---

### Step 15: Stop the Server

Press:

```text
Ctrl + C
```

in the terminal.

The Express server will stop.

---

## Viva Questions

1. What is Express.js?
2. What is middleware in Express.js?
3. What is REST API?
4. Difference between GET and POST methods?
5. What is the purpose of `express.json()` middleware?
6. How is routing implemented in Express.js?
7. What is error-handling middleware?
8. Difference between PUT and PATCH methods?
9. Why do we use `next()` in middleware?
10. What is the role of `app.listen()` in Express.js?

These steps can be directly written in your practical journal under the **Procedure** section.


If you want to test **all GET, POST, PUT, and DELETE methods using only a browser**, then GET requests can be tested directly from the browser URL bar, but POST, PUT, and DELETE cannot be sent directly from the browser address bar because browsers only send GET requests when you enter a URL.

### Method 1: Test GET Requests Directly

Start the server:

```bash
node app.js
```

Open browser:

#### GET All Users

```text
http://localhost:3000/users
```

Output:

```json
[
  { "id": 1, "name": "Rahul" },
  { "id": 2, "name": "Priya" }
]
```

#### GET Single User

```text
http://localhost:3000/users/1
```

Output:

```json
{ "id": 1, "name": "Rahul" }
```

---

## Method 2: Test POST, PUT, DELETE Using Browser Console

Open browser and press:

```text
F12 → Console
```

### POST Request

Paste:

```javascript
fetch('http://localhost:3000/users', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        name: 'Amit'
    })
})
.then(res => res.json())
.then(data => console.log(data));
```

Output:

```json
{
  "id": 3,
  "name": "Amit"
}
```

---

### PUT Request

Paste:

```javascript
fetch('http://localhost:3000/users/2', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        name: 'Priya Sharma'
    })
})
.then(res => res.json())
.then(data => console.log(data));
```

Output:

```json
{
  "id": 2,
  "name": "Priya Sharma"
}
```

---

### DELETE Request

Paste:

```javascript
fetch('http://localhost:3000/users/1', {
    method: 'DELETE'
})
.then(res => res.json())
.then(data => console.log(data));
```

Output:

```json
[
  {
    "id": 1,
    "name": "Rahul"
  }
]
```

---

## Method 3: Test Using Simple HTML Forms (Recommended for Practical Exam)

Create a file named `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>REST API Test</title>
</head>
<body>

<h2>Add User</h2>
<input type="text" id="username" placeholder="Enter Name">
<button onclick="addUser()">POST User</button>

<script>
function addUser() {
    fetch('http://localhost:3000/users', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            name: document.getElementById('username').value
        })
    })
    .then(res => res.json())
    .then(data => alert(JSON.stringify(data)));
}
</script>

</body>
</html>
```

Open this file in a browser and click the button to test the POST API.

---

### Important Viva Answer

**Can all REST methods be tested directly from the browser URL bar?**

**Answer:** No. Only **GET** requests can be tested directly from the browser URL bar. For **POST**, **PUT**, and **DELETE** requests, we must use:

* Postman
* Browser Developer Console (Fetch API)
* HTML Forms with JavaScript
* API testing tools

This is the correct theoretical answer for your practical exam.
