# Joshh-Dev.github.io

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>To-Do List</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f4f4f4;
        color: #333;
        margin: 0;
        padding: 0;
        transition: background-color 0.3s, color 0.3s;
    }
    .container {
        max-width: 600px;
        margin: 20px auto;
        background-color: #fff;
        border-radius: 5px;
        padding: 20px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        transition: background-color 0.3s;
    }
    h1 {
        text-align: center;
        color: #333;
    }
    #todo-list {
        margin-top: 20px;
        padding: 0;
    }
    #todo-list li {
        list-style-type: none;
        margin-bottom: 10px;
        display: flex;
        align-items: center;
        padding: 10px;
        border-radius: 5px;
        background-color: #f9f9f9;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }
    #todo-list img {
        margin-right: 20px;
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }
    .task-text {
        flex-grow: 1;
        color: #333;
    }
    .btn {
        padding: 8px 16px;
        background-color: #4CAF50;
        color: #fff;
        border: none;
        border-radius: 3px;
        cursor: pointer;
        transition: background-color 0.3s;
    }
    .btn:hover {
        background-color: #45a049;
    }
    .delete-btn {
        background-color: #f44336;
        margin-left: 10px;
    }
    .delete-btn:hover {
        background-color: #cc3731;
    }
    .completed {
        text-decoration: line-through;
        opacity: 0.6;
    }
    /* Dark Mode */
    .dark-mode {
        background-color: #222;
        color: #fff;
    }
    .dark-mode .container {
        background-color: #333;
        box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
    }
    .dark-mode .dropdown-content {
        background-color: #333;
        color: #fff;
    }
</style>
</head>
<body>
    <div class="container" id="container">
        <h1>To-Do List</h1>
        <input type="text" id="todo-input" placeholder="Add new task" style="color: #000;">
        <input type="file" id="image-input" style="color: #000;">
        <button class="btn" onclick="addTodo()">Add</button>
        <ul id="todo-list"></ul>
    </div>
    <div class="dropdown" style="position: fixed; top: 10px; right: 10px;">
        <button class="btn" onclick="toggleDarkMode()">☀️</button>
    </div>

    <script>
        function addTodo() {
            var todoInput = document.getElementById("todo-input");
            var todoText = todoInput.value;
            var imageInput = document.getElementById("image-input");
            var imageFile = imageInput.files[0];
            
            if (todoText.trim() !== "") {
                var todoList = document.getElementById("todo-list");
                var li = document.createElement("li");
                var img = document.createElement("img");
                if (imageFile) {
                    var reader = new FileReader();
                    reader.onload = function(event) {
                        img.src = event.target.result;
                    };
                    reader.readAsDataURL(imageFile);
                } else {
                    img.src = "default-image.png"; // Default image if no image is selected
                }
                var textNode = document.createTextNode(todoText);
                var deleteBtn = document.createElement("button");
                deleteBtn.textContent = "Delete";
                deleteBtn.classList.add("btn", "delete-btn");
                deleteBtn.onclick = function () {
                    li.remove();
                };
                var checkBtn = document.createElement("button");
                checkBtn.textContent = "Check";
                checkBtn.classList.add("btn", "check-btn");
                checkBtn.onclick = function () {
                    li.classList.toggle("completed");
                };
                li.appendChild(img);
                li.appendChild(textNode);
                li.appendChild(deleteBtn);
                li.appendChild(checkBtn);
                todoList.appendChild(li);
                todoInput.value = "";
                imageInput.value = ""; // Reset file input after adding task
            } else {
                alert("Please enter a valid task.");
            }
        }

        function toggleDarkMode() {
            var container = document.getElementById("container");
            container.classList.toggle("dark-mode");
        }

        // Initialize To-Do list with predefined tasks
        window.onload = function() {
            var predefinedTasks = ["Task 1", "Task 2", "Task 3"]; // Add your predefined tasks here
            var todoList = document.getElementById("todo-list");
            predefinedTasks.forEach(function(task) {
                var li = document.createElement("li");
                var textNode = document.createTextNode(task);
                var deleteBtn = document.createElement("button");
                deleteBtn.textContent = "Delete";
                deleteBtn.classList.add("btn", "delete-btn");
                deleteBtn.onclick = function () {
                    li.remove();
                };
                var checkBtn = document.createElement("button");
                checkBtn.textContent = "Check";
                checkBtn.classList.add("btn", "check-btn");
                checkBtn.onclick = function () {
                    li.classList.toggle("completed");
                };
                li.appendChild(textNode);
                li.appendChild(deleteBtn);
                li.appendChild(checkBtn);
                todoList.appendChild(li);
            });
        };
    </script>
</body>
</html>
