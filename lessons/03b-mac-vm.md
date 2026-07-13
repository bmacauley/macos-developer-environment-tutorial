# 03b · Bonus: A macOS VM

You just built a Linux lab. But here's a fun trick: on an Apple Silicon Mac, you can also run **macOS inside a window on your Mac** — a second, throwaway copy of the very operating system you're using right now.

This is an **optional detour**. If you just want to get on with the course, skip straight to Lesson 04 — nothing later depends on this. But a macOS VM is genuinely useful, so it's worth knowing it exists.

**What you'll learn:** when a macOS VM is handy, why it needs Apple Silicon, and how to build one in UTM.

---

## Why would you want a *Mac* inside your Mac?

A Linux VM lets you learn a *different* operating system safely. A macOS VM is different — it's a clean, disposable copy of **the same** OS, which turns out to be handy for:

- **Testing on a fresh Mac** — see exactly what a brand-new user experiences, with none of your settings or clutter.
- **Trying risky installs** — run a sketchy installer or a big system change on the same OS as your real Mac, without risking your real Mac.
- **Trying a beta macOS** — kick the tyres on a new macOS version before you put it on your actual machine.

Think of it as a second, factory-fresh Mac you can create, break, and throw away.

## The two big catches (read these first)

Before you get excited, two hard limits:

1. **Apple Silicon only.** This works on **M1, M2, M3, M4, M5** Macs (2020 and later). Older **Intel** Macs *cannot* virtualise macOS — the technology (Apple's Virtualization framework) simply isn't there. Not sure which you have? Open the Apple menu → **About This Mac** and look for "Apple M…" versus "Intel".
2. **Apple's licence allows up to 2 macOS VMs** running at once, and only on genuine Apple hardware. That's plenty for learning — just know the rule exists.

There's also a practical catch: a macOS VM is **big**. The download is around 14 GB and the VM wants **60–80 GB** of disk. Make sure you have the room before you start.

## Step 1 — Get the macOS restore image

Linux installs from an **ISO** file. macOS is different — it installs from a **restore image**, a file ending in **`.ipsw`** (the same format used to restore an iPhone).

The easy path: **UTM can download it for you.** In the next step, when you choose to virtualise macOS, UTM offers to fetch the **latest macOS** straight from Apple — no hunting required. If you'd rather grab it yourself, restore images are published for each macOS version, but letting UTM do it is simplest.

> It's a big download (~14 GB). Start it, then read the rest of this lesson while it finishes.

## Step 2 — Create the VM in UTM

You already have UTM from Lesson 03. Open it, then:

1. Click the **+** to create a new VM and choose **Virtualize** (never Emulate — you're running Apple Silicon on Apple Silicon, so virtualising is fast and correct).
2. Choose **macOS 12+**.
3. **Boot image:** either let UTM **download the latest macOS** for you, or **Browse** to an `.ipsw` you already have.
4. **Memory:** give it **8192 MB** (8 GB). macOS is heavier than Linux — don't go below 4 GB.
5. **CPU cores:** the default is fine.
6. **Storage:** **64 GB** or more. Like before, this is a *maximum* that grows as needed, but macOS genuinely uses a lot.
7. Give it a name like `macos-sandbox` and click **Save**.

## Step 3 — Install macOS inside the VM

Select the new VM and press the big **▶ Play** button. UTM installs macOS from the restore image — this takes a while (often 15–30 minutes) and the window may look blank or restart a few times. That's normal; let it work.

When it finishes, you'll land in the familiar **macOS Setup Assistant** — the same "Welcome, choose your country" flow you saw when you first set up your Mac. Click through it:

1. Pick your region and language.
2. **Skip signing in with your Apple Account** when offered. Some Apple services (iCloud, the App Store, iMessage) don't work reliably inside a VM, and you don't want your real account tangled up in a throwaway machine. Choose **Set Up Later**.
3. Create a simple local user with a password you'll remember.

You now have a second macOS running in a window. Open its Safari, its Settings, its Finder — it's a complete, isolated Mac, and nothing you do to it can touch your real one.

## A note on snapshots

In Lesson 03 you learned to take **snapshots** of the Linux VM. Heads-up: with UTM's Apple-based VMs (which is what macOS uses), **snapshots aren't available** the same way. Instead, once your VM is set up the way you like it and **powered off**, right-click it in UTM and choose **Clone** to make a duplicate. Keep the clone as your clean starting point, and experiment on the copy.

> Same idea as a snapshot — a spare, clean copy to fall back to — just done by duplicating the whole VM instead.

---

## Challenge

*(Apple Silicon Macs only — if you're on an Intel Mac, just read along; this one isn't possible for you.)*

1. Confirm your Mac is Apple Silicon via **About This Mac**.
2. In UTM, create a new **Virtualize → macOS** VM and let UTM download the latest macOS.
3. Install it and click through Setup Assistant, choosing **Set Up Later** instead of signing in with an Apple Account.
4. Once it's running, **shut the VM down** and make a **Clone** of it named `macos-clean`.
5. Boot the clone, change something (set a wild wallpaper), then throw that clone away — proof that it's truly disposable.

This lesson is optional, so mark it complete if you did it — or just carry on to Lesson 04, where we get to work inside the Linux machine.

> **Glossary:** *restore image / `.ipsw`* = the file macOS installs from (macOS's equivalent of an ISO) · *Apple Silicon* = Macs with Apple's own M-series chips · *Virtualization framework* = Apple's built-in technology that lets a Mac run another OS · *clone* = a full duplicate of a VM, used here in place of a snapshot.
