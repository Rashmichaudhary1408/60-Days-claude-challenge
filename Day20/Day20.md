# Day 20: Build an AI Face Puzzle Game

**Turn your face into an interactive puzzle game.**

Today's project is a browser game that takes a photo of you from your webcam, slices it into tiles, scrambles them, and challenges you to put your face back together as fast as possible. It was built with an AI-assisted workflow: I wrote a detailed prompt, had an AI model generate the complete app, then tested and refined it myself.

---

## What I Built

**Face Shuffle** is a single-file web game (`face-puzzle.html`) with no frameworks and no external dependencies.

1. Open the page and allow webcam access.
2. Take a photo of your face.
3. Pick a difficulty: 3×3, 4×4, or 5×5.
4. Drag pieces onto each other to swap them.
5. Beat the clock and see your name on the leaderboard.

---

## Features

| Area | Details |
|------|---------|
| Camera | Webcam access with `getUserMedia()`, front camera preferred, live mirrored preview, snapshot to canvas |
| Fallback | If camera permission is denied or unavailable, a clear message appears and you can upload a photo instead |
| Puzzle | Photo is cropped to a square and sliced into equal pieces; the shuffle is always solvable |
| Controls | Mouse drag on desktop and touch drag on mobile (Pointer Events); dropping a piece on another swaps them; pieces snap to the nearest cell |
| Feedback | Pink border while dragging, green border when a piece is in its correct cell |
| Stats | Live timer in `mm:ss.t`, move counter, and "correctly placed / total" counter |
| Win | Automatic detection, timer stops instantly, results overlay with time, moves and difficulty |
| Leaderboard | Top 5 best times saved in `localStorage` with date, time, moves and grid size |
| Buttons | Take Photo, Retake Photo, Play Again, New Photo, Reshuffle |
| Extras | Hold-to-peek button to preview the finished photo, confetti on win, reduced-motion support |

---

## How to Run

You need a modern browser (Chrome, Firefox, or Safari) and a webcam.

**Option 1: open the file directly**

Download `face-puzzle.html` and double-click it. Most browsers allow camera access for local files.

**Option 2: run a local server (most reliable)**

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000/face-puzzle.html`.

> The camera API only works over **HTTPS or localhost**. If you host the game, use GitHub Pages (which serves over HTTPS).

---

## How It Works

### 1. Capturing the photo
The video stream plays in a `<video>` element. When you press **Take Photo**, the centre square of the current frame is drawn onto a `<canvas>`, mirrored so it matches the preview, and exported as a JPEG data URL.

### 2. Slicing without cutting
Rather than creating separate images, each tile is a `div` that uses the full photo as its background. With `background-size` set to `n × 100%` and a computed `background-position`, each tile shows exactly its own slice of the face.

### 3. A shuffle that is always solvable
Because moves in this game are **swaps of any two pieces**, every possible arrangement can be reached and undone. That means any permutation is solvable. The shuffle uses Fisher–Yates and repeats if the result happens to be already solved.

> Note: this differs from the classic sliding 15-puzzle, where only half of all arrangements are solvable.

### 4. One input system for mouse and touch
The game uses **Pointer Events** (`pointerdown`, `pointermove`, `pointerup`) with `touch-action: none` on the board. One code path handles mouse, finger, and stylus. On release, the pointer position is converted to a row and column to find the drop cell, then the two pieces swap.

### 5. Win detection and scoring
After every move the game counts pieces whose position matches their index. When the count equals the total, the timer stops, the result is added to the `localStorage` list, the list is sorted by time, and the top 5 are kept.

---

## Tech Stack

- HTML5, CSS3, vanilla JavaScript (ES5-style, no build step)
- `MediaDevices.getUserMedia()` for the camera
- Canvas API for capturing and cropping
- Pointer Events for drag and touch
- `localStorage` for the leaderboard

---

## Challenges and Lessons

- **Camera permissions are strict.** Browsers require a secure context, and users can deny access. Planning a graceful fallback (upload a photo) made the app much more usable.
- **Mirroring matters.** A webcam preview is mirrored, so the saved photo had to be mirrored too, or the puzzle would look reversed.
- **Safari quirks.** The video element needs `playsinline` and `muted` for the stream to play inline on iOS.
- **Pointer Events beat separate mouse and touch handlers.** Less code, fewer bugs, and the same behavior everywhere.
- **Good prompts get good code.** A numbered feature list with clear technical requirements produced a complete, working first version.

---

## Prompt Used

The game was generated from a prompt asking for a complete single-file HTML app with: camera access, puzzle generation at three difficulties, mouse and touch drag-and-drop with swapping and snapping, a live timer and move counter, win detection with a results screen and top-5 leaderboard, and a responsive, modern UI. It also required no frameworks, graceful handling of denied camera permission, and no placeholder comments.

---

## Screenshots

Add your own screenshots to a `screenshots/` folder and update the file names below.

| Camera | Choose difficulty |
|--------|-------------------|
| ![Camera preview](screenshots/01-camera.png) | ![Difficulty](screenshots/02-difficulty.png) |

| Gameplay | Results and leaderboard |
|----------|-------------------------|
| ![Gameplay](screenshots/03-gameplay.png) | ![Results](screenshots/04-results.png) |

---

## Ideas for Next Time

- Pick between several shuffle styles, such as a sliding-tile mode
- Add sound effects and a "best time" ribbon
- Face detection to auto-centre the crop on your face
- Share your result as an image
- Daily challenge with a shared seed

---

## Project Structure

```
day20/
├── face-puzzle.html
├── screenshots/
└── day20.md
```

---

**Day 20 complete.** Built, tested, and shipped a game that uses your own face as the board.