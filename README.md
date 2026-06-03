# 🎮 My First Godot Game

A 2D platformer built following the **"How to make a Video Game - Godot Beginner Tutorial"** by [Brackeys](https://www.youtube.com/watch?v=LOhfqjmasi0).

My first complete game in game development. ✅ **Tutorial finished!**

The player runs and jumps across platforms, collects coins to score points, avoids enemies (which can be defeated by jumping on them), and respawns on death. Includes UI score text and sound effects/music.

---

## ✨ Features

- Side-scrolling platformer movement (run, jump, gravity)
- Tilemap-based world with platforms
- Collectible coins that increase the score
- Enemies with patrol movement that kill the player on contact (and can be stomped from above)
- Death and respawn system
- On-screen score counter (UI)
- Sound effects and background music

---

## 📁 Scenes

### `player.tscn`
The main character scene.

- **Root node:** `CharacterBody2D` — handles movement, gravity, jumping, and collision detection
- **AnimatedSprite2D:** Animations (`idle`, `running`, `jump`) from the `knight.png` spritesheet (32x32 px each)
- **CollisionShape2D:** Hitbox for the character
- **Script:** Reads input for horizontal movement and jumping, applies gravity, flips the sprite by direction, and switches animations based on state

### `coin.tscn`
A collectible pickup.

- **Root node:** `Area2D` — detects when the player overlaps
- **AnimatedSprite2D:** Spinning coin animation
- **CollisionShape2D:** Pickup area
- **Script:** On player entry, plays a sound, adds to the score, and removes itself

### `slime.tscn` (Enemy)
The patrolling enemy.

- **Root node:** `Area2D` (or `CharacterBody2D`) with patrol movement using `RayCast2D` to detect ledges/walls and turn around
- **AnimatedSprite2D:** Movement animation
- **Behavior:** Kills the player on side contact; defeated when the player lands on top

### `game.tscn`
The main game scene.

- **Root node:** `Node2D` — general scene container
- **Camera2D:** Zoomed in to scale up the pixel art world
- **TileMap:** The level layout (platforms and ground) with collision
- **Player:** Instance of `player.tscn`
- **Coins / Enemies:** Instances placed throughout the level
- **CanvasLayer / UI:** `Label` displaying the current score
- **Audio:** `AudioStreamPlayer` for background music

---

## 🎯 Gameplay

| Action | Key |
| --- | --- |
| Move left / right | `←` / `→` (or `A` / `D`) |
| Jump | `Space` |

Collect coins to raise your score, stomp enemies from above, and avoid touching them from the side.

---

## 🛠️ Engine

- [Godot Engine 4](https://godotengine.org/)

---

## 🖌️ Assets

- [Brackeys' Platformer Assets](https://brackeysgames.itch.io/brackeys-platformer-bundle)

---

## 📺 Tutorial

- [Brackeys - How to make a Video Game (Godot)](https://www.youtube.com/watch?v=LOhfqjmasi0)
- [Finished Project (Brackeys' GitHub)](https://github.com/Brackeys/first-game-in-godot)

---

## 🚀 Where to go from here

- Add more levels and a level-transition system
- Add a main menu and game-over screen
- Add more enemy types and hazards
- Export to web/desktop and share it!
