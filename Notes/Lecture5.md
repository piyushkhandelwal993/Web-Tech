### Lecture Plan: Selecting and Modifying DOM Elements; Event Handling
#### Duration: 2 Hours

---

### Lecture Breakdown

#### Part 1: Selecting and Modifying DOM Elements (45 Minutes)

**1. Introduction to the DOM (5 Minutes)**
- **Explanation:**
  - The Document Object Model (DOM) is a programming interface for web documents.
  - It represents the structure of a document as a tree of nodes.

**Checkpoint Questions:**
  - What is the DOM?
  - How does the DOM represent a web document?

---

**2. Selecting DOM Elements (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Methods:**
    - `document.getElementById(id)`: Selects an element by its ID.
    - `document.getElementsByClassName(className)`: Selects all elements with a given class.
    - `document.getElementsByTagName(tagName)`: Selects all elements with a given tag name.
    - `document.querySelector(selector)`: Selects the first element that matches a CSS selector.
    - `document.querySelectorAll(selector)`: Selects all elements that match a CSS selector.

- **Examples:**
  ```javascript
  let header = document.getElementById("header");
  let items = document.getElementsByClassName("item");
  let paragraphs = document.getElementsByTagName("p");
  let firstItem = document.querySelector(".item");
  let allItems = document.querySelectorAll(".item");
  ```

**Checkpoint Questions:**
  - How do you select an element by its ID?
  - What is the difference between `querySelector` and `querySelectorAll`?

---

**3. Modifying DOM Elements (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Properties:**
    - `element.innerHTML`: Gets or sets the HTML content of an element.
    - `element.textContent`: Gets or sets the text content of an element.
    - `element.style`: Gets or sets the inline style of an element.
    - `element.setAttribute(name, value)`: Sets the value of an attribute.
    - `element.classList.add(className)`: Adds a class to an element.
    - `element.classList.remove(className)`: Removes a class from an element.

- **Examples:**
  ```javascript
  header.innerHTML = "<h1>Welcome!</h1>";
  firstItem.textContent = "Updated item";
  firstItem.style.color = "red";
  firstItem.setAttribute("data-value", "10");
  firstItem.classList.add("highlight");
  firstItem.classList.remove("item");
  ```

**Checkpoint Questions:**
  - How do you change the HTML content of an element?
  - How can you add a class to an element?

---

**4. Edge Cases and Tricky Concepts (10 Minutes)**
- **Examples and Explanations:**
  - **Non-existing Elements:** What happens if you try to select or modify a non-existing element.
  - **Live NodeLists vs. Static NodeLists:** Difference between `getElementsByClassName` (live) and `querySelectorAll` (static).
  - **Handling Special Characters:** Using `textContent` vs. `innerHTML` to avoid XSS attacks.

**Examples:**
  ```javascript
  let nonExistent = document.getElementById("nonExistent");
  if (nonExistent) {
    nonExistent.textContent = "This will not cause an error.";
  }
  let liveList = document.getElementsByClassName("item");
  let staticList = document.querySelectorAll(".item");
  document.body.appendChild(document.createElement("div")).className = "item";
  console.log(liveList.length); // Updated length
  console.log(staticList.length); // Original length
  ```

**Checkpoint Questions:**
  - What is a live NodeList?
  - How can you avoid XSS attacks when modifying the DOM?

---

#### Part 2: Event Handling (45 Minutes)

**1. Introduction to Event Handling (5 Minutes)**
- **Explanation:**
  - Events are actions or occurrences that happen in the browser.
  - Event handling is the process of capturing and responding to these events.

**Checkpoint Questions:**
  - What is an event in the context of web development?
  - Why is event handling important?

---

**2. Adding Event Listeners (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Method:**
    - `element.addEventListener(event, function)`: Registers an event handler.

- **Examples:**
  ```javascript
  header.addEventListener("click", function() {
    alert("Header clicked!");
  });
  firstItem.addEventListener("mouseover", function() {
    firstItem.style.backgroundColor = "yellow";
  });
  ```

**Checkpoint Questions:**
  - How do you add an event listener to an element?
  - What is the purpose of the `addEventListener` method?

---

**3. Removing Event Listeners and Event Object (15 Minutes)**
- **Step-by-Step Explanation:**
  - **Method:**
    - `element.removeEventListener(event, function)`: Removes an event handler.
  - **Event Object:**
    - Provides information about the event.
    - Common properties: `type`, `target`, `currentTarget`, `preventDefault()`, `stopPropagation()`.

- **Examples:**
  ```javascript
  function handleClick(event) {
    alert("Event type: " + event.type);
    event.target.style.backgroundColor = "blue";
  }
  header.addEventListener("click", handleClick);
  header.removeEventListener("click", handleClick);
  ```

**Checkpoint Questions:**
  - How do you remove an event listener?
  - What is the `event` object?

---

**4. Edge Cases and Tricky Concepts (10 Minutes)**
- **Examples and Explanations:**
  - **Event Delegation:** Using a single event listener for multiple elements.
  - **Preventing Default Actions:** Using `preventDefault()` to stop the default behavior of an event.
  - **Propagation and Bubbling:** Understanding `stopPropagation()` and event bubbling.

- **Examples:**
  ```javascript
  document.body.addEventListener("click", function(event) {
    if (event.target.classList.contains("item")) {
      alert("Item clicked!");
    }
  });
  document.querySelector("a").addEventListener("click", function(event) {
    event.preventDefault();
    alert("Link clicked but not followed!");
  });
  document.querySelector(".child").addEventListener("click", function(event) {
    event.stopPropagation();
    alert("Child clicked!");
  });
  ```

**Checkpoint Questions:**
  - What is event delegation?
  - How do you prevent the default action of an event?
  - What is event bubbling?

---

**5. Post Lecture Project: Image Slider/Carousel (20 Minutes)**
- **Step-by-Step Explanation:**
  - Create HTML structure for the slider.
  - Use JavaScript to handle the slide transitions and events.

- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Image Slider</title>
      <style>
          .slider { width: 300px; height: 200px; overflow: hidden; }
          .slides { display: flex; transition: transform 0.5s ease-in-out; }
          .slide { min-width: 100%; }
      </style>
  </head>
  <body>
      <div class="slider">
          <div class="slides">
              <img src="image1.jpg" class="slide" alt="Image 1">
              <img src="image2.jpg" class="slide" alt="Image 2">
              <img src="image3.jpg" class="slide" alt="Image 3">
          </div>
      </div>
      <button id="prev">Previous</button>
      <button id="next">Next</button>
      <script>
          let index = 0;
          const slides = document.querySelector(".slides");
          const totalSlides = document.querySelectorAll(".slide").length;

          document.getElementById("next").addEventListener("click", function() {
              index = (index + 1) % totalSlides;
              slides.style.transform = "translateX(" + (-index * 100) + "%)";
          });

          document.getElementById("prev").addEventListener("click", function() {
              index = (index - 1 + totalSlides) % totalSlides;
              slides.style.transform = "translateX(" + (-index * 100) + "%)";
          });
      </script>
  </body>
  </html>
  ```

**Checkpoint Questions:**
  - How do you handle click events for the slider buttons?
  - How do you transition between slides using JavaScript?

---

### Summary and Q&A (10 Minutes)
- **Recap key concepts:**
  - Selecting and Modifying DOM Elements
  - Event Handling
  - Practical application through an image slider

- **Questions from students.**
