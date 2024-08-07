### Lecture Plan: Variables, Data Types, and Operators; Control Structures: if, else, switch
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Variables, Data Types, and Operators (1 Hour)

**1. Introduction to Variables and Data Types (20 Minutes)**
- **Step-by-Step Explanation:**
  - **Variables:** Containers for storing data values. Declared using `var`, `let`, or `const`.
  - **Data Types:**
    - **Primitive:** String, Number, Boolean, Null, Undefined, Symbol, BigInt.
    - **Example:**
      ```javascript
      let name = "John";  // String
      let age = 30;       // Number
      let isStudent = true; // Boolean
      let emptyValue = null; // Null
      let uninitialized; // Undefined
      ```

**Checkpoint Questions:**
  - What are variables?
  - Name three ways to declare a variable in JavaScript.
  - List the primitive data types in JavaScript.

---

**2. Operators in JavaScript (20 Minutes)**
- **Step-by-Step Explanation:**
  - **Arithmetic Operators:** `+`, `-`, `*`, `/`, `%`, `++`, `--`.
  - **Assignment Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`.
  - **Comparison Operators:** `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=`.
  - **Logical Operators:** `&&`, `||`, `!`.

- **Examples:**
  ```javascript
  let a = 10;
  let b = 5;
  let sum = a + b;        // 15
  let difference = a - b; // 5
  let product = a * b;    // 50
  let quotient = a / b;   // 2
  let remainder = a % b;  // 0
  let isEqual = (a == b); // false
  let isNotEqual = (a != b); // true
  let isGreater = (a > b);   // true
  let logicalAnd = (a > b && b < 10); // true
  ```

**Checkpoint Questions:**
  - What is the difference between `==` and `===`?
  - How do you increment a variable by 1?
  - What does the `%` operator do?

---

**3. Control Structures: if, else, switch (20 Minutes)**
- **Step-by-Step Explanation:**
  - **If Statement:** Executes a block of code if a specified condition is true.
  - **Else Statement:** Executes a block of code if the condition is false.
  - **Else If Statement:** Specifies a new condition if the first condition is false.
  - **Switch Statement:** Evaluates an expression and executes code based on matching case.

- **Examples:**
  ```javascript
  let number = 10;

  if (number > 0) {
    console.log("The number is positive.");
  } else if (number < 0) {
    console.log("The number is negative.");
  } else {
    console.log("The number is zero.");
  }

  let fruit = "apple";

  switch (fruit) {
    case "apple":
      console.log("You chose an apple.");
      break;
    case "banana":
      console.log("You chose a banana.");
      break;
    default:
      console.log("Unknown fruit.");
  }
  ```

**Checkpoint Questions:**
  - What is the purpose of an `else if` statement?
  - How does a `switch` statement differ from multiple `if-else` statements?

---

**Break (10 Minutes)**

---

#### Part 2: Building a Simple Calculator (50 Minutes)

**1. Project Setup and Basic Structure (10 Minutes)**
- **Step-by-Step Explanation:**
  - Create a basic HTML structure with input fields and buttons.
  - Link JavaScript file to HTML.

- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Simple Calculator</title>
  </head>
  <body>
      <h1>Simple Calculator</h1>
      <input type="number" id="num1" placeholder="Enter first number">
      <input type="number" id="num2" placeholder="Enter second number">
      <select id="operator">
          <option value="add">+</option>
          <option value="subtract">-</option>
          <option value="multiply">*</option>
          <option value="divide">/</option>
      </select>
      <button onclick="calculate()">Calculate</button>
      <p id="result"></p>
      <script src="script.js"></script>
  </body>
  </html>
  ```

---

**2. JavaScript Implementation (30 Minutes)**
- **Step-by-Step Explanation:**
  - Get values from input fields.
  - Perform calculations based on selected operator.
  - Display result.

- **Example:**
  ```javascript
  function calculate() {
      let num1 = parseFloat(document.getElementById("num1").value);
      let num2 = parseFloat(document.getElementById("num2").value);
      let operator = document.getElementById("operator").value;
      let result;

      if (operator === "add") {
          result = num1 + num2;
      } else if (operator === "subtract") {
          result = num1 - num2;
      } else if (operator === "multiply") {
          result = num1 * num2;
      } else if (operator === "divide") {
          result = num1 / num2;
      }

      document.getElementById("result").innerText = "Result: " + result;
  }
  ```

**Checkpoint Questions:**
  - How do you get the value of an input field in JavaScript?
  - How can you convert a string to a floating-point number in JavaScript?

---

**3. Post Lecture Questions (10 Minutes)**
- **To measure understanding and retention:**
  - Explain how you would handle division by zero in the calculator example.
  - Modify the calculator to include a modulus operation.
  - Write a function that uses a `switch` statement to determine the day of the week based on a given number (1 for Monday, 7 for Sunday).

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Variables, Data Types, Operators
  - Control Structures
  - Practical application through a simple calculator

- **Questions from students.**

This structured approach, with checkpoints and post-lecture questions, ensures that students not only understand the concepts but can also apply them practically.
