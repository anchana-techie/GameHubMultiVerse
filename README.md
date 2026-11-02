# 🎮 Game Hub

A single-file (`index.html`) browser game hub for playing with friends online. No server or build step – just open the file. Optional **invite-only accounts with an admin dashboard** (Firebase) can be switched on – see [FIREBASE_SETUP.md](FIREBASE_SETUP.md). Architecture and documentation: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Games

### 🎯 Number Game
Guess a secret number in turns.
- **N** = how many digits are correct (anywhere), **P** = how many are in the correct position.
- Faster win = more points (`11 − attempts`, minimum 3).
- Guess History is shown as a table (Name / Number / Position).
- Personal colouring panel and a scratchpad (pen, eraser, undo, clear) for your notes.
- Settings: rounds, difficulty (3/4/5 digits), time per guess, max guesses.

### 🕵️ Who Is the Spy?
3–15 players. Everyone gets a secret word on their own screen; the spy's word is different (or missing). **The spy is always told they're the spy.**
- At the start of each round a full-page **secret-role screen** says "You are a Civilian / a Spy – your word is …" (Raja Rani: "You are the 👑 King" etc.). Press *I'm ready* or wait ~8 s.
- Players give clues in order (person 1, 2, 3 …) and keep cycling. Clues appear in a **chat on the right** (avatar + name + clue); a **clue sheet** of chips, grouped by round and in turn order, sits on the left.
- Anyone who suspects the spy presses **🗳️ Voting Needed** – all active players vote; most votes is out.
  - **Spy caught** → round over, civilians win.
  - **Civilian voted out** → eliminated (can't give clues or vote), play continues. The spy wins when civilians left ≤ spies left (2 players left with 1 spy).
  - **Tie / no votes** → nobody is out.
- Scoring: catch the spy = +2 per civilian, +1 extra for each civilian who voted for the spy; spy wins = +3 for the spy.
- Settings: rounds, clue time, voting time, number of spies, spy word mode, random/custom words.

### 👑 Raja Rani
3–20 players. Secret roles are dealt; the Police must find the Thief. A wrong guess hands the Police's points to the Thief.
- Settings: rounds, time for the Police to guess.

### 🎨 Scribblio (draw & guess)
2–12 players, room based. Each turn one player gets a secret word and draws it; everyone else guesses in the chat.
- **Layout:** players on the left (rank, points, and a ✏️ next to the emoji of whoever is drawing), the canvas in the middle, the chat on the right.
- **Blanks & letter count:** guessers see the word as `_ _ _ _ _` with the number of letters next to it (multi-word answers show one count per word).
- **Letter hints:** after ⅓ of the drawing time one letter appears in its position (`_ _ a _ _`), after ⅔ a second one (`_ _ a _ b`). Short words never get fully revealed.
- **Guessing:** type guesses in the chat. A correct guess is announced without showing the word and turns that player green; players who already guessed can chat privately with the drawer. A near-miss gets a private "very close!" nudge.
- **Scoring:** a guesser earns 100–500 points depending on how much time was left; the drawer earns the average of what the guessers earned. The turn ends early when everybody has guessed. Everyone draws once per round.
- **Drawer tools:** 12 colours, 4 brush sizes, eraser, undo, clear.
- **Settings:** rounds, drawing time (30 sec – 3 min), one random word or pick from 3, letter hints on/off, built-in words or your own comma-separated list.
- If the drawer leaves or stays offline for 8 seconds the turn is skipped. A player who refreshes mid-turn gets the drawing back.

### ♟️ Chess (2–4 seats, computer fills empty seats)
The **host chooses the number of players** (2, 3 or 4). Seats nobody joins are played by the **computer** (Easy / Medium / Hard) – e.g. host picks 4 and only 3 people join, the 4th seat is a computer.
- **2 seats** – classic chess: castling, en passant, promotion (choose the piece), stalemate, insufficient material, 50-move and threefold-repetition draws, resign and offer/accept draw. Alone you can play the computer (choose your colour) or pass-and-play.
- **3 seats** – hexagon board (96 squares, files A–L, ranks 1–12; White → Black → Red, clockwise). Bishops, queens and kings may pass through the centre point. **Last king standing wins**; a checkmated (or stalemated) player is out and their pieces are removed. Pawns promote at the end of their file; no en passant.
- **4 seats** – cross board (Yellow → Blue → Red → Green). **Points:** pawn 1, knight 3, bishop 5, rook 5, queen 9 (promoted queen 1), checkmate +20, stalemated player +20. Out players' pieces turn grey and stay as obstacles (capturable for 0). Highest score wins when one player is left or the game is drawn. Pawns promote to a queen on rank 8.
- Round points: 2P win 2 / draw 1; 3P 3 / 1 / 0 by finishing order; 4P = points scored; computers never score.
- Settings: rounds, number of players, computer strength, pass-and-play (2 seats, alone), your colour, random or rotating seats, clock (1–30 min) + increment, legal-move hints.
- **Controls:** click a piece, then a highlighted square – or **drag and drop** it (touch works too). 🔄 rotates your view.
- **Look:** a big, centred board in the hub's space theme with neon piece colours. **All players' timers sit in one row above the board**; the moves list is below it. The last move's start and end squares stay **yellow**. When it is your turn an **astronaut pops up in the bottom-left corner holding a flag: "It is your turn ! ♟️"** and keeps popping until you move.
- A player who leaves, is kicked, or is offline for 60 s on their turn is **out: their pieces are removed from the board** (they fade away) and the others carry on – on the 2-player board the opponent wins. A see-through airlock cutscene plays on top, so everyone can still see the board. Once fewer than 2 humans are left (in a game that started with several), everyone sees "Less players than required" and goes back to the room. Running out of time loses.

### 🎲 Dots and Boxes
2–20 players, room based. A grid of dots; on your turn you **roll the dice** and may draw **that many lines** between neighbouring dots. The line that closes a box claims it – the box is tinted in your colour and **your emoji is stamped inside**. Every player gets a **different emoji** (your avatar if nobody else has it, otherwise a free one). The round ends when every box is taken; 1 box = 1 point.
- Tap a line between two dots to draw it. Your lines are coloured with your colour; the latest line glows.
- Players and their box counts are shown above the board; the dice tumble for everyone when someone rolls.
- Settings: rounds, dots across (3–10), dots down (3–10), 1 or 2 dice, optional **bonus line for closing a box**, time to roll and to draw (a turn that times out is skipped).
- **Play again:** after the last round the host presses **New game – same room, scores carry on**; the series total keeps adding up.
- A player who leaves forfeits their remaining turns (their boxes stay on the board); the game stops if fewer than 2 players are left. Needs internet (online rooms only).

### 🏁 Ludo
Up to **6 players**, room based (also playable alone against the computer, offline). Classic rules: roll a **6** to bring a token out, travel once round the ring, go up your home column and finish with an exact roll. Land on a lone opponent to send their token back to the yard; start squares and ★ squares are safe. A 6, a capture or a token home gives another roll; three 6s in a row lose the turn. Finishing order scores points.
- **Settings (host):** rounds, **board** (4-colour for up to 4 players, 6-colour for up to 6), **colours nobody sits on** – *played by the computer* or *left empty* (so 2 people can play on the 4-colour board with 2 computers, or on their own), computer strength, time per roll/move (when it runs out the game plays for you).
- Captures play a burst animation on the square. A player who leaves or is kicked is **out and their tokens vanish** (a see-through airlock scene plays over the board, so the game stays visible).

### ✊ Rock Paper Scissors
Everyone throws ✊ ✋ ✌️ in secret; all throws are revealed together. **2 players** (or you vs the computer): first to 1–4 throw wins takes the round. **3+ players**: the throws that lose knock their players out until one is left; all three signs (or only one) is a draw and everyone throws again. Settings: rounds, computer players (a lone player always gets one), throw target, time to choose. Works offline against the computer.

### 🎄 ChristMom ChristChild / 🪔 Diwali Daddy Diwali Kid
Secret-Santa style draws. Names and emails are entered, a random matching (nobody gets themselves) is made, and each person is emailed their match. Pairs are never shown on screen.

## Kicking players & too few players
- The **host** sees a ✖ next to every other player (room header, Scribblio player list, chess seat cards) – in the lobby and **during a game**. A kicked player is sent home with a message, the others see an airlock scene, and the kicked player can join again with the room code (from the lobby).
- If someone leaves or is kicked mid-game and the game no longer has enough players (Spy 3, Raja Rani 3, Scribblio 2), everyone sees an ejection-style **"Less players than required – taking you to the room"** scene and is returned to the room lobby. Chess hands the leaver's seat to the computer and stops once fewer than 2 humans are left.

## Look & feel
The whole hub has a space theme: a twinkling starfield behind every screen, and on the home page a spinning Saturn with tilted rings, a rotating Earth with the Moon orbiting it, a rocket, a UFO, shooting stars, and astronauts hopping on the lunar surface around a planted flag. The game cards are glass panels that glow in each game's colour on hover. All motion is switched off automatically for visitors who have "reduce motion" enabled in their system settings.

## How to play online
1. Open `index.html` (host it on any static host, e.g. GitHub Pages, Netlify, or open locally).
2. Pick a game, enter your name and avatar, and **Create room**.
3. Share the **room code** or **Invite link** with friends. They open the page and **Join room**.
4. In the lobby the host changes the room settings and presses **Start game**.

### Host controls
- **⏹ Exit game (keep room)** – leave the running game and return to the lobby; everyone stays in the room and the host can change settings.
- **✖ Close room** – closes the room for everyone (asks for confirmation).
- **🚪 Leave room** (guests) – asks for confirmation, then removes you from the room.
- Players who disconnect can rejoin with the room code while the room is open.

## Technical notes
- Online play uses [PeerJS](https://peerjs.com) (WebRTC). The **host's browser acts as the server** – the host must keep the tab open and in front. Secret words/roles are only sent to the player they belong to.
- If friends can't connect (e.g. mobile data vs Wi-Fi, strict firewalls), use **Connection help** on the entry screen to add a free TURN relay (e.g. from metered.ca). Everyone in the room should enter the same details.
- The email games use [EmailJS](https://www.emailjs.com). Enter your Service ID, Template ID and Public key in the email settings. In your EmailJS template set **To Email** to `{{to_email}}` and put `{{{message_html}}}` (three braces) in the body.
- Pop-ups (confirmations and notifications) live in their own layer above the page, so they always respond to clicks, the Esc key and clicks on the dark backdrop.
- Scribblio drawing strokes are sent as small batches straight to the host and relayed to everyone; they are not part of the full game-state update, which keeps drawing smooth.
- Names, rosters and settings are stored in your browser (localStorage) only.
- Online rooms and the email games need an internet connection (PeerJS and EmailJS). Chess and the Number Game also run fully offline on one device – see **Offline mode** below.

## 🚀 Ejection cutscene
Whenever someone is voted out, exposed or eliminated, **every player's screen** plays a full-page, Among-Us-style scene (~8 s): alarm lights, the airlock opens and the astronaut (in the player's suit colour, with their emoji on the visor) tumbles out into space while the verdict types onto the screen. It has synthesised sound (🔊 toggle, remembered), and can be skipped with **Skip**, Esc, Enter or Space. Results, balloons and the next screen appear afterwards. With "reduce motion" enabled a calmer version plays.
- **Who Is the Spy?** – a tie or no votes: an empty airlock, "No one was ejected." Voted-out civilian: "*Name was not the Spy.* The Spy is still among you…"; if that hands the Spy the win, the scene ends with "*… was the Spy all along – the Spy wins!*". Spy caught: "*Name was the Spy.* The Civilians win!"
- **Raja Rani** – on reveal: Thief caught → "*Name was the Thief!* 🦹"; wrong guess → "*Name was not the Thief.* They were the 👸 Queen… the real Thief slips away with the Police's points"; Police out of time → an empty airlock, "No one was ejected."
- **Chess 3P / 4P** – each checkmated / stalemated / timed-out / resigned / departed player is ejected (their colour on the suit). The next player's clock starts after the scene.

## 📡 System pages
| Page | Where it appears |
|---|---|
| **Loading** | Start-up (loads the multiplayer engine with a fallback CDN, fonts), and while creating / joining a room (with Cancel). |
| **No internet** | When the browser goes offline (auto-hides when back). Buttons: Try again · Offline mode · Continue anyway. |
| **Offline mode** | Explains what works without internet and lets you start those games (`#/offline-mode`, or the home-page card). |
| **404** | Unknown in-app route (e.g. `#/whatever`) and, as `404.html`, any missing address on static hosts. |
| **Error** | Uncaught errors, a game that crashes while running, or a library that fails to load. Reload · Back to the hub · Try to continue · copy technical details. |

**Offline mode:** ♟️ Chess (vs computer or pass & play) and 🎯 Number Game (solo) run on one device with no internet (an "offline room" – the host engine runs locally, no PeerJS). Spy, Raja Rani, Scribblio, online rooms and the e-mail draws need internet. Over https (or localhost) a service worker (`sw.js`) saves the hub after the first visit so it opens offline too; opened as a plain file it already works offline.

Preview any page: `#/loading`, `#/error`, `#/no-internet`, `#/404`, `#/offline-mode`.

## Files
- `index.html` – the entire app (HTML, CSS and JavaScript).
- `404.html` – standalone "page not found" page for static hosts (GitHub Pages, Netlify, …).
- `offline.html` – fallback shown by the service worker if the hub can't open and isn't saved yet.
- `sw.js` – service worker for offline use (keep next to `index.html`).
- `README.md` – this file.
- `firebase-config.js`, `firestore.rules`, `FIREBASE_SETUP.md` – optional accounts, invites and admin view (Firebase).
- `docs/ARCHITECTURE.md`, `docs/architecture.svg` – architecture diagram and documentation.
