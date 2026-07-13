# The Toolsmith's Course

A hands-on, self-guided course that teaches a teenager the core tools of software development — the macOS setup, the command line, a Linux virtual machine, the developer toolkit (git, Python, Node), and modern AI tools — by actually using them to build and publish real things.

It's designed for a 16-year-old with some computer exposure, and it's built so that **the course website is itself one of the lessons**: it's published for free with GitHub Pages, and editing/re-publishing it is part of the learning.

## What's inside

| Lesson | Topic |
|--------|-------|
| 00 | Welcome & Your First Repo (git + GitHub basics) |
| 01 | The Mac Foundation (Terminal, Command Line Tools, Homebrew) |
| 02 | Command-Line Basics (navigation, files, pipes, permissions) |
| 03 | Build Your Lab — the VM (UTM + Ubuntu, snapshots) |
| 04 | Running a Linux Machine (sudo, apt, users, services, SSH) |
| 05 | The Developer Toolkit (VS Code, git branches, Python, Node) |
| 06 | AI & Claude Tools (prompting, agentic tools, MCP) |
| 07 | Capstone & What's Next (build + publish a personal site) |

Each lesson ends with a **Challenge** and a "Mark complete" button; progress is saved in the browser.

## How to read it locally

The site is plain HTML + Markdown, no build step. From this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in a browser. (Opening `index.html` directly by double-clicking won't work, because the page fetches the lesson files — you need a small local server, which the command above provides.)

## How to publish it with GitHub Pages

This is the exact workflow the course teaches, so it's a nice one to do together.

1. **Create a repo on GitHub.** Go to [github.com](https://github.com), click **New repository**, name it (e.g. `tools-course`), leave it empty (no README), and create it.

2. **Push this folder to it.** In a terminal, from inside this folder:

   ```bash
   git init
   git add .
   git commit -m "Initial course"
   git branch -M main
   git remote add origin git@github.com:YOURNAME/tools-course.git   # or the https:// address
   git push -u origin main
   ```

3. **Turn on Pages.** On the repo's GitHub page: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / folder: `/ (root)` → Save.**

4. **Wait ~1–2 minutes**, refresh, and GitHub shows the live URL:
   `https://YOURNAME.github.io/tools-course/`

5. **Give your son that URL** plus the repo address (so Lesson 00's `git clone` step works for him).

That's it — the course is live and free to host.

## Editing the course

- Lesson text lives in `lessons/*.md` — plain Markdown, edit in any editor.
- To add, remove, or reorder lessons, edit `lessons.json` (the sidebar reads from it).
- Styling and behavior are all in `index.html` (inline CSS + a little JavaScript).
- The `.nojekyll` file tells GitHub Pages to serve the files as-is.

After any change: `git add . && git commit -m "..." && git push`, and Pages updates automatically.

## Notes on accuracy

Version-specific steps (Ubuntu **26.04 LTS**, UTM **4.7.5+**) were current as of July 2026. For anything about AI/Claude products, the course deliberately points to [docs.claude.com](https://docs.claude.com) rather than hard-coding details that change.
