### Lecture Plan: Milestone Project 4 - Develop a Small Content Management System (CMS) with PHP and MySQL
#### Programming Language: PHP
#### Duration: 2 Hours
#### Other Specifications: Cover edge cases, tricky concepts, and exceptions that may be asked in interviews.

---

### Lecture Breakdown

#### Part 1: Project Overview and Setup (30 Minutes)

**1. Introduction to Content Management Systems (CMS) (10 Minutes)**
- **Step-by-Step Explanation:**
  - **Definition:** A CMS is a software application used to create, manage, and modify digital content.
  - **Examples:** WordPress, Joomla, Drupal.
  - **Purpose:** Understand the basics of a CMS and what the final project aims to achieve.
  - **Core Features:**
    - User authentication
    - Content creation and editing
    - Database storage for posts, pages, and users

**Checkpoint Questions:**
  - What is a CMS, and why is it important?
  - Name three common features of a CMS.

---

**2. Project Setup: Environment and Database (20 Minutes)**
- **Step-by-Step Explanation:**
  - **PHP and MySQL Setup:** Ensure the development environment is ready (XAMPP, WAMP, or MAMP).
  - **Database Design:**
    - **Tables:** Users, Posts, Categories.
    - **Fields:** id (Primary Key), title, content, author, created_at, updated_at.
    - **Relationships:** One-to-many (User to Posts), many-to-many (Posts to Categories).

- **Example Database Schema:**
  ```sql
  CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      username VARCHAR(50) UNIQUE NOT NULL,
      password VARCHAR(255) NOT NULL,
      role ENUM('admin', 'editor', 'user') NOT NULL,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );

  CREATE TABLE posts (
      id INT AUTO_INCREMENT PRIMARY KEY,
      title VARCHAR(255) NOT NULL,
      content TEXT NOT NULL,
      author_id INT,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
      updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
      FOREIGN KEY (author_id) REFERENCES users(id)
  );

  CREATE TABLE categories (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(100) UNIQUE NOT NULL
  );

  CREATE TABLE post_categories (
      post_id INT,
      category_id INT,
      FOREIGN KEY (post_id) REFERENCES posts(id),
      FOREIGN KEY (category_id) REFERENCES categories(id),
      PRIMARY KEY(post_id, category_id)
  );
  ```

**Checkpoint Questions:**
  - How would you design a database schema for a CMS?
  - What are the relationships between the tables in the CMS database?

---

#### Part 2: Developing the CMS (90 Minutes)

**1. User Authentication and Authorization (30 Minutes)**
- **Step-by-Step Explanation:**
  - **Login and Registration:**
    - **Password Hashing:** Using `password_hash()` and `password_verify()` to securely store and check passwords.
    - **Session Management:** Implementing login sessions to keep users authenticated.
  - **Role-Based Access Control:**
    - Admins can manage users and posts.
    - Editors can create and edit posts.
    - Users can view posts.

- **Example Code:**
  ```php
  session_start();

  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $username = $_POST['username'];
      $password = $_POST['password'];

      // Query database for user
      $stmt = $pdo->prepare("SELECT * FROM users WHERE username = ?");
      $stmt->execute([$username]);
      $user = $stmt->fetch();

      if ($user && password_verify($password, $user['password'])) {
          $_SESSION['user_id'] = $user['id'];
          $_SESSION['role'] = $user['role'];
          header("Location: dashboard.php");
      } else {
          echo "Invalid username or password!";
      }
  }
  ```

**Edge Cases & Tricky Concepts:**
  - **SQL Injection:** Use prepared statements to prevent SQL injection.
  - **Session Hijacking:** Implement session regeneration after login.
  - **Brute Force Attacks:** Implement account lockout after multiple failed login attempts.

**Checkpoint Questions:**
  - How can you securely store user passwords in a CMS?
  - What is the purpose of role-based access control in a CMS?

---

**2. Content Creation and Management (40 Minutes)**
- **Step-by-Step Explanation:**
  - **Creating Posts:**
    - Form for creating new posts with fields for title, content, and categories.
    - Storing posts in the database with `INSERT` SQL statements.
  - **Editing and Deleting Posts:**
    - **Editing:** Fetch post data, display in form, update in database.
    - **Deleting:** Confirm deletion and remove post from the database.
  - **Content Validation:** Ensure title and content are not empty; check for valid category selections.

- **Example Code:**
  ```php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $title = $_POST['title'];
      $content = $_POST['content'];
      $author_id = $_SESSION['user_id'];

      if (!empty($title) && !empty($content)) {
          $stmt = $pdo->prepare("INSERT INTO posts (title, content, author_id) VALUES (?, ?, ?)");
          $stmt->execute([$title, $content, $author_id]);
          echo "Post created successfully!";
      } else {
          echo "Title and content cannot be empty!";
      }
  }
  ```

**Edge Cases & Tricky Concepts:**
  - **XSS Attacks:** Use `htmlspecialchars()` to sanitize user input before displaying.
  - **Content Overwrite:** Implement version control or warning if another user is editing the same post.
  - **Race Conditions:** Use transactions to ensure atomic operations when multiple users are updating data simultaneously.

**Checkpoint Questions:**
  - How do you prevent XSS attacks when displaying user-generated content?
  - What measures would you take to avoid race conditions in a CMS?

---

**3. Displaying Content and User Roles (20 Minutes)**
- **Step-by-Step Explanation:**
  - **Fetching and Displaying Posts:**
    - Query the database for posts and display them on the homepage.
    - Implement pagination for better performance with large data sets.
  - **User Role-Based Display:**
    - Show edit and delete options only to users with appropriate roles.
    - Hide certain posts or content based on user roles.

- **Example Code:**
  ```php
  $stmt = $pdo->query("SELECT * FROM posts ORDER BY created_at DESC LIMIT 10");
  while ($row = $stmt->fetch()) {
      echo "<h2>" . htmlspecialchars($row['title']) . "</h2>";
      echo "<p>" . htmlspecialchars($row['content']) . "</p>";

      if ($_SESSION['role'] == 'admin' || $_SESSION['user_id'] == $row['author_id']) {
          echo "<a href='edit_post.php?id=" . $row['id'] . "'>Edit</a>";
          echo "<a href='delete_post.php?id=" . $row['id'] . "'>Delete</a>";
      }
  }
  ```

**Edge Cases & Tricky Concepts:**
  - **Access Control:** Ensure only authorized users can see or modify content.
  - **Pagination:** Handle edge cases like no posts available or navigating beyond available pages.

**Checkpoint Questions:**
  - How would you implement pagination for displaying posts?
  - How do you ensure that only authorized users can edit or delete posts?

---

#### Part 3: Post Lecture Questions and Q&A (30 Minutes)

**1. Post Lecture Questions:**
  - How would you implement user role management in a CMS?
  - Explain how you would prevent SQL injection and XSS attacks in your CMS.
  - How can you ensure data consistency when multiple users are editing content simultaneously?

**2. Q&A and Discussion:**
  - Address any questions students have about the project.
  - Discuss potential improvements and optimizations.

---

### Summary and Conclusion
- **Recap:** Covered user authentication, content creation and management, and displaying content based on user roles.
- **Final Thoughts:** Reinforce the importance of security, scalability, and user experience in CMS development.
