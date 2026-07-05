# Inkball

A Java desktop puzzle game inspired by Inkball, built with Gradle and the Processing graphics library. Players draw temporary lines to redirect moving balls into matching colored holes while managing time, score, obstacles, spawners, and level-specific rules.

## Features

- Mouse-drawn collision lines that reflect moving balls.
- Color-matching hole capture with score rewards and penalties.
- Multiple levels loaded from text layout files.
- JSON-driven level configuration for timers, spawn intervals, ball queues, and score modifiers.
- Spawners that release balls over time.
- Colored walls that bounce balls and can recolor them.
- Acceleration tiles that change ball velocity.
- Hole attraction behavior that pulls nearby balls inward.
- Pause, restart, timer, score display, and end-of-level handling.
- Unit test coverage for core game entities and configuration logic.

## Tech Stack

- Java
- Gradle
- Processing Core
- JUnit 5
- Mockito
- JaCoCo

## Project Structure

| Path | Purpose |
| --- | --- |
| `src/main/java/inkball/App.java` | Main Processing application, game loop, input handling, score, timer, level flow, and rendering. |
| `src/main/java/inkball/Level.java` | Loads layouts, owns level entities, updates collisions, handles scoring, and manages level completion. |
| `src/main/java/inkball/Ball.java` | Moving ball entity with velocity, color, radius, and rendering behavior. |
| `src/main/java/inkball/PlayerDrawnLine.java` | Player-created line segments, line deletion, and ball reflection logic. |
| `src/main/java/inkball/Wall.java` | Wall collision and ball recoloring behavior. |
| `src/main/java/inkball/Hole.java` | Hole attraction, capture validation, score changes, and ball reset behavior. |
| `src/main/java/inkball/AccelerateTile.java` | Directional acceleration tiles. |
| `src/main/java/inkball/ConfigReader.java` | Reads JSON level and scoring configuration. |
| `src/main/resources/inkball/` | Game sprites for balls, holes, walls, tiles, spawners, and acceleration tiles. |
| `src/test/java/inkball/` | Unit tests for gameplay classes. |
| `config.json` | Level sequence, timers, spawn intervals, ball queues, and score modifiers. |
| `level1.txt`, `level2.txt`, `level3.txt` | Text-based level layouts. |

## Requirements

- Java 17 or later recommended
- Gradle wrapper included, so a local Gradle installation is not required

## Run

Clone the repository:

```bash
git clone https://github.com/fanwy16/Inkball.git
cd Inkball
```

Start the game:

```bash
./gradlew run
```

On Windows:

```bash
gradlew.bat run
```

## Controls

| Action | Control |
| --- | --- |
| Draw a line | Left click and drag |
| Remove a line | Right click near the line |
| Remove a line alternative | `Ctrl` + left click |
| Pause or resume | Space |
| Restart current level | `R` |
| Restart after game end | `R` |

## Gameplay

Balls spawn into the level and move continuously. The player draws black line segments to redirect them toward holes. A ball scores when it enters a matching colored hole. A grey ball or grey hole acts as a wildcard. Sending a ball to the wrong hole applies the configured penalty and returns the ball to play.

Levels are time-limited. Clearing all queued and active balls completes the level. Remaining time is converted into score during the end-of-level bonus phase.

## Level Configuration

Game progression is defined in `config.json`. Each level can specify:

- `layout`: the text file used to build the board
- `time`: the level timer in seconds
- `spawn_interval`: delay between ball spawns
- `score_increase_from_hole_capture_modifier`: multiplier for successful captures
- `score_decrease_from_wrong_hole_modifier`: multiplier for penalties
- `balls`: ordered queue of ball colors to spawn

Layout files use character tokens to place entities:

| Token | Meaning |
| --- | --- |
| `X` | Default wall |
| `1` to `4` | Colored walls |
| `S` | Spawner |
| `H0` to `H4` | Colored holes |
| `B0` to `B4` | Starting balls |
| `A0` to `A3` | Acceleration tiles: up, down, left, right |

## Build And Test

Create a runnable jar:

```bash
./gradlew jar
```

Run tests:

```bash
./gradlew test
```

Generate the JaCoCo report:

```bash
./gradlew jacocoTestReport
```

## License

This project is released under the MIT License. See `LICENSE` for details.
