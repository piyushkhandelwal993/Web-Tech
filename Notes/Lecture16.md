### Lecture Plan: File Handling in PHP - Reading and Writing Files
#### Duration: 2 Hours
#### Programming Language: PHP
#### Topic: File Handling - Reading and Writing Files
#### Example: Uploading and Displaying User Profile Pictures
#### Other Specifications: Cover edge cases, tricky concepts, and exceptions that may be asked in interviews.

---

### Lecture Breakdown

#### Part 1: Introduction to File Handling in PHP (15 Minutes)

**1. Basics of File Handling**
- **Step-by-Step Explanation:**
  - **File Handling:** PHP provides functions to read from, write to, and manipulate files.
  - **Common Functions:**
    - `fopen()`: Opens a file.
    - `fread()`: Reads data from a file.
    - `fwrite()`: Writes data to a file.
    - `fclose()`: Closes an open file.
    - `file_exists()`: Checks if a file exists.
    - `unlink()`: Deletes a file.
  - **Example:**
    ```php
    $file = fopen("example.txt", "w");
    fwrite($file, "Hello, World!");
    fclose($file);
    ```

**Checkpoint Questions:**
- What are the basic functions used for file handling in PHP?
- How do you open a file in write mode?

---

#### Part 2: Reading from Files (25 Minutes)

**1. Reading Methods**
- **Step-by-Step Explanation:**
  - **Reading a File:**
    - `fread()`: Reads a specific number of bytes from a file.
    - `fgets()`: Reads a line from a file.
    - `file_get_contents()`: Reads the entire file into a string.
  - **Example:**
    ```php
    $file = fopen("example.txt", "r");
    $content = fread($file, filesize("example.txt"));
    fclose($file);
    echo $content;
    ```

**2. Edge Cases and Tricky Concepts:**
- **Empty Files:** What happens if the file is empty or doesn't exist?
  - Handle with `file_exists()` or check file size.
- **Binary Files:** Ensure correct mode (e.g., `rb` for reading binary files).
- **Example:**
  ```php
  if (file_exists("example.txt")) {
      $file = fopen("example.txt", "r");
      if (filesize("example.txt") > 0) {
          $content = fread($file, filesize("example.txt"));
      } else {
          $content = "File is empty.";
      }
      fclose($file);
  } else {
      $content = "File does not exist.";
  }
  echo $content;
  ```

**Checkpoint Questions:**
- How do you read the entire content of a file in PHP?
- What should you check before reading from a file?

---

#### Part 3: Writing to Files (25 Minutes)

**1. Writing Methods**
- **Step-by-Step Explanation:**
  - **Writing to a File:**
    - `fwrite()`: Writes to a file.
    - `file_put_contents()`: Writes data to a file (overwrites existing data).
  - **Example:**
    ```php
    $file = fopen("example.txt", "w");
    fwrite($file, "This is a new line.");
    fclose($file);
    ```

**2. Edge Cases and Tricky Concepts:**
- **Overwriting Files:** `file_put_contents()` overwrites the file; use `FILE_APPEND` to add to existing content.
- **File Permissions:** Ensure the script has the necessary permissions to write to the file.
- **Example:**
  ```php
  $filename = "example.txt";
  if (is_writable($filename)) {
      file_put_contents($filename, "Appending this line.\n", FILE_APPEND);
  } else {
      echo "File is not writable.";
  }
  ```

**Checkpoint Questions:**
- What happens when you write to a file that already contains data?
- How can you append data to a file without overwriting the existing content?

---

#### Part 4: Uploading and Displaying User Profile Pictures (30 Minutes)

**1. Handling File Uploads**
- **Step-by-Step Explanation:**
  - **Form Handling:**
    - Use `enctype="multipart/form-data"` in the form.
    - Access uploaded files using `$_FILES`.
  - **Example:**
    ```php
    if ($_SERVER['REQUEST_METHOD'] == 'POST') {
        $target_dir = "uploads/";
        $target_file = $target_dir . basename($_FILES["profilePic"]["name"]);
        if (move_uploaded_file($_FILES["profilePic"]["tmp_name"], $target_file)) {
            echo "The file ". basename($_FILES["profilePic"]["name"]). " has been uploaded.";
        } else {
            echo "Sorry, there was an error uploading your file.";
        }
    }
    ```
  - **Displaying the Uploaded Image:**
    ```php
    echo '<img src="uploads/' . htmlspecialchars(basename($_FILES["profilePic"]["name"])) . '" />';
    ```

**2. Edge Cases and Tricky Concepts:**
- **File Size Limits:** Handle file size limits using `$_FILES['profilePic']['size']` and server configurations (`php.ini`).
- **File Type Validation:** Validate file type using `mime_content_type()` or `pathinfo()`.
- **Security Considerations:** Prevent directory traversal attacks by sanitizing file names.
- **Example:**
  ```php
  $allowed_types = ['image/jpeg', 'image/png', 'image/gif'];
  $file_type = mime_content_type($_FILES["profilePic"]["tmp_name"]);
  if (in_array($file_type, $allowed_types)) {
      // Safe to upload
  } else {
      echo "Invalid file type.";
  }
  ```

**Checkpoint Questions:**
- How do you handle file uploads in PHP?
- What are some security considerations when uploading files?

---

#### Part 5: Post Lecture Questions (15 Minutes)
- **To measure understanding and retention:**
  - How would you handle an error if the file does not exist when trying to read it?
  - Write a function to check if a file is writable before attempting to write to it.
  - Modify the file upload script to only allow images less than 1MB in size.

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Reading and Writing Files
  - File Uploads and Security Considerations

- **Questions from students.**
