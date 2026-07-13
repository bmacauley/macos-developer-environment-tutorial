# 05 · The Developer Toolkit

You have a workbench (the Mac), a practice lab (the VM), and command-line fluency. Now we add the tools you actually *build software* with: a proper code editor, git used well, and two programming runtimes — Python and Node.js — along with the package managers that come with them.

You can do this lesson on your **Mac**, in your **VM**, or both. Doing it in the VM first (where mistakes are free) and then on the Mac is a great way to practice.

**What you'll learn:** VS Code, git branches and GitHub done properly, Python + pip, Node + npm, and virtual environments.

---

## A real code editor: VS Code

You installed VS Code in Lesson 01 (`brew install --cask visual-studio-code`). It's a free editor that understands code — coloring it, catching mistakes, and running it. Open your course folder in it:

```bash
cd ~/projects/tools-course     # or wherever you cloned it
code .                          # open the current folder in VS Code
```

> If `code` isn't found, open VS Code manually, press <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>, type "Shell Command: Install 'code' command in PATH", and hit Enter. Now `code .` works.

Three features to try immediately:

- The **built-in terminal** (<kbd>Ctrl</kbd>+<kbd>`</kbd>) — editor and terminal in one window.
- The **Explorer** sidebar — your files as a clickable tree.
- **Extensions** (the blocks icon) — install "Python" and "GitLens" to start.

## Git, level 2: branches

In Lesson 00 you learned the core loop: `add`, `commit`, `push`. Now the piece that makes git powerful for real work — **branches**.

A branch is a parallel copy of your project where you can try something without disturbing the main version. If it works, you **merge** it back in; if not, you throw the branch away.

```bash
git status                      # what's changed and what branch am I on?
git branch                      # list branches (main is the default)
git switch -c experiment        # create and switch to a new branch
# ...make some changes, then...
git add .
git commit -m "Try a new idea"
git switch main                 # go back to the safe main branch
git merge experiment            # bring the idea into main
git branch -d experiment        # delete the finished branch
```

Two more everyday commands:

```bash
git log --oneline               # a compact history of commits
git diff                        # exactly what lines changed since last commit
```

### Connecting to GitHub the right way (SSH keys)

Remember how `git push` awkwardly asked for a password in Lesson 00? The clean fix is an **SSH key** — a pair of files that proves it's you, so you never type a password again.

```bash
ssh-keygen -t ed25519 -C "your-github-email@example.com"
# press Enter to accept the default location; set a passphrase or leave blank
cat ~/.ssh/id_ed25519.pub       # this prints your PUBLIC key
```

Copy that public key. On GitHub: **Settings → SSH and GPG keys → New SSH key**, paste it, save. Test it:

```bash
ssh -T git@github.com           # should greet you by your username
```

Now clones and pushes using the `git@github.com:...` (SSH) address just work, no passwords. This is a genuine "graduation" moment — you're set up like a professional.

## Python

Python is a friendly, wildly popular language — great for automation, data, and AI. Ubuntu already has it; on the Mac, install a clean copy with Homebrew:

```bash
brew install python        # on the Mac
python3 --version          # check it (Linux and Mac both use python3)
```

Run Python interactively — a calculator that talks back:

```bash
python3
```
```python
>>> 2 + 2
4
>>> print("hello from python")
hello from python
>>> exit()
```

Now write a real (tiny) program. Make `hello.py`:

```python
name = input("What's your name? ")
print(f"Hello, {name}! You just ran a Python program.")
```

Run it:

```bash
python3 hello.py
```

### pip and virtual environments

**pip** installs Python libraries (other people's code you can use). But installing everything system-wide gets messy fast, so the standard practice is a **virtual environment** — a sandbox of libraries for *one* project:

```bash
python3 -m venv venv          # create a virtual environment named "venv"
source venv/bin/activate      # turn it on (your prompt shows "(venv)")
pip install requests          # installs ONLY inside this project
python3 -c "import requests; print(requests.get('https://api.github.com').status_code)"
deactivate                    # turn it off
```

The idea — isolate each project's dependencies — is one you'll meet again in every language. Always add `venv/` to your `.gitignore` (it's already in this course's).

## Node.js and npm

**Node.js** runs JavaScript outside the browser; **npm** is its package manager (the biggest software library in the world). Install on the Mac:

```bash
brew install node
node --version
npm --version
```

A one-line program:

```bash
node -e "console.log('hello from node')"
```

npm packages work like pip: `npm install <package>` adds a library to the current project, recording it in a `package.json` file. Fun demo — run a tool *without* installing it, using `npx`:

```bash
npx cowsay "I am a cow running from npm"
```

## Tying it together: a tiny script

Make a script that greets you, in a new file `greet.sh`:

```bash
#!/bin/bash
echo "Today is $(date)"
echo "You are $(whoami) on $(hostname)"
echo "Python says:"; python3 -c "print('  2 to the 10th is', 2**10)"
```

Make it executable and run it — this uses everything from Lesson 02's `chmod`:

```bash
chmod +x greet.sh
./greet.sh
```

You just wrote a shell script that calls Python. That's real tool-building.

---

## Challenge

1. Open the course folder in VS Code and edit a lesson using its built-in terminal to commit the change.
2. Set up an SSH key and add it to GitHub; confirm with `ssh -T git@github.com`.
3. Create a git branch, make a change, commit it, merge it back to `main`, and delete the branch.
4. Write and run the `hello.py` Python program, then set up a virtual environment and `pip install requests` inside it.
5. Run the `npx cowsay` demo, and write + run the `greet.sh` script.

Mark complete when your SSH key works and you've merged a branch. One tool category left — the newest and most powerful.

> **Glossary:** *VS Code* = code editor · *branch* = a parallel line of work · *merge* = combine a branch back in · *SSH key* = passwordless proof of identity · *pip / npm* = package managers for Python / Node · *virtual environment* = per-project library sandbox · *script* = a saved file of commands you can rerun.
