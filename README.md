# Build a Real Portfolio Site with Antigravity 2.0 and GitHub MCP

> A hands-on codelab by **Geeta Kakrani** — AI Consultant, Google Developer Expert (AI/ML & TPU)  
> 🔗 LinkedIn: [linkedin.com/in/geetakakrani](https://www.linkedin.com/in/geetakakrani)

> **Note:** No prior AI or agent experience needed for this codelab — we'll build the concepts up from scratch before writing any commands.

---

## 📋 Table of Contents

1. [What is Generative AI?](#1-what-is-generative-ai)
2. [What is Agentic AI?](#2-what-is-agentic-ai)
3. [What is Antigravity 2.0 — and how is it different?](#3-what-is-antigravity-20--and-how-is-it-different)
4. [Install the Antigravity CLI (agy)](#4-install-the-antigravity-cli-agy)
5. [Build a Real Portfolio Website](#5-build-a-real-portfolio-website)
6. [What is MCP?](#6-what-is-mcp)
7. [Set up the GitHub MCP Server](#7-set-up-the-github-mcp-server)
8. [Push Your Site to GitHub with a Simple Prompt](#8-push-your-site-to-github-with-a-simple-prompt)
9. [Recap](#9-recap)
10. [What's Next](#10-whats-next)

---

## 1. What is Generative AI?

Old-style AI could only **sort or predict** things that already exist — "is this email spam or not," "will this customer cancel or not." It picked from options you gave it.

**Generative AI creates something brand new that didn't exist before** — text, images, code, audio, video — just from a plain description you type in.

Think of it like this: a calculator can only compute numbers you give it. Generative AI is like an artist who, when you say "paint me a sunset over mountains," actually paints a new picture — one that never existed before — based on everything it has learned from millions of other paintings.

**Simple everyday examples:**
- You type "Write a birthday message for my mother" → Gemini/ChatGPT writes a fresh message for you
- You type "Draw a cat wearing a spacesuit" → an image tool like Midjourney creates a picture
- You type "Write me a Python function to add two numbers" → GitHub Copilot writes the actual code

Large Language Models (LLMs) like Gemini, GPT, and Claude are the text-and-code branch of generative AI. Under the hood, they work like a very advanced autocomplete — predicting the next most likely word, over and over, based on patterns learned from huge amounts of text.

> ⚠️ **Warning:** Generative AI **predicts**, it doesn't truly "understand" like a human does. It can sometimes confidently produce something wrong (called a "hallucination") — always double-check important facts it gives you.

This idea — describing what you want in plain language and getting real output back — is the foundation everything else in this codelab builds on.

---

## 2. What is Agentic AI?

Generative AI on its own just **answers and stops**. You ask, it replies, done. If you want the next step done, you have to ask again and do the work yourself.

**Agentic AI takes it further — it doesn't just answer, it acts**, running in a loop until the actual goal is finished:

1. **Plan** — break the goal into steps
2. **Act** — use a real tool (write a file, run a command, search the web, call an API)
3. **Observe** — check whether that step worked
4. **Repeat** — keep going, and fix its own mistakes, until the goal is actually done

**A simple everyday example:**
- Generative AI: you ask "what should a good grocery list for a birthday party look like?" — it writes you a list, and stops. You still have to go buy everything yourself.
- Agentic AI: you say "order everything needed for my daughter's birthday party" — the agent checks what you already have, decides what's missing, actually places the order, and confirms once it's done.

**A coding example (what we'll do today):**
- Generative AI: you ask "what would the code for a portfolio website look like?" — it shows you code in the chat, and you'd have to copy it into files yourself.
- Agentic AI (Antigravity): you say "build me a portfolio website" — the agent actually creates the real `index.html`, `styles.css`, and `script.js` files on your computer, checks that they work, and tells you when it's done.

> ⚠️ **Note:** An agent is not magic — it still makes mistakes sometimes. The value is that it handles the repetitive typing and file-juggling, while you stay in charge of reviewing what it did.

**Antigravity 2.0** is Google's dedicated platform for exactly this — a place to run these goal-driven agents, in parallel, from your desktop, terminal, or your own code.

---

## 3. What is Antigravity 2.0 — and how is it different?

If you've used **Gemini CLI** before, here's what changed with Antigravity 2.0:

| Feature | Gemini CLI (old) | Antigravity 2.0 |
|---|---|---|
| Interface | Terminal only | Desktop App + CLI + SDK |
| Agent model | Single agent | Parallel multi-agent |
| Plugins | Extensions | Antigravity Plugins |
| Status (mid-2026) | Retired for consumers | Active |

> ⚠️ **Warning:** Gemini CLI was retired for consumer accounts (free, Pro, Ultra) on **June 18, 2026**. If you have old `gemini` command workflows, this codelab's `agy` commands are the replacement.

Antigravity 2.0 isn't one single tool — it's an ecosystem with **three surfaces that all share the same underlying agent**, so an improvement to the agent reaches all three at once:

- **Antigravity 2.0 (Desktop App)** — your mission control. Launch multiple agents in parallel, schedule background tasks. Not a code editor by itself.
- **Antigravity IDE** — a full VS Code–style editor with the same agent built in, for when you want to code alongside the agent directly.
- **Antigravity CLI (`agy`)** — the terminal version. Everything the Desktop App can do, from your command line. This is what we'll use today.

---

## 4. Install the Antigravity CLI (agy)

`agy` is a Go binary — install it with Google's official installer script. There is no npm package for it.

**macOS / Linux**
```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

**Windows (PowerShell)**
```bash
irm https://antigravity.google/cli/install.ps1 | iex
```

**Windows (cmd.exe) — alternative**
```bash
curl -fsSL https://antigravity.google/cli/install.cmd -o install.cmd && install.cmd && del install.cmd
```

Reference: [antigravity.google/docs/cli-install](https://antigravity.google/docs/cli-install)

**Verify and authenticate:**
```bash
agy --version
agy
```

> ⚠️ **Tip:** If `agy --version` says "command not found" right after installing, close and reopen your terminal — the installer updates your PATH, which only takes effect in a fresh terminal window.

On first run, `agy` opens a browser tab — sign in with your personal Gmail (not corporate/school). You'll land here:

```
◆ Welcome to Antigravity CLI
  Authenticated as: yourname@gmail.com
  Model: gemini-3.5-flash
  Type /help for commands
>
```

---

## 5. Build a Real Portfolio Website

**macOS / Linux**
```bash
mkdir -p ~/antigravity-portfolio
cd ~/antigravity-portfolio
agy
```

**Windows**
```bash
mkdir antigravity-portfolio
cd antigravity-portfolio
agy
```

At the `agy` prompt, describe the outcome — this is called **vibe coding**: you state intent, the agent handles implementation.

```
Create a personal portfolio website for me.
Requirements:
- Separate index.html, styles.css, and script.js files
- Sections: Hero with name and title, About, Skills (as tags), Projects (3 sample cards), Contact
- Dark theme with one accent color, responsive layout using CSS Flexbox/Grid
- Add a working "scroll to section" nav bar
Do not start a server.
```

Watch `agy` plan the file structure, write each file, and report what it created — this is a real, working site, not a placeholder.

**Preview it locally.** Exit with `Ctrl+C`, then:

```bash
python3 -m http.server 8080
```

> ⚠️ **Windows Note:** On Windows, `python3` is often not recognised — the installer usually only registers `python`. If you get a "not found" error, run `python -m http.server 8080` instead.

Open [http://localhost:8080](http://localhost:8080) and check your portfolio site loads and the nav bar scrolls correctly.

> ✅ **Tip:** Ask `agy` to tweak anything you don't like in plain English — "make the accent color teal instead" or "make the Projects cards clickable." It edits the existing files rather than starting over.

---

## 6. What is MCP?

**MCP (Model Context Protocol)** is an open standard that lets your agent securely call tools exposed by an external server — instead of you writing custom integration code for every service you want it to talk to.

**Simple analogy:** think of MCP like a universal charging cable. Before USB-C, every phone had its own different charger — one cable per brand, per socket. USB-C became one standard plug that just works everywhere. MCP does the same thing for AI agents — instead of writing separate custom code to connect your agent to GitHub, Google Drive, a database, or Slack, each of those services just plugs into your agent the same standard way, through an MCP server.

Without MCP, if you wanted your agent to push code to GitHub, you'd have to script the GitHub API calls yourself. With MCP, you point `agy` at a **GitHub MCP server**, and the agent can call tools like `create_repository`, `push_files`, and `create_issue` directly from a plain-English request.

Antigravity CLI, the Desktop App, and the IDE all read MCP servers from the same config, so a server you set up once works everywhere:

- Global (every project): `~/.gemini/config/mcp_config.json`
- Per-project (this workspace only): `.agents/mcp_config.json`

We'll use the per-project file so it only applies to this portfolio folder.

---

## 7. Set up the GitHub MCP Server

Inside your `antigravity-portfolio` folder, create the config folder:

```bash
mkdir .agents
```

Create a **GitHub Personal Access Token** first (classic, with `repo` scope) at [github.com/settings/tokens](https://github.com/settings/tokens), and keep it copied.

Then create `.agents/mcp_config.json` (Notepad on Windows is fine) with this content, replacing the placeholder:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_TOKEN_HERE"
      }
    }
  }
}
```

> 🔴 **CAUTION:** Never commit this file with a real token inside it. Before pushing anything, add `.agents/mcp_config.json` to a `.gitignore` file in this folder.

Restart `agy` inside this folder and confirm the server loaded:

```bash
cd ~/antigravity-portfolio
agy
```

```
/mcp
```

You should see `github` listed as an active server with its tools. The first time the agent actually uses one of these tools, Antigravity will ask you to approve it — allow it.

---

## 8. Push Your Site to GitHub with a Simple Prompt

Now, still inside the same `agy` session, ask for the whole thing in plain English:

```
Create a new public GitHub repository called "my-portfolio-site" under my account.
Push all the files in this folder to it as the initial commit.
Use the commit message "Initial portfolio site built with Antigravity".
```

Watch `agy`:
1. Call the GitHub MCP server to create the repository
2. Initialize git locally if needed and stage your files
3. Push the commit
4. Report back the repository URL

Open the URL it gives you — your portfolio site's code is now live on GitHub, and you never typed a single `git` or `gh` command by hand.

> ✅ **Tip:** From here, any future change is the same pattern: edit the site by describing what you want, then say "commit and push this with an appropriate message" — the agent handles git entirely through the MCP connection.

---

## 9. Recap

| Concept | What it means |
|---|---|
| Generative AI | Models that create new content, not just classify it |
| Agentic AI | An AI that plans, uses tools, and acts toward a goal on its own |
| Antigravity 2.0 | Google's agent platform — Desktop App, IDE, and CLI sharing one agent |
| `agy` | The terminal surface of Antigravity 2.0 |
| Vibe coding | Describing the outcome you want; the agent writes the implementation |
| MCP | An open protocol exposing external tools (like GitHub) to your agent |
| `mcp_config.json` | Where MCP servers are registered — globally or per project |

> ⚠️ **Note:** Antigravity is a fast-changing, recently launched product (May 2026). Command names and config paths may shift — do a quick dry run a day or two before presenting this live.

---

## 10. What's Next

- 📖 Antigravity docs: [antigravity.google/docs](https://antigravity.google/docs)
- ⚙️ CLI install & reference: [antigravity.google/docs/cli-install](https://antigravity.google/docs/cli-install)
- 🔌 Explore more official MCP servers (Google Workspace, Google Developer Knowledge, and others) in the Antigravity docs
- 👤 Author's LinkedIn: [linkedin.com/in/geetakakrani](https://www.linkedin.com/in/geetakakrani)

---

*Built with ❤️ using Antigravity 2.0 and GitHub MCP*
