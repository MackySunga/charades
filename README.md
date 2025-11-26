# Charades Party Game (HTML / CSS / JavaScript)

A multi-screen, Christmas-themed **Charades** game designed for events and classrooms.  
Run entirely in the browser with three coordinated views:

- 🎛️ **Admin screen** – host controls rounds, timer, scores, and sounds  
- 🎭 **Player screen** – active player sees their secret words and chooses a category  
- 👀 **Audience screen** – projector view showing scores, timer, and correctly guessed words

State is synced across tabs using `localStorage` + `BroadcastChannel`, so everything stays in sync as long as all pages are opened from the same folder.

---

## ✨ Features

### Core game flow

- Up to **4 players** per game (with names editable on the Admin side)
- Each round:
  1. Admin selects the **current player** (1–4).
  2. Player chooses **one of 9 categories** on the player screen.
  3. Admin clicks **Show Player Words** to reveal **5 random words** for that player (no timer yet).
  4. Admin clicks **Start Game** to start the timer.
  5. Admin clicks on words that were guessed correctly.
  6. When time runs out or the host clicks **End Round**, the round ends and all words are revealed on the audience screen.

### Categories (player’s choice)

The player can pick from **9 different categories**, for example:

- Actions  
- Movies  
- Professions  
- Philippine Flavor  
- Animals  
- Places  
- Food & Drinks  
- Sports  
- Things at Home  

(You can edit the words and categories inside `game.js`.)

The player can **reselect a category** any time **before** the round starts (i.e., while the timer is not running).

### Scoring & words

- Each word marked as **correct** gives **+1 point** to the current player.
- Correct words are:
  - Marked as **✓ Correct** in the Admin view.
  - Highlighted for the **Player** (with a tick).
  - Shown to the **Audience** as part of the “guessed words” list.
- When **all 5 words** are marked correct in a round:
  - `all_winner.wav` plays (celebration sound).
- After the round ends:
  - The **Audience** sees **all 5 words**:
    - Correct words highlighted.
    - Missed words shown with a dim/“missed” style.
  - **No additional score** can be assigned (buttons no longer affect points once the round is inactive).

### Timing & round control

From the **Admin** screen:

- Set **round duration in seconds**.
- **Show Player Words** (no timer yet; just reveal words to the player).
- **New Words** – reroll a different set of 5 words in the same category.
- **Start Game** – start the round timer using the currently selected category and word set.
- **End Round** – stop the timer early and finish the round.
- **Reset Scores** – set all players’ scores back to 0.
- **Restart Game** – reset scores and round state, keeping player names and banner.

The **timer** is visible on Admin, Player, and Audience screens.

### Sounds & soundboard

All sounds are played from the **Admin** screen:

- `correct_star.wav` – plays every time a word is marked correct.
- `all_winner.wav` – plays automatically when all 5 words are correct in a round.

Built-in **soundboard** (buttons on Admin) to manually trigger:

- `all_winner.wav` – **All Winner**
- `audience_clap.wav` – **Audience Clap**
- `buzz_me.wav` – **Buzz Me**
- `countdown.wav` – **Countdown**
- `heartbeat.wav` – **Heartbeat**
- `wrong_buzz.wav` – **Wrong Buzz**

> ⚠️ Many browsers require at least one user interaction before audio can play, so make sure the admin clicks somewhere on the page first (like pressing a button) before relying on sounds.

### Audience splash screen & banner

On the **Admin** screen:

- Upload an event banner image (e.g., your logo or event poster).  
  This banner is displayed on both:
  - The **Audience splash screen** (pre-game)
  - The **Audience game view**

You also have manual control over the audience view:

- **Show Splash on Audience** – switch the projector to a “Welcome / Waiting” splash screen.
- **Show Game View on Audience** – show the active game (category, player name, timer, scores, words).

### Round end behaviour

When a round ends (timer hits zero **or** admin clicks **End Round**):

- Timer stops for everyone.
- Audience status shows **“ROUND ENDED”** and reveals all words.
- Player status also shows a clear “ROUND ENDED” message.
- No further scoring can happen (score buttons are effectively locked, since the round is no longer active).

### Christmas theme 🎄

The included CSS makes everything look **festive**:

- Dark red background
- Gold highlights
- Glowing timer and spotlight on the active player
- Festive styling for category buttons and cards

You can remove or adjust this theme by editing or removing the Christmas overrides at the bottom of `styles.css`.

---

## 📁 Project Structure

Typical structure:

```text
.
├── admin.html          # Control panel for host (admin)
├── audience.html       # Projector / audience-facing screen
├── player.html         # Player-facing screen with secret words
├── styles.css          # Shared styling + Christmas theme overrides
├── game.js             # Main game logic and state sync
├── correct_star.wav    # Sound when a word is marked correct
├── all_winner.wav      # Sound when all 5 words correct
├── audience_clap.wav   # Soundboard - crowd cheer
├── buzz_me.wav         # Soundboard - buzzer
├── countdown.wav       # Soundboard - countdown sound
├── heartbeat.wav       # Soundboard - tense heartbeat
└── wrong_buzz.wav      # Soundboard - wrong / error sound
