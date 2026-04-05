# Squeeze Box

An endless side-scrolling platformer that switches between 2D and 3D rendering every level.

## Play

**Live:** https://randyhaylor.github.io/squeezebox/

**Controls:** Hold the JUMP button to charge, release to jump. Hold longer = jump higher. Press again in air for a double jump. Hold a third time to store a jump for when you land.

## Features

- 2D canvas and Three.js 3D over-the-shoulder rendering that alternates each level
- Charge-and-release jump mechanic with visual squish
- Double jump and stored landing jump
- Coins to collect (gold = 1pt, pink = 3pt) in formations (lines, grids, arcs)
- Ground enemies that hop in place
- Flying bat enemies on later levels
- Gap stages (jumping) and enemy stages (dodging) that alternate
- Levels get progressively longer and faster
- Portrait mobile layout (400x711)
- Demo AI on title screen showing jump variations
- Pause screen with full instructions and enemy/coin visuals

## Hosting

- **GitHub Pages:** https://randyhaylor.github.io/squeezebox/
  - Source: `RandyHaylor/RandyHaylor.github.io` repo, `squeezebox/` folder
  - Deploys automatically on push to main
- **VM (dev/testing):** nginx on headless Ubuntu VM, tunneled via ngrok
  - Deploy: `ssh root@<vm-ip> /opt/deploy.sh`

## Tech

Single HTML file, vanilla JS + Three.js from CDN. No build step, no dependencies to install.

## Development

```
# Edit locally
vi ~/cloud-runner/index.html

# Push to game repo
cd ~/cloud-runner && git add -A && git commit -m "msg" && git push

# Deploy to VM for testing
ssh root@<vm-ip> /opt/deploy.sh

# Deploy to GitHub Pages
cp ~/cloud-runner/index.html ~/RandyHaylor.github.io/squeezebox/index.html
cd ~/RandyHaylor.github.io && git add -A && git commit -m "msg" && git push
```
