# 03 · Build Your Lab (the VM)

Now for the fun part. You're going to create a **virtual machine** — a complete, separate computer that runs *inside* your Mac in its own window. It has its own operating system (Linux), its own files, and its own settings. And here's the magic: **you can't break your real Mac by messing with it.** Delete the wrong thing, install something weird, wipe the whole system — worst case, you throw the VM away and make a new one in ten minutes.

This is your practice lab for the rest of the course.

**What you'll learn:** what a VM is, how to install UTM and Ubuntu Linux, and how to take snapshots so you can rewind mistakes.

---

## What's a virtual machine, really?

Your Mac's hardware (processor, memory, disk) is powerful enough to *pretend* to be a second computer. Software called a **hypervisor** carves off a slice of those resources and runs another operating system on it, fooling that OS into thinking it has its own real hardware. The result — the pretend computer — is a **virtual machine (VM)**. The real computer is the **host**; the VM is the **guest**.

Why professionals use VMs constantly:

- **Safety** — experiment freely; the guest is isolated from the host.
- **Linux on a Mac** — the servers that run the internet almost all run Linux. A VM lets you learn Linux without a second computer.
- **Snapshots** — freeze the VM's exact state, then restore it later like a save point in a game.
- **Disposability** — a broken VM is deleted and replaced, not repaired.

We'll run **Ubuntu**, the most popular beginner-friendly flavor of Linux, using **UTM**, a free VM app for Mac. (You installed UTM in Lesson 01 with `brew install --cask utm`. If you skipped it, run that now, or get it from [mac.getutm.app](https://mac.getutm.app).)

## Step 1 — Download the Ubuntu disk image

An operating system is installed from an **ISO file** — a single file that represents an installation disk.

1. Go to [ubuntu.com/download](https://ubuntu.com/download).
2. On an **Apple Silicon** Mac (M1–M5), you need the **ARM64 / "for ARM"** build of **Ubuntu Server 26.04 LTS**. On an **Intel** Mac, get the regular 64-bit (AMD64) server image.
3. It's a smaller download than the desktop edition (around 2–3 GB) — start it, then read the rest of this lesson while it finishes.

> **Why Server, not Desktop?** Ubuntu Server has **no graphical desktop** — no windows, no mouse, just a text prompt. That's exactly how the real machines running the internet work, and it's the whole point of this course: getting comfortable driving a computer entirely by typing. It's also far lighter, so the VM is faster and uses less disk. Everything you'll do lives at the command line.

> "LTS" means **Long-Term Support** — the stable version that gets 5 years of updates. Always pick LTS for learning; you want boring and reliable, not bleeding-edge.

## Step 2 — Create the VM in UTM

1. Open **UTM** and click the **+** to create a new VM, then choose **Virtualize** (not Emulate — virtualizing is much faster and correct for a matching ARM/Intel guest).
2. Choose **Linux**.
3. On an Apple Silicon Mac, tick **Use Apple Virtualization** if offered — it's smoother on modern macOS.
4. **Boot ISO image** → Browse → select the Ubuntu `.iso` you downloaded.
5. **Memory:** give it **2048 MB** (2 GB). A server has no desktop to run, so it needs far less than a graphical Ubuntu — 4 GB is generous if you have RAM to spare.
6. **CPU cores:** the default is fine (2 is plenty for a server).
7. **Storage:** **20 GB**. This is a *maximum* size that grows as needed, so it won't immediately eat your disk.
8. Give it a name like `ubuntu-lab` and click **Save**.

## Step 3 — Install Ubuntu inside the VM

Select your new VM and press the big **▶ Play** button. A window opens and boots the Ubuntu Server installer. It's **text-only** — you navigate with the **arrow keys**, <kbd>Tab</kbd>, and <kbd>Enter</kbd>, not the mouse. Work through the screens:

1. Pick your language and keyboard.
2. Choose **Ubuntu Server** (the normal one, not "minimized").
3. **Network:** leave it as-is — it picks up an address automatically.
4. **Proxy / mirror:** skip both (just press <kbd>Enter</kbd> to accept the defaults).
5. **Storage:** accept **use an entire disk** — remember, "the disk" here is the fake 20 GB one, *not* your Mac. This is completely safe. Confirm when it warns you it will erase it.
6. **Profile setup:** enter your name, a server name, a username, and a **password you'll remember** (you'll type it a lot in Lesson 04).
7. **Install OpenSSH server:** when you reach this screen, **tick it on** (press <kbd>Space</kbd>). This lets you log into the server from your Mac's Terminal later — you'll use it in Lesson 04.
8. Skip the list of optional "snaps," let it install, and when it finishes choose **Reboot Now**. If it asks you to "remove the installation medium," just press <kbd>Enter</kbd> — UTM handles it.

When it reboots, you'll land on a plain text **login prompt** — no desktop, no icons, just `ubuntu-lab login:`. Type your username, press <kbd>Enter</kbd>, type your password (the screen shows *nothing* as you type — that's normal), and press <kbd>Enter</kbd>. You're in. That black screen with a prompt **is** your server — the same experience as logging into a real machine in a data centre.

> **No desktop? That's intentional.** There's no Firefox, no Files app, no settings window — and there's nothing wrong. A server is pure command line. Everything in Lesson 04 happens right here at this prompt.

## Step 4 — The most important VM habit: snapshots

A **snapshot** saves the VM's *entire* current state so you can jump back to it. Before trying anything risky, take one. If it goes wrong, restore and it's like it never happened.

In UTM, with the VM selected, look for the snapshot option (in newer UTM it's in the VM's toolbar/menu while running, or right-click the VM). Take one now and name it `fresh-install`. That's your clean starting point for the whole course.

> Think of snapshots like save points. Take one *before* the boss fight (a risky command), not after you've already lost.

## A note on two "terminals"

From here on you'll have **two** places to type commands, and it's important not to mix them up:

- Your **Mac's Terminal** — controls your real Mac.
- The **VM's console** (the Ubuntu Server window) — controls the Linux guest.

Lesson 04 lives almost entirely inside the **VM's** terminal. When in doubt, run `whoami` and `hostname` — they'll tell you which machine you're on.

---

## Challenge

1. Download the correct Ubuntu Server 26.04 LTS ISO for your Mac's chip.
2. Create and install an Ubuntu Server VM in UTM with at least 2 GB RAM and ~20 GB disk, and tick **Install OpenSSH server** during setup.
3. Log in at the console prompt and run `whoami` and `hostname` to confirm where you are.
4. Take a snapshot named `fresh-install`.
5. As a test of your nerve: inside the VM, create a file in your home folder (`touch test.txt`), then restore your snapshot and watch it vanish. Now you *understand* snapshots.

Mark complete once you're staring at your own Linux machine. Next, we learn to run it like an admin.

> **Glossary:** *VM* = a computer running inside your computer · *host* = your Mac · *guest* = the VM · *hypervisor* = the software that runs the VM · *ISO* = an installer disk in a file · *LTS* = the stable, long-supported version · *snapshot* = a restorable save point of the VM.
