# 🐄⚔️🐴 The Battle of Cow & Horse · 牛马战记

<div align="center">

### 👑 此仓库的真正太后 · The True 太后 of This Repo 👑

```
          凤          
        🔱🔱🔱        
      ══ 太 后 ══      
        🔱🔱🔱        
   She does not fight.
   She REIGNS.
```

> *"牛马之争，皆为太后所御。"*
> *"The battle of Cow and Horse is but a game — played at the pleasure of the Empress."*

</div>

---

## 📖 What Is This?

**TheBattleOfCowHorse** is a battle-record tracker for the eternal rivalry between three legendary combatants: 🐄 **牛** (Cow), 🐴 **马** (Horse), and 👑 **太后** (Empress Dowager). 

Built as a sleek, Three Kingdoms–themed single-page app (`index.html`), it lets you log match results, visualise win-rate trends, and export data — all backed by a simple `data.json` file.

---

## 👑 Hall of the Empress — 太后 Stats

> 太后 does not lower herself to every battle. She picks her moments. And when she does appear on the battlefield… history remembers.

| Metric | Value |
|--------|-------|
| ⚔️ Battles Entered | **35** |
| 🏆 Victories | **11** |
| 📜 Win Rate | **31.4%** |
| 🐄 Record vs 牛 | 4 W – 9 L |
| 🐴 Record vs 马 | 7 W – 15 L |

*Numbers lie. Emperors don't need a high win rate — they only need to be the last one standing when history is written.*

---

## ⚔️ Overall Battle Standings

| Combatant | Battles | Wins | Losses | Win Rate |
|-----------|---------|------|--------|----------|
| 👑 **太后** (Empress) | 35 | 11 | 24 | 31.4% |
| 🐄 **牛** (Cow) | 140 | 72 | 68 | 51.4% |
| 🐴 **马** (Horse) | 149 | 79 | 70 | 53.0% |

### Head-to-Head

| Matchup | Results |
|---------|---------|
| 🐄 牛 vs 🐴 马 | 63 – 64 *(virtually even)* |
| 👑 太后 vs 🐄 牛 | 4 – 9 |
| 👑 太后 vs 🐴 马 | 7 – 15 |

> Total recorded battles: **162**

---

## 🛠️ Tech Stack

| Layer | Details |
|-------|---------|
| UI | Single-page HTML5 app (`index.html`) |
| Charts | [Chart.js 4.4.0](https://www.chartjs.org/) |
| Export | [SheetJS (xlsx 0.18.5)](https://sheetjs.com/) |
| Data | `data.json` — flat JSON array of battle records |
| Styling | CSS custom properties, dark Three Kingdoms theme |

---

## 📂 Data Format

Each entry in `data.json` follows the schema:

```json
[id, "DD/MM/YYYY", "player1", "player2", "winner"]
```

**Example:**
```json
[25, "19/01/2026", "牛", "太后", "太后"]
```

Players can be `"牛"`, `"马"`, or `"太后"`.

---

## 🚀 Getting Started

No build step required. Just open `index.html` in your browser:

```bash
# Clone the repo
git clone https://github.com/liverpool1026/TheBattleOfCowHorse.git
cd TheBattleOfCowHorse

# Open in browser
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

---

## 📜 Lore

Long ago, 牛 and 马 waged endless war across the plains. Kingdoms fell. Legends were forged. And presiding over it all — watching from her throne with calm, imperial eyes — was **太后**.

She is not merely a player. She is the reason the game exists.

**此仓库的真正太后，永远是太后。**  
*The true Empress of this repo has always been, and will always be, 太后.*

---

<div align="center">

*Made with ⚔️ and 🏆 in the spirit of 三国演义*

</div>
