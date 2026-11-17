# Ex03 To-Do List using JavaScript
## Date:17.11.2026

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
## TODO.html
```

<!DOCTYPE html>
<html>
<head>
    <title>My To-Do List</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h1>My To-Do List</h1>
        <p>Organize your daily tasks!</p>

        <div class="input-box">
            <input type="text" id="taskInput"
                   placeholder="Enter your task">
            <button onclick="addTask()">Add</button>
        </div>

        <div class="filters">
            <button onclick="filterTasks('all')">All</button>
            <button onclick="filterTasks('pending')">Pending</button>
            <button onclick="filterTasks('completed')">Completed</button>
        </div>

        <ul id="taskList"></ul>

        <button class="clear"
                onclick="clearCompleted()">
            Clear Completed
        </button>
    </div>

    <script src="script.js"></script>
</body>
</html>
```
## Style.css
```

body {
    font-family: Arial, sans-serif;
    background: #e8eaf6;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
}

.container {
    background: white;
    width: 350px;
    padding: 25px;
    border-radius: 12px;
    box-shadow: 0 4px 15px #aaa;
    text-align: center;
}

h1 {
    color: #3949ab;
}

p {
    color: gray;
}

.input-box {
    display: flex;
    gap: 8px;
}

input {
    flex: 1;
    padding: 10px;
    border: 1px solid #aaa;
    border-radius: 5px;
    min-width: 0;
}

button {
    padding: 10px;
    border: none;
    background: #3949ab;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background: #283593;
}

.filters {
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
    gap: 5px;
}

.filters button {
    flex: 1;
    font-size: 12px;
}

ul {
    padding: 0;
    list-style: none;
}

li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #f1f2f9;
    padding: 10px;
    margin: 8px 0;
    border-radius: 5px;
    gap: 5px;
}

li span {
    flex: 1;
    overflow-wrap: anywhere;
    text-align: left;
}

.completed {
    text-decoration: line-through;
    color: gray;
}

.actions {
    display: flex;
    gap: 5px;
}

.actions button {
    padding: 6px;
    font-size: 12px;
}

.clear {
    background: #e53935;
    width: 100%;
    margin-top: 10px;
}
```
## Script.js
```

let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
let currentFilter = "all";

function saveTasks() {
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

function addTask() {
    let input = document.getElementById("taskInput");
    let text = input.value.trim();

    if (text === "") {
        alert("Please enter a task!");
        return;
    }

    tasks.push({
        text: text,
        completed: false
    });

    input.value = "";
    saveTasks();
    displayTasks();
}

function displayTasks() {
    let list = document.getElementById("taskList");
    list.innerHTML = "";

    let filteredTasks = tasks.filter(task => {
        if (currentFilter === "pending")
            return !task.completed;

        if (currentFilter === "completed")
            return task.completed;

        return true;
    });

    filteredTasks.forEach(task => {
        let index = tasks.indexOf(task);

        let li = document.createElement("li");

        let span = document.createElement("span");
        span.textContent = task.text;

        if (task.completed) {
            span.classList.add("completed");
        }

        let actions = document.createElement("div");
        actions.className = "actions";

        let doneBtn = document.createElement("button");
        doneBtn.textContent = task.completed ? "Undo" : "Done";
        doneBtn.onclick = () => toggleTask(index);

        let editBtn = document.createElement("button");
        editBtn.textContent = "Edit";
        editBtn.onclick = () => editTask(index);

        let deleteBtn = document.createElement("button");
        deleteBtn.textContent = "Delete";
        deleteBtn.onclick = () => deleteTask(index);

        actions.append(doneBtn, editBtn, deleteBtn);
        li.append(span, actions);
        list.appendChild(li);
    });
}

function toggleTask(index) {
    tasks[index].completed = !tasks[index].completed;
    saveTasks();
    displayTasks();
}

function editTask(index) {
    let newText = prompt("Edit your task:", tasks[index].text);

    if (newText !== null && newText.trim() !== "") {
        tasks[index].text = newText.trim();
        saveTasks();
        displayTasks();
    }
}

function deleteTask(index) {
    tasks.splice(index, 1);
    saveTasks();
    displayTasks();
}

function filterTasks(filter) {
    currentFilter = filter;
    displayTasks();
}

function clearCompleted() {
    tasks = tasks.filter(task => !task.completed);
    saveTasks();
    displayTasks();
}

displayTasks();
```

## OUTPUT

<img width="1795" height="903" alt="Screenshot 2026-11-17 153326" src="https://github.com/user-attachments/assets/27ee9077-df37-481c-8256-218661ea61d0" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
