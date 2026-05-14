# Setup

A 30-minute walkthrough from "downloaded the folder" to "working Cowork Project." Plain English, defines every term on first use. If you get stuck, jump to the Troubleshooting section at the bottom.

## What you're getting

A folder that holds your team's shared context (strategy, customers, analytics, rituals) plus two starter skills (hydrate-knowledge and prd). You'll point Claude Cowork at this folder, fill in placeholders with your real content, and your team gets a shared brain Claude can use.

## Before you start

You'll need:

- A paid Claude plan (Pro, Max, Team, or Enterprise). Claude Cowork requires this.
- A Mac or Windows machine. Linux isn't supported by the desktop app yet.
- Google Drive desktop sync installed (or another shared folder service your team uses).
- About 30 minutes.

## Step 1: Download this template

On the GitHub page for this template, click the green **Code** button, then **Download ZIP**. Unzip it. You should see a folder containing `README.md`, `CLAUDE.md`, and folders for `team`, `customers`, `knowledge`, `analytics`, and a hidden `.claude`.

If `.claude` isn't visible, see Step 10 below.

## Step 2: Place it in your shared Drive

Move the folder into the part of Google Drive your team syncs. For example: `~/Library/CloudStorage/GoogleDrive-you@company.com/Shared drives/Product/Team OS/`.

Why a shared Drive: anyone on your team can sync the folder locally and create their own Cowork Project pointing at the same content. Updates anyone makes propagate automatically.

If you don't have a shared Drive yet, a personal Drive folder works for now. You can move it later.

## Step 3: Install Claude Desktop

Go to [claude.com/download](https://claude.com/download) and download the desktop app for your platform. Run the installer. Sign in with your Anthropic account.

When the app opens, you'll see three tabs at the top: **Chat**, **Cowork**, and **Code**. We'll use Cowork.

> **Cowork** is Anthropic's tab for non-developers. It can read your files, browse the web, and use connected tools (Drive, Gmail, Calendar, Slack, and more) without you opening a terminal.

## Step 4: Open the Cowork tab

Click **Cowork** at the top. If the app prompts you to upgrade, you need a paid plan first. See "Before you start."

## Step 5: Create a Cowork Project

In Cowork, click **+ New Project** (or similar, depending on app version). Give it a name like "Team OS" or your team's name.

> A **Cowork Project** is a persistent workspace with its own files, connected folder, and instructions. Use one project per team or major workstream.

When prompted to connect a folder, select the Team OS folder you placed in Drive in Step 2.

## Step 6: Paste the folder instructions

In your new Cowork Project's settings, find the **folder instructions** panel (sometimes called "project instructions" depending on app version). Open `CLAUDE.md` from the Team OS folder, copy its full contents, and paste them into that panel.

Why: this gives Cowork the doc index for your folder structure so it knows what's where.

Save.

## Step 7: First prompt

Back in the main Cowork window, type:

```
Show me what's in this Team OS and explain what each folder is for.
```

Cowork should describe the structure you just connected. If it says it can't see the folder, see Troubleshooting.

## Step 8: Bootstrap your OS

Cowork doesn't surface skills as typeable slash commands the way Claude Code does, so you invoke a skill by asking for it in plain language. Type:

```
Run the hydrate-knowledge skill.
```

or, if you have a product homepage you'd like Cowork to pull from:

```
Run the hydrate-knowledge skill using https://yourproduct.com
```

Claude will find the skill in `.claude/skills/hydrate-knowledge/SKILL.md` and walk you through it. It reads from whatever MCPs you have connected (Drive, Gmail, Calendar, Slack, Linear, InsightStack, etc.) and pre-fills the placeholders in your OS with real content. You'll confirm every value before anything is written.

> An **MCP** (Model Context Protocol) connector is how Cowork talks to outside tools. To connect more MCPs, click the **+** button next to the prompt box and select **Connectors** or **MCP servers**.

If you don't have any MCPs connected yet, the skill falls back to interview mode and asks you 5-8 questions.

When the skill finishes, your `CLAUDE.md`, `knowledge/strategy.md`, `knowledge/competitive.md`, and `team/roster.md` will be populated.

## Step 9: Try the operational skill

Type:

```
Run the prd skill.
```

This walks you through drafting a PRD. The skill is opinionated: it pulls customer evidence from InsightStack and exports to Linear. If you don't use those tools, the skill still teaches the shape and you can adapt it.

If you don't have InsightStack or Linear connected, the skill will tell you which MCP it needs and stop gracefully.

## Step 10: Reveal the hidden folder (Mac)

The `.claude/` folder where skills live starts with a dot, which means macOS Finder hides it by default. To see it, open Finder, navigate to your Team OS folder, and press **Cmd + Shift + .** (period). The hidden folder appears.

On Windows, hidden folders are also hidden by default. In File Explorer, go to **View** → check **Hidden items**.

Why this matters: when you add new skills, you'll create folders under `.claude/skills/`.

## Step 11: Share with your team

In Google Drive, share the Team OS folder with your teammates (Editor access if they'll update content, Viewer if read-only).

Each teammate then:

1. Syncs the folder to their machine via Drive.
2. Installs Claude Desktop and signs in.
3. Creates their own Cowork Project pointing at the synced folder.
4. Pastes the contents of `CLAUDE.md` into their project's folder instructions.

They're now working from the same OS as you. Updates you make to files in Drive show up for them after sync, and vice versa.

## Troubleshooting

**Cowork can't see the folder.** Make sure the folder is fully synced locally before connecting. In Drive desktop, the folder should have a green checkmark, not a cloud icon. If the issue persists, re-create the Cowork Project and reconnect.

**Slash commands like `/prd` don't autocomplete in Cowork.** That's expected. Cowork only registers slash commands from installed plugins, not from the workspace folder. Invoke skills by name instead, e.g., "Run the prd skill." Claude reads the SKILL.md from `.claude/skills/` and follows it.

**Claude can't find the skill when I ask for it by name.** Confirm `.claude/skills/<skill-name>/SKILL.md` exists in the folder Cowork is pointed at, and that the file has valid frontmatter with a `name:` field. If you've just added or updated a skill in Drive, also re-paste `CLAUDE.md` into Cowork's folder-instructions panel so Claude knows the skill exists.

**Folder instructions don't seem to apply.** Some app versions require you to restart the Cowork session after editing folder instructions. Close and reopen the project.

**Cowork keeps asking what tools to use even after I hydrated.** Hydration fills your OS placeholders, but Cowork still uses MCPs per-prompt. You can pre-authorize tools in Project settings.

## Glossary

- **Cowork Project**: a persistent workspace in Claude Cowork with its own files, connected folder, and instructions.
- **Skill**: a reusable prompt Claude runs when you ask for it by name, like "run the prd skill." Lives under `.claude/skills/`.
- **Doc index**: the `README.md` in each folder that lists what's there and where to look for what.
- **Folder instructions**: text Cowork applies whenever you work in a connected folder. We paste `CLAUDE.md` into this panel during setup.
- **MCP**: Model Context Protocol. How Cowork talks to outside tools like Drive, Gmail, Slack, Linear.
- **Hydrate**: bootstrap. The hydrate-knowledge skill fills your OS placeholders with real content.
