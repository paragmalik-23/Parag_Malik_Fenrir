# PixelVault: Online Gaming Platform (Developer Specification & Verification Guide)

## 1. Project Overview

### 1.1 Summary
PixelVault is a simple online gaming website. The site runs in any web browser and contains three simple games: Rock Paper Scissors, Flappy Bird, and Word Scramble. These games open and play in popup windows (modals). The website tracks user scores and total games played. It saves these scores on the user's computer using the browser's localStorage. The website is built using standard HTML, CSS, and JavaScript.

### 1.2 Core Deliverables
The developer must deliver these files inside a folder named `PixelVault/`:
1. `index.html`: The layout of the website using semantic HTML tags.
2. `styles.css`: The styling sheet containing the color variables, mobile layouts, and card hover effects.
3. `app.js`: Main JavaScript file to manage the layout, popup windows, mute settings, and statistics updates.
4. `games.js`: JavaScript file containing the logic for the three games.
5. `README.md`: Text documentation explaining how to open the site, check the games, and list file license sources.
6. `assets/`: Folder holding the brand images and audio files:
   * `assets/images/logo.svg`: Brand logo.
   * `assets/images/rps_card.png`: Cover card image for Rock Paper Scissors.
   * `assets/images/bird_card.png`: Cover card image for Flappy Bird.
   * `assets/images/word_card.png`: Cover card image for Word Scramble.
   * `assets/audio/click.mp3`: Click sound for buttons and cards.
   * `assets/audio/score.mp3`: Sound played when points are scored or choices are made.
   * `assets/audio/gameover.mp3`: Sound played when a game ends.
   * `assets/audio/cyber_beats.mp3`: Loop background music track.

### 1.3 Target Audience
* **Audience:** Casual players looking for quick games in a web browser without creating accounts.
* **Goals:** Fast loading times, clear button hovers, sound feedback, and persistent scores that stay saved when reloading the page.

---

## 2. Layout Structure & UI Architecture

The page is a single-page layout with five parts:

### 2.1 Navigation Bar (Header)
A structural header fixed at the top of the page:
* **Brand Logo:** The name `PixelVault` in bold Orbitron font with a neon gold shadow glow.
* **Anchor Links:** Menu buttons pointing to the Catalog grid and the Stats dashboard.
* **Global Sound Toggle:** An interactive speaker button to turn the background music and sound effects on or off.

### 2.2 Hero Banner
The introduction area at the top of the viewport:
* **Main Slogan:** Bold gaming text in Orbitron font.
* **CTA Button:** Highlighted button that scrolls the page down to the games catalog.
* **Welcome Message:** Dynamic text greeting return users (e.g., "Welcome back, Player! Ready to beat your Flappy Bird high score of 150?"). If no stats are saved, it shows "Welcome to PixelVault, Guest!".

### 2.3 Games Selection Catalog
A grid layout displaying three game cards. Cards feature:
* Dark card background surfaces matching Gunmetal.
* Game cover PNG cards.
* List of current local scores (wins or high score).
* Card scale-up animation and gold glow outlines on hover.
* "Play Now" action buttons that open the gameplay popup.

### 2.4 Statistics Dashboard
A section rendering saved localStorage data:
* Header reading "VAULT PERSISTENT CORE" in Orbitron font.
* Columns displaying: Total Games Played, Rock Paper Scissors wins, Flappy Bird high score, and Word Scramble correct words count.
* **Reset Stats Button:** Triggers a confirmation check, deletes user statistics from localStorage, and updates all numbers on the page to 0 immediately.

### 2.5 Footer Section
The bottom section containing copyright details, author name, and brand closing line: *Play instantly, challenge your limits on PixelVault.*

---

## 3. Brand Identity & Design Tokens

Developers must use only the tokens defined below.

### 3.1 Color Tokens Palette
* **Background Surface (Obsidian Space):** HEX #0F0F10 (Primary background).
* **Card Fills & Borders (Gunmetal):** HEX #2A2B30 (Card panels, borders, and outlines).
* **Neon Accent (Retro Gold):** HEX #FFC107 (Active buttons, focus borders, glow text, active lines).
* **Secondary Brand Accent (Neon Purple):** HEX #9C27B0 (Subheadings, passive text links, passive outlines).

