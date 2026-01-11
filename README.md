# megaman-like-vibing

Refine the prompts modal of Megaman until it finalizes the game mechanism

# Role: Senior HTML5 Game Developer & Pixel Artist
# Task: Create a fully functional "Mega Man" clone in a SINGLE HTML file (HTML + CSS + Vanilla JS).
# Constraints: NO external assets (images/sounds), NO game engines (Phaser/Unity). Use Canvas API for all rendering.

## 1. ARCHITECTURE & ENGINE
- Create a `Game` class to manage the loop using `requestAnimationFrame`.
- Implement a `deltaTime` system to ensure smooth movement regardless of framerate.
- **Input Handling:** Create an `InputHandler` class listening to 'keydown' and 'keyup'. Map keys: ArrowLeft/Right (Move), Z (Jump), X (Shoot).
- **Collision System:** Implement AABB (Axis-Aligned Bounding Box) collision detection for Player vs Map and Player vs Enemy.

## 2. LEVEL DESIGN (The Map)
- Use a 2D Array (Tilemap) to represent the level.
  - 0 = Air (Empty)
  - 1 = Ground/Wall (Solid color: Dark Blue #003366 with Light Blue border)
  - 2 = Spikes (Triangle shape, Red #FF0000, kills player instantly)
- The map must be wide (at least 3 screens wide) to demonstrate scrolling.
- **Camera:** Implement a `Camera` object that follows the `Player.x` but clamps to map boundaries.

## 3. PLAYER CHARACTER ("BlueBot") - EXTREMELY DETAILED VISUALS & MOVESET
Create a `Player` class. Do not use generic rectangles. Draw the character using `ctx` primitives (rects, arcs) to look like a robot.
- **Dimensions:** 40px height, 30px width.
- **Visuals (Procedural Drawing):**
  - *Color Palette:* Cyan (#00FFFF) for body/helmet, Dark Blue (#0000FF) for limbs.
  - *Facing:* Flip drawing based on `facingRight` boolean.
- **State Machine & Animation Frames:**
  1.  **IDLE State:** Draw player standing. Add a "breathing" effect (scale height by 1% every 500ms).
  2.  **RUN State:** When moving on ground.
      - *Frame 1:* Legs slightly apart.
      - *Frame 2:* Legs wide apart.
      - Switch frames every 150ms.
  3.  **JUMP State:** When `vy < 0`. Draw one leg bent up, one leg straight down.
  4.  **FALL State:** When `vy > 0`. Draw both legs slightly bent up.
  5.  **SHOOT Action:** Independent of movement. Draw an arm extended horizontally forward.
      - *Projectile:* Small yellow circle (radius 4px). High velocity X.
  6.  **HURT State:** When hit by enemy.
      - *Behavior:* Knockback (reverse velocity X, jump up Y).
      - *Visual:* Flash sprite opacity (visible/invisible) every 4 frames.
- **Physics Specs:**
  - Gravity: 0.6
  - Jump Strength: -10
  - Move Speed: 4
  - Friction: 0.8 (for smooth stopping)

## 4. ENEMIES ("Metool Clone")
Create an `Enemy` class.
- **Visuals:** Hard Hat (Yellow semi-circle), Black feet.
- **AI Logic:** Simple Patrol. Move Left until hitting a wall/edge, then Move Right.
- **Interaction:**
  - If Bullet hits Enemy: Enemy dies (disappears + particle explosion effect).
  - If Player hits Enemy: Player takes damage + Knockback.

## 5. AUDIO (Synthesized)
Use `window.AudioContext` to generate sounds programmatically (Oscillators).
- `playSound('jump')`: Short square wave, rising frequency.
- `playSound('shoot')`: Short triangle wave, high to low drop.
- `playSound('hit')`: Noise wave (static) for impact.

## 6. UI & WRAPPER
- Canvas size: 800x600.
- Draw a Health Bar in the top-left (Vertical segments, like NES Mega Man).
- Add a "Start Screen" overlay: "PRESS Z TO START".
- Add "Game Over" and "Victory" states.

## 7. FINAL CODE STRUCTURE
- Combine everything into one single valid HTML file.
- Add comments explaining the physics logic (for educational purposes).
- Ensure the code handles window resizing gracefully (centers the canvas).

Please generate the complete, runnable code now.
