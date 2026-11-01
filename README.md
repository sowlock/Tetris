Java Tetris

A single-player Tetris-style game built in Java, with game logic developed and tested before a desktop graphical user interface (GUI) is added.

Eisenhower Matrix and MVP

- Important & Urgent — Do (Version 1.0 MVP):
  - A 10-column × 20-row board and five tetromino types: I, S, O, L, and Z.
  - Left/right movement, clockwise rotation, and collision checks.
  - Automatic downward movement and manual soft drop.
  - Piece locking, complete-row clearing, and score tracking.
  - Piece spawning, game-over detection, and restart.
  - A desktop GUI displaying the board, score, and game state, with keyboard controls.
  - Pause/resume so the player can stop and continue a session.

- Important & Not Urgent — Schedule (Version 2.0+):
  - A next-piece preview.
  - Saved local high scores.
  - Levels with increasing fall speed.
  - A ghost piece and hard drop.
  - A hold-piece feature.
  - Wall kicks for rotations near obstacles.

- Not Important & Urgent — Delegate (Use existing Java libraries):
  - Window creation, buttons, and layout using Swing.
  - Drawing colored blocks and text using AWT/Java2D.
  - Keyboard-event dispatch using Swing key bindings.
  - Scheduling GUI ticks using `javax.swing.Timer.

- Not Important & Not Urgent — Delete (Cut from this project):
  - Online multiplayer and matchmaking.
  - User accounts and cloud synchronization.
  - A 3D game engine and elaborate animations.
  - An AI player or automated solver.
  - Custom music, sound effects, and theme packs.

Exact version 1.0 behavior

- Board: 10 columns and 20 visible rows. Locked blocks are stored separately from the falling piece.
- Pieces: I, S, O, L, and Z, represented using predefined rotation states. O rotation has no visible effect.
- Selection: Choose each new piece randomly from the five types: I, S, O, L, and Z.
- Spawning: Place a new piece at a defined top-center location. If its occupied cells cannot fit, enter game over.
- Movement: Left/right moves one cell when valid. Down attempts a one-cell soft drop. Up attempts a clockwise rotation. Invalid moves and rotations leave the piece unchanged; there are no wall kicks.
- Gravity: Attempt a downward step every 700 milliseconds while running. Keep this value configurable in the code; difficulty does not increase in version 1.0.
- Locking: When a gravity or soft-drop step cannot move the piece downward, lock it immediately. There is no lock delay.
- Rows: After locking, clear all full rows at once, shift surviving rows down, and insert empty rows at the top.
- Scoring: Award 100, 300, 500, or 800 points for clearing 1, 2, 3, or 4 rows in one placement. Movement alone awards no points.
- State: Start a new game when the application opens. Support running, paused, and game-over states. Pausing stops gameplay updates; restart resets board, score, state, and active piece.
- GUI: Show the board, score, controls, and a clear paused/game-over message. Provide a restart button and keyboard shortcuts: arrows for movement/rotation, P for pause/resume, and R for restart.
- Scope: One player, offline, one session at a time. No accounts, external assets, APIs, or persistent storage are required.

MVP 

Version 1.0 is complete when a player can launch the desktop application, move and rotate falling pieces, clear rows, see the correct score, pause/resume, reach game over, and restart without relaunching. 

Tech stack

- Language: Java
- Libraries: Swing for the GUI and timer, AWT/Java2D for graphics, and Random for piece selection.
- Tools: javac, java, Git, GitHub, and a Java editor or IDE.
- Testing: A Java test runner with explicit checks and reproducible inputs.
- Storage: An in-memory board array, piece object, score, and game state; no saved sessions.
- External data: None; the game runs offline.
- Diagram: Manually create in draw.io.

Project structure and responsibilities

Tetris/
├── README.md                 # Design outline, matrix, and milestone plan
├── .gitignore
├── src/
│   └── tetris/
│       ├── Main.java         # Final GUI entry point
│       ├── model/
│       │   ├── Board.java    # Locked cells, placement checks, row clearing
│       │   ├── Tetromino.java# Five types and their rotation states
│       │   └── Piece.java    # Active type, rotation, and board position
│       ├── engine/
│       │   ├── GameEngine.java # Movement, ticks, locking, spawning, score
│       │   └── GameState.java  # RUNNING, PAUSED, GAME_OVER
│       ├── console/
│       │   └── ConsoleMain.java # Temporary, turn-based debugging driver
│       └── ui/
│           ├── GameFrame.java # Window, labels, controls, and timer
│           └── GamePanel.java # Board rendering and key bindings
├── tests/
│   └── tetris/              # Rule and state-transition checks
└── docs/
    └── Tetris.png   # Diagram export


