### Lecture Plan: Array Methods; Object Properties and Methods
#### Duration: 2 Hours
#### Example: To-do List Application

---

### Lecture Breakdown

#### Part 1: Array Methods (50 Minutes)

**1. Introduction to Arrays (5 Minutes)**
- **Step-by-Step Explanation:**
  - Arrays are used to store multiple values in a single variable.
  - **Syntax:**
    ```javascript
    let arrayName = [item1, item2, item3];
    ```
  - **Example:**
    ```javascript
    let fruits = ["Apple", "Banana", "Cherry"];
    ```

---

**2. Common Array Methods (25 Minutes)**
- **Step-by-Step Explanation:**
  - **`push()` and `pop()`**
    - Adds/removes elements from the end of the array.
    ```javascript
    fruits.push("Orange"); // ["Apple", "Banana", "Cherry", "Orange"]
    fruits.pop(); // ["Apple", "Banana", "Cherry"]
    ```
  - **`shift()` and `unshift()`**
    - Adds/removes elements from the beginning of the array.
    ```javascript
    fruits.unshift("Grape"); // ["Grape", "Apple", "Banana", "Cherry"]
    fruits.shift(); // ["Apple", "Banana", "Cherry"]
    ```
  - **`slice()` and `splice()`**
    - `slice(start, end)` returns a new array with selected elements.
    ```javascript
    let citrus = fruits.slice(1, 3); // ["Banana", "Cherry"]
    ```
    - `splice(start, deleteCount, item1, item2, ...)` changes the contents of an array.
    ```javascript
    fruits.splice(1, 1, "Lemon", "Kiwi"); // ["Apple", "Lemon", "Kiwi", "Cherry"]
    ```
  - **`forEach()`**
    - Executes a provided function once for each array element.
    ```javascript
    fruits.forEach(function(item, index) {
        console.log(index, item);
    });
    ```
  - **`map()`**
    - Creates a new array with the results of calling a provided function on every element.
    ```javascript
    let upperFruits = fruits.map(function(item) {
        return item.toUpperCase();
    }); // ["APPLE", "LEMON", "KIWI", "CHERRY"]
    ```
  - **`filter()`**
    - Creates a new array with all elements that pass the test implemented by the provided function.
    ```javascript
    let longFruits = fruits.filter(function(item) {
        return item.length > 5;
    }); // ["Banana", "Cherry"]
    ```

---

**3. Edge Cases and Tricky Concepts (10 Minutes)**
- **Edge Cases:**
  - Using `slice()` with negative indices.
  - Modifying an array while iterating over it.
  - Behavior of `splice()` when deleteCount is 0.

- **Tricky Concepts:**
  - Difference between `map()` and `forEach()`.
  - Mutability of arrays when using methods like `splice()`.

- **Examples:**
  ```javascript
  let numbers = [1, 2, 3, 4, 5];
  let sliced = numbers.slice(-2); // [4, 5]

  let modifiedArray = [1, 2, 3];
  modifiedArray.forEach((item, index) => {
      modifiedArray[index] = item * 2; // [2, 4, 6]
  });

  let noDeletion = ["a", "b", "c"];
  noDeletion.splice(1, 0, "d"); // ["a", "d", "b", "c"]
  ```

---

**4. Checkpoint Questions (10 Minutes)**
  - What is the difference between `push()` and `unshift()`?
  - How does `splice()` differ from `slice()`?
  - What is the primary difference between `map()` and `forEach()`?
  - Provide an example of using `filter()` to create a new array.

---

#### Part 2: Object Properties and Methods (50 Minutes)

**1. Introduction to Objects (5 Minutes)**
- **Step-by-Step Explanation:**
  - Objects are collections of key-value pairs.
  - **Syntax:**
    ```javascript
    let objectName = {
        key1: value1,
        key2: value2
    };
    ```
  - **Example:**
    ```javascript
    let person = {
        firstName: "John",
        lastName: "Doe",
        age: 30
    };
    ```

---

**2. Accessing and Modifying Properties (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Dot Notation:**
    ```javascript
    console.log(person.firstName); // John
    person.age = 31;
    ```
  - **Bracket Notation:**
    ```javascript
    console.log(person["lastName"]); // Doe
    person["age"] = 32;
    ```
  - **Adding and Deleting Properties:**
    ```javascript
    person.middleName = "William";
    delete person.age;
    ```

---

**3. Methods in Objects (10 Minutes)**
- **Step-by-Step Explanation:**
  - Functions stored in objects are called methods.
  - **Example:**
    ```javascript
    let car = {
        brand: "Toyota",
        start: function() {
            console.log("Car started");
        }
    };
    car.start(); // Car started
    ```

---

**4. Edge Cases and Tricky Concepts (10 Minutes)**
- **Edge Cases:**
  - Accessing properties that do not exist.
  - Deleting non-configurable properties.

- **Tricky Concepts:**
  - Difference between `undefined` and `null` in object properties.
  - Using `this` keyword in methods.

- **Examples:**
  ```javascript
  let book = {
      title: "1984",
      author: "George Orwell"
  };
  console.log(book.publisher); // undefined

  Object.defineProperty(book, "year", {
      value: 1949,
      configurable: false
  });
  // delete book.year; // TypeError: Cannot delete property 'year' of #<Object>
  ```

---

**5. Checkpoint Questions (10 Minutes)**
  - How do you access a property using bracket notation?
  - What is the difference between `undefined` and `null`?
  - Provide an example of an object method.
  - How would you add a new property to an existing object?

---

#### Part 3: To-do List Application (20 Minutes)

**1. Project Setup and Basic Structure (10 Minutes)**
- **Step-by-Step Explanation:**
  - Create a basic HTML structure with an input field and a button.
  - Link JavaScript file to HTML.

- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>To-do List</title>
  </head>
  <body>
      <h1>To-do List</h1>
      <input type="text" id="taskInput" placeholder="Enter a task">
      <button onclick="addTask()">Add Task</button>
      <ul id="taskList"></ul>
      <script src="script.js"></script>
  </body>
  </html>
  ```

---

**2. JavaScript Implementation (10 Minutes)**
- **Step-by-Step Explanation:**
  - Add tasks to the list.
  - Use array methods to manage tasks.
  - Display tasks using DOM manipulation.

- **Example:**
  ```javascript
  let tasks = [];

  function addTask() {
      let taskInput = document.getElementById("taskInput");
      let task = taskInput.value;
      if (task) {
          tasks.push(task);
          displayTasks();
          taskInput.value = "";
      }
  }

  function displayTasks() {
      let taskList = document.getElementById("taskList");
      taskList.innerHTML = "";
      tasks.forEach(function(task, index) {
          let listItem = document.createElement("li");
          listItem.textContent = task;
          taskList.appendChild(listItem);
      });
  }
  ```

---

**3. Post Lecture Questions (10 Minutes)**
- **To measure understanding and retention:**
  - Modify the to-do list application to allow users to delete tasks.
  - How would you use `splice()` to remove an item from the array?
  - Write a function that uses an object method to print a custom message.

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Array Methods
  - Object Properties and Methods
  - Practical application through a to-do list

- **Questions from students.**
