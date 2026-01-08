# Goat Fish Tank

A relaxing, interactive aquarium visualization featuring goat-fish hybrids swimming in an underwater environment. Built with vanilla JavaScript and HTML5 Canvas.

## What is this?

An animated fish tank where the fish are actually small crosses between fish and goats - they have fish bodies with tails and fins, but also goat heads with horns, ears, snouts, rectangular pupils, and beards. They swim around peacefully until disturbed. The tank also includes bottom-feeding sheatfish (catfish) that lazily scavenge along the bottom.

## Features

### Interactive Elements
- **Click fish** to spook them - they'll spin rapidly, react with personality-driven commentary, and zoom away
- **Click empty water** to spawn a burst of bubbles
- **Spacebar** scares all fish at once
- **'F' key** toggles fullscreen mode
- **'X' key** resets the tank to a fresh state
- **'K' key** sets your Anthropic API key for AI commentary
- **'C' key** triggers fish commentary immediately
- **Menu button** (mobile & tablet) - access all controls via touch-friendly menu

### Visual Elements
- Goat-fish with distinct features:
  - Fish body, tail, and fins
  - Goat head with protruding snout and nostrils
  - Curved horns
  - Triangular ears
  - Horizontal rectangular pupils (like real goats)
  - Beard
  - Random colors for variety
- Sheatfish (catfish) bottom feeders:
  - Long, low bodies for bottom feeding
  - Animated sucker mouths
  - Multiple whiskers (barbels) that sway
  - Muddy brown coloration
  - Slow, peaceful movement along the bottom
- Rising bubbles with realistic physics:
  - Speed variation based on size
  - Expansion as they rise (pressure decrease)
  - Gentle wobble and drift
  - Acceleration due to buoyancy
- Tall swaying seaweed/plants
- Short grass undergrowth
- Water gradient background (lighter at top, darker at bottom)
- Smooth animations with no ghosting trails

### AI-Powered Fish Commentary
- **Claude Haiku integration** for witty, sarcastic fish commentary
- Fish "speak" via speech bubbles that follow them around
- **Regular commentary** appears every 45 seconds (when API key is configured)
  - Randomized topics and tones for variety:
    - Topics include existential observations, gossip, philosophical musings, snarky remarks, and more
    - Tones range from sarcastic and dry to anxious, grumpy, and melodramatic
  - Commentary is context-aware, reflecting:
    - Current tank conditions and fish distribution
    - Individual fish personalities and behaviors
    - Social dynamics and activity levels
- **Spooked reactions** generate instant personality-driven responses when fish are startled
  - Each fish reacts based on its personality (anxious, chill, hyperactive, lazy, curious, or grumpy)
  - Reactions vary from panicked to sarcastically annoyed to melodramatically traumatized
  - Falls back to classic bleats ("BAAA!", "MEHHH!") when no API key is set
- Set your Anthropic API key with the 'K' key or via the mobile menu

### Hidden Personality System
- Each goat-fish has a unique personality that affects behavior:
  - **Personality types**: anxious, chill, hyperactive, lazy, curious, grumpy
  - **Social preference**: ranges from loner (0) to social butterfly (1)
  - **Depth preference**: ranges from surface lover (0) to deep diver (1)
- Fish track hidden statistics:
  - Total times spooked
  - Total distance traveled
  - Nearby friends count
  - Time since last spook
- These traits influence AI commentary and create unique tank dynamics

### Technical Features
- **Responsive**: Fills entire browser window and adapts to resize
- **Scalable**: Number of fish, bubbles, plants, and grass automatically scale with viewport size
- **Mobile-optimized**:
  - Reduced fish population on mobile devices (6-12 vs 15-25 on desktop)
  - Touch-friendly menu system with hamburger button
  - Menu provides easy access to all controls without keyboard
- **Persistent State**: All positions and animation states save to localStorage on page unload and restore on reload
  - Goat-fish positions, velocities, sizes, colors, and personality traits
  - Hidden statistics (spook counts, distance traveled, social dynamics)
  - Sheatfish positions and movement
  - Bubble positions and speeds
  - Plant and grass positions
  - Animation timing for continuous swaying motion
  - Anthropic API key (stored securely in localStorage)
- Fish velocities are clamped on reload to prevent "super speed" bugs
- Reset functionality to clear state and start fresh
- Fullscreen support for immersive viewing

## Usage

1. Open `index.html` in a web browser
2. Press **'f'** to enter fullscreen for the best experience (or use menu on mobile)
3. *Optional*: Press **'k'** to set your Anthropic API key for AI-powered fish commentary
4. Click on fish to spook them
5. Click on water to create bubbles
6. Press **spacebar** for chaos (or use "Scare All Fish" in menu on mobile)
7. Press **'c'** to trigger fish commentary immediately (if API key is set)
8. Press **'x'** to reset the tank
9. Sit back and relax while your goat-fish make sarcastic observations

## Technical Details

- Pure vanilla JavaScript - no frameworks or libraries
- HTML5 Canvas for rendering
- localStorage for state persistence
- Claude Haiku 4.5 (claude-haiku-4-5-20251001) for AI commentary
- Responsive scaling based on viewport area:
  - Goat-fish: ~1 per 100,000 pixels
    - Desktop: min 15, max 25
    - Mobile (<768px): min 6, max 12
  - Sheatfish: 2-3 catfish (bottom feeders)
  - Bubbles: ~1 per 100,000 pixels (min 8)
  - Plants: ~1 per 100px width (min 12)
  - Grass: ~1 per 15px width (min 50)

## Why?

Because the world needs more goat-fish swimming peacefully in virtual tanks.
