# 02 · Command-Line Basics

This is the most important lesson in the course. Once you're comfortable moving around and manipulating files from the terminal, everything else — Linux, servers, git, AI agents — becomes approachable, because they *all* speak this language.

**What you'll learn:** the filesystem as a tree, navigating it, creating and moving files, reading files, wildcards, pipes, and permissions.

---

## The filesystem is a tree

Your files live in a branching tree of folders (folders are called **directories** in terminal-land). At the very top is `/`, the **root**. Your personal stuff lives in your **home directory**, written as `~`.

Three commands tell you where you are and what's around you:

```bash
pwd     # "print working directory" — where am I right now?
ls      # "list" — what's in here?
cd      # "change directory" — move somewhere else
```

Try a little tour:

```bash
cd ~            # go home
pwd             # confirm where you are
ls              # see your home folder's contents
ls -la          # the same, but detailed and including hidden files
```

`ls -la` deserves a look. The `-l` gives a **l**ong, detailed listing; the `-a` shows **a**ll files including hidden ones (names starting with a `.`). Those flags can combine into `-la`. Most commands take flags like this.

### Moving around

```bash
cd ~/projects    # go into a specific folder
cd ..            # go UP one level (.. means "the parent")
cd -             # go back to where you just were
cd               # with nothing after it, jumps home
```

> **The killer shortcut: Tab completion.** Start typing a file or folder name and press <kbd>Tab</kbd>. The shell finishes it for you. Type `cd ~/proj` then <kbd>Tab</kbd> and it completes to `~/projects/`. Use this constantly — it's faster and prevents typos.

## Making and removing things

```bash
mkdir practice           # make a directory called "practice"
cd practice
touch notes.txt          # create an empty file
mkdir -p a/b/c           # make nested folders in one go (-p = make parents)
ls -R                    # list recursively (everything, including subfolders)
```

Copy, move, rename, delete:

```bash
cp notes.txt notes-backup.txt     # copy
mv notes.txt journal.txt          # rename (move within the same folder)
mv journal.txt a/                 # move into folder "a"
rm notes-backup.txt               # remove a file
rm -r a                           # remove a folder and everything in it
```

> **⚠️ `rm` is permanent.** There's no Trash, no undo. `rm -r` deletes a whole tree instantly. Read the command before you press Enter, *especially* if it contains `rm`. A good habit: run `ls` first to see exactly what you're about to delete.

## Reading files without opening an app

```bash
cat journal.txt       # dump the whole file to the screen
less bigfile.txt      # scroll through a long file (press q to quit)
head -n 5 file.txt    # first 5 lines
tail -n 5 file.txt    # last 5 lines
wc -l file.txt        # count the lines
```

Let's make a file with content to play with:

```bash
echo "apples" > fruit.txt      # > writes (and OVERWRITES) 
echo "bananas" >> fruit.txt    # >> appends a new line
echo "cherries" >> fruit.txt
cat fruit.txt
```

Notice the difference: `>` replaces the file's contents, `>>` adds to the end. Mixing these up is a classic beginner mistake — `>` will happily erase a file.

## Wildcards

The `*` character means "anything." It lets one command hit many files:

```bash
ls *.txt          # every file ending in .txt
rm test-*         # every file starting with "test-"
cp *.txt backup/  # copy all text files into backup/
```

## Pipes: connecting tools together

This is the idea that makes the command line powerful. Every tool does *one small thing* and prints text. The **pipe** `|` takes the output of one tool and feeds it as input to the next. You chain simple tools into something smart.

```bash
ls -la | wc -l                       # count how many items are in a folder
cat fruit.txt | sort                 # sort the lines alphabetically
history | grep git                   # find every git command you've ever run
ls | grep ".txt"                     # list only names containing ".txt"
```

`grep` searches text for a pattern. Combined with a pipe it becomes a filter for *anything*. Read `ls | grep ".txt"` as: "list everything, then keep only the lines with `.txt`."

Once this clicks — small tools + pipes = big results — you're thinking like a command-line user.

## Permissions (a first taste)

Run `ls -l` and look at the cryptic start of each line, like `-rw-r--r--`. That's **permissions**: who is allowed to read, write, and execute each file. You'll meet these properly on Linux in Lesson 04, but here's the one command to know:

```bash
chmod +x script.sh    # make a file executable (runnable as a program)
```

## Getting help

Two ways to figure out what a command does:

```bash
man ls        # the full manual (press q to quit)
ls --help     # a shorter summary (works for most tools)
```

Nobody memorizes all the flags. Knowing how to *look them up* is the real skill.

---

## Challenge

Do this entirely in the terminal, no mouse:

1. In `~/projects`, make a folder `cli-practice` and `cd` into it.
2. Create three files: `red.txt`, `green.txt`, `blue.txt`, each containing the name of the colour (use `echo` and `>`).
3. Make a folder called `colours` and move all three `.txt` files into it with a single command using a wildcard.
4. Use `cat` with a wildcard to print all three files at once.
5. Use a pipe to count how many files are in the `colours` folder.
6. Look up what the `-h` flag does for `ls` using `ls --help` (hint: try `ls -lh` afterward).

Mark complete when you can do all six without looking back at the examples. Next, we build a whole separate computer to practice on.

> **Glossary:** *directory* = folder · *`~`* = home · *`/`* = root · *flag* = an option like `-l` · *pipe (`|`)* = feed one tool's output into another · *grep* = search text · *chmod* = change permissions.
