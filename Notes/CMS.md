Here’s a simplified CMS with minimal functionalities in PHP, covering user authentication, content creation, and content display. I'll include basic features such as user login, role-based access, and the ability to create, edit, and delete posts.

### Assumptions:
1. **Users**: Two roles - Admin and Editor.
2. **Posts**: A user can create, edit, and delete posts.
3. **Authentication**: Simple login with password hashing.
4. **Database**: MySQL with basic schema.

### Database Schema
```sql
CREATE DATABASE cms;

USE cms;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin', 'editor') NOT NULL,
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
```

### 1. `db.php` - Database Connection
```php
<?php
$host = 'localhost';
$db = 'cms';
$user = 'root';
$pass = '';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$db", $user, $pass);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    die("Could not connect to the database: " . $e->getMessage());
}
?>
```

### 2. `register.php` - User Registration (For Admin to Create Users)
```php
<?php
require 'db.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'];
    $password = password_hash($_POST['password'], PASSWORD_BCRYPT);
    $role = $_POST['role'];

    $stmt = $pdo->prepare("INSERT INTO users (username, password, role) VALUES (?, ?, ?)");
    $stmt->execute([$username, $password, $role]);

    echo "User registered successfully!";
}
?>

<form method="POST" action="">
    Username: <input type="text" name="username" required><br>
    Password: <input type="password" name="password" required><br>
    Role:
    <select name="role">
        <option value="admin">Admin</option>
        <option value="editor">Editor</option>
    </select><br>
    <button type="submit">Register</button>
</form>
```

### 3. `login.php` - User Login
```php
<?php
require 'db.php';
session_start();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'];
    $password = $_POST['password'];

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
?>

<form method="POST" action="">
    Username: <input type="text" name="username" required><br>
    Password: <input type="password" name="password" required><br>
    <button type="submit">Login</button>
</form>
```

### 4. `dashboard.php` - User Dashboard
```php
<?php
require 'db.php';
session_start();

if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit;
}

echo "Welcome, " . $_SESSION['role'] . "!<br>";
?>

<a href="create_post.php">Create Post</a><br>
<a href="logout.php">Logout</a>

<h2>Your Posts</h2>

<?php
$stmt = $pdo->prepare("SELECT * FROM posts WHERE author_id = ?");
$stmt->execute([$_SESSION['user_id']]);

while ($post = $stmt->fetch()) {
    echo "<h3>" . htmlspecialchars($post['title']) . "</h3>";
    echo "<p>" . htmlspecialchars($post['content']) . "</p>";
    echo "<a href='edit_post.php?id=" . $post['id'] . "'>Edit</a> | ";
    echo "<a href='delete_post.php?id=" . $post['id'] . "'>Delete</a><br><br>";
}
?>
```

### 5. `create_post.php` - Create New Post
```php
<?php
require 'db.php';
session_start();

if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit;
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $title = $_POST['title'];
    $content = $_POST['content'];
    $author_id = $_SESSION['user_id'];

    if (!empty($title) && !empty($content)) {
        $stmt = $pdo->prepare("INSERT INTO posts (title, content, author_id) VALUES (?, ?, ?)");
        $stmt->execute([$title, $content, $author_id]);
        header("Location: dashboard.php");
    } else {
        echo "Title and content cannot be empty!";
    }
}
?>

<form method="POST" action="">
    Title: <input type="text" name="title" required><br>
    Content: <textarea name="content" required></textarea><br>
    <button type="submit">Create Post</button>
</form>
```

### 6. `edit_post.php` - Edit Post
```php
<?php
require 'db.php';
session_start();

if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit;
}

$post_id = $_GET['id'];

$stmt = $pdo->prepare("SELECT * FROM posts WHERE id = ? AND author_id = ?");
stmt->execute([$post_id, $_SESSION['user_id']]);
$post = $stmt->fetch();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $title = $_POST['title'];
    $content = $_POST['content'];

    if (!empty($title) && !empty($content)) {
        $stmt = $pdo->prepare("UPDATE posts SET title = ?, content = ? WHERE id = ?");
        $stmt->execute([$title, $content, $post_id]);
        header("Location: dashboard.php");
    } else {
        echo "Title and content cannot be empty!";
    }
}
?>

<form method="POST" action="">
    Title: <input type="text" name="title" value="<?= htmlspecialchars($post['title']) ?>" required><br>
    Content: <textarea name="content" required><?= htmlspecialchars($post['content']) ?></textarea><br>
    <button type="submit">Update Post</button>
</form>
```

### 7. `delete_post.php` - Delete Post
```php
<?php
require 'db.php';
session_start();

if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit;
}

$post_id = $_GET['id'];

$stmt = $pdo->prepare("DELETE FROM posts WHERE id = ? AND author_id = ?");
$stmt->execute([$post_id, $_SESSION['user_id']]);

header("Location: dashboard.php");
?>
```

### 8. `logout.php` - User Logout
```php
<?php
session_start();
session_destroy();
header("Location: login.php");
?>
```

### Summary:
- **Basic Functionality**: User registration, login, post creation, editing, deletion, and listing.
- **Security Considerations**: Password hashing, session management, user-specific content management.
- **Role-Based Access**: Separate actions for admin and editor roles (though minimal in this example).

This minimal CMS can be extended with additional features such as role-based content access, richer content management, and more advanced security measures.
