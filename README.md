# Goat Fish Tank

A relaxing, interactive aquarium visualization featuring goat-fish hybrids swimming in an underwater environment. Built with vanilla JavaScript and HTML5 Canvas.

## What is this?

An animated fish tank where the fish are actually small crosses between fish and goats - they have fish bodies with tails and fins, but also goat heads with horns, ears, snouts, rectangular pupils, and beards. They swim around peacefully until disturbed.

## Features

### Interactive Elements
- **Click fish** to spook them - they'll spin rapidly, bleat ("BAAA!", "MEHHH!", "😱"), and zoom away
- **Click empty water** to spawn a burst of bubbles
- **Spacebar** scares all fish at once
- **'F' key** toggles fullscreen mode

### Visual Elements
- Goat-fish with distinct features:
  - Fish body, tail, and fins
  - Goat head with protruding snout and nostrils
  - Curved horns
  - Triangular ears
  - Horizontal rectangular pupils (like real goats)
  - Beard
  - Random colors for variety
- Rising bubbles with gentle wobble
- Tall swaying seaweed/plants
- Short grass undergrowth
- Water gradient background (lighter at top, darker at bottom)
- Smooth animations with no ghosting trails

### Technical Features
- **Responsive**: Fills entire browser window and adapts to resize
- **Scalable**: Number of fish, bubbles, plants, and grass automatically scale with viewport size
- **Persistent State**: All positions and animation states save to localStorage on page unload and restore on reload
  - Fish positions, velocities, sizes, and colors
  - Bubble positions and speeds
  - Plant and grass positions
  - Animation timing for continuous swaying motion
- Fish velocities are clamped on reload to prevent "super speed" bugs
- Fullscreen support for immersive viewing

## Usage

1. Open `goattank.html` in a web browser
2. Press **'f'** to enter fullscreen for the best experience
3. Click on fish to spook them
4. Click on water to create bubbles
5. Press **spacebar** for chaos
6. Sit back and relax

## Technical Details

- Pure vanilla JavaScript - no frameworks or libraries
- HTML5 Canvas for rendering
- localStorage for state persistence
- Responsive scaling based on viewport area:
  - Fish: ~1 per 50,000 pixels (min 15)
  - Bubbles: ~1 per 50,000 pixels (min 20)
  - Plants: ~1 per 100px width (min 12)
  - Grass: ~1 per 15px width (min 50)

## Why?

Because the world needs more goat-fish swimming peacefully in virtual tanks.
