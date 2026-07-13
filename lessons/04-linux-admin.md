# 04 · Running a Linux Machine

Everything you learned in Lesson 02 works here too — Linux and macOS both descend from the same Unix family, so `cd`, `ls`, `cat`, and pipes all behave the same. This lesson adds the skills that make you the **administrator** of a machine: installing software, managing users and permissions, running background services, and connecting to it remotely.

**Do all of this inside your Ubuntu VM.** Take a fresh snapshot first — call it `before-lesson-04` — so you can experiment fearlessly.

---

## `sudo`: doing admin things

Most of the time you act as a normal user who can only touch your own files. To change the *system* — install software, edit system settings — you temporarily become the all-powerful **root** user with `sudo` ("**s**uper**u**ser **do**"):

```bash
sudo apt update
```

It'll ask for your password (the one you made during install). Typing shows nothing — normal.

> **`sudo` is a loaded gun.** As root there are no guardrails; a wrong command can wreck the system. That's *exactly* why we're on a VM — so a mistake costs you a snapshot restore, not your computer. Read every `sudo` command before running it.

## `apt`: Ubuntu's package manager

Remember Homebrew on the Mac? Linux has the same idea built in. On Ubuntu it's called **apt**. The core commands:

```bash
sudo apt update              # refresh the list of available software
sudo apt upgrade             # update installed software
sudo apt install <package>   # install something
sudo apt remove <package>    # uninstall it
apt search <keyword>         # find a package
```

Always run `update` before `install` so apt knows what's currently available. Let's install some tools you'll use:

```bash
sudo apt update
sudo apt install -y git curl htop neofetch
```

The `-y` means "yes, don't ask me to confirm." Now try:

```bash
neofetch     # a pretty summary of the system — screenshot this, it looks cool
htop         # a live view of running programs (press q to quit)
```

## Users and permissions, properly

Linux was built for many people to share one machine, so it takes **who-can-do-what** seriously. Every file has an **owner**, a **group**, and a set of permissions for *owner / group / everyone else*.

Run `ls -l` and decode a line like `-rw-r--r--`:

```
-  rw-  r--  r--
│  │    │    └── everyone else: read only
│  │    └─────── group: read only
│  └──────────── owner: read + write
└─────────────── type (- = file, d = directory)
```

The three permission types are **r**ead, **w**rite, and e**x**ecute. Change them with `chmod`. The clearest way for beginners is the letter form:

```bash
chmod +x deploy.sh      # add execute permission (make it runnable)
chmod -w notes.txt      # remove write permission (protect it)
chmod u+rwx,go-rwx secret.txt   # owner gets all; group/others get nothing
```

Change *ownership* with `chown`:

```bash
sudo chown yourname somefile     # make yourself the owner
```

### Make a second user (see multi-user Linux in action)

```bash
sudo adduser testkid             # creates a user + home folder, asks for a password
groups testkid                   # what groups is this user in?
sudo usermod -aG sudo testkid    # add them to the "sudo" group = give admin rights
su - testkid                     # switch into that user's session
whoami                           # confirms you're now "testkid"
exit                             # go back to yourself
```

This is exactly how servers manage teams: each person a user, permissions granted by group. You just did real system administration.

## Where things live in Linux

Linux has a tidy, predictable layout. A quick tour with `ls`:

| Path | What's there |
|------|--------------|
| `/home/you` | your personal files (this is `~`) |
| `/etc` | system configuration files |
| `/var/log` | log files — where programs record what happened |
| `/usr/bin` | installed programs (commands) |
| `/tmp` | temporary scratch space, wiped on reboot |

Explore safely: `ls /etc`, `cat /etc/os-release` (shows which Linux you're running), `ls /var/log`.

## Services: programs that run in the background

A **service** (or "daemon") is a program that runs quietly in the background — a web server, a database, a scheduler. Ubuntu manages these with **systemctl**. Let's install a real web server and control it:

```bash
sudo apt install -y nginx
sudo systemctl status nginx      # is it running? (press q to exit)
sudo systemctl stop nginx        # stop it
sudo systemctl start nginx       # start it
sudo systemctl enable nginx      # start automatically on boot
```

Your server has no browser, so ask for the page from the command line instead:

```bash
curl http://localhost                 # fetch the page and print it
curl -s http://localhost | head -n 5  # just the first few lines
```

You'll see the raw HTML of the "Welcome to nginx" page — a real web server you started, running on your own Linux machine, answering your request. `curl` is how you talk to web servers without a browser, and it's the same software powering a huge chunk of the internet.

## Reaching the VM from your Mac with SSH

**SSH** ("secure shell") lets you control one computer's terminal from another over the network. It's how engineers manage servers all over the world. Let's SSH from your **Mac's** terminal into your **VM**.

Inside the VM, make sure the SSH server is installed and running, then find the VM's address. (If you ticked **Install OpenSSH server** back in Lesson 03, it's already here — these commands just confirm it, and do no harm if it's already set up.)

```bash
sudo apt install -y openssh-server
sudo systemctl enable --now ssh
ip addr | grep "inet "     # look for an address like 192.168.x.x
```

Now, on your **Mac's** Terminal (not the VM), connect:

```bash
ssh yourname@192.168.x.x    # use the address you just found
```

Type `yes` to trust it the first time, then your VM password. Your Mac terminal is now driving the Linux box. Run `neofetch` — you'll see the *VM's* info, proving you're remote. This exact skill is how you'd manage a cloud server later.

> **If SSH can't connect:** UTM's default networking sometimes isolates the VM. In the VM's settings in UTM, set the network mode to **Bridged** (or **Shared**) and reboot. This is a normal, real-world networking hiccup — troubleshooting it *is* the lesson.

---

## Challenge

Inside your VM:

1. Update the system and install `git`, `htop`, and `neofetch`. Screenshot `neofetch`.
2. Create a file, remove your own write permission with `chmod`, try to edit it and watch it refuse, then restore write access.
3. Create a second user, give them sudo rights, switch into their account, and switch back.
4. Install nginx and load its welcome page with `curl http://localhost`. Then stop the service and confirm `curl` can no longer reach it.
5. **Boss level:** SSH from your Mac's terminal into your VM and run a command there.

Mark complete when you've SSH'd in successfully. You now run a Linux machine. Next, the tools you'll build things *with*.

> **Glossary:** *sudo* = run as admin/root · *apt* = Ubuntu's package manager · *chmod / chown* = change permissions / ownership · *service (daemon)* = a background program · *systemctl* = controls services · *SSH* = remote terminal access to another machine.
