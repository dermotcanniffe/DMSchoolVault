# 🧠 Using AI Helpers

⬅ [[02 - Reference/Reference Home|Reference Home]]

This vault uses the **Gemini Scribe** plugin — an AI that can read your notes and help you write, plus do all the math so you don't have to. I've set up two ready-made helper "agents" for you.

## The two helpers I made for you

Both live in `gemini-scribe/Prompts/` and load automatically as prompt options inside Gemini Scribe.

### 1. DM Math & Rules Helper
Your patient rules-and-numbers buddy. It does every calculation for you and explains things simply. Ask it things like:
- "A goblin has 8 Dexterity — what's its bonus?"
- "Set a DC for picking a rusty lock."
- "Is two ogres a fair fight for four level-3 characters?"
- "Fill in the ability scores for a friendly blacksmith NPC."

### 2. Stat Block Generator
Give it a vibe or a monster name and it hands back a complete, table-ready stat block with **every number filled in** (AC, HP, modifiers, attack bonuses, average damage). Ask it:
- "Make a stat block for a nervous cult acolyte, easy fight for level 2."
- "Give me a scary swamp creature for four level-5 players."

## How to use a helper (once Gemini Scribe is set up)
1. Add your Google Gemini API key in the plugin settings (Settings → Community plugins → Gemini Scribe). Without a key it can't talk to the AI.
2. Open the Gemini Scribe chat panel.
3. Pick the prompt/agent from the selector (the two above will appear by name).
4. Type your question, or open a template note first so the AI can see and fill it in.

> [!tip] Filling a template with AI
> Open an [[03 - Templates/Templates Home|template]] (say the NPC one), start the DM Math & Rules Helper, and ask "fill in the blanks for a suspicious dockside merchant." Because Gemini Scribe reads the current note, it fills your fields in place.

---

## FoundryVTT connection (the "let's see if it works" part)

You mentioned a **FoundryVTT** world with an **MCP plugin**, and hoping to pull random stat blocks from it. Here's the honest state of it:

The bridge is **[foundry-vtt-mcp](https://github.com/adambdooley/foundry-vtt-mcp)** by Adam Dooley. It's officially built for Claude Desktop, but under the hood its MCP server is a standard local **stdio** process — and Gemini Scribe can spawn that same process instead. So we can drive your Foundry world from Gemini Scribe directly.

### How the pieces fit
```
Gemini Scribe (Obsidian)  →  spawns  →  Foundry MCP server (node, stdio)
      →  WebSocket  →  "Foundry MCP Bridge" module  →  your Foundry world
```
- The MCP server doesn't care which app launches it, so Gemini Scribe works in place of Claude Desktop.
- The bridge's "needs Claude Pro" note only applies to *Claude Desktop* — going through Gemini Scribe sidesteps that entirely.

### What you need in place
1. **Foundry module:** in Foundry, install the "Foundry MCP Bridge" module and **enable** it in Module Management. (You must be logged in as the **GM** — the bridge only talks to a GM user.)
2. **MCP server on disk:** the node server that Gemini Scribe will launch. The **manual install** gives the cleanest known path:
   ```
   git clone https://github.com/adambdooley/foundry-vtt-mcp.git
   cd foundry-vtt-mcp
   npm install
   npm run build
   ```
   After this, the server lives at:
   `foundry-vtt-mcp/packages/mcp-server/dist/index.js`
   > If you used the Windows *installer* instead, it configured things for Claude Desktop and may not expose this path cleanly. For the Gemini Scribe route, the manual clone/build above is the reliable option. Note the full path to `index.js` — you'll need it below.
3. **Node.js 18+** installed and on your PATH (the `node` command must work in a terminal).

### Wiring it into Gemini Scribe (stdio server)
In Obsidian → Settings → **Gemini Scribe**:
1. Turn on **Show advanced settings** (the MCP section only appears when this is on).
2. Scroll to **MCP servers** and toggle **Enable MCP servers** on.
3. Click **Add server** and choose Transport = **Stdio (local process)**.
4. Fill it in:
   - **Name:** `foundry`
   - **Command:** `node`
   - **Arguments** (one per line):
     ```
     C:\full\path\to\foundry-vtt-mcp\packages\mcp-server\dist\index.js
     ```
   - **Environment variables** (one `KEY=VALUE` per line):
     ```
     FOUNDRY_HOST=localhost
     FOUNDRY_PORT=31415
     ```
     (These are the bridge's defaults. If your Foundry runs on a different port, use that instead.)
5. Click **Test connection**. If Foundry is running with the module enabled, it should discover the tools (get-character, search-compendium, dnd5e-create-npc, list-creatures-by-criteria, and more).
6. Set **tool trust**: leave read-only tools (searching, reading characters) trusted for convenience, and keep anything that *writes* to your world (create-actor, manage-actors, update-token) **untrusted** so it asks before changing your live game.
7. Save.

> [!warning] Order of operations matters
> Start **Foundry first** (world loaded, logged in as GM, module enabled), *then* let Gemini Scribe connect. If Foundry isn't up, Test connection will fail — that's expected, just start Foundry and retry. Config changes need the server toggled off/on (or a plugin restart) to take effect.

### Using it
Open the Gemini Scribe agent, pick the **Stat Block Generator** or **DM Math & Rules Helper**, and ask things like:
- "Find all CR 5 humanoids in my Foundry compendium."
- "Pull my character Scabs's stats from Foundry."
- "Create an NPC acolyte in my Foundry world, easy fight for level 2."

The agent will call the Foundry tools when the request needs live world data, and fall back to generating from scratch when it doesn't.

### If it won't connect
This is a chain of live services (Node, Foundry, the module, the socket), so if a link is down it won't work. Checklist:
- Is **Foundry running** with the world loaded and you logged in as **GM**?
- Is the **Foundry MCP Bridge module enabled** (and showing connected in its settings)?
- Does `node "C:\...\dist\index.js"` run in a terminal without errors?
- Is the **port** right (`FOUNDRY_PORT`) — match it to your Foundry?
- Turn on **Debug mode** in Gemini Scribe for detailed MCP logs.

**Fallback:** even with none of this, the **Stat Block Generator works on its own** and invents correct stat blocks from scratch. You only lose the "read from my existing world" part.

> [!note] What's yours to do vs mine
> I researched the exact setup and wrote these steps, but the install (git/npm), the Foundry module, the Gemini API key, and clicking through the MCP settings all happen on your machine in live apps I can't reach from here. If Test connection fails, paste me the Debug log and I'll help you read it.
