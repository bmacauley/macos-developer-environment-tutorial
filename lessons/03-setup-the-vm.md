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
2. On an **Apple Silicon** Mac (M1–M5), you need the **ARM64 / "for ARM"** build of **Ubuntu Desktop 26.04 LTS**. On an **Intel** Mac, get the regular 64-bit (AMD64) desktop image.
3. It's a big download (several GB) — start it, then read the rest of this lesson while it finishes.

> "LTS" means **Long-Term Support** — the stable version that gets 5 years of updates. Always pick LTS for learning; you want boring and reliable, not bleeding-edge.

## Step 2 — Create the VM in UTM

1. Open **UTM** and click the **+** to create a new VM, then choose **Virtualize** (not Emulate — virtualizing is much faster and correct for a matching ARM/Intel guest).
2. Choose **Linux**.
3. On an Apple Silicon Mac, tick **Use Apple Virtualization** if offered — it's smoother on modern macOS.
4. **Boot ISO image** → Browse → select the Ubuntu `.iso` you downloaded.
5. **Memory:** give it **4096 MB** (4 GB). If your Mac has 16 GB or more, **8192 MB** (8 GB) feels much nicer.
6. **CPU cores:** the default is fine (4 is plenty).
7. **Storage:** **30–40 GB**. This is a *maximum* size that grows as needed, so it won't immediately eat your disk.
8. Give it a name like `ubuntu-lab` and click **Save**.

## Step 3 — Install Ubuntu inside the VM

Select your new VM and press the big **▶ Play** button. A window opens and boots the Ubuntu installer. Then, inside that window:

1. Choose **Try or Install Ubuntu**.
2. Pick your language and keyboard.
3. Choose a **normal installation**.
4. When it asks about disks, let it use the **entire disk** — remember, "the disk" here is the fake 30 GB one, *not* your Mac. This is completely safe.
5. Create your user: a name, a username, and a **password you'll remember** (you'll type it a lot in Lesson 04). Turn on "log in automatically" if you like.
6. Let it install (a few minutes) and, when prompted, **restart**. If it asks you to "remove the installation medium," just press <kbd>Enter</kbd> — UTM handles it.

You now have a Linux desktop running in a window on your Mac. Poke around — open its Firefox, its files, its settings. Nothing you do here can touch your Mac.

> **If the screen resolution is tiny or things feel clunky**, that's normal at first. Inside Ubuntu, open its "Terminal" app and run `sudo apt update && sudo apt install -y spice-vdagent` then restart the VM — this improves the display and lets the window resize. (Don't worry about what those commands mean yet; Lesson 04 explains `apt` and `sudo`.)

## Step 4 — The most important VM habit: snapshots

A **snapshot** saves the VM's *entire* current state so you can jump back to it. Before trying anything risky, take one. If it goes wrong, restore and it's like it never happened.

In UTM, with the VM selected, look for the snapshot option (in newer UTM it's in the VM's toolbar/menu while running, or right-click the VM). Take one now and name it `fresh-install`. That's your clean starting point for the whole course.

> Think of snapshots like save points. Take one *before* the boss fight (a risky command), not after you've already lost.

## A note on two "terminals"

From here on you'll have **two** places to type commands, and it's important not to mix them up:

- Your **Mac's Terminal** — controls your real Mac.
- The **VM's Terminal** (inside the Ubuntu window) — controls the Linux guest.

Lesson 04 lives almost entirely inside the **VM's** terminal. When in doubt, run `whoami` and `hostname` — they'll tell you which machine you're on.

---

## Challenge

1. Download the correct Ubuntu 26.04 LTS ISO for your Mac's chip.
2. Create and install an Ubuntu VM in UTM with at least 4 GB RAM and ~30 GB disk.
3. Log into the Ubuntu desktop and open its Terminal app.
4. Take a snapshot named `fresh-install`.
5. As a test of your nerve: inside the VM, create a file on the desktop, then restore your snapshot and watch it vanish. Now you *understand* snapshots.

Mark complete once you're staring at your own Linux machine. Next, we learn to run it like an admin.

> **Glossary:** *VM* = a computer running inside your computer · *host* = your Mac · *guest* = the VM · *hypervisor* = the software that runs the VM · *ISO* = an installer disk in a file · *LTS* = the stable, long-supported version · *snapshot* = a restorable save point of the VM.
