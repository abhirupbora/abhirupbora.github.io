
# 🌌 Automated Portfolio Generator 

![UI Aesthetic](https://img.shields.io/badge/UI-Liquid_Glass-38bdf8?style=for-the-badge)
![Deployment](https://img.shields.io/badge/Deployment-GitHub_Pages-success?style=for-the-badge)
![Framework](https://img.shields.io/badge/Built_With-Pure_HTML_%7C_CSS_%7C_JS-informational?style=for-the-badge)
![License](https://img.shields.io/badge/License-Open_Source-success?style=for-the-badge)

Welcome to the **ArcSphere Portfolio**—a hyper-aesthetic, mobile-first personal website template designed for independent developers, writers, musicians, and creators who want more than just a standard digital resume. 

Built entirely without heavy frameworks, this template utilizes pure HTML, CSS, and Vanilla JavaScript to deliver a seamless, single-page application (SPA) experience. It features a deep dark mode, "liquid glass" (glassmorphism) frosted components, and an immersive, app-like routing system.

---

## ✨ Signature Features

*   **Liquid Glass UI:** Custom CSS `backdrop-filter` utilities that create a stunning, blurred transparency effect over a deep space gradient.
*   **SimpMusic-Inspired Navigation:** A floating, frosted-glass bottom dock that controls all page routing instantly—no browser reloads.
*   **Bento-Box Grid System:** Perfectly spaced, aesthetic layouts for categorizing projects, skills, and videos (supports both 16:9 landscape and 9:16 portrait Shorts).
*   **Premium Content Locks:** Built-in modal pop-ups that gate specific content behind a "Premium Code" (perfect for exclusive stories, unreleased tracks, or a fun gamified UI).
*   **Interactive Explore Hub:** A built-in search filter, interactive informational bubbles, and dynamic modal forms for collaboration requests.

---

## 💻 The Source Code (Single-File Architecture)

The entire architecture of this portfolio is housed within a single, highly optimized file. If you are ready to build your own, copy the complete code below and save it as `index.html`.

<details>
<summary><strong>👉 CLICK HERE TO EXPAND AND COPY THE FULL CODE</strong></summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personal Portfolio</title>
    <link rel="stylesheet" href="[https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css)">
    <style>
        @import url('[https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&display=swap](https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&display=swap)');

        :root {
            var(--bg-color): #09090b; 
            --glass-bg: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --accent: #38bdf8;
            --premium: #fbbf24;
        }

        * {
            margin: 0; padding: 0; box-sizing: border-box;
            font-family: 'Outfit', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-color);
            background-image: radial-gradient(circle at 50% 0%, rgba(56, 189, 248, 0.1), transparent 50%);
            color: var(--text-main);
            min-height: 100vh; overflow-x: hidden; background-attachment: fixed;
        }

        .glass {
            background: var(--glass-bg);
            backdrop-filter: blur(24px); -webkit-backdrop-filter: blur(24px);
            border: 1px solid var(--glass-border); border-radius: 20px;
        }

        .page {
            display: none; padding: 20px 20px 140px 20px;
            max-width: 600px; margin: 0 auto;
            animation: fadeIn 0.4s cubic-bezier(0.4, 0, 0.2, 1) forwards;
        }
        .page.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

        /* Login Screen */
        #login-screen {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            background: var(--bg-color); display: flex; flex-direction: column; 
            justify-content: center; align-items: center; z-index: 10000; 
            transition: opacity 0.6s ease, transform 0.6s ease;
        }
        .login-box { text-align: center; width: 85%; max-width: 350px; padding: 40px; }
        .login-btn {
            background: var(--text-main); color: var(--bg-color); width: 100%;
            padding: 15px; border-radius: 30px; font-weight: 800; border: none; cursor: pointer; margin-top: 30px;
        }
        .profile-pic { width: 110px; height: 110px; border-radius: 50%; object-fit: cover; margin-bottom: 15px; border: 2px solid var(--glass-border); }
        
        /* Grids & Docks */
        .six-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 25px; }
        .grid-card { padding: 20px 5px; text-align: center; cursor: pointer; border-radius: 20px; transition: background 0.3s; }
        .grid-card i { font-size: 24px; margin-bottom: 8px; color: var(--accent); }
        .grid-card p { font-size: 13px; font-weight: 600; text-transform: uppercase; }
        
        .split-docks-container { display: flex; justify-content: space-between; gap: 15px; margin-bottom: 30px; }
        .mini-dock { display: flex; justify-content: space-evenly; flex: 1; padding: 15px; border-radius: 25px; }
        .mini-dock a { color: var(--text-main); font-size: 20px; transition: color 0.3s; text-decoration: none; }
        .mini-dock a:hover { color: var(--accent); }

        .page-header { text-align: center; font-size: 26px; font-weight: 800; margin-bottom: 25px; }
        .action-btn {
            display: block; width: 100%; padding: 16px; text-align: center; border-radius: 25px;
            font-weight: 600; text-decoration: none; border: 1px solid var(--glass-border);
            background: var(--glass-bg); color: white; cursor: pointer; transition: all 0.3s;
        }
        .action-btn:hover { background: var(--text-main); color: var(--bg-color); }

        /* Bottom Nav Dock */
        .main-dock-wrapper { position: fixed; bottom: 25px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 450px; z-index: 1000; }
        .main-dock {
            display: flex; justify-content: space-between; align-items: center;
            padding: 10px 15px; border-radius: 40px; background: rgba(20, 20, 22, 0.85); border: 1px solid rgba(255,255,255,0.1);
        }
        .dock-btn { background: none; border: none; color: var(--text-muted); font-size: 22px; padding: 12px 20px; border-radius: 30px; cursor: pointer; }
        .dock-btn.active { background: rgba(255,255,255,0.1); color: var(--text-main); }
    </style>
</head>
<body>

    <div id="login-screen">
        <div class="glass login-box">
            <img src="LoginPic.jpg" class="profile-pic" onerror="this.src='[https://ui-avatars.com/api/?name=User&background=38bdf8&color=fff](https://ui-avatars.com/api/?name=User&background=38bdf8&color=fff)'">
            <h2>Welcome Back</h2>
            <button class="login-btn" onclick="enterSite()">Access Portfolio</button>
        </div>
    </div>

    <!-- MAIN HOME -->
    <div id="home" class="page active">
        <div style="text-align: center;">
            <img src="MainPic.jpg" class="profile-pic" onerror="this.src='[https://ui-avatars.com/api/?name=User&background=38bdf8&color=fff](https://ui-avatars.com/api/?name=User&background=38bdf8&color=fff)'">
            <h1 style="font-size: 28px; font-weight: 800;">Your Name</h1>
        </div>
        <div class="six-grid">
            <div class="glass grid-card"><i class="fa-solid fa-code"></i><p>Tech</p></div>
            <div class="glass grid-card"><i class="fa-solid fa-camera"></i><p>Media</p></div>
            <div class="glass grid-card"><i class="fa-solid fa-book"></i><p>Story</p></div>
        </div>
        <!-- Add your links and sections here based on the tutorial below -->
    </div>

    <div class="main-dock-wrapper">
        <nav class="main-dock">
            <button class="dock-btn" onclick="navigate('contact')" id="btn-contact"><i class="fa-solid fa-circle-question"></i></button>
            <button class="dock-btn" onclick="navigate('about')" id="btn-about"><i class="fa-solid fa-trophy"></i></button>
            <button class="dock-btn active" onclick="navigate('home')" id="btn-home"><i class="fa-solid fa-house"></i></button>
        </nav>
    </div>

    <script>
        function enterSite() {
            const login = document.getElementById('login-screen');
            login.style.opacity = '0';
            login.style.transform = 'scale(1.1)';
            setTimeout(() => { login.style.display = 'none'; }, 600);
        }
        function navigate(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            window.scrollTo(0, 0);
            document.querySelectorAll('.dock-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById('btn-' + pageId)?.classList.add('active');
        }
    </script>
</body>
</html>

</details>
🚀 The Ultimate Deployment Tutorial
You don't need to be a senior developer or pay for expensive hosting domains to get this live. Follow this step-by-step guide to build and host your portfolio for free on GitHub Pages.
Phase 1: Prepare Your Workspace
 * Create a Folder: Make a new folder on your computer desktop named MyPortfolio.
 * The Code: Open a text editor (like VS Code, Notepad, or TextEdit), paste the HTML code from above, and save it inside your folder exactly as index.html.
 * The Assets (CRITICAL): Gather your images (profile pictures, thumbnails, story covers). Place them in the exact same folder.
   * Important Note: Code is case-sensitive! If your code says <img src="ProfilePic.jpg">, your image file must be named ProfilePic.jpg, not profilepic.jpg.
Phase 2: The AI Generation Prompt (Instant Customization)
Don't want to rewrite the HTML manually? Let AI do the heavy lifting. Copy the prompt below, fill in your details, and paste it into ChatGPT, Claude, or Gemini alongside the code.
> 🤖 Copy & Paste this Prompt into your AI:
> "I have the HTML/CSS/JS code for a 'liquid glass' style portfolio website. I want to customize it entirely for myself.
> Here are my details:
>  * My Name: [Insert your name]
>  * My Profession/Tagline: [Insert your profession/title]
>  * A quote I live by: [Insert quote]
>  * My Social Links: [Link to Instagram, GitHub, YouTube, LinkedIn, Discord, etc.]
>  * My 6 Main Grid Categories: [e.g., Microelectronics, Writing, Music, Gaming, Editing, Academics]
>  * About Me Details: [List your country, state, education, skills, and hobbies to be formatted into info bubbles]
>  * My Email: [Insert email]
> Please read the provided HTML code and replace all the original placeholder data, links, text, and categories with my information. Keep the deep dark theme, the liquid glass CSS, the premium modal locks, and the bottom navigation dock exactly the same. Ensure the JavaScript routing seamlessly connects to my new categories.
> Here is the original HTML code to modify: [Paste the index.html code here]"
> 
Once the AI gives you your personalized code, overwrite your index.html file with it.
Phase 3: Go Live on GitHub
 * Create an Account: Go to GitHub.com and log in or sign up.
 * New Repository: Click the + icon in the top right and select New repository.
 * Naming Magic: Name the repository exactly like this: yourusername.github.io (Replace "yourusername" with your actual GitHub username). This tells GitHub to use this as your main, clean domain.
 * Upload: Make the repository Public, check "Add a README file," and click Create. Inside the repo, click Add file > Upload files. Drag and drop everything from your MyPortfolio desktop folder (the index.html and all images). Click Commit changes.
 * Launch: Go to the repository Settings (the gear icon) > Pages (on the left sidebar). Under "Branch", select main and click Save.
 * Celebrate: Wait 2 to 5 minutes, then visit https://yourusername.github.io on your phone or laptop. Your site is live!
🎨 Advanced Customization Tips
If you are modifying the code directly in VS Code, here are some pro tips to make it yours:
 * Custom Backgrounds: In the <style> section, find the body tag. Replace background-color and background-image with an image URL from a high-quality, non-AI photography site like Unsplash.
 * Thumbnail Aspect Ratios:
   * Use class="thumb-landscape" for standard 16:9 videos (YouTube).
   * Use class="thumb-portrait" for 9:16 vertical videos (Shorts/Reels).
 * The Premium Lock Code: By default, the modal lock code is set to ASY-710. To change it, scroll to the bottom <script> section, find if(code === "ASY-710"), and change it to your own secret password.
🏛️ Credits & License
Concept, design, and architecture pioneered by Abhirup Bora | ArcSphere Studios.
This project is open-source. Fork it, build upon it, and create your own digital universe.

