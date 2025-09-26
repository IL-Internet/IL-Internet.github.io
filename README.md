### [*IL-Internet repositories viewer*](https://il-internet.github.io/)
>
> Below is the HTML code of my personal repositories viewer.
> 
> It is automatically updated without the need for manual updating.
>
> **Made with AI `Model: DeepSeek-R1`**.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>IL-Internet | GitHub Projects</title>
    <link
      href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500&family=Inter:wght@400;600&display=swap"
      rel="stylesheet"
    />
    <link rel="icon" href="icon.svg" type="image/svg+xml" />
    <style>
      :root {
        --bg: #111;
        --card-bg: #1b1b1b;
        --text: #eee;
        --accent: #0ff;
        --light-gray: #aaa;
      }

      body {
        margin: 0;
        padding: 0;
        font-family: "Inter", sans-serif;
        background-color: var(--bg);
        color: var(--text);
      }

      header {
        text-align: center;
        padding: 4rem 1rem 2rem;
        background: linear-gradient(135deg, #0ff2, #000);
        animation: pulseBG 10s ease-in-out infinite;
      }

      @keyframes pulseBG {
        0% {
          background-position: 0% 50%;
        }

        50% {
          background-position: 100% 50%;
        }

        100% {
          background-position: 0% 50%;
        }
      }

      header h1 {
        font-family: "Orbitron", sans-serif;
        font-size: 3rem;
        color: var(--accent);
        margin: 0;
      }

      header p {
        font-style: italic;
        color: var(--light-gray);
        margin-top: 0.5rem;
        font-size: 1.1rem;
      }

      .grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
        gap: 2rem;
        padding: 2rem;
        max-width: 1200px;
        margin: 0 auto;
      }

      .card {
        background: var(--card-bg);
        border-radius: 12px;
        padding: 1.5rem;
        box-shadow: 0 4px 20px rgba(0, 255, 255, 0.1);
        transition: transform 0.3s ease, box-shadow 0.3s ease;
        border: 1px solid #0ff3;
      }

      .card:hover {
        transform: translateY(-5px);
        box-shadow: 0 8px 25px rgba(0, 255, 255, 0.25);
      }

      .card a {
        font-size: 1.3rem;
        color: var(--accent);
        font-weight: 600;
        text-decoration: none;
        display: inline-block;
        margin-bottom: 0.5rem;
      }

      .card a:hover {
        text-decoration: underline;
      }

      .card p {
        font-size: 0.95rem;
        color: var(--light-gray);
        line-height: 1.5;
      }

      footer {
        text-align: center;
        padding: 2rem;
        font-size: 0.9rem;
        color: #666;
        background-color: #1a1a1a;
        border-top: 1px solid #0ff3;
      }

      footer a {
        color: var(--accent);
        text-decoration: none;
        font-weight: 600;
      }

      footer a:hover {
        text-decoration: underline;
      }

      .loading {
        text-align: center;
        padding: 2rem;
        color: var(--accent);
        font-style: italic;
      }
    </style>
  </head>

  <body>
    <header>
      <h1>IL-Internet</h1>
      <p>Explore my deployed GitHub projects</p>
    </header>

    <main class="grid">
      <div class="loading">Loading projects...</div>
      <!-- Cards will be inserted here by JavaScript -->
    </main>

    <footer>
      &copy; 2025 IL-Internet —
      <a href="https://github.com/il-internet" target="_blank"
        >GitHub Profile</a
      >
    </footer>

    <script>
      // Fetch GitHub repos and generate cards
      document.addEventListener("DOMContentLoaded", async () => {
        const grid = document.querySelector(".grid");
        const username = "IL-Internet"; // Your GitHub username

        try {
          const response = await fetch(
            `https://api.github.com/users/${username}/repos`
          );
          const repos = await response.json();

          // Clear loading message
          grid.innerHTML = "";

          // Filter and display repos
          repos.forEach((repo) => {
            // Skip forks and empty repos
            if (repo.fork || repo.size === 0) return;

            const card = document.createElement("div");
            card.className = "card";

            // Check if GitHub Pages is enabled (has a gh-pages branch or /docs)
            const ghPagesUrl = `https://${username}.github.io/${repo.name}`;

            card.innerHTML = `
            <a href="${repo.homepage || ghPagesUrl}" target="_blank">${
              repo.name
            }</a>
            <p>${repo.description || "No description available."}</p>
            <small>${repo.language || "Code"} • ${new Date(
              repo.updated_at
            ).toLocaleDateString()}</small>
          `;

            grid.appendChild(card);
          });

          // Fallback if no repos found
          if (grid.children.length === 0) {
            grid.innerHTML =
              '<div class="card"><p>No projects found. Check back later!</p></div>';
          }
        } catch (error) {
          grid.innerHTML =
            '<div class="card"><p>Failed to load projects. <a href="https://github.com/IL-Internet?tab=repositories" target="_blank">View on GitHub</a></p></div>';
          console.error("Error fetching repos:", error);
        }
      });
    </script>
  </body>
</html>
```
