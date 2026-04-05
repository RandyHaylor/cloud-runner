# Cloud Runner

Side-scrolling endless platformer with 2D/3D rendering that alternates every level. Single HTML file, no build step.

## Stack

- Vanilla JS (no framework)
- Canvas 2D for 2D levels
- Three.js r128 (CDN) for 3D levels
- Single file: `index.html`

## Architecture

The game has four distinct concerns mixed into one file:

1. **Game state & config** — `S` object and `CONFIG` constants
2. **Game logic** — physics, collision, scoring, level end detection in `update()`
3. **Level generation** — `buildLevel()`, `genIntro()`, `genEnemy()`, `genGap()`
4. **Rendering** — `draw2D()` and `draw3D()` plus Three.js scene setup

## How Levels Work

- Each level is pre-built as physical platforms placed in the world
- A dark `levelEnd` marker platform is placed at the end of each level's content
- When the player physically reaches 30% across the marker, the level switches
- Intro stage shows "Get Ready", awards no points, transitions silently to Level 1
- Real levels award +100 points and show "STAGE CLEAR"
- Levels alternate: intro -> gaps -> enemies -> gaps -> enemies...
- 2D levels generate 2.4x more content to compensate for different scroll scale vs 3D

## How 2D/3D Switching Works

- Level 1: 3D
- Even levels: 2D
- Odd levels 3+: 3D with randomized camera height/angle
- Camera Y tracks smoothed ground level (doesn't follow jumps)
- `switchMode()` handles canvas visibility toggling

## Gameplay Features

- Variable jump: tap for short hop, hold for full jump
- Gold coins (1pt), pink big coins (3pt), some float high
- Ground enemies: hop in place, dodge by timing
- Flying enemies (level 5+): purple bats that bob up/down on enemy mega-platforms
- Enemy stages: one solid mega-platform, no gaps
- Gap stages: series of platforms with jumps, no enemies
- Floating point text on coin pickup and stage clear
- Particle effects: jump dust, coin burst, death explosion, stage clear smoke

## Hosting

- Developed on host at `/home/aikenyon/cloud-runner/`
- Deployed to VM via git: `git push` then `/opt/deploy.sh` on VM
- VM serves via nginx on port 80, exposed via ngrok
- Game container is fixed 400x711px portrait layout

## Next Steps

**Major refactor needed before adding features:**

1. **Separate level generation from rendering** — `buildLevel()` currently creates game objects that have `mesh:null` properties baked in for Three.js. Level generation should produce pure data (positions, types, sizes). Renderers should own mesh creation/destruction independently. This will fix the tight coupling between game logic and Three.js.

2. **Separate 2D and 3D renderers into modules** — `draw2D()` and `draw3D()` plus all Three.js setup should be extractable. Each renderer reads from game state and manages its own visual objects. Switching renderers should be as simple as swapping which draw function runs.

3. **Comprehensive unit testing** — The game logic (physics, collision, level generation, scoring, stage transitions) is all testable without any rendering. Extract pure functions and add tests for:
   - Collision detection edge cases
   - Level generation produces valid, completable levels
   - Score awards correctly (intro=0, real levels=100, coins=1/3)
   - Stage type progression (intro->gaps->enemies->gaps->...)
   - 2D/3D scale factor applied correctly to level content
   - Variable jump mechanics (tap vs hold)
   - Enemy behavior (hop timing, flyer bob range)

4. **Split into multiple files** — Once tested, break `index.html` into:
   - `game.js` — state, config, physics, collision
   - `levels.js` — level generation, stage progression
   - `render2d.js` — canvas 2D renderer
   - `render3d.js` — Three.js renderer
   - `input.js` — input handling
   - `index.html` — just markup and imports
