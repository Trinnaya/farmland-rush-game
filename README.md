# Farmland Rush

A 2D top-down rescue game built in **Java Swing**. You drive a rescue van around a
farmland map, pick up injured animals, correctly diagnose them, and deliver them to
the vet —all before a 3-minute timer runs out.

![Uploading Screen Recording 2026-09-01 at 8.42.11 PM.gif…]()

## The game

There are five unwell pets on the farm, all waiting to be rescued. The player goes
around and picks them up, and for each one completes a task — filling out the pet's
name, its species, a pre-screen diagnosis, and specifying which vet it should be sent
to for cure. After that, the player takes them to the hospital. There is a time limit
of 3 minutes. Doing the tasks correctly and sending the pets to the vet successfully
completes the game.

### The five patients

Each animal hints at its problem in its speech bubble; the rescue form is only
counted as correct if all four fields match:

| Animal | Species | Diagnosis | Correct vet |
|---|---|---|---|
| Whiskers | Cow | Skin Infection | Dr. Patel (Dermatology) |
| Chirpy | Chick | Tooth Decay | Dr. Lee (Dentistry) |
| Oinky | Pig | Ankle Dislocation | Dr. Brown (Orthopedics) |
| Coco | Sheep | Food Poisonous | Dr. Jones (Toxicology) |
| Clucky | Duck | Heart Condition | Dr. Smith (ER vet, Cardiology) |

## Controls

| Input | Action |
|---|---|
| **Enter** | Start the game (on the instructions screen) / open the rescue form (when an animal is picked up) |
| **W A S D** | Drive the van up / left / down / right |
| **Mouse click** | Pick up an animal (when the van is next to it) |

The van can only travel on **grass tiles** — water and scenery block it.

## What this demonstrates

- **Object-oriented design** — responsibilities are split across focused classes:
  a start screen (`StartFrame`, `TeamFrame`), the game world and its state
  (`GamePanel`), and a separate data-entry window (`TaskFrame`). Game progress is
  tracked with encapsulated per-animal state (rescued / following / correctly
  treated), and the task window reports results back to the game through a small
  shared interface.
- **Event-driven programming** — the game runs on Swing `Timer`s (a 50 ms loop for
  van movement and a 1-second countdown), with `KeyListener` and `MouseListener`
  handling input and `ActionListener` driving the form's Submit button and dialogs.
- **GUI construction** — a custom `paintComponent` renders a sprite-based tile map
  (a 25×19 grid), plus scenery, characters, speech bubbles, and a HUD timer. The UI
  spans multiple windows and uses form controls (`JTextField`, `JRadioButton`,
  `JComboBox`, `JList`) for the rescue task.

## Project structure

```
GUI-project/
├── MainApplication.java   # entry point
├── RescuePanel.java       # the game itself
├── TaskFrame.java         # the rescue/diagnosis form
├── ui-assets/             # all sprite images (tiles, van, animals, buildings, UI)
└── .vscode/launch.json    # run configuration (sets the working directory)
```

- **`MainApplication.java`** — the entry point (`main`). Builds the start screen
  (`StartFrame`) with the title, a **Start** button, a **Team Members** button
  (opens `TeamFrame`), and **Exit**. Clicking Start launches the game.
- **`RescuePanel.java`** — the heart of the project. Its `GamePanel` draws the map
  and characters, runs the game loop, handles keyboard/mouse input, checks
  van-vs-grass collisions, manages the countdown, and computes the final score.
- **`TaskFrame.java`** — the "Rescue Task" window. Collects the player's answers
  (name, species, diagnosis, vet) and checks them against the correct values for
  that animal.
- **`ui-assets/`** — all PNG sprites: map tiles (grass, water), the van, the five
  animals, buildings and fences, flowers and trees, and UI images (menu, dialogue
  bubble, start button).

## Running it

**Requirements:** JDK 17 or newer (developed on JDK 21). No external libraries — it
uses only the built-in Java Swing/AWT toolkit.

### In VS Code (recommended)

1. **Open this folder directly**: `File → Open Folder…` → select `GUI-project`.
   (The Explorer title should read **GUI-PROJECT**.)
2. Press **F5** and choose **“Run Farmland Rush”**, or click the ▶ Run button above
   `main` in `MainApplication.java`.

> **Important:** the images are loaded with paths relative to `ui-assets/`, so the
> program must be launched with `GUI-project` as its working directory. The included
> `.vscode/launch.json` sets this automatically — just make sure you opened
> `GUI-project` itself (not a parent folder), or the sprites will render blank.

### From the terminal

```sh
# from inside the GUI-project folder
javac -d out *.java
java -cp out Project3_6581147.MainApplication
```

Run it from the `GUI-project` directory so the `ui-assets/` paths resolve.

## Team

6581147 Trinnaya Damrongpatharawat
6581053 Jinjutha Yolsirivat
6581178 Kyaw Zin Thant
6481227 Chartwut Piriyapanyaporn
6680251
 Phurilap Kitlertpaisan
