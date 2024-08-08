### Lecture Plan: Defining and Using Functions; Working with Arrays
#### Duration: 2 Hours
#### Programming Language: PHP

---

### Lecture Breakdown

#### Part 1: Defining and Using Functions (45 Minutes)

**1. Introduction to Functions in PHP (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Function Declaration:**
    - Functions are blocks of code that can be repeatedly called.
    - **Syntax:**
      ```php
      function functionName($parameters) {
          // code to be executed
      }
      ```
  - **Function Invocation:**
    - Calling a function to execute the code inside it.
    - **Syntax:**
      ```php
      functionName($arguments);
      ```
  - **Example:**
    ```php
    function greet($name) {
        echo "Hello, " . $name . "!";
    }

    greet("Alice");  // Output: Hello, Alice!
    ```

**Checkpoint Questions:**
  - How do you define a function in PHP?
  - How do you call a function in PHP?

---

**2. Parameters and Return Values (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Parameters:**
    - Functions can accept parameters (inputs) to perform operations.
    - **Example:**
      ```php
      function add($a, $b) {
          return $a + $b;
      }

      echo add(3, 4);  // Output: 7
      ```
  - **Return Values:**
    - Functions can return values.
    - **Example:**
      ```php
      function multiply($a, $b) {
          return $a * $b;
      }

      $result = multiply(3, 4);
      echo $result;  // Output: 12
      ```

**Checkpoint Questions:**
  - What is a function parameter?
  - How do you return a value from a function in PHP?

---

**3. Edge Cases and Tricky Concepts (20 Minutes)**
- **Default Parameters:**
  - **Example:**
    ```php
    function greet($name = "Guest") {
        echo "Hello, " . $name . "!";
    }

    greet();  // Output: Hello, Guest!
    ```
- **Variable Scope:**
  - **Global and Local Variables:**
    - **Example:**
      ```php
      $x = 10;

      function myFunction() {
          global $x;
          echo $x;
      }

      myFunction();  // Output: 10
      ```
- **Recursive Functions:**
  - **Example:**
    ```php
    function factorial($n) {
        if ($n == 0) {
            return 1;
        } else {
            return $n * factorial($n - 1);
        }
    }

    echo factorial(5);  // Output: 120
    ```

**Checkpoint Questions:**
  - What is a default parameter?
  - Explain the difference between global and local variables.
  - How does a recursive function work?

---

#### Part 2: Working with Arrays (45 Minutes)

**1. Introduction to Arrays (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Arrays:**
    - Arrays are used to store multiple values in a single variable.
    - **Syntax:**
      ```php
      $array = array("value1", "value2", "value3");
      ```
  - **Example:**
    ```php
    $fruits = array("Apple", "Banana", "Cherry");
    echo $fruits[1];  // Output: Banana
    ```

**Checkpoint Questions:**
  - How do you define an array in PHP?
  - How do you access elements in an array?

---

**2. Associative Arrays and Array Functions (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Associative Arrays:**
    - Arrays with named keys.
    - **Example:**
      ```php
      $ages = array("Alice" => 25, "Bob" => 30, "Charlie" => 35);
      echo $ages["Bob"];  // Output: 30
      ```
  - **Common Array Functions:**
    - `count()`, `array_push()`, `array_pop()`, `array_merge()`
    - **Example:**
      ```php
      $numbers = array(1, 2, 3, 4);
      array_push($numbers, 5);
      print_r($numbers);  // Output: Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 )
      ```

**Checkpoint Questions:**
  - What is an associative array?
  - How do you add an element to an array in PHP?

---

**3. Edge Cases and Tricky Concepts (20 Minutes)**
- **Multi-dimensional Arrays:**
  - **Example:**
    ```php
    $matrix = array(
        array(1, 2, 3),
        array(4, 5, 6),
        array(7, 8, 9)
    );
    echo $matrix[1][2];  // Output: 6
    ```
- **Array Iteration:**
  - **Foreach Loop:**
    - **Example:**
      ```php
      $colors = array("Red", "Green", "Blue");

      foreach ($colors as $color) {
          echo $color . " ";
      }
      // Output: Red Green Blue
      ```
- **Array Key Handling:**
  - **Example:**
    ```php
    $ages = array("Alice" => 25, "Bob" => 30);

    foreach ($ages as $name => $age) {
        echo "$name is $age years old. ";
    }
    // Output: Alice is 25 years old. Bob is 30 years old.
    ```

**Checkpoint Questions:**
  - How do you define a multi-dimensional array?
  - What is the purpose of a `foreach` loop?

---

#### Part 3: Example - Contact Form with Validation (30 Minutes)

**1. HTML Form Setup (10 Minutes)**
- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Contact Form</title>
  </head>
  <body>
      <form method="post" action="contact.php">
          <label for="name">Name:</label>
          <input type="text" id="name" name="name"><br>
          <label for="email">Email:</label>
          <input type="email" id="email" name="email"><br>
          <label for="message">Message:</label><br>
          <textarea id="message" name="message"></textarea><br>
          <input type="submit" value="Submit">
      </form>
  </body>
  </html>
  ```

---

**2. PHP Validation Script (20 Minutes)**
- **Example:**
  ```php
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $name = $_POST['name'];
      $email = $_POST['email'];
      $message = $_POST['message'];
      $errors = array();

      if (empty($name)) {
          $errors[] = "Name is required.";
      }
      if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
          $errors[] = "Invalid email format.";
      }
      if (empty($message)) {
          $errors[] = "Message is required.";
      }

      if (empty($errors)) {
          echo "Form submitted successfully.";
          // Here you can process the form data (e.g., send an email, save to database)
      } else {
          foreach ($errors as $error) {
              echo $error . "<br>";
          }
      }
  }
  ?>
  ```

**Checkpoint Questions:**
  - How do you retrieve form data in PHP?
  - How do you validate an email address in PHP?

---

#### Post Lecture Questions

1. How would you modify the contact form to include a phone number with validation?
2. Write a function in PHP that accepts an array of numbers and returns the sum of the even numbers.
3. Explain how to handle file uploads in PHP using an example.

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Function declaration and invocation
  - Working with arrays
  - Form validation
- **Questions from students.**
