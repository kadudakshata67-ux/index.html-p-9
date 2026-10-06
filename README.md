<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Personal To-Do List</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="bg-gray-100 min-h-screen">

  <!-- Main Container -->
  <div class="max-w-xl mx-auto px-4 py-10">

    <!-- Heading -->
    <div class="text-center mb-8">
      <h1 class="text-4xl font-bold text-blue-600">
        My To-Do List
      </h1>

      <p class="text-gray-500 mt-2">
        Organize your tasks and stay productive
      </p>
    </div>


    <!-- To-Do Card -->
    <div class="bg-white rounded-2xl shadow-lg p-6">

      <!-- Add Task -->
      <div class="flex flex-col sm:flex-row gap-3 mb-6">

        <input
          type="text"
          id="taskInput"
          placeholder="Enter a new task..."
          class="flex-1 px-4 py-3 border border-gray-300
                 rounded-lg focus:outline-none
                 focus:ring-2 focus:ring-blue-500"
        >

        <button
          id="addTaskButton"
          class="bg-blue-600 text-white px-6 py-3
                 rounded-lg font-semibold
                 hover:bg-blue-700 transition"
        >
          Add Task
        </button>

      </div>


      <!-- Task List -->
      <ul id="taskList" class="space-y-3">
        <!-- Tasks will be added here using JavaScript -->
      </ul>


      <!-- Empty Message -->
      <p
        id="emptyMessage"
        class="text-center text-gray-400 py-6"
      >
        No tasks yet. Add a task to get started!
      </p>

    </div>

  </div>


  <!-- JavaScript -->
  <script>

    // Get HTML elements
    const taskInput = document.getElementById("taskInput");
    const addTaskButton = document.getElementById("addTaskButton");
    const taskList = document.getElementById("taskList");
    const emptyMessage = document.getElementById("emptyMessage");


    // Add Task Function
    function addTask() {

      const taskText = taskInput.value.trim();

      // Check if input is empty
      if (taskText === "") {
        alert("Please enter a task.");
        return;
      }


      // Create list item
      const listItem = document.createElement("li");

      listItem.className =
        "flex items-center justify-between gap-3 " +
        "bg-gray-50 border border-gray-200 " +
        "rounded-lg p-4";


      // Create left section
      const leftSection = document.createElement("div");

      leftSection.className =
        "flex items-center gap-3 flex-1";


      // Create checkbox
      const checkbox = document.createElement("input");

      checkbox.type = "checkbox";

      checkbox.className =
        "w-5 h-5 accent-blue-600 cursor-pointer";


      // Create task text
      const taskTextElement =
        document.createElement("span");

      taskTextElement.textContent = taskText;

      taskTextElement.className =
        "text-gray-700 break-words";


      // Mark task as completed
      checkbox.addEventListener("change", function() {

        if (checkbox.checked) {

          taskTextElement.classList.add(
            "line-through",
            "text-gray-400"
          );

        } else {

          taskTextElement.classList.remove(
            "line-through",
            "text-gray-400"
          );

        }

      });


      // Create delete button
      const deleteButton =
        document.createElement("button");

      deleteButton.textContent = "Delete";

      deleteButton.className =
        "bg-red-500 text-white px-3 py-2 " +
        "rounded-lg text-sm font-semibold " +
        "hover:bg-red-600 transition";


      // Delete task
      deleteButton.addEventListener("click", function() {

        listItem.remove();

        updateEmptyMessage();

      });


      // Add elements to left section
      leftSection.appendChild(checkbox);
      leftSection.appendChild(taskTextElement);


      // Add sections to list item
      listItem.appendChild(leftSection);
      listItem.appendChild(deleteButton);


      // Add task to list
      taskList.appendChild(listItem);


      // Clear input
      taskInput.value = "";

      // Focus input
      taskInput.focus();

      // Hide empty message
      updateEmptyMessage();

    }


    // Update empty message
    function updateEmptyMessage() {

      if (taskList.children.length === 0) {

        emptyMessage.classList.remove("hidden");

      } else {

        emptyMessage.classList.add("hidden");

      }

    }


    // Add task when button is clicked
    addTaskButton.addEventListener("click", addTask);


    // Add task when Enter key is pressed
    taskInput.addEventListener("keydown", function(event) {

      if (event.key === "Enter") {
        addTask();
      }

    });

  </script>

</body>
</html>
