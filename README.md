# 🎮 My First Godot Game

Project built following the **"How to make a Video Game - Godot Beginner Tutorial"** by [Brackeys](https://www.youtube.com/watch?v=LOhfqjmasi0).

My first "Hello World" in game development.

---

## 📁 Scenes

### `player.tscn`
The main character scene.

- **Root node:** `CharacterBody2D` — handles movement with collision detection
- **AnimatedSprite2D:** `idle` animation with 4 frames from the `knight.png` spritesheet (32x32 px each), looping at 10 fps
- **CollisionShape2D:** Circle shape with radius 6, used as the character's hitbox

### `game.tscn`
The main game scene.

- **Root node:** `Node2D` — general scene container
- **Camera2D:** 4x zoom to scale up the pixel art world
- **Player:** Instance of `player.tscn` placed at position (1, 0)

---

## 🛠️ Engine

- [Godot Engine 4](https://godotengine.org/)

---

## 📺 Tutorial

- [Brackeys - How to make a Video Game (Godot)](https://www.youtube.com/watch?v=LOhfqjmasi0)
