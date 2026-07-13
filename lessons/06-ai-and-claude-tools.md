# 06 · AI & Claude Tools

The newest tool in the box is AI — and it's a different *kind* of tool. A hammer does exactly what you make it do. An AI assistant can read your code, explain it, write some for you, and even run commands on your behalf. Used well, it's like having a patient senior engineer sitting next to you. Used lazily, it's a way to end up with code you don't understand. This lesson is about being in the first group.

**What you'll learn:** how to think about AI tools, how to prompt well, what "agentic" tools and MCP are, and the golden rule for learning with AI.

---

## The golden rule (read this twice)

> **Never paste code you can't explain.**

AI can hand you a working answer in seconds. The temptation is to copy it and move on. Resist it. Before you use any code an AI gives you, make yourself explain, out loud or in a comment, *what each part does*. If you can't, ask the AI to explain it — that's one of the things it's best at. The goal of this whole course is for **you** to be the capable one; AI is a tool that accelerates a skilled person, not a replacement for having the skill.

A good mental model: AI is a **calculator for words and code**. A calculator didn't make math pointless — it made people who *understand* math faster. Same deal here.

## Ways you'll meet Claude

There are a few different shapes the same underlying AI comes in. You don't need all of them; know they exist:

- **The chat assistant** (in a browser or app) — you type questions, it answers. Best for explaining concepts, planning, debugging error messages, and reviewing your code.
- **Claude Code** — a version that lives in your **terminal** and can actually read and edit files in a project and run commands. This is the one that fits everything you've learned in this course.
- **The API** — a way for *programs you write* to send text to Claude and get responses back, so you can build AI into your own apps.

Because product details change over time, when you want specifics — what's available, how to install something, current limits — the right move is to check the official docs at **[docs.claude.com](https://docs.claude.com)** rather than trusting a half-remembered tutorial. Knowing *where the source of truth is* beats memorizing details that expire.

## Prompting: how to ask well

The quality of what you get out of an AI depends heavily on how you ask. Four habits that make a big difference:

1. **Give context.** "Fix this" is weak. "This is a Python script meant to read a CSV and print row counts; it crashes with this error: `<paste error>` — here's the code: `<paste code>`" is strong.
2. **Say what "done" looks like.** "Explain it simply, for someone who just learned what a variable is." "Give me the shortest version." "Keep my style, just fix the bug."
3. **Ask for the reasoning, not just the answer.** "Walk me through *why*, step by step." You learn far more, and you catch mistakes — AI can be confidently wrong.
4. **Iterate.** Treat it like a conversation. "That worked, but now make it handle an empty file." Refining beats trying to write one perfect mega-prompt.

> Try this now: paste an error message from an earlier lesson (say, a command that failed) into a Claude chat and ask, *"What does this error mean and what are two things I could try?"* Notice how much faster that is than searching blindly — and how you still make the final decision.

## "Agentic" tools and MCP

Newer AI tools are **agentic** — instead of just replying with text, they can take **actions**: create a file, run a command, search the web, edit code across a whole project, and check their own work. You describe a goal ("set up a new Python project with tests") and the agent carries out the steps, showing you what it's doing.

For an agent to *act*, it needs to connect to real tools and data. The standard way that happens is called **MCP** — the **Model Context Protocol**. Think of MCP like a **USB port for AI**: a universal plug that lets an assistant connect to things — your files, GitHub, a database, a design app — without a custom hookup for each one. When you hear "connect a tool" or "add a connector," that's usually MCP under the hood.

You don't need to build one to benefit. Just understand the shape: **the model** (the brain) + **tools it can call** (hands) + **MCP** (the standard wiring between them). That mental model will make agentic tools far less mysterious.

## A safe way to experiment: point AI at your VM

Here's a great use of everything you've built. Your VM is a disposable playground, which makes it the *perfect* place to let an AI tool try things. If you use a terminal-based agent, run it against a project **inside the VM** (or a throwaway folder), take a snapshot first, and let it work. Worst case, you restore the snapshot. You get the speed of an agent with none of the risk to anything real — which is exactly the safety mindset from Lesson 03 applied to a new tool.

## Where AI helps most in *this* course

- **Stuck on an error?** Paste it and ask what it means.
- **A command did something you didn't expect?** Ask it to explain the command flag by flag.
- **Want a challenge?** Ask it to quiz you on Lesson 02's commands, or invent a small project using Lesson 05's tools.
- **Reviewing your own code?** Ask "what's a cleaner way to write this, and why?" — then judge the answer yourself.

---

## Challenge

1. Take an error or a command from an earlier lesson and ask a Claude chat to explain it, step by step. Then explain it back in your own words in a note file.
2. Ask the AI to generate a short shell or Python script for a small task you choose — then **add a comment above every line explaining what it does.** If you can't comment a line, ask what it means until you can.
3. Write one paragraph, in your own words, explaining what MCP is and why it's useful. (Teaching it back is the test of understanding.)
4. Look up one thing about Claude's tools on [docs.claude.com](https://docs.claude.com) — practice using the real source instead of guessing.

Mark complete when your generated script is fully commented in your own words. Then, the capstone.

> **Glossary:** *prompt* = what you ask the AI · *agentic* = an AI that takes actions, not just replies · *MCP* = the standard "USB port" that connects AI to tools and data · *API* = how your own programs talk to the AI · *the golden rule* = never use code you can't explain.
