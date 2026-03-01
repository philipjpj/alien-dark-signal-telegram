# 🛸 ALIEN: DARK SIGNAL — Telegram RPG Bot

A complete text-based RPG set in the Alien universe, designed for Telegram.

---

## ⚖️ LEGAL NOTICE & DISCLAIMER

This is a non-commercial, fan-made project created purely for educational and experimental purposes, including research and software development practice with Python and related technologies.

### Intellectual Property Disclaimer

This project is inspired by the Alien franchise.  
Alien and all related names, characters, concepts, and imagery are trademarks and intellectual property of their respective rights holders, including 20th Century Studios.

This repository is:
- not affiliated with
- not endorsed by
- not sponsored by
- and not associated with

the official rights holders in any way.

No monetization is involved. No commercial use is intended.  
This project is distributed exclusively for study, experimentation, and portfolio purposes.

---

## 🚀 QUICK SETUP

### 1. Clone / download the project
```bash
cd alien_dark_signal
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure the bot
```bash
cp .env.example .env
```
Edit `.env` and enter your **BOT_TOKEN** from [@BotFather](https://t.me/BotFather).

### 4. Run
```bash
python bot.py
```

---

## 📁 PROJECT STRUCTURE

```
alien_dark_signal/
├── bot.py                        ← Main entry point
├── config.py                     ← Global configuration
├── requirements.txt
├── .env.example
│
├── database/
│   ├── models.py                 ← Player model (SQLAlchemy)
│   └── db.py                     ← Async session management
│
├── game/
│   ├── i18n.py                   ← Localization (IT/EN/ES)
│   ├── scene_engine.py           ← Scene engine
│   ├── combat.py                 ← Combat system
│   ├── npcs.py                   ← NPCs, achievements, daily missions
│   └── scenes/
│       └── chapter1.json         ← Complete Chapter 1 (+ lore)
│
├── handlers/
│   └── main_handlers.py          ← All callbacks and commands
│
└── localization/
    ├── it.json
    ├── en.json
    └── es.json
```

---

## 🎮 GAME MECHANICS

### Character Stats (1–10)
| Stat | Usage |
|------|-------|
| Strength | Combat, physical actions |
| Intelligence | Puzzles, hacking, hidden lore |
| Stealth | Avoiding xenomorphs, infiltration |
| Engineering | Repairing, building traps |
| Endurance | HP, survival in hostile environments |
| Charisma | Convincing NPCs, leadership |
| Luck | Random modifier |
| Adaptability | Bonus in new situations |

### Available Backgrounds
- 🪖 **Colonial Marine** — Strength/Endurance
- 🔬 **W-Y Scientist** — Intelligence/Stealth
- 🔧 **Technician** — Engineering/Endurance
- 🧠 **Survivor** — Adaptability/Luck
- 🤖 **Synthetic** — Intelligence, no panic

### Psychological Traits
- 🧊 Cold and Rational
- ⚡ Instinctive and Brave
- 👁️ Paranoid
- 💗 Empathetic

### XP & Level Up System
- XP earned from scenes, brave choices, lore found, combat
- Every level (100 XP × level): +2 stat points to distribute
- Maximum level: 20

### Daily Mission
- Available every 24h
- Streak bonus for 7 consecutive days
- XP + rare items

### Permadeath (Nostromo Mode)
- Permanent death, no checkpoints
- Exclusive storylines and secret ending
- Special title: ☠️ The True Survivor

---

## 📖 STORY — ALIEN: DARK SIGNAL

**Year 2197.** Weyland-Yutani has declared the xenomorph threat extinct. A lie.

**Prometheus Station Theta** — classified Omega — has been silent for 72 hours. The player leads a rapid response team toward the truth behind **Project Architect**: hybrid xenomorphs with Engineer DNA, capable of planning, learning, and adapting.

### Chapters
1. **Theta's Silence** — Arrival, first contact, uncovering the secret
2. **The Architects** — Descent into lower levels, internal betrayal
3. **Black Code** — Secret databases, the AJAX-7 revelation
4. **The Architect Queen** — Multi-phase final boss
5. **Signal Home** — Escape, 4 alternate endings

### Main NPCs
- 🤖 **AJAX-7** — Ambiguous synthetic; loyalty depends on your choices
- 🪖 **Cpl. Sarah Chen** — Colonial Marine, protective
- 🔬 **Dr. Marcus Okafor** — Xenobiologist, accomplice?
- 🎖️ **Lt. Ray Vance** — Commander, mission-focused
- 🧬 **Dr. Petra Morel** — Survivor, knows the truth

---

## 🔧 ADDING CHAPTERS

Create `game/scenes/chapter2.json` following the same structure as `chapter1.json`:

```json
{
  "chapter": 2,
  "title": {"en": "THE ARCHITECTS", ...},
  "intro": {"en": "...", ...},
  "scenes": {
    "c2_scene1": {
      "id": "c2_scene1",
      "text": {"en": "...", "it": "...", "es": "..."},
      "choices": [...]
    }
  },
  "lore_entries": {...}
}
```

The scene engine **automatically loads** all JSON files in the `scenes/` folder.

---

## 🌐 TELEGRAM COMMANDS

| Command | Function |
|---------|----------|
| `/start` | Main menu |
| `/profilo` | Character sheet |
| `/inventario` | Owned items |
| `/archivio` | Collected lore |
| `/mappa` | ASCII station map |
| `/obiettivi` | Achievements |
| `/salva` | Manual save |

---

## ☁️ SERVER DEPLOYMENT

To run 24/7 on a VPS (e.g., Ubuntu):

```bash
# With systemd
sudo nano /etc/systemd/system/alien-bot.service
```

```ini
[Unit]
Description=Alien Dark Signal Telegram Bot
After=network.target

[Service]
Type=simple
User=ubuntu
WorkingDirectory=/home/ubuntu/alien_dark_signal
ExecStart=/usr/bin/python3 /home/ubuntu/alien_dark_signal/bot.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable alien-bot
sudo systemctl start alien-bot
```

---

## 📊 DATABASE

SQLite by default (local file `alien_dark_signal.db`).  
For PostgreSQL in production, update your `.env`:
```
DATABASE_URL=postgresql+asyncpg://user:pass@localhost/aliendb
```
And add `asyncpg` to the requirements.

---

*Weyland-Yutani Corp — "Building Better Worlds"*  