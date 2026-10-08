# Water Rings

A small interactive toy built around one everyday observation: a glass of ice water leaves a ring on the table. Here the cup is a stamp and the table is the canvas. Set a cup down, lift it, and watch the mark slowly dry.

**Play it:** https://minghan1994.github.io/water-stain/

## How to play

- Pick a cup from the panel, then press and hold on the table to set it down. The longer you hold, the darker the mark.
- Each cup leaves its own footprint: a thin ring, a wide foot ring, a rounded square, a rippled ring from a fluted glass, or the five feet of a soda bottle.
- Choose **Finger**, touch a wet mark and drag to lead the water out in that direction.
- **Drying** controls slow down, speed up, pause, or wipe the table.
- Keyboard: `1`–`6` switch cups, hold `Space` to set the cup down.

## How it works

Everything runs in a single `index.html` with WebGL2, no build step and no dependencies.

- **The table is a wetness map.** An off-screen floating-point texture stores how much water sits on each point of the table. A second channel stores the faint mineral residue water leaves behind.
- **Cups are stamps.** Each cup's base is a signed-distance shape. While a cup is down, every frame adds water under that shape, with noise so no two marks are identical, plus a few condensation droplets around glass cups.
- **Drying is a simulation, not an animation.** Each frame, water evaporates at a rate varied by noise, so thin parts dry first and marks break up into fragments. Water only levels out between wet cells, so the edge stays pinned like a real drop's contact line, and evaporation at the edge leaves a faint tide line.
- **Rendering.** The wood is generated once per resize. The final pass darkens and slightly cools wet wood, darkens the rim, adds a specular highlight from the water surface's slope, and draws the cup.
- **Photographed cups.** Glass photos shot on white are multiplied over the table like a transmission filter, and their brightness gradients bend the table seen through them. Shadows come from each photo's own silhouette, and the glass focuses a caustic into the shadow, tinted by the drink.
- **The finger** reads the wetness under the fingertip. Touching water loads it up, and dragging draws a crisp rivulet that thins and fades as the load runs out, while the source mark gives up a little water.

## Files

- `index.html` — the whole app. Cup photos are embedded as base64 so the file runs on its own.
- `cups/` — the cropped cup photos, kept as separate files for editing.

## Run locally

Open `index.html` in a recent Chrome, Safari or Firefox. No server needed.
