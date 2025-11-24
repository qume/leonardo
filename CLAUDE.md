# Leonardo - Simple Platformer Game

## Project Overview
A browser-based 2D platformer game built entirely with vanilla HTML5, CSS, and JavaScript. The player controls a character that must navigate platforms, collect coins, and reach the goal star.

## Technology Stack
- **HTML5 Canvas** - For rendering graphics
- **Vanilla JavaScript** - Game logic and physics
- **CSS3** - UI styling
- **No external dependencies** - Completely self-contained in a single HTML file

## File Structure
```
leonardo/
├── platformer.html    # Single-file game (all HTML, CSS, JS)
└── CLAUDE.md         # This file
```

## How to Run
Simply open `platformer.html` in any modern web browser. No build process or server required.

## Game Mechanics

### Player Controls
- **Movement**: Arrow Keys or WASD
- **Jump**: Space, W, or Up Arrow
- Player character is a red square with eyes

### Game Elements
1. **Player** (platformer.html:66-79)
   - Red 30x30 pixel square character
   - Physics: gravity (0.5), jump power (12), movement speed (5)
   - Collision detection with platforms

2. **Platforms** (platformer.html:82-91)
   - 8 platforms including ground
   - Green colored with texture borders
   - Collision detection on all sides (top, bottom, left, right)

3. **Coins** (platformer.html:94-102)
   - 7 collectible gold coins
   - Each coin worth 10 points
   - Disappear when collected

4. **Goal** (platformer.html:104-111)
   - Star emoji at position (700, 140)
   - Reaching it awards 100 bonus points and wins the game

### Physics System
- Gravity: Constant downward acceleration (0.5)
- Collision detection: AABB (Axis-Aligned Bounding Box) method
- Platform collision handles: landing on top, hitting from below, side collisions
- Player respawns at start if falling off bottom

### Scoring
- Coins: +10 points each
- Goal reached: +100 points
- Score persists until manual reset

## Code Organization

### Key Functions

**Player Movement** (platformer.html:134-193)
- `updatePlayer()` - Handles input, physics, collision detection
- Horizontal movement applied immediately
- Vertical movement uses gravity and jump mechanics
- Collision response for platforms

**Collectibles** (platformer.html:196-204)
- `updateCoins()` - Check and handle coin collection

**Win Condition** (platformer.html:207-214)
- `checkGoal()` - Detect goal collision and handle victory

**Rendering** (platformer.html:217-285)
- `drawPlayer()` - Renders player character with eyes
- `drawPlatforms()` - Renders all platforms with texture
- `drawCoins()` - Renders uncollected coins with shine effect
- `drawGoal()` - Renders goal star
- `draw()` - Main render function that draws entire scene

**Game Loop** (platformer.html:302-308)
- `gameLoop()` - Updates game state and renders at ~60 FPS using requestAnimationFrame

**Game Management**
- `resetPlayerPosition()` - Returns player to starting position
- `resetGame()` - Full game reset (score, coins, player position)

### Game State
All game state stored in global variables:
- `player` object - position, velocity, dimensions, physics properties
- `platforms` array - static platform data
- `coins` array - coin positions and collection status
- `goal` object - goal position and dimensions
- `score` - current score
- `keys` object - tracks pressed keys for input

## Common Modifications

### Adding New Platforms
Add entries to the `platforms` array (platformer.html:82-91):
```javascript
{ x: 400, y: 300, width: 100, height: 20, color: '#2ecc71' }
```

### Adding More Coins
Add entries to the `coins` array (platformer.html:94-102):
```javascript
{ x: 300, y: 250, width: 20, height: 20, collected: false }
```

### Adjusting Physics
Modify player properties (platformer.html:66-79):
- `speed` - horizontal movement speed
- `jumpPower` - jump height (higher = higher jump)
- `gravity` - fall speed (higher = faster fall)

### Changing Difficulty
- Increase gravity for harder jumps
- Decrease jump power for shorter jumps
- Adjust platform positions to create harder/easier paths
- Add more platforms for easier gameplay
- Add moving platforms (requires new logic)

### Styling Changes
CSS styling in `<style>` tag (platformer.html:7-48)
- Canvas size: 800x600 (line 55)
- Color scheme can be modified in CSS variables

## Architecture Notes

### Single File Design
The entire game is self-contained in one HTML file for simplicity and portability. This makes it:
- Easy to share and deploy
- Simple to understand for beginners
- No build process required
- Can run locally without a server

### Canvas Rendering
Uses 2D canvas context with immediate mode rendering:
- Clear canvas each frame
- Redraw all elements every frame
- No sprite sheets or image assets

### State Management
Simple global state - appropriate for a small game like this. For larger projects, consider:
- Game state object
- Entity component system
- Scene management

## Future Enhancement Ideas

### Easy Additions
- Sound effects (jump, coin collect, win)
- Background music
- Multiple levels
- Lives system
- Timer/speedrun mode
- High score persistence (localStorage)

### Moderate Complexity
- Moving platforms
- Enemies/hazards
- Double jump mechanic
- Wall jump ability
- Power-ups (speed boost, higher jump)
- Particle effects

### Advanced Features
- Level editor
- Physics improvements (friction, acceleration curves)
- Sprite animations
- Mobile touch controls
- Multiplayer/ghost racing
- Procedural level generation

## Performance Notes
- Game runs at browser's refresh rate (typically 60 FPS)
- Very lightweight - no performance concerns for this simple game
- Canvas clearing and redrawing is efficient for this scale
- Could optimize with dirty rectangles for larger games

## Browser Compatibility
Works in all modern browsers that support:
- HTML5 Canvas
- ES6 JavaScript (arrow functions, const/let)
- requestAnimationFrame
- No polyfills needed for modern browsers

## Testing
Manual testing checklist:
- [ ] Player movement (left, right)
- [ ] Jumping mechanics
- [ ] Platform collision (top, sides, bottom)
- [ ] Coin collection
- [ ] Score tracking
- [ ] Goal detection and win condition
- [ ] Reset button functionality
- [ ] Fall-off respawn
- [ ] Controls with both arrow keys and WASD

## Known Limitations
- No mobile/touch support
- Single level only
- No save/load functionality
- No sound/music
- Simple collision detection (no slopes or complex shapes)
- No animation frames (static sprites)

## Development History
Created with Claude Code as a demonstration of a simple but complete game implementation using only vanilla web technologies.
