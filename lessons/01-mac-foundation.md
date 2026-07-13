# 01 · The Mac Foundation

Before you can build things, you need a well-set-up workbench. This lesson turns a normal Mac into a developer's Mac. It's mostly one-time setup, and you'll use everything you install here for years.

**What you'll learn:** the Terminal and your shell, Apple's developer tools, Homebrew (the app store for command-line tools), and how to keep it all tidy.

---

## The Terminal and the shell

The **Terminal** is an app — a window. The **shell** is the program running *inside* that window that reads your commands. On modern Macs the default shell is called **zsh**.

Open Terminal (<kbd>Cmd</kbd>+<kbd>Space</kbd> → "Terminal"). You'll see a **prompt** ending in `%`. That's the shell waiting for you. Try:

```bash
whoami      # prints your username
date        # prints the current date and time
echo "hi"   # prints whatever you give it
```

`echo` just repeats text back. Boring alone, but it's how you'll inspect things later.

> **Tip:** the terminal has memory. Press the <kbd>↑</kbd> arrow to bring back the last command instead of retyping it. Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to cancel a command that's stuck or running too long. These two shortcuts alone will save you hours.

## Apple's Command Line Tools

Apple ships a bundle of essential developer tools (including git and a C compiler) that isn't installed by default. Trigger the installer:

```bash
xcode-select --install
```

A dialog appears — click **Install** and wait. If it says the tools are "already installed," you're set.

## Homebrew — the missing package manager

Here's the big one. A **package manager** installs, updates, and removes software with a single command, and handles all the fiddly dependencies for you. On Linux this is built in; on macOS the community made one called **Homebrew**, and essentially every developer uses it.

Install it by pasting the command from [brew.sh](https://brew.sh) into your terminal (always get it from the official site, never a random blog):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

It'll ask for your Mac password (typing shows nothing — that's normal, just type and press <kbd>Enter</kbd>) and take a few minutes.

> **Apple Silicon note:** at the end, Homebrew prints two lines starting with `echo` and `eval` telling you to add it to your PATH. **Run those two lines.** They make the `brew` command findable in future terminal sessions. If you skip this, `brew` will seem to "not exist" in a new window.

Check it worked:

```bash
brew --version
```

### Using Homebrew

The pattern is simple and worth memorizing:

```bash
brew install <name>     # install a tool
brew uninstall <name>   # remove it
brew upgrade            # update everything
brew list               # what do I have installed?
brew search <name>      # is there a package for this?
```

Let's install three genuinely useful tools right now:

```bash
brew install git wget tree
```

- **git** — a newer version than Apple's, kept up to date by brew.
- **wget** — downloads files from the internet by URL.
- **tree** — draws a folder as a little diagram (you'll like this in Lesson 02).

Try it:

```bash
tree ~/Desktop
```

## Casks: installing real apps from the terminal

Homebrew can also install normal Mac apps (the kind with windows and icons). Those are called **casks**:

```bash
brew install --cask visual-studio-code   # the code editor we'll use in Lesson 05
brew install --cask utm                  # the virtual machine app for Lesson 03
```

Installing apps by typing their names — instead of hunting for download buttons — is a small superpower. And because it's just text, you could put all your installs in one file and set up a brand-new Mac in minutes. (That's a real thing engineers do; it's called a "dotfiles" or "setup script.")

## Keeping things tidy

A couple of habits that pay off:

- **Make a home for your projects.** Create one folder and keep all your code in it:

  ```bash
  mkdir -p ~/projects
  ```

  From now on, projects live in `~/projects`.

- **Update occasionally.** Once a week or so:

  ```bash
  brew update && brew upgrade
  ```

  `&&` means "if the first command succeeds, run the second too."

---

## Challenge

1. Install the Apple Command Line Tools and Homebrew.
2. Use Homebrew to install `git`, `wget`, and `tree`, then run `tree ~/Desktop` and read the diagram it draws.
3. Install VS Code and UTM as casks (you'll need both later).
4. Create your `~/projects` folder.

Then mark this lesson complete. Your workbench is ready — next we learn to actually *use* the terminal.

> **Glossary:** *shell / zsh* = the program that reads your commands · *prompt* = the `%` where you type · *package manager* = installs software by name · *Homebrew (`brew`)* = the Mac package manager · *cask* = a windowed app installed via brew · *PATH* = the list of places the shell looks to find commands.
