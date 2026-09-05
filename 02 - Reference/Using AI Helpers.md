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

**What's true right now:**
- Gemini Scribe *does* support MCP (Model Context Protocol) servers — the mechanism that would let it talk to your Foundry MCP plugin.
- But in this vault it's currently **turned off**. In the plugin's data it shows `mcpEnabled: false` with no servers configured.

**To try connecting it (you'll need to do this in Obsidian, I can't click it from here):**
1. In Gemini Scribe settings, find the **MCP** section and enable it.
2. Add your FoundryVTT MCP server. You'll need the connection details from your Foundry MCP plugin — usually a URL/port (often something like `http://localhost:PORT`) and possibly a key. Check that plugin's docs/settings for the exact address.
3. Make sure FoundryVTT is **running** and the MCP plugin is active when you try — if Foundry is closed, the connection will just fail.
4. Reconnect/restart the server in the Gemini Scribe MCP panel, then ask the Stat Block Generator something like "pull a random NPC stat block from my Foundry world."

**If it doesn't connect** (very possible — this depends entirely on your Foundry MCP plugin's setup, which I can't see or test from here):
- No problem. The **Stat Block Generator** above works fully on its own and will invent a correct stat block from scratch. You lose nothing except the "pull from my existing world" convenience.
- If you want, tell me the name/docs of the Foundry MCP plugin you installed and I can help you work out the exact connection settings.

> [!note] Why I can't just wire it up for you
> The MCP connection, the API key, and enabling these agents all happen inside Obsidian's UI and depend on live services (Gemini's API, your running Foundry). I've created every file they use and given you the exact steps, but those buttons are yours to click.
