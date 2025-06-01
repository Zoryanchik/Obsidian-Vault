<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced Cat Photo App</title>
    <style>
        /* General Styles */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            transition: background 0.5s, color 0.5s;
        }

        /* Dark Mode */
        .dark-mode {
            background-color: #333;
            color: white;
        }

        /* Navbar */
        nav {
            background: #007BFF;
            padding: 15px;
            text-align: center;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 10px;
            font-size: 18px;
        }

        /* Gallery */
        .gallery img {
            width: 100px;
            cursor: pointer;
            margin: 5px;
        }
        .large-image {
            width: 300px;
            display: block;
            margin: 10px auto;
        }

        /* Rating System */
        .stars {
            font-size: 24px;
            cursor: pointer;
        }
        .stars span:hover, .stars span.active {
            color: gold;
        }
    </style>
</head>
<body>

    <!-- Navigation Bar -->
    <nav>
        <a href="#photos">Cat Photos</a>
        <a href="#gallery">Gallery</a>
        <a href="#form">Submit a Cat Photo</a>
        <button onclick="toggleDarkMode()">Toggle Dark Mode</button>
    </nav>

    <main>

        <!-- Cat Photos Section -->
        <section id="photos">
            <h1>Cat Photo App</h1>
            <p>Everyone loves <a href="https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg">cute cats</a>!</p>
            <a href="https://freecatphotoapp.com">
                <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg" alt="A cute orange cat lying on its back.">
            </a>
        </section>

        <!-- Gallery Section -->
        <section id="gallery">
            <h2>Cat Photo Gallery</h2>
            <img class="large-image" id="mainImage" src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg" alt="Large cat image">
            <div class="gallery">
                <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg" alt="Lasagna" onclick="changeImage(this)">
                <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/cats.jpg" alt="Group of cats" onclick="changeImage(this)">
                <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg" alt="Running cats" onclick="changeImage(this)">
            </div>
        </section>

        <!-- Rating System -->
        <section>
            <h2>Rate This Cat Photo</h2>
            <div class="stars" onclick="rateCat(event)">
                <span>★</span> <span>★</span> <span>★</span> <span>★</span> <span>★</span>
            </div>
            <p id="ratingMessage">Click a star to rate!</p>
        </section>

        <!-- Form Section -->
        <section id="form">
            <h2>Submit a Cat Photo</h2>
            <form onsubmit="return validateForm()">
                <input type="text" id="catPhotoURL" placeholder="Enter cat photo URL" required>
                <button type="submit">Submit</button>
            </form>
        </section>

    </main>

    <footer>
        <p>No Copyright - <a href="https://www.freecodecamp.org">freeCodeCamp.org</a></p>
    </footer>

    <script>
        // Dark Mode Toggle
        function toggleDarkMode() {
            document.body.classList.toggle("dark-mode");
        }

        // Image Gallery Function
        function changeImage(img) {
            document.getElementById("mainImage").src = img.src;
        }

        // Form Validation
        function validateForm() {
            let url = document.getElementById("catPhotoURL").value;
            if (url === "") {
                alert("Please enter a valid cat photo URL.");
                return false;
            }
            alert("Cat photo submitted successfully!");
            return true;
        }

        // Rating System
        function rateCat(event) {
            let stars = document.querySelectorAll(".stars span");
            let index = Array.from(stars).indexOf(event.target);
            if (index !== -1) {
                stars.forEach((star, i) => {
                    star.classList.toggle("active", i <= index);
                });
                document.getElementById("ratingMessage").innerText = `You rated this ${index + 1} stars!`;
            }
        }
    </script>

</body>
</html>
![[Pasted image 20250326232058.png]]
