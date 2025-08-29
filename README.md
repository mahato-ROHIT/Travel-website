<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sammy's Travel Portfolio</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Hero Section -->
  <header class="hero">
    <div class="hero-text">
      <h1>Hi, I'm Sammy 🌍</h1>
      <p>Frontend Developer | Traveler | Explorer</p>
      <a href="#projects" class="btn">Explore My Work</a>
    </div>
  </header>

  <!-- About Section -->
  <section id="about">
    <h2>About Me</h2>
    <p>I’m a passionate web developer who loves creating websites inspired by travel and adventure ✈️.</p>
  </section>

  <!-- Projects (Travel Destinations style) -->
  <section id="projects">
    <h2>My Projects</h2>
    <div class="project-cards">
      <div class="card">
        <img src="images/travel-site.png" alt="Travel Website">
        <h3>🌴 Travel Website</h3>
        <p>A modern website showcasing beautiful destinations using HTML, CSS, JS.</p>
      </div>
      <div class="card">
        <img src="images/todo.png" alt="To-Do List">
        <h3>📝 To-Do List</h3>
        <p>An advanced To-Do List app with animations and local storage.</p>
      </div>
    </div>
  </section>

  <!-- Skills -->
  <section id="skills">
    <h2>Skills</h2>
    <ul>
      <li>HTML5 & CSS3</li>
      <li>JavaScript (ES6+)</li>
      <li>React.js</li>
      <li>GitHub & Deployment</li>
    </ul>
  </section>

  <!-- Contact -->
  <section id="contact">
    <h2>Contact Me</h2>
    <p>📧 Email: yourname@email.com</p>
    <p>🔗 GitHub: <a href="https://github.com/your-username">your-username</a></p>
  </section>

  <footer>
    <p>© 2025 Sammy | Travel Portfolio</p>
  </footer>
  
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  color: #333;
}

.hero {
  background: url('images/hero-bg.jpg') no-repeat center center/cover;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: white;
}

.hero-text h1 {
  font-size: 3rem;
}

.btn {
  background: #ff6347;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 25px;
}

section {
  padding: 50px;
  text-align: center;
}

.project-cards {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.card {
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  width: 250px;
}

footer {
  background: #222;
  color: white;
  text-align: center;
  padding: 20px;
}
  
</style>
</body>
</html>


