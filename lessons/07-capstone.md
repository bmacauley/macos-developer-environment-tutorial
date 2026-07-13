# 07 · Capstone & What's Next

Time to prove it to yourself. In this final lesson you'll combine every tool from the course into one real project — and publish it to the internet with your name on it. No new concepts here; just you, using what you now know.

**The mission:** build a small personal website, develop it inside your Linux VM, version it with git, and publish it live with GitHub Pages — the same way this very course is published.

---

## Why this project

It touches everything:

- **Terminal & files** (Lesson 02) to create and organise it.
- **The VM** (Lessons 03–04) as your safe development machine.
- **Git, GitHub, an editor, and maybe Python/Node** (Lessons 00, 05).
- **AI** (Lesson 06) as your on-call helper when you get stuck.

And at the end there's a real URL you can send to a friend.

## Step 1 — Set up the project

Work inside your **VM** (take a snapshot first — old habit, good habit). Make sure git and a text editor are available (`sudo apt install -y git`; on a server you'll edit right in the console with `nano`, which is already installed — or `vim` if you're feeling brave):

```bash
mkdir -p ~/projects/my-site
cd ~/projects/my-site
git init                     # start a fresh repo
```

## Step 2 — Build the site

Create an `index.html`. Start simple — you can make it fancier later:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Your Name</title>
  <style>
    body { font-family: system-ui, sans-serif; max-width: 640px; margin: 60px auto; padding: 0 20px; line-height: 1.6; }
    h1 { color: #2b6cff; }
  </style>
</head>
<body>
  <h1>Hi, I'm Your Name</h1>
  <p>I just finished a course on developer tools. Here's what I learned to do:</p>
  <ul>
    <li>Drive a computer from the command line</li>
    <li>Run my own Linux machine in a virtual machine</li>
    <li>Use git and GitHub like a developer</li>
    <li>Write and run Python and JavaScript</li>
  </ul>
  <p>This page is hosted for free on GitHub Pages.</p>
</body>
</html>
```

Preview it: your server has no browser, so serve the page and fetch it with `curl` to confirm it's really there:

```bash
python3 -m http.server 8000 &    # start a tiny web server in the background
curl http://localhost:8000       # print your page's HTML to the screen
kill %1                          # stop the background server
```

> The real *visual* preview comes at the end of this lesson: once it's live on GitHub Pages, you'll open the URL in your **Mac's** browser and see it rendered for real.

> **Optional flex:** add a second page, or use `npx` to pull in a tool, or write a small Python script that generates part of the page. Stretch as far as you're curious.

## Step 3 — Commit your work

The core loop from Lesson 00, now second nature:

```bash
git add .
git commit -m "My first personal website"
```

## Step 4 — Publish to GitHub

1. On [github.com](https://github.com), create a **new repository** called `my-site` (leave it empty — no README).
2. Connect your local repo to it and push, using the **SSH** address.

> **First push from the VM?** The SSH key you made in Lesson 05 lives on your **Mac** — this VM is a *different* machine, so GitHub doesn't recognise it yet. Set up a key here too (same steps as Lesson 05, but run inside the VM):
>
> ```bash
> ssh-keygen -t ed25519 -C "your-github-email@example.com"   # press Enter through every prompt
> cat ~/.ssh/id_ed25519.pub                                   # copy the whole line it prints
> ```
>
> Add it on GitHub under **Settings → SSH and GPG keys → New SSH key**, paste, and save. Confirm with `ssh -T git@github.com` (it should greet you by name). Now the push below will work.

```bash
git branch -M main
git remote add origin git@github.com:YOURNAME/my-site.git
git push -u origin main
```

## Step 5 — Turn on GitHub Pages

1. On your repo's GitHub page: **Settings → Pages**.
2. Under **Source**, choose **Deploy from a branch**, pick **main** and the **/ (root)** folder, and **Save**.
3. Wait a minute or two, refresh, and GitHub shows your live URL: `https://YOURNAME.github.io/my-site/`.

Open it. That's *your* website, on the real internet, built and shipped entirely with the tools you learned. Send the link to someone.

---

## Final Challenge

Complete the mission end to end: a personal `index.html`, developed in your VM, committed with git, pushed to GitHub, and live on GitHub Pages at your own URL. When the link works in a browser, you've earned the last checkmark.

---

## Where to go next

You now have the foundation. Pick whatever pulls you:

- **Go deeper on a language.** Build something small and real in Python (a script that automates a chore) or JavaScript (an interactive web page). Projects teach more than tutorials.
- **Learn more git.** Try contributing to an open-source project — even fixing a typo in someone's docs teaches the "pull request" workflow real teams use.
- **Explore the cloud.** The SSH skills from Lesson 04 transfer directly to renting a real Linux server. Many providers have free tiers for learning.
- **Automate your setup.** Write a script that installs all your favourite Homebrew tools at once — your own "new Mac in one command."
- **Build with AI.** Now that you understand the tools, use agentic AI to move faster on bigger projects — always following the golden rule from Lesson 06.
- **Improve this course.** It's your repo now. Add a lesson, fix something, restyle the site. Teaching (even your future self) is the best way to lock in what you know.

## A last word

Every professional engineer started exactly where you are: typing commands they didn't fully understand into a black window, breaking things, and rebuilding them. The difference between someone who "can use computers" and someone who *builds* with them isn't talent — it's exactly the hours you just put in. You have the workbench, the lab, and the toolkit. Go make things.

> **Glossary:** *`python3 -m http.server`* = a quick local web server · *remote* = the GitHub copy your local repo pushes to · *GitHub Pages* = free website hosting from a repo · *pull request* = proposing your changes to someone else's project.
