# Procedural 3D/2D Game — Exploration Plan

## Goal
Explore genre + engine options for a game with procedurally generated graphics.
Before committing to an engine, build a single sample HTML page showing rough
visual style for each candidate genre, to compare aesthetics before proceeding.

## Genre candidates
1. Platformer (2D side-view)
2. 2D tile game (top-down, biome-based)
3. Space sim (2D/3D starfield + planets)
4. Arcade shooter — vertical scrolling, 1945-style
5. Racing game (2D/3D, procedural track)

Other genres considered but not currently prioritized:
- Roguelike dungeon crawler (BSP/cellular-automata generated rooms)
- Voxel/Minecraft-like exploration (noise terrain + marching cubes)
- Endless runner / arcade

## Engine options discussed
- **Godot** (GDScript/C#) — fast iteration, free, good runtime mesh/terrain generation via SurfaceTool/ArrayMesh
- **Unity** (C#) — most mature ecosystem for proc-gen (noise terrain, marching cubes, WFC, L-systems tutorials), jobs/burst for perf
- **Unreal** (C++/Blueprints) — best visual fidelity (Nanite/Lumen), built-in PCG framework, steeper learning curve
- **Bevy** (Rust) — ECS-centric, DIY, younger ecosystem
- **Three.js / raw WebGL** — for browser games, full control over procedural mesh generation, more infra to build yourself

## Sample graphics page plan
**Format:** Single self-contained HTML file (Artifact), vanilla Canvas2D/JS —
no external libraries/CDNs (Artifacts block external script loads). Tab
navigation to flip between demo panels. Each panel has a "regenerate" button
(new random seed) but is otherwise a static visual mockup — no gameplay,
physics, or full interactivity.

### Panels
1. **Platformer** — layered parallax background (noise-based hills/mountains),
   procedural platform placement (random-walk / jump-reachability), tile-based
   ground with color/texture variation.
2. **2D tile game** — Perlin/value-noise biome tilemap (grass, water, sand,
   forest), tile variety, simple auto-tiling edges.
3. **Space sim** — parallax starfield, procedurally generated planets (layered
   noise surface texture, ring systems), ship silhouette for scale.
4. **Arcade shooter (1945-style)** — top-down vertical-scroll background
   (noise clouds/terrain), procedurally scattered enemy formations, player
   ship + bullet patterns.
5. **Racing game** — procedural track via spline-based curve generation,
   scenery scatter (trees/barriers) along track edges, simple car sprite,
   top-down or slight-perspective view.

### Purpose / non-goals
- Purely a visual-style comparison to inform genre + engine choice.
- Not a prototype of gameplay, physics, or engine-specific rendering (e.g.
  Three.js/WebGL polish) — result will look rougher than a real engine build.

## Mockups built (`mockups/`)
Five self-contained HTML/Canvas2D mockups built per the panels above, each
with a "Regenerate" button and one added layer of visual complexity
(clouds/foreground for platformer, decorative props for tile game, asteroid
belt for space sim, boss+power-ups for arcade shooter, elevation shading +
cloud shadows for racing).

## Direction change: game asset packs
Decision: the quality/variety of actual game assets (sprites, tiles, props,
effects) will help determine which genre gets the most advanced/complex
graphics treatment going forward — so before picking one genre to build out,
generate procedural asset packs across genres to compare.

**Racing dropped from asset-pack scope.** The user wants a first-person-view
racing game, not top-down — the existing top-down racing mockup/approach
doesn't apply, so racing needs a separate FPV-specific exploration later and
is excluded from the current asset pack round.

### Asset pack format (`assets/<game>/index.html`)
Per game (platformer, tile_game, space_sim, arcade_shooter): one
self-contained HTML page with a category grid (Characters, Tiles/Environment,
Props, Effects/UI). Each asset:
- Has its own procedural generator (seeded RNG) shown on a small canvas
- Per-asset "↻" regenerate button for variety exploration
- Per-asset "⬇" download button (canvas.toDataURL → PNG) for static export
- Page-level "Regenerate All" button

## Status
- Mockups complete (`mockups/1_platformer.html` … `mockups/5_racing.html`).
- Asset packs complete (`assets/platformer/`, `assets/tile_game/`,
  `assets/space_sim/`, `assets/arcade_shooter/`) — racing excluded pending
  FPV redesign.
- Next step: review asset packs for quality/variety, decide which genre gets
  the most advanced graphics treatment, then explore FPV racing separately.