### 3.2 Typography Tokens
* **Titles, Headers, Logos, and Score Counters:** Orbitron (Google Fonts).
* **Content Copy, Metrics, and Lists:** Inter (Google Fonts).

### 3.3 Visual Motion
* Card hover scale-up: `transform: scale(1.03)` with a smooth 0.3-second transition.
* Modal popups: Smooth opacity transition from hidden to visible over 0.25 seconds.
* Active buttons: Press down scale effect (`transform: scale(0.97)`) on click.

---

## 4. Gameplay Logic & Engines

### 4.1 Rock Paper Scissors
* **Buttons:** Choice selections for Rock, Paper, and Scissors.
* **Computer Choice:** Selected randomly on every turn.
* **Game Mechanics:** Compares user choice and computer choice to determine victory, defeat, or tie outcome. Updates score panel and stats immediately.

### 4.2 Flappy Bird
* **Board:** HTML5 canvas element size 400x400.
* **Controls:** Spacebar or mouse click makes the bird jump up.
* **Speed:** Starts at a standard scroll velocity. The movement speed increases by 5% every time 5 obstacles are cleared.
* **Game Over:** Triggers when the bird hits canvas boundaries (floor/ceiling) or collides with obstacle pipes. Plays `gameover.mp3`.

### 4.3 Word Scramble
* **Scramble:** Scrambles letters of a selected word on start.
* **Guesser:** User types answer guess in input field and hits submit.
* **Matching:** Correct guess plays `score.mp3` and loads next word. Incorrect guess plays click sound. Hint button displays the first letter of the word.

---

## 5. Persistence & localStorage Configuration

All scores must be stored under the localStorage key name `pixelvault_stats`.

### 5.1 JSON Storage Schema
```json
{
  "total_games_played": 15,
  "games": {
    "rps": {
      "played": 5,
      "wins": 3,
      "losses": 1,
      "ties": 1,
      "high_score": 3
    },
    "flappy": {
      "played": 6,
      "wins": 0,
      "losses": 6,
      "ties": 0,
      "high_score": 142
    },
    "scramble": {
      "played": 4,
      "wins": 2,
      "losses": 2,
      "ties": 0,
      "high_score": 12
    }
  }
}
```

---

## 6. Technical Quality & Acceptance Criteria

### 6.1 DOM & Code Organization
* Separation of concerns: JavaScript controls UI events (`app.js`) and game engines (`games.js`) separately.
* Separation of HTML/JS: No inline handlers inside index.html (no `onclick`). Binds listeners dynamically.
* Framework limits: No external framework scripts (React, Vue, jQuery) can be imported.

### 6.2 Layout Breakdown
* **Mobile (<576px):** Single-column grid cards list, navbar items wrap.
* **Tablet (576px - 992px):** Two-column cards grid layout.
* **Desktop (>992px):** Three-column horizontal cards grid.

### 6.3 Sound Level & Routing
* Looped background music played at low volume.
* SFX played at standard volume.
* Navbar toggle button mutes all audio elements instantly.

---

## 7. Quality Assurance Checklist

Verify execution against these checklist items before submission:
1. Double-clicking `index.html` locally loads the entire page and navbar with zero console errors.
2. Clicking navbar links smooth-scrolls to target blocks.
3. Resizing viewport to 360px width causes no layout clipping or horizontal scrolls.
4. Rock Paper Scissors correctly declares game outcomes and counts player wins.
5. Canvas Flappy Bird registers jump inputs and pipe collisions trigger game over.
6. Word Scramble scrambles letters on start and registers correct answers.
7. Statistics dashboard updating is persistent and updates on live completions without manual reload.
8. Mute toggle terminates looped music tracks and silences SFX immediately.
9. Wiping stats clears local storage and updates numbers on screen instantly.
