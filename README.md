# task3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Portfolio Website</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f4f4f4;
      color: #333;
    }

    header, nav, section, footer {
      padding: 20px;
    }

    header {
      background: #333;
      color: #fff;
      text-align: center;
    }

    nav {
      background: #444;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 15px;
    }

    nav a {
      color: #fff;
      text-decoration: none;
      font-weight: bold;
    }

    section {
      background: #fff;
      margin: 20px auto;
      max-width: 1000px;
      border-radius: 8px;
      padding: 20px;
    }

    h2 {
      border-bottom: 2px solid #ddd;
      padding-bottom: 10px;
    }

    .project, .product, .todo-item {
      border: 1px solid #ccc;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
    }

    .todo-list input[type="text"] {
      width: 70%;
      padding: 8px;
    }

    .todo-list button {
      padding: 8px 12px;
      margin-left: 10px;
    }

    .controls {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-bottom: 10px;
    }

    .controls label {
      display: flex;
      flex-direction: column;
    }

    footer {
      text-align: center;
      background: #333;
      color: #fff;
      padding: 10px;
    }

    @media (max-width: 600px) {
      nav {
        flex-direction: column;
        align-items: center;
      }

      .todo-list input[type="text"] {
        width: 100%;
        margin-bottom: 10px;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>My Portfolio</h1>
    <p>Web Developer | JavaScript Enthusiast</p>
  </header>

  <nav>
    <a href="#about">About</a>
    <a href="#projects">Projects</a>
    <a href="#contact">Contact</a>
    <a href="#todo">To-Do App</a>
    <a href="#products">Products</a>
  </nav>

  <!-- About Section -->
  <section id="about">
    <h2>About Me</h2>
    <p>I’m a web developer skilled in HTML, CSS, and JavaScript. I enjoy creating responsive, interactive web applications.</p>
  </section>

  <!-- Projects Section -->
  <section id="projects">
    <h2>My Projects</h2>
    <div class="project">
      <h3>Portfolio Website</h3>
      <p>A personal website with multiple sections showcasing my skills.</p>
    </div>
    <div class="project">
      <h3>To-Do List App</h3>
      <p>Task manager with persistent storage using localStorage.</p>
    </div>
    <div class="project">
      <h3>Product Filter Page</h3>
      <p>Product listing interface with category and price sorting features.</p>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact">
    <h2>Contact Me</h2>
    <p>Email: example@example.com</p>
    <p>LinkedIn: <a href="https://linkedin.com/in/yourprofile" target="_blank">linkedin.com/in/yourprofile</a></p>
  </section>

  <!-- To-Do App Section -->
  <section id="todo">
    <h2>To-Do List</h2>
    <div class="todo-list">
      <input type="text" id="taskInput" placeholder="Enter a task..." />
      <button onclick="addTask()">Add</button>
      <div id="taskList"></div>
    </div>
  </section>

  <!-- Product Listing Section -->
  <section id="products">
    <h2>Product Listing</h2>
    <div class="controls">
      <label>
        Filter by Category:
        <select id="filterCategory" onchange="filterProducts()">
          <option value="all">All</option>
          <option value="tech">Tech</option>
          <option value="fashion">Fashion</option>
        </select>
      </label>
      <label>
        Sort by Price:
        <select id="sortPrice" onchange="filterProducts()">
          <option value="default">Default</option>
          <option value="asc">Low to High</option>
          <option value="desc">High to Low</option>
        </select>
      </label>
    </div>
    <div id="productList"></div>
  </section>

  <footer>
    &copy; 2025 Your Name | All Rights Reserved
  </footer>

  <!-- JavaScript Section -->
  <script>
    // --- To-Do App Logic ---
    const taskInput = document.getElementById("taskInput");
    const taskList = document.getElementById("taskList");

    function loadTasks() {
      const tasks = JSON.parse(localStorage.getItem("tasks") || "[]");
      taskList.innerHTML = tasks.map((task, i) =>
        `<div class="todo-item">${task}
         <button onclick="deleteTask(${i})">Delete</button></div>`
      ).join("");
    }

    function addTask() {
      const value = taskInput.value.trim();
      if (!value) return;
      const tasks = JSON.parse(localStorage.getItem("tasks") || "[]");
      tasks.push(value);
      localStorage.setItem("tasks", JSON.stringify(tasks));
      taskInput.value = "";
      loadTasks();
    }

    function deleteTask(index) {
      const tasks = JSON.parse(localStorage.getItem("tasks") || "[]");
      tasks.splice(index, 1);
      localStorage.setItem("tasks", JSON.stringify(tasks));
      loadTasks();
    }

    // --- Product Listing Logic ---
    const products = [
      { name: "Smartphone", price: 800, category: "tech" },
      { name: "Headphones", price: 150, category: "tech" },
      { name: "T-Shirt", price: 20, category: "fashion" },
      { name: "Sneakers", price: 100, category: "fashion" }
    ];

    function filterProducts() {
      const category = document.getElementById("filterCategory").value;
      const sort = document.getElementById("sortPrice").value;

      let filtered = [...products];
      if (category !== "all") {
        filtered = filtered.filter(p => p.category === category);
      }

      if (sort === "asc") {
        filtered.sort((a, b) => a.price - b.price);
      } else if (sort === "desc") {
        filtered.sort((a, b) => b.price - a.price);
      }

      const list = filtered.map(p =>
        <div class="product"><strong>${p.name}</strong><br/>Price: $${p.price}</div>
      ).join("");
      document.getElementById("productList").innerHTML = list;
    }

    // Initial Load
    loadTasks();
    filterProducts();
  </script>
</body>
</html>
