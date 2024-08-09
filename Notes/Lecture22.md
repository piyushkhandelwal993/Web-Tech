### Lecture Plan: Mini Project Integration - Integrated User Management System
#### Programming Language: PHP
#### Duration: 2 Hours
#### Other Specifications: Cover edge cases, tricky concepts, and interview-related exceptions.

---

### Lecture Breakdown

#### Part 1: Overview of the Integrated User Management System (20 Minutes)

**1. Introduction to the Project**
- **Step-by-Step Explanation:**
  - **Objective:** Integrate the mini projects created in previous lectures (e.g., User Registration, Login System, Profile Management) into a cohesive user management system.
  - **Key Features:**
    - User Registration and Validation
    - Secure Login and Session Management
    - Profile Management and Data Persistence
    - Role-based Access Control (optional for advanced learning)

- **Project Structure:**
  - **File Organization:**
    - `index.php` – Main entry point.
    - `register.php` – User registration.
    - `login.php` – User login.
    - `profile.php` – User profile management.
    - `logout.php` – User logout.
    - `config.php` – Database connection settings.
    - `functions.php` – Common functions like input validation, session management, etc.

**Checkpoint Questions:**
  - What are the key components needed for a user management system?
  - Why is session management crucial in a user management system?

---

#### Part 2: User Registration and Validation (20 Minutes)

**1. Setting Up User Registration**
- **Step-by-Step Explanation:**
  - **HTML Form for Registration:**
    - Fields: Username, Email, Password, Confirm Password.
    - Example:
      ```html
      <form action="register.php" method="post">
          <input type="text" name="username" placeholder="Username" required>
          <input type="email" name="email" placeholder="Email" required>
          <input type="password" name="password" placeholder="Password" required>
          <input type="password" name="confirm_password" placeholder="Confirm Password" required>
          <button type="submit">Register</button>
      </form>
      ```

- **2. PHP Validation Logic:**
  - **Input Validation:** Check for empty fields, valid email format, password length.
  - **Password Matching:** Ensure that `password` and `confirm_password` match.
  - **Edge Case:** Handling already registered emails and usernames.
    ```php
    if ($password !== $confirm_password) {
        echo "Passwords do not match!";
    }
    // Check if email or username already exists in the database.
    ```

- **3. Storing User Data Securely:**
  - **Password Hashing:** Use `password_hash()` to securely store passwords.
  - **Example:**
    ```php
    $hashed_password = password_hash($password, PASSWORD_DEFAULT);
    ```

**Checkpoint Questions:**
  - Why is password hashing important in user registration?
  - What edge cases should be considered when validating user registration data?

---

#### Part 3: User Login and Session Management (20 Minutes)

**1. Creating the Login Functionality**
- **Step-by-Step Explanation:**
  - **HTML Form for Login:**
    - Fields: Username/Email, Password.
    - Example:
      ```html
      <form action="login.php" method="post">
          <input type="text" name="username" placeholder="Username or Email" required>
          <input type="password" name="password" placeholder="Password" required>
          <button type="submit">Login</button>
      </form>
      ```

- **2. PHP Login Logic:**
  - **Validating User Credentials:** Fetch user data from the database and verify password using `password_verify()`.
  - **Session Management:** Start a session and store user information upon successful login.
    ```php
    if (password_verify($password, $hashed_password_from_db)) {
        session_start();
        $_SESSION['user_id'] = $user_id;
        header("Location: profile.php");
    } else {
        echo "Invalid credentials!";
    }
    ```

- **3. Handling Edge Cases:**
  - **Incorrect Password/Username:** Return appropriate error messages without revealing whether the username or password was incorrect.
  - **Account Lockout:** Implement a lockout mechanism after multiple failed login attempts to prevent brute-force attacks.

**Checkpoint Questions:**
  - How do you securely verify a password in PHP?
  - What are some potential security risks during the login process?

---

#### Part 4: Profile Management and Data Persistence (20 Minutes)

**1. Displaying User Profile Data**
- **Step-by-Step Explanation:**
  - **Fetching Data:** Retrieve user data from the database using the session ID.
  - **Example:**
    ```php
    $user_id = $_SESSION['user_id'];
    $query = "SELECT * FROM users WHERE id = $user_id";
    $result = mysqli_query($conn, $query);
    $user = mysqli_fetch_assoc($result);
    ```

- **2. Updating Profile Information:**
  - **Form for Updating Profile:**
    - Fields: Username, Email, Password (optional).
    - Example:
      ```html
      <form action="profile.php" method="post">
          <input type="text" name="username" value="<?php echo $user['username']; ?>" required>
          <input type="email" name="email" value="<?php echo $user['email']; ?>" required>
          <button type="submit">Update Profile</button>
      </form>
      ```

- **3. Handling Edge Cases:**
  - **Preventing Unauthorized Access:** Ensure only the logged-in user can view and edit their profile.
  - **Data Validation:** Validate the updated data, similar to the registration process.
  - **Exception Handling:** Handle cases where the database update fails, e.g., due to a network issue.

**Checkpoint Questions:**
  - How do you ensure that only authenticated users can access their profile page?
  - What should you do if a database update fails while updating a user’s profile?

---

#### Part 5: Role-Based Access Control and Security Considerations (Optional for Advanced Learners) (10 Minutes)

**1. Implementing Role-Based Access Control (RBAC)**
- **Step-by-Step Explanation:**
  - **Roles:** Define roles such as `admin`, `user`, etc., in the database.
  - **Access Control:** Restrict access to certain pages or functionalities based on user roles.
    ```php
    if ($_SESSION['role'] !== 'admin') {
        header("Location: unauthorized.php");
    }
    ```

**2. Security Best Practices**
- **Input Sanitization:** Prevent SQL injection by using prepared statements.
- **Cross-Site Scripting (XSS):** Sanitize output to prevent XSS attacks.

**Checkpoint Questions:**
  - What is the purpose of role-based access control?
  - How do prepared statements protect against SQL injection?

---

#### Part 6: Integration and Testing (20 Minutes)

**1. Integrating All Components**
- **Step-by-Step Explanation:**
  - **Bringing It All Together:** Combine the registration, login, and profile management components into a single project.
  - **Navigation:** Ensure smooth navigation between different pages.

- **2. Testing the System**
  - **Functional Testing:** Test each functionality, such as registration, login, and profile management.
  - **Edge Case Testing:** Test edge cases like invalid inputs, session hijacking, and improper role access.
  - **User Experience:** Ensure the user interface is intuitive and responsive.

**3. Handling Common Exceptions**
- **Database Connectivity Issues:** Implement error handling to manage database connection failures.
- **Session Timeout:** Handle session timeouts gracefully, redirecting users to the login page.

**Post-Lecture Questions:**
  - How would you handle a scenario where a user’s session times out while they are editing their profile?
  - Describe how you would implement a password reset functionality in the user management system.
  - What are the key differences between `isset()` and `empty()` in PHP, and when should you use each in the context of this project?

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - User Registration, Login, Profile Management, Session Management
  - Security considerations and edge case handling
- **Questions from students.**
