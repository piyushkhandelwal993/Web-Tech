### Lecture Plan: Milestone Project 3 - Create a PHP-based Web Form that Stores and Displays Submitted Data
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Introduction and Setup (20 Minutes)

**1. Overview of the Project (5 Minutes)**
- **Step-by-Step Explanation:**
  - Introduction to the project and its objectives.
  - Overview of the form submission process: creating a form, handling form data, storing data in a database, and displaying the data.
  - Importance of form validation and data security.

**Checkpoint Questions:**
  - What are the main steps involved in creating a PHP-based web form that stores and displays data?
  - Why is form validation important?

---

**2. Setting Up the Environment (15 Minutes)**
- **Step-by-Step Explanation:**
  - Setting up a local server (e.g., XAMPP, WAMP).
  - Creating a new PHP project directory.
  - Creating a database and table for storing form data.

- **Example:**
  ```sql
  CREATE DATABASE form_data;
  USE form_data;
  CREATE TABLE submissions (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(100),
      email VARCHAR(100),
      message TEXT,
      submission_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

**Checkpoint Questions:**
  - How do you set up a local PHP development environment?
  - What SQL command creates a new database?
  - How do you create a table in SQL?

---

#### Part 2: Creating and Validating the Form (30 Minutes)

**1. Creating the HTML Form (10 Minutes)**
- **Step-by-Step Explanation:**
  - Basic HTML structure of the form.
  - Form elements: input fields, textarea, submit button.

- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Contact Form</title>
  </head>
  <body>
      <form action="submit.php" method="POST">
          <label for="name">Name:</label>
          <input type="text" id="name" name="name" required><br><br>
          <label for="email">Email:</label>
          <input type="email" id="email" name="email" required><br><br>
          <label for="message">Message:</label><br>
          <textarea id="message" name="message" rows="4" required></textarea><br><br>
          <input type="submit" value="Submit">
      </form>
  </body>
  </html>
  ```

**Checkpoint Questions:**
  - What attributes are used in the `<form>` tag to specify the form submission method and action?
  - How do you make an input field required in HTML?

---

**2. Handling Form Submission and Validation (20 Minutes)**
- **Step-by-Step Explanation:**
  - Capturing form data using PHP's `$_POST` superglobal.
  - Validating the data to ensure it meets required criteria.
  - Sanitizing the data to prevent security issues such as SQL injection.

- **Example:**
  ```php
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $name = htmlspecialchars(trim($_POST['name']));
      $email = htmlspecialchars(trim($_POST['email']));
      $message = htmlspecialchars(trim($_POST['message']));

      if (empty($name) || empty($email) || empty($message)) {
          echo "All fields are required.";
      } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
          echo "Invalid email format.";
      } else {
          // Proceed to store data in database
      }
  }
  ?>
  ```

**Checkpoint Questions:**
  - What is the purpose of `$_POST` in PHP?
  - How do you sanitize user input in PHP?
  - What function is used to validate an email address in PHP?

---

#### Part 3: Storing and Displaying Data (40 Minutes)

**1. Storing Form Data in the Database (20 Minutes)**
- **Step-by-Step Explanation:**
  - Connecting to the MySQL database using PHP's `mysqli` or `PDO`.
  - Inserting validated data into the database table.

- **Example:**
  ```php
  <?php
  $servername = "localhost";
  $username = "root";
  $password = "";
  $dbname = "form_data";

  $conn = new mysqli($servername, $username, $password, $dbname);

  if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
  }

  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $name = htmlspecialchars(trim($_POST['name']));
      $email = htmlspecialchars(trim($_POST['email']));
      $message = htmlspecialchars(trim($_POST['message']));

      if (empty($name) || empty($email) || empty($message)) {
          echo "All fields are required.";
      } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
          echo "Invalid email format.";
      } else {
          $stmt = $conn->prepare("INSERT INTO submissions (name, email, message) VALUES (?, ?, ?)");
          $stmt->bind_param("sss", $name, $email, $message);
          $stmt->execute();
          echo "Submission successful!";
          $stmt->close();
      }
  }

  $conn->close();
  ?>
  ```

**Checkpoint Questions:**
  - How do you connect to a MySQL database in PHP?
  - What is the purpose of prepared statements in SQL?
  - How do you handle database connection errors in PHP?

---

**2. Displaying Stored Data (20 Minutes)**
- **Step-by-Step Explanation:**
  - Retrieving data from the database.
  - Displaying the data in an HTML table.

- **Example:**
  ```php
  <?php
  $conn = new mysqli($servername, $username, $password, $dbname);

  if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
  }

  $sql = "SELECT name, email, message, submission_date FROM submissions";
  $result = $conn->query($sql);

  if ($result->num_rows > 0) {
      echo "<table><tr><th>Name</th><th>Email</th><th>Message</th><th>Date</th></tr>";
      while($row = $result->fetch_assoc()) {
          echo "<tr><td>" . $row["name"]. "</td><td>" . $row["email"]. "</td><td>" . $row["message"]. "</td><td>" . $row["submission_date"]. "</td></tr>";
      }
      echo "</table>";
  } else {
      echo "0 results";
  }

  $conn->close();
  ?>
  ```

**Checkpoint Questions:**
  - How do you retrieve data from a MySQL database in PHP?
  - What function is used to fetch a row as an associative array in PHP?
  - How do you display database results in an HTML table?

---

### Post Lecture Questions

1. **Explain how you would handle empty form submissions in PHP.**
2. **How can you ensure that email addresses entered in the form are valid?**
3. **Describe the steps to prevent SQL injection in a PHP-based form.**
4. **What are some potential edge cases you need to consider when handling form data?**
5. **How would you modify the project to allow users to update their submitted data?**
6. **What exceptions might occur during database interactions, and how would you handle them?**

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Form creation and validation.
  - Data sanitization and security.
  - Database interactions: storing and retrieving data.
  - Handling edge cases and exceptions.

- **Questions from students.**
