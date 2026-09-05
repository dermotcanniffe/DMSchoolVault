# ⚔️ Combat & Encounter Math

⬅ [[02 - Reference/Reference Home|Reference Home]]

Combat is just the [[02 - Reference/Dice and Rolls|roll + bonus ≥ target]] pattern, repeated in a set order. Here's the order and the targets, with the math handled for you.

## The turn order (a round)
1. **Roll initiative** at the start: everyone rolls d20 + their Dexterity modifier. Highest goes first. (Let players add their own; you just sort the numbers high → low.)
2. On their turn each creature can usually: **move**, take **one action** (attack, cast, dash, help...), and maybe a **bonus action**.
3. Go down the initiative order, then start again at the top. That's a "round" (6 seconds in-game).

> [!tip] Tracking initiative without stress
> Write names top-to-bottom on paper or a whiteboard as people call out numbers, highest first. No adding on your part.

## Attacking (the one repeated check)
> Attacker rolls **d20 + attack bonus**. If it's **≥ the target's AC**, it hits.

- **AC = Armor Class** = how hard someone is to hit. It's a single number on the sheet.
- On a hit, roll the weapon/spell's **damage dice** and subtract from the target's **hit points (HP)**.
- At **0 HP** a monster is down. (Players go unconscious and make death saves — a d20, 10+ is a success, three successes stabilize, three failures is death.)

**Critical hit:** a natural 20 always hits and you roll the damage dice **twice** (then add the bonus once). No extra math beyond rolling more dice.

## "Is this fight fair?" — the simple version
The official encounter-balancing math is genuinely fiddly. Skip it. Use this rule-of-thumb table instead, then adjust by feel:

| You want the fight to be... | Rough guide for a party of 4 |
|-----------------------------|------------------------------|
| Easy warm-up | enemies' total is weak; party wins comfortably |
| A fair challenge | roughly **one "solid" enemy per player** at a matching level |
| Scary / risky | add an extra enemy, or make one clearly tougher |
| Deadly (use rarely) | outnumber or out-power the party noticeably |

> [!tip] Let a tool do the real math
> If you want proper balance numbers, don't compute them by hand — use an encounter builder (e.g. the free **Kobold Fight Club / Koboldplus** site) or ask the [[02 - Reference/Using AI Helpers|AI helper]]: "Is [these monsters] a fair fight for 4 level-3 characters?" It'll tell you and suggest tweaks.

## Fastest ways to reduce table math
- **Average damage:** instead of rolling, monsters can just deal the average number printed on their stat block. One less roll and add.
- **Group weak enemies:** roll one attack for a swarm, or say "three goblins, two hit."
- **Round HP down** to easy numbers (a "27 HP" ogre can just be 25). Nobody notices.
- **Hand players the adding:** they total their own attack and damage; you only listen for the final number and compare to AC/HP.
