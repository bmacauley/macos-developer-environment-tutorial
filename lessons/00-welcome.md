# 00 · Welcome & Your First Repo

Welcome. By the end of this course you'll have your own developer setup on your Mac, a private Linux computer that lives *inside* your Mac to break and rebuild as much as you like, and a real feel for the tools that professional engineers use every day.

This isn't a "watch and nod" course. Every lesson ends with a **Challenge** — you're not done until you've actually done it. The little circle next to each lesson in the sidebar fills in when you click *Mark this lesson complete*, so you can always see how far you've come.

## How this course is built (and why that matters)

The website you're reading right now is itself a lesson. It's just a folder of text files published on the internet for free using **GitHub Pages**. Once you finish this lesson, *you* will own that folder, and you'll be able to edit these lessons, add your own notes, and re-publish — all with the same tools engineers use to ship real software.

That's the whole philosophy here: **the best way to learn a tool is to use it for something real.**

## The mindset: what is a "tool," really?

A tool is anything that turns a slow, manual, error-prone job into a fast, repeatable one. A hammer does it for nails. In computing:

- The **terminal** turns "click through 40 folders" into one line you can save and reuse.
- **Git** turns "final_v2_REALfinal.zip" into a clean history you can rewind.
- A **virtual machine** turns "I'm scared to break my computer" into "let me try the dangerous thing on a copy."
- **AI tools** turn "I don't know where to start" into a conversation.

You already use tools. This course is about using *better* ones, and understanding them well enough that you're the one in control — not the tool.

## What you'll need

- A Mac (Apple Silicon — M1/M2/M3/M4/M5 — is ideal; an Intel Mac works too with small tweaks noted along the way).
- About 30 GB of free disk space by the time you reach the VM lesson.
- A **GitHub account** — free. We'll make one below.
- Curiosity and a willingness to type things you don't fully understand yet. That feeling is normal and goes away.

---

## Your first tool: Git & GitHub

**Git** is a "time machine" for files. It records snapshots of your work so you can see what changed, go back, and combine work from different people. **GitHub** is a website that stores git projects online so you can back them up and share them.

Every project lives in a **repository** ("repo") — just a folder that git is watching.

### Step 1 — Make a GitHub account

Go to [github.com](https://github.com) and sign up. Pick a username you wouldn't be embarrassed to put on a résumé one day (this becomes a public profile). Verify your email.

### Step 2 — Check whether git is already installed

Open the **Terminal** app (press <kbd>Cmd</kbd>+<kbd>Space</kbd>, type "Terminal", hit <kbd>Enter</kbd>) and type:

```bash
git --version
```

If you see a version number, great. If macOS pops up a box offering to install "command line developer tools," click **Install** and wait a few minutes. We'll cover this properly in Lesson 01.

### Step 3 — Tell git who you are

Git stamps your name on every snapshot. Set it once:

```bash
git config --global user.name "Your Name"
git config --global user.email "the-email-you-used-on-github@example.com"
```

### Step 4 — Get this course onto your computer

Whoever set up this course will give you a link to it on GitHub (it looks like `https://github.com/username/tools-course`). In the terminal, run:

```bash
cd ~/Desktop
git clone https://github.com/USERNAME/tools-course.git
cd tools-course
```

- `cd ~/Desktop` means "change directory to the Desktop" (`~` is shorthand for your home folder).
- `git clone` downloads the whole repo.
- The last `cd` steps into the folder you just downloaded.

> **Not published yet?** If you're reading this from a folder someone handed you, that's fine — skip to the Challenge and come back to the git steps once the repo is online. The README file in this folder has the publishing instructions.

### Step 5 — Make your first change

Open the folder in a text editor (even TextEdit works for now; we'll install a real one in Lesson 05). Find `lessons/00-welcome.md` and add a line at the very bottom, like:

```
Started this course on: <today's date>
```

Save it. Back in the terminal, run these three commands — the **core git loop** you'll repeat thousands of times:

```bash
git add lessons/00-welcome.md      # stage the change ("I mean to keep this")
git commit -m "Add my start date"  # save a snapshot with a message
git push                           # upload it to GitHub
```

Refresh your repo page on GitHub — your change is there, online, forever. You just used version control like a professional.

> If `git push` asks for a password and rejects your GitHub password, that's expected — GitHub needs a **token** or **SSH key** instead. Don't worry about it yet; Lesson 05 sets this up properly. For now, cloning and committing locally is enough.

---

## Challenge

1. Create a GitHub account and set your `user.name` and `user.email` in git.
2. Get the course folder onto your computer (clone it, or open the folder you were given).
3. Add your start date to the bottom of this lesson file and commit the change with a clear message.

When those three are done, click **Mark this lesson complete** and move on to Lesson 01.

> **Glossary so far:** *repo* = a folder git watches · *clone* = download a repo · *commit* = a saved snapshot · *push* = upload commits to GitHub · *terminal* = the text window where you type commands.
