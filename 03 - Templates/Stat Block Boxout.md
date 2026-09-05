# 🧩 Stat Block Boxout (snippet)

⬅ [[03 - Templates/Templates Home|Templates Home]]

A collapsible stat block you can paste into any note. The `-` after `[!example]` makes it **start collapsed** — you see just the title and click to open it. Every line inside needs a leading `>` to stay in the box.

> [!tip] Fastest way to fill one
> Paste the block below, then ask the [[gemini-scribe/Prompts/statblock-generator|Stat Block Generator]] to fill it in — it already outputs in this exact format, so you can drop its answer straight over the placeholder.

---

Copy from here:

> [!example]- 📊 Stat Block — {Name}
> *{Size} {Type}, {Alignment}*
>
> - **Armor Class:** {AC}
> - **Hit Points:** {HP} ({dice})
> - **Speed:** {speed}
>
> | STR | DEX | CON | INT | WIS | CHA |
> |:-:|:-:|:-:|:-:|:-:|:-:|
> | {n (±)} | {n (±)} | {n (±)} | {n (±)} | {n (±)} | {n (±)} |
>
> - **Skills:** {skill +X}
> - **Senses:** {senses}, Passive Perception {n}
> - **Languages:** {languages}
> - **Challenge Rating:** {CR} ({XP}) · **Proficiency Bonus:** +{n}
>
> **Traits**
> - **{Trait}:** {what it does}
>
> **Actions**
> - **{Action}:** {+X to hit, reach/range, damage already averaged, e.g. 7 (1d8+3) slashing}

---

> [!note] Reuse across notes
> If you'll use a creature in several places, make it its own note in `02 - Reference/Stat Blocks/` and embed it with `![[Creature Name]]` wherever you need it — edit once, updates everywhere.
