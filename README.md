# 🎮 My First Godot Game

A 2D platformer built following the **"How to make a Video Game - Godot Beginner Tutorial"** by [Brackeys](https://www.youtube.com/watch?v=LOhfqjmasi0).

My first complete game in game development. ✅ **Tutorial finished!**

The player runs and jumps through a world built with a tilemap and platforms, collects coins that add points, dodges a slime enemy, and dies when falling into a killzone (with slow motion and a level reload). Includes on-screen helper text and background music.

---

## ✨ Features

- Platformer movement: run, jump, and gravity (`SPEED = 300`, `JUMP_VELOCITY = -400`)
- World built with `TileMapLayer` and a tileset with collisions
- Platforms: one static and one animated moving platform
- Collectible coins with a pickup animation and sound that add to the score
- Slime enemy that patrols and reverses direction when its RayCasts detect edges/walls
- Killzone that kills the player, applies slow motion, and reloads the level
- GameManager that keeps track of the score
- On-screen helper text with a pixel font
- Background music with autoplay

---

## 🗂️ Project structure

```
res://
├── scenes/      coin, game, killzone, music, platform, player, slime (.tscn)
├── scripts/     coin, game_manager, killzone, player, slime (.gd)
└── assets/
    ├── sprites/ knight.png, coin.png, slime_green.png, platforms.png, world_tileset.png
    ├── sounds/  coin.wav
    ├── music/   time_for_adventure.mp3
    └── fonts/   PixelOperator8-Bold.ttf
```

---

## 📁 Scenes & Scripts

### `player.tscn` + `player.gd`
The main character.

- **Root node:** `CharacterBody2D`
- **AnimatedSprite2D:** `knight.png` spritesheet (32x32 px) with `idle`, `run`, and `jump` animations (10 fps, looping)
- **CollisionShape2D:** `CircleShape2D` with radius 6
- **Logic (`player.gd`):** applies gravity when not on the floor, jumps with the `jump` action, reads the axis with `move_left` / `move_right`, flips the sprite based on direction, and switches between `idle` / `run` / `jump` based on state

### `coin.tscn` + `coin.gd`
Collectible coin.

- **Root node:** `Area2D` (with `collision_mask = 2`)
- **AnimatedSprite2D:** spinning coin animation (`coin.png`, 16x16 px, 12 frames)
- **CollisionShape2D:** `CircleShape2D` with radius 5
- **PickupSound:** `AudioStreamPlayer2D` on the `SFX` bus playing `coin.wav`
- **AnimationPlayer:** `pickup` animation that plays the effect, plays the sound, and calls `queue_free()` at the end
- **Logic (`coin.gd`):** when the player enters (`_on_body_entered`) it calls `game_manager.add_point()` and plays the `pickup` animation

### `slime.tscn` + `slime.gd`
The enemy.

- **Root node:** `Node2D`
- **AnimatedSprite2D:** slime animation (`slime_green.png`, 24x24 px, 4 frames at 10 fps)
- **Killzone:** an instance of `killzone.tscn` as a child, with its own `CollisionShape2D` (kills the player on contact)
- **RayCastRight / RayCastLeft:** detect walls/edges to reverse direction
- **Logic (`slime.gd`):** moves at `SPEED = 60`; when a RayCast collides it flips the direction and the sprite

### `platform.tscn`
Platform the player stands on.

- **Root node:** `AnimatableBody2D`
- **Sprite2D:** region of the `platforms.png` sprite
- **CollisionShape2D:** `RectangleShape2D` (29x7) with `one_way_collision` enabled (you can jump up through it)

### `killzone.tscn` + `killzone.gd`
Death zone.

- **Root node:** `Area2D` (with `collision_mask = 3`)
- **Timer:** controls the delay before reloading
- **Logic (`killzone.gd`):** when the player enters it prints "You died!", sets `Engine.time_scale = 0.5` (slow motion), removes the player's `CollisionShape2D`, and starts the Timer; when the Timer times out it restores `time_scale = 1` and reloads the current scene

### `music.tscn`
Background music.

- **Root node:** `AudioStreamPlayer2D` playing `time_for_adventure.mp3` with `autoplay`

### `game.tscn` + `game_manager.gd`
The main game scene.

- **Root node:** `Node2D`
- **GameManager:** `Node` with `game_manager.gd` (unique name `%GameManager`); holds `score` and `add_point()`
- **Player:** instance of `player.tscn` with a child `Camera2D` (3x zoom) with limits
- **StaticBody2D + TileMapLayer:** the world drawn with the `world_tileset.png` tileset and collisions
- **Killzone:** instance of `killzone.tscn` with a `WorldBoundaryShape2D` at the bottom of the level
- **Slime:** instance of `slime.tscn`
- **Coins:** container with two coins (`Coin`, `Coin2`)
- **Labels:** helper text ("Space to jump", "Falling hurts") using the `PixelOperator8-Bold.ttf` font
- **Platforms:** one static platform and another (`Platform2`) animated with an `AnimationPlayer` (`move` animation in ping-pong loop)

---

## 🎯 Controls

| Action | Input |
| --- | --- |
| Move left / right | `move_left` / `move_right` |
| Jump | `jump` (Space) |

Collect the coins to raise your score, avoid the slime, and don't fall into the killzone.

---

## 🛠️ Engine

- [Godot Engine 4](https://godotengine.org/) (scene format 3 / 4)

---

## 🖌️ Assets

- Sprites: `knight.png`, `coin.png`, `slime_green.png`, `platforms.png`, `world_tileset.png`
- Sound: `coin.wav`
- Music: `time_for_adventure.mp3`
- Font: `PixelOperator8-Bold.ttf`
- [Brackeys' Platformer Assets](https://brackeysgames.itch.io/brackeys-platformer-bundle)

---

## 📺 Tutorial

- [Brackeys - How to make a Video Game (Godot)](https://www.youtube.com/watch?v=LOhfqjmasi0)
- [Finished Project (Brackeys' GitHub)](https://github.com/Brackeys/first-game-in-godot)

---

## 🚀 Where to go from here

- Display the score on screen (update a Label from the GameManager)
- Add more levels and transitions between them
- Add a main menu and a game over screen
- Add more enemy types and hazards
- Export to web/desktop and share it
