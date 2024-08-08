### Lecture Plan: Working with Forms, GET and POST Methods; Form Handling and Validation
#### Programming Language: PHP
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Working with Forms and GET/POST Methods (45 Minutes)

**1. Introduction to Forms and HTTP Methods (15 Minutes)**
- **Step-by-Step Explanation:**
  - **HTML Form Basics:**
    - `<form>` tag, `action`, and `method` attributes.
    - **GET Method:** Appends form data to the URL.
    - **POST Method:** Sends form data as HTTP request body.
  - **Example: Simple Form:**
    ```html
    <form action="process_form.php" method="GET">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name">
        <input type="submit" value="Submit">
    </form>
    ```

**Checkpoint Questions:**
  - What is the difference between GET and POST methods?
  - When would you use the GET method over POST?

---

**2. Handling Form Data with PHP (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Accessing Form Data:**
    - Using `$_GET` and `$_POST` superglobals.
    - **Example:**
      ```php
      <?php
      if ($_SERVER["REQUEST_METHOD"] == "POST") {
          $name = $_POST['name'];
          echo "Hello, " . htmlspecialchars($name) . "!";
      }
      ?>
      ```

**Checkpoint Questions:**
  - How do you access data submitted via the POST method in PHP?
  - Why is it important to use `htmlspecialchars()` when displaying user input?

---

**3. User Registration Form Example (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Form Structure:**
    ```html
    <form action="register.php" method="POST">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">

        <label for="password">Password:</label>
        <input type="password" id="password" name="password">

        <label for="email">Email:</label>
        <input type="email" id="email" name="email">

        <input type="submit" value="Register">
    </form>
    ```
  - **PHP Handling:**
    ```php
    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $username = $_POST['username'];
        $password = $_POST['password'];
        $email = $_POST['email'];

        // Sanitize input
        $username = htmlspecialchars($username);
        $email = htmlspecialchars($email);

        // Example Output
        echo "Username: " . $username . "<br>";
        echo "Email: " . $email;
    }
    ?>
    ```

**Checkpoint Questions:**
  - How do you create a form that submits data using the POST method?
  - How do you ensure user input is safe to display on a webpage?

---

#### Part 2: Form Validation and Edge Cases (45 Minutes)

**1. Basic Form Validation (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Client-Side vs. Server-Side Validation:**
    - Client-side validation for user experience.
    - Server-side validation for security.
  - **PHP Validation:**
    ```php
    <?php
    $usernameErr = $emailErr = "";
    $username = $email = "";

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        if (empty($_POST["username"])) {
            $usernameErr = "Username is required";
        } else {
            $username = htmlspecialchars($_POST["username"]);
        }

        if (empty($_POST["email"])) {
            $emailErr = "Email is required";
        } elseif (!filter_var($_POST["email"], FILTER_VALIDATE_EMAIL)) {
            $emailErr = "Invalid email format";
        } else {
            $email = htmlspecialchars($_POST["email"]);
        }
    }
    ?>
    ```
  - **Example Form with Validation:**
    ```html
    <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="POST">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
        <span><?php echo $usernameErr; ?></span>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email">
        <span><?php echo $emailErr; ?></span>

        <input type="submit" value="Register">
    </form>
    ```

**Checkpoint Questions:**
  - Why is server-side validation necessary even if client-side validation is performed?
  - How do you validate an email address in PHP?

---

**2. Advanced Validation and Edge Cases (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Common Edge Cases:**
    - Empty input fields.
    - Invalid email format.
    - SQL Injection.
  - **Example Validation:**
    ```php
    <?php
    $passwordErr = "";
    $password = "";

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        if (empty($_POST["password"])) {
            $passwordErr = "Password is required";
        } elseif (strlen($_POST["password"]) < 8) {
            $passwordErr = "Password must be at least 8 characters long";
        } else {
            $password = htmlspecialchars($_POST["password"]);
        }
    }
    ?>
    ```
  - **Additional Form Handling:**
    - **Example: Preventing SQL Injection:**
      ```php
      $conn = new mysqli($servername, $username, $password, $dbname);
      $stmt = $conn->prepare("INSERT INTO users (username, email, password) VALUES (?, ?, ?)");
      $stmt->bind_param("sss", $username, $email, $password);
      $stmt->execute();
      ```

**Checkpoint Questions:**
  - How do you handle edge cases like empty input fields and invalid data formats in PHP?
  - What measures can you take to prevent SQL injection in PHP?

---

**3. Post Lecture Questions (15 Minutes)**
- **To measure understanding and retention:**
  - Create a user registration form that includes a username, password, and email. Implement both client-side and server-side validation.
  - Write PHP code to validate that the password is at least 8 characters long and contains at least one number and one special character.
  - How would you modify your form handling to prevent SQL injection?

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Working with forms in PHP
  - GET and POST methods
  - Form handling and validation
  - Handling edge cases and preventing security vulnerabilities

- **Questions from students.**
