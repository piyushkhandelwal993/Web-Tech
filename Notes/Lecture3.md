### Lecture Plan: Function Declaration and Invocation; Scope and Closures
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Function Declaration and Invocation (45 Minutes)

**1. Introduction to Functions (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Function Declaration:** A function is a reusable block of code designed to perform a specific task.
  - **Syntax:**
    ```javascript
    function functionName(parameters) {
        // code to be executed
    }
    ```
  - **Function Invocation:** Calling a function to execute the code inside it.
    ```javascript
    functionName(arguments);
    ```
  - **Example:**
    ```javascript
    function greet(name) {
        console.log("Hello, " + name + "!");
    }

    greet("Alice");  // Output: Hello, Alice!
    ```

**Checkpoint Questions:**
  - How do you declare a function in JavaScript?
  - How do you call (invoke) a function?
  - What is the purpose of parameters in a function?

---

**2. Function Expressions and Arrow Functions (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Function Expression:** Functions can also be defined using expressions.
    ```javascript
    const greet = function(name) {
        console.log("Hello, " + name + "!");
    };

    greet("Bob");  // Output: Hello, Bob!
    ```
  - **Arrow Functions:** A shorter syntax for writing function expressions.
    ```javascript
    const greet = (name) => {
        console.log("Hello, " + name + "!");
    };

    greet("Charlie");  // Output: Hello, Charlie!
    ```

**Checkpoint Questions:**
  - What is the difference between a function declaration and a function expression?
  - How do arrow functions differ from regular functions?

---

**3. Example: Function to Calculate Factorial (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Factorial Function:** A function to calculate the factorial of a number using recursion.
  - **Example:**
    ```javascript
    function factorial(n) {
        if (n === 0 || n === 1) {
            return 1;
        } else {
            return n * factorial(n - 1);
        }
    }

    console.log(factorial(5));  // Output: 120
    ```
  - **Edge Cases and Exceptions:**
    - **Negative Numbers:** Factorial is not defined for negative numbers.
    - **Non-integer Values:** Factorial is typically defined for non-negative integers.
    - **Large Numbers:** Factorial grows very fast and can result in large values.

**Checkpoint Questions:**
  - How does the factorial function handle the base case?
  - What happens if you pass a negative number to the factorial function?
  - How can you modify the factorial function to handle non-integer inputs?

---

#### Part 2: Scope and Closures (45 Minutes)

**1. Understanding Scope (20 Minutes)**
- **Step-by-Step Explanation:**
  - **Global Scope:** Variables declared outside any function.
  - **Local Scope:** Variables declared inside a function.
  - **Block Scope:** Variables declared inside a block (e.g., with `let` or `const`).

  - **Examples:**
    ```javascript
    // Global Scope
    let globalVar = "I am global";

    function myFunction() {
        // Local Scope
        let localVar = "I am local";
        console.log(globalVar);  // Accessible
        console.log(localVar);   // Accessible
    }

    myFunction();
    console.log(localVar);  // Uncaught ReferenceError: localVar is not defined
    ```

**Checkpoint Questions:**
  - What is the difference between global and local scope?
  - How does block scope differ from function scope?
  - Why is `localVar` not accessible outside the function?

---

**2. Introduction to Closures (25 Minutes)**
- **Step-by-Step Explanation:**
  - **Closures:** A closure is a function that has access to its own scope, the scope of the outer function, and the global scope.
  - **Example:**
    ```javascript
    function outerFunction(outerVariable) {
        return function innerFunction(innerVariable) {
            console.log("Outer Variable: " + outerVariable);
            console.log("Inner Variable: " + innerVariable);
        };
    }

    const newFunction = outerFunction("outside");
    newFunction("inside");  // Output: Outer Variable: outside, Inner Variable: inside
    ```
  - **Tricky Concepts and Edge Cases:**
    - **Closures and Loops:** Using closures inside loops can be tricky and may lead to unexpected behavior.
    - **Memory Leaks:** Closures can sometimes cause memory leaks if not used carefully.

  - **Examples:**
    ```javascript
    // Closure in a loop
    for (var i = 0; i < 3; i++) {
        setTimeout(function() {
            console.log(i);  // Output: 3, 3, 3
        }, 1000);
    }

    // Fixing the closure issue in a loop
    for (let i = 0; i < 3; i++) {
        setTimeout(function() {
            console.log(i);  // Output: 0, 1, 2
        }, 1000);
    }
    ```

**Checkpoint Questions:**
  - What is a closure in JavaScript?
  - How can closures be used to create private variables?
  - What are some potential issues with using closures in loops?

---

#### Part 3: Post Lecture Questions and Summary (30 Minutes)

**1. Post Lecture Questions (15 Minutes)**
- **To measure understanding and retention:**
  - Write a function that calculates the factorial of a number using a for loop.
  - Explain how you would prevent memory leaks when using closures.
  - Modify the factorial function to handle cases where the input is not a positive integer.

**2. Summary and Q&A (15 Minutes)**
- **Recap key concepts:**
  - Function Declaration and Invocation
  - Scope (Global, Local, Block)
  - Closures and their applications
- **Questions from students.**
