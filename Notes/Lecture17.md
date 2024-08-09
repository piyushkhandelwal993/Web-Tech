### Lecture Plan: PHP Security - Preventing SQL Injection and XSS
#### Duration: 2 Hours
#### Programming Language: PHP

---

### Lecture Breakdown

#### Part 1: Introduction to PHP Security (10 Minutes)
- **Step-by-Step Explanation:**
  - **Overview:**
    - Importance of web security in PHP applications.
    - Common security vulnerabilities: SQL Injection and Cross-Site Scripting (XSS).
  - **Real-World Relevance:**
    - Impact of security breaches on businesses and users.
    - Importance in interviews and real-world applications.

**Checkpoint Questions:**
  - Why is security important in web applications?
  - What are some common security threats in PHP?

---

#### Part 2: SQL Injection (40 Minutes)

**1. Understanding SQL Injection (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Definition:** SQL Injection is a code injection technique that exploits a vulnerability in the application's software by manipulating SQL queries.
  - **How It Happens:**
    - User input is directly inserted into SQL queries without proper validation or sanitization.
  - **Example of Vulnerable Code:**
    ```php
    $username = $_POST['username'];
    $password = $_POST['password'];
    $query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
    $result = mysqli_query($conn, $query);
    ```

**Checkpoint Questions:**
  - What is SQL Injection?
  - How can SQL Injection occur in a PHP application?

**2. Preventing SQL Injection (20 Minutes)**
- **Step-by-Step Explanation:**
  - **Prepared Statements:** Using prepared statements with bound parameters.
    - **Example:**
      ```php
      $stmt = $conn->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
      $stmt->bind_param("ss", $username, $password);
      $stmt->execute();
      $result = $stmt->get_result();
      ```
  - **Edge Cases and Tricky Concepts:**
    - **Edge Case:** Handling special characters in user input.
    - **Tricky Concept:** Why using `mysqli_real_escape_string()` alone is not enough.
  - **Exceptions:**
    - **Interview Focus:** Explain why prepared statements are preferred over manual sanitization.

**Checkpoint Questions:**
  - What are prepared statements?
  - How do prepared statements help in preventing SQL Injection?

**3. Implementing a Secure User Authentication System (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Secure Login System:** Example of a secure user authentication system using prepared statements.
  - **Example:**
    ```php
    $username = $_POST['username'];
    $password = $_POST['password'];

    $stmt = $conn->prepare("SELECT id, password_hash FROM users WHERE username = ?");
    $stmt->bind_param("s", $username);
    $stmt->execute();
    $stmt->bind_result($user_id, $stored_hash);
    $stmt->fetch();

    if (password_verify($password, $stored_hash)) {
        echo "Login successful!";
    } else {
        echo "Invalid username or password.";
    }
    ```

**Checkpoint Questions:**
  - How does the `password_verify()` function work in PHP?
  - Why is it important to use prepared statements in user authentication?

---

#### Part 3: Cross-Site Scripting (XSS) (30 Minutes)

**1. Understanding XSS (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Definition:** Cross-Site Scripting (XSS) is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users.
  - **How It Happens:**
    - User input is not properly sanitized, allowing scripts to be injected into the webpage.
  - **Example of Vulnerable Code:**
    ```php
    echo "Welcome, " . $_GET['username'];
    ```

**Checkpoint Questions:**
  - What is Cross-Site Scripting (XSS)?
  - How can XSS be exploited in a PHP application?

**2. Preventing XSS (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Output Escaping:** Escaping user input before displaying it in the browser.
    - **Example:**
      ```php
      echo "Welcome, " . htmlspecialchars($_GET['username'], ENT_QUOTES, 'UTF-8');
      ```
  - **Edge Cases and Tricky Concepts:**
    - **Edge Case:** Handling different types of encoding (e.g., UTF-8).
    - **Tricky Concept:** Differentiating between input sanitization and output escaping.
  - **Exceptions:**
    - **Interview Focus:** Explain why output escaping is crucial even if input sanitization is done.

**Checkpoint Questions:**
  - What is output escaping?
  - Why is `htmlspecialchars()` important in preventing XSS?

**3. Implementing XSS Prevention in User Authentication (5 Minutes)**
- **Step-by-Step Explanation:**
  - **Secure Display:** Ensuring that all user inputs displayed back on the page are properly escaped.
  - **Example:**
    ```php
    echo "User profile: " . htmlspecialchars($user_profile, ENT_QUOTES, 'UTF-8');
    ```

**Checkpoint Questions:**
  - How do you ensure user inputs are safely displayed on the page?
  - What function is commonly used to prevent XSS in PHP?

---

#### Part 4: Post Lecture Questions and Summary (10 Minutes)

**1. Recap Key Concepts:**
  - **SQL Injection:**
    - Understanding and preventing SQL Injection.
    - Importance of prepared statements.
  - **Cross-Site Scripting (XSS):**
    - How XSS works and how to prevent it using output escaping.

**2. Post Lecture Questions:**
  - Explain a scenario where SQL Injection could occur and how you would prevent it.
  - Why is output escaping necessary even if input validation is implemented?
  - How would you handle displaying user-generated content safely on a webpage?

**3. Q&A Session:**
  - Open floor for students to ask any questions related to PHP security, SQL Injection, or XSS.

---
