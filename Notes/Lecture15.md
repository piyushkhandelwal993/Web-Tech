### Lecture Plan: Sessions and Cookies in PHP
#### Topic: Managing Sessions, Using Cookies; Example: User Login System
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Introduction to Sessions and Cookies (30 Minutes)

**1. Overview of Sessions and Cookies (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Sessions:**
    - A session is a way to store information (in variables) to be used across multiple pages.
    - Sessions are stored on the server.
    - **Example:**
      ```php
      session_start();
      $_SESSION['username'] = 'JohnDoe';
      ```
  - **Cookies:**
    - Cookies are small files stored on the client’s computer.
    - Cookies are sent to the server with every request.
    - **Example:**
      ```php
      setcookie('username', 'JohnDoe', time() + (86400 * 30), "/"); // 86400 = 1 day
      ```

**2. Differences Between Sessions and Cookies (5 Minutes)**
- Sessions are more secure than cookies because they are stored on the server.
- Cookies can persist across multiple sessions, while session data is typically lost when the session ends.
- **Example Scenario:** Use sessions to store user login information, and cookies to remember a user’s preference for the site theme.

**3. Security Considerations (10 Minutes)**
- **Edge Cases & Tricky Concepts:**
  - **Session Hijacking:**
    - Attackers can steal session IDs and impersonate users.
    - Mitigation: Regenerate session IDs periodically using `session_regenerate_id()`.
  - **Cookie Theft:**
    - If cookies are not secured, attackers can intercept them.
    - Mitigation: Set the `HttpOnly` and `Secure` flags on cookies.
    ```php
    setcookie('username', 'JohnDoe', time() + (86400 * 30), "/", "", true, true); // Secure and HttpOnly
    ```

**Checkpoint Questions:**
- What is the main difference between sessions and cookies?
- How can you make cookies more secure?

---

#### Part 2: Managing Sessions in PHP (40 Minutes)

**1. Starting and Ending Sessions (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Starting a Session:**
    ```php
    session_start();
    ```
  - **Storing and Accessing Session Variables:**
    ```php
    $_SESSION['user_id'] = 123;
    echo $_SESSION['user_id'];
    ```
  - **Ending a Session:**
    - **Destroying a session:**
      ```php
      session_destroy();
      ```
    - **Unsetting session variables:**
      ```php
      session_unset();
      ```
  - **Example:** Implementing a logout feature that ends the session.

**2. Session Handling Across Multiple Pages (10 Minutes)**
- **Explanation:**
  - Ensure `session_start()` is called at the beginning of every script where session data is needed.
  - **Example:**
    ```php
    // On login page
    session_start();
    $_SESSION['username'] = 'JohnDoe';

    // On another page
    session_start();
    echo 'Welcome ' . $_SESSION['username'];
    ```

**3. Handling Session Timeout (10 Minutes)**
- **Edge Cases & Tricky Concepts:**
  - **Session Expiry:**
    - Sessions should expire after a period of inactivity for security reasons.
    - Implementing session timeout:
      ```php
      session_start();
      if (isset($_SESSION['LAST_ACTIVITY']) && (time() - $_SESSION['LAST_ACTIVITY'] > 1800)) {
          // last request was more than 30 minutes ago
          session_unset();     // unset $_SESSION variable for the runtime
          session_destroy();   // destroy session data in storage
      }
      $_SESSION['LAST_ACTIVITY'] = time(); // update last activity time stamp
      ```
  - **Interview Tip:** Be ready to discuss how to handle session timeouts and refresh tokens.

**Checkpoint Questions:**
- How do you ensure a session is available on multiple pages?
- How can you implement session timeouts?

---

#### Part 3: Using Cookies in PHP (30 Minutes)

**1. Setting and Retrieving Cookies (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Setting a Cookie:**
    ```php
    setcookie('user', 'JohnDoe', time() + (86400 * 30), "/"); // 86400 = 1 day
    ```
  - **Retrieving a Cookie:**
    ```php
    if(isset($_COOKIE['user'])) {
        echo "User is " . $_COOKIE['user'];
    }
    ```
  - **Example:** Implementing a “Remember Me” feature on a login form.

**2. Deleting Cookies (10 Minutes)**
- **Explanation:**
  - To delete a cookie, set its expiration date to a past time.
  - **Example:**
    ```php
    setcookie('user', '', time() - 3600, "/");
    ```

**3. Handling Cookie Expiry and Security (10 Minutes)**
- **Edge Cases & Tricky Concepts:**
  - **Cookie Expiry:**
    - What happens when cookies expire? Discuss cookie renewal.
  - **Secure Cookies:**
    - Ensure cookies are transmitted securely over HTTPS.
    ```php
    setcookie('user', 'JohnDoe', time() + (86400 * 30), "/", "", true, true);
    ```

**Checkpoint Questions:**
- How do you set a cookie that lasts for 7 days?
- What is the purpose of the `HttpOnly` flag on cookies?

---

#### Part 4: Building a User Login System (30 Minutes)

**1. Login Form and Session Management (15 Minutes)**
- **Step-by-Step Explanation:**
  - Create a simple login form.
  - On successful login, start a session and store user data.
  - **Example:**
    ```php
    // login.php
    session_start();
    if($_POST['username'] == 'admin' && $_POST['password'] == 'password') {
        $_SESSION['user'] = 'admin';
        header("Location: dashboard.php");
    } else {
        echo "Invalid credentials.";
    }
    ```

**2. Remember Me Feature Using Cookies (10 Minutes)**
- **Explanation:**
  - Use cookies to store login information if the user opts for “Remember Me.”
  - **Example:**
    ```php
    if(isset($_POST['remember'])) {
        setcookie('username', $_POST['username'], time() + (86400 * 30), "/");
    }
    ```

**3. Edge Cases & Tricky Concepts (5 Minutes)**
- **Handling Invalid Logins:** What happens if a user enters the wrong credentials multiple times?
- **Interview Tip:** Be ready to discuss securing login systems against common attacks (e.g., brute force, SQL injection).

**Post Lecture Questions:**
- How would you handle a situation where a user tries to log in from multiple devices simultaneously?
- What are some common security risks associated with sessions and cookies, and how can you mitigate them?
- Describe how you would implement a “Remember Me” feature that automatically logs users in the next time they visit the site.

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Managing sessions and using cookies in PHP.
  - Practical application through a user login system.

- **Questions from students.**

This plan covers the essential concepts of sessions and cookies in PHP, along with edge cases, tricky scenarios, and interview-relevant questions to ensure a comprehensive understanding.
