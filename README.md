# Cloud Runner

An endless side-scrolling platformer that switches between 2D and 3D rendering every level.

## Play

Open `index.html` in a browser, or visit the live version hosted via ngrok (URL changes on restart).

**Controls:** Space/ArrowUp or tap the JUMP button. Hold for a higher jump, tap for a short hop.

## Features

- 2D canvas and Three.js 3D rendering that alternates each level
- Randomized camera angles in 3D mode
- Coins to collect (gold = 1pt, pink = 3pt)
- Ground enemies that hop in place
- Flying bat enemies on later levels
- Gap stages (jumping) and enemy stages (dodging) that alternate
- Levels get progressively longer and faster
- Portrait mobile layout (400x711)

## Tech

Single HTML file, vanilla JS + Three.js from CDN. No build step, no dependencies to install.

## Development

Built and hosted on a headless Ubuntu 22.04 VM sandbox managed by Claude Code.

```
git push                    # push changes
ssh root@<vm-ip> /opt/deploy.sh   # deploy to VM
```
