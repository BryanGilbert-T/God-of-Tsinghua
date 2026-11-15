# God of Tsinghua

**A 2D, top-down RPG shooter developed in C with Allegro 5.**

God of Tsinghua is a game project themed around National Tsing Hua University (NTHU). Players choose a character and weapon, explore tile-based stages, fight enemies, and work toward a high score. The project was developed for the **Introduction to Programming (I) final project** and extends an Allegro 5 course template with additional gameplay and interface systems.

**Tech stack:** C (C11) · Allegro 5 · Make · Xcode / desktop IDE toolchains

> **Project status:** Source code is available in this repository. The build instructions below describe the existing project setup; a clean build across operating systems has not been independently verified.

## Gameplay

- **Character selection:** Choose from four character configurations, each with different movement speed and health.
- **Weapon selection:** Use an SMG, sniper rifle, or batarang-style weapon, each with its own firing behavior and stats.
- **Mouse-aimed combat:** Aim with the cursor and shoot while navigating maps and avoiding enemy attacks.
- **Tile-based levels:** Move through maps loaded from text files, with walls, spawn points, and enemy placement.
- **Combat systems:** Projectile movement, enemy collisions, damage, knockback, and player health.
- **Progression and UI:** In-game currency, character/weapon selection screens, pause/menu controls, settings, and win/loss flows.
- **Leaderboard:** Submit a name and score to a locally stored leaderboard.
- **Audio and visuals:** Sprite rendering, animations, sound effects, and background music through Allegro add-ons.

## Controls

| Action | Input |
| --- | --- |
| Move | **W / A / S / D** (default keys) |
| Aim | **Mouse cursor** |
| Shoot | **Left mouse button** |
| Start from main menu | **Enter** or click **Play** |
| Select character / weapon | **Mouse** in the selection screen |
| Pause, settings, leaderboard | **On-screen buttons** |

Some key bindings and audio options are configurable in the game settings.

## Technical Design

The game uses a **modular, event-driven C architecture** rather than C++ classes:

- **Game loop and input:** `game.c` initializes Allegro, registers keyboard/mouse/timer events, and coordinates updates and rendering.
- **Scene management:** A `Scene` struct contains function pointers for initialization, update, rendering, and cleanup; `change_scene()` switches between game screens.
- **Gameplay entities:** Dedicated modules manage player movement, enemies, bullets, weapons, and collision handling.
- **Map system:** `map.c` loads level layouts and spawn information from files in `Assets/`.
- **UI and progression:** Separate modules implement the menu, customization, settings, loading screens, and a file-backed leaderboard.
- **Asset management:** Allegro image, font, audio, and primitive add-ons provide rendering and media support.

This project is a practical example of **C programming, data structures, function-pointer-based interfaces, real-time event handling, and modular software organization**.

## Repository Layout

```text
God-of-Tsinghua/
├── Final_Codes/          # Primary game source, Makefile, and game assets
├── Final_Codes_XCode16/  # Alternative source/project directory for Xcode 16
├── Exercises/            # Course exercises retained for reference
├── docs/                 # Allegro installation and IDE setup notes
└── README.md
```

Notable modules in `Final_Codes/` include `game.c`, `game_scene.c`, `player.c`, `enemy.c`, `bullet.c`, `weapon.c`, `map.c`, `menu_scene.c`, `costumize_scene.c`, `leaderboard.c`, and `utility.c`.

## Getting Started

### Prerequisites

- A C compiler and compatible development environment
- **Allegro 5**, including the primitives, image, font, TTF, audio, and audio-codec add-ons
- `make` for the included Makefile workflow (or a supported IDE configuration)

See the repository's [Allegro installation guide](docs/README.md) for OS-specific dependency setup instructions.

### Clone the repository

```bash
git clone https://github.com/BryanGilbert-T/God-of-Tsinghua.git
cd God-of-Tsinghua
```

### Build from source

The `Final_Codes/Makefile` defines a `game` target:

```bash
cd Final_Codes
make
./game
```

**Build caveat:** The Makefile was inherited from an earlier project setup and may require updating its source-file list and platform-specific compiler settings. Some source files use Microsoft-specific secure CRT functions, such as `strcpy_s` and `fscanf_s`, which may require compatibility changes when building with GCC/Clang outside Windows. The commands above document the intended entry point, **not a verified clean-build guarantee**.

For **Windows**, use a configured Allegro/Visual Studio environment and refer to [the setup instructions](docs/README.md#windows). For **macOS**, see the [macOS setup guide](docs/README.md#mac-os) and the `Final_Codes_XCode16/` directory where appropriate. The project has not been tested here on these configurations.

### Important: Run with assets available

The game loads relative paths such as `Assets/map0.txt`, `Assets/Minecraft.ttf`, and `Assets/audio/...`. Start the executable with `Final_Codes/` as the working directory, or otherwise ensure the `Assets/` directory is accessible from the working directory.

## Screenshots and Demo

<img width="391" height="380" alt="image" src="https://github.com/user-attachments/assets/50c6026e-66a7-41d0-9651-4bc86e08f961" />

<img width="410" height="395" alt="image" src="https://github.com/user-attachments/assets/5fb35caa-0729-48cf-b790-1229c27c31e7" />

<img width="386" height="374" alt="image" src="https://github.com/user-attachments/assets/8a280cd9-fe4c-493a-95c8-fed35eede7b9" />

More information watch it here: https://www.youtube.com/watch?v=nOXN3rpvxRA

## References

- [Allegro 5 — Official website](https://liballeg.org/)
- [Allegro 5 — Reference manual](https://liballeg.org/a5docs/trunk/)
- [Allegro installation guide in this repository](docs/README.md)
