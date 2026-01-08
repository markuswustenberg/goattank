# Agent Guide - Goat Fish Tank

Technical documentation for AI agents working on this codebase.

## Project Structure

Single-file application: `goattank.html`
- All HTML, CSS, and JavaScript in one file
- No external dependencies or build process
- ~700 lines of vanilla JavaScript

## Architecture Overview

### Main Classes

1. **GoatFish** (lines ~86-373)
   - Constructor accepts `savedState` for localStorage restoration
   - `toJSON()` serializes position, velocity, size, colors
   - `spook()` triggers panic animation (spin + zoom + bleat)
   - `update()` handles movement, collision, spooked state
   - `draw()` renders body, head, snout, ears, horns, eyes, beard, bleat text
   - **Important**: Velocities are clamped on load (lines 68-69) to prevent saved spooked speeds

2. **Bubble** (lines ~383-441)
   - Rising animation with wobble
   - **Important**: Speed clamped on load (line 390) - saved bubbles get scaled by 0.4x
   - Speed range: 0.3-0.8 px/frame

3. **Plant** (lines ~444-482)
   - Tall seaweed with swaying segments
   - Uses time-based animation for sway
   - Accepts either x position (number) or savedState (object)

4. **Grass** (lines ~495-557)
   - Short ground cover with sway animation
   - Drawn behind plants (z-order)
   - Time-based sway animation

### Core Functions

- `init()` (line ~35): Setup, event listeners, initial creation
- `resizeCanvas()` (line ~28): Window resize handler, recreates plants/grass
- `createGoatFish()` (line ~559): Factory with localStorage fallback
- `createBubbles()` (line ~603): Factory with localStorage fallback
- `createPlants()` (line ~469): Factory with localStorage fallback
- `createGrass()` (line ~534): Factory with localStorage fallback
- `saveAll()` (line ~587): Persists all state to localStorage on unload
- `animate(timestamp)` (line ~648): Main render loop

## State Management

### localStorage Keys
- `goatFishState`: JSON array of fish states
- `bubbleState`: JSON array of bubble states
- `plantState`: JSON array of plant states
- `grassState`: JSON array of grass states
- `animationTime`: Float timestamp for animation continuity

### Animation Time Preservation
- `animationTimeOffset` (line ~636): Offset loaded from localStorage
- `currentAnimationTime` (line ~637): `timestamp + animationTimeOffset`
- Saved on unload (line 598) to preserve grass/plant sway phases

## Coordinate System

- Origin (0,0) is top-left
- Canvas fills entire window via `window.innerWidth/innerHeight`
- Fish position is center of fish body
- Plants/grass positioned by x coordinate at bottom (y = canvas.height)

## Scaling Constants

Fish count: `Math.max(15, Math.floor(area / 50000))` (line 580)
Bubble count: `Math.max(20, Math.floor(area / 50000))` (line 622)
Plant count: `Math.max(12, Math.floor(canvas.width / 100))` (line 487)
Grass count: `Math.max(50, Math.floor(canvas.width / 15))` (line 552)

## Critical Gotchas

1. **Velocity Clamping Required**
   - Fish velocities must be clamped on load (lines 68-69)
   - Without clamping, saved "spooked" velocities persist forever
   - Fish normal speed: vx ±1, vy ±0.5
   - Spooked speed: 8x in random direction

2. **Bubble Speed Scaling**
   - Old bubbles had speed 0.5-2.0, new range is 0.3-0.8
   - On load, multiply saved speed by 0.4 and clamp (line 390)

3. **Plant/Grass Constructor Overload**
   - Accepts either numeric x position OR savedState object
   - Check `typeof xOrSavedState === 'object'` to distinguish (line 360 for Plant, line 497 for Grass)

4. **Animation Time**
   - Both plants and grass receive `currentAnimationTime` not raw `timestamp`
   - This preserves animation phase across reloads

5. **Canvas Resize Behavior**
   - Resizing recreates plants and grass (loses unsaved state)
   - Fish and bubbles are NOT recreated on resize

## Event Handlers

- **Click**: Check if fish clicked, else spawn bubbles (line 64)
- **Spacebar**: Spook all fish (line 58)
- **'F' key**: Toggle fullscreen (line 49)
- **beforeunload**: Save all state (line 43)
- **resize**: Resize canvas, recreate plants/grass (line 40)

## Render Order (Z-index)

1. Background gradient (top)
2. Grass
3. Plants
4. Bubbles
5. Fish
6. Bleat text (bottom/front)

## Adding New Features

### New Interactive Element
1. Add class with constructor(savedState) pattern
2. Implement `toJSON()` for state serialization
3. Add create function with localStorage loading
4. Add to `saveAll()` function
5. Add to render loop in correct z-order
6. Update scaling if viewport-dependent

### New Animation
1. Use `currentAnimationTime` not raw `timestamp`
2. Consider phase randomization for variety
3. Test that it persists across page reloads

### New Interaction
1. Add event listener in `init()`
2. Use `canvas.getBoundingClientRect()` for mouse coords
3. Check collision/proximity to existing elements

## Color Scheme

- Background gradient: `#1a5f7a` (top) → `#0e4d66` (mid) → `#083344` (bottom)
- Plants: HSL 100-140°, 50% sat, 35% light
- Grass: HSL 110-140°, 60% sat, 25-40% light
- Fish: Random hue, 70% sat, 60% light (body)
- Horns/ears: Body hue ±30°, 50-60% sat, 40-50% light

## Performance Notes

- Full canvas clear each frame (no trails)
- Gradient recreated each frame (could optimize)
- No culling - all elements drawn even if off-screen
- Typical counts on 1920x1080: ~40 fish, ~40 bubbles, ~19 plants, ~128 grass

## Testing Tips

1. **State Persistence**: Close tab, reopen - everything should be identical
2. **Velocity Clamping**: Spook fish, reload immediately - should be normal speed
3. **Animation Continuity**: Note grass position, reload - should continue from same position
4. **Resize Behavior**: Resize window - fish stay in place, plants/grass redistribute
5. **Fullscreen**: Press 'f' - should fill screen with no chrome

## Common Tasks

**Add new fish behavior:**
- Modify `GoatFish.update()` for movement logic
- Modify `GoatFish.draw()` for visual changes

**Change animation speed:**
- Adjust multipliers in `plant.draw(time)` or `grass.draw(time)`
- Look for `time * 0.001` or `time * 0.002` factors

**Modify spawn rates:**
- Change divisors in create functions (50000, 100, 15, etc.)
- Change minimums (15, 20, 12, 50)

**Add new keyboard shortcut:**
- Add to keydown handler starting line 48
- Check `e.key` value and add logic

## Code Conventions

- Classes use PascalCase: `GoatFish`, `Bubble`, `Plant`, `Grass`
- Factory functions use camelCase: `createGoatFish()`, `createBubbles()`
- No semicolons (consistent throughout)
- Save functions are silent on failure (catch blocks empty)
- All position/size values relative to `s` (size) for fish drawing
