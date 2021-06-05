---
title: My first game!
date: 2020-07-23
tags:
  - projects
  - game dev
layout: layouts/post.njk
---

I did it, I made my first game! The last time I made a game was for my final year project in uni but I am too ashamed to talk about that so let me distract you with some gameplay instead!

<img class="center" src="/img/gameplay.gif" alt="A gif showing gameplay of dodge the creep" style="width: 40%;"/>

Pretty cool huh? Okay but truth be told, I followed [this tutorial](https://docs.godotengine.org/en/stable/getting_started/step_by_step/your_first_game.html) and after about ~6 hours, I created my first game with Godot! The tutorial is extremely informative and it holds your hands all the way from start to end. While this may not necessarily be the best way to learn, it is definitely a good approach to gaining familiarity with Godot's interface and capabilities.

After making a game, what is the first thing that you should do? You play it of course! That was what I did, I played the game multiple times and frankly, it was just too easy! I guess that is to be expected since the tutorial is called "your first game", not how to build the next WoW killer haha. Instead of starting on a new game, I wanted to make this game more unique and challenging. Since I lack experience in creating game assets, I thought that maybe the fastest way to accomplish this is to introduce new but **simple** game mechanics and interactions.

I brainstormed for a bit (literally 3 mins lol) and came up with these:

- Mobs spawning in different sizes
- The game gets progressively harder the longer you survive

## Feature 1: Varying Mob Size Implementation

For mobs to spawn in different sizes, I need to do 2 things:

1. I need to understand how to modify the size of 1 mob
2. I need to programmatically randomise the size of a mob as they spawn

### Task 1: Modify the size of 1 mob

The first thing that comes to mind when you want to modify the size of something is to change its dimensions but I was unable to find any property that is related to "length" or "width" in the inspector. I thought for a while and remembered that in one of the earlier sections of the tutorial, we were asked to use 0.75 under the `scale` property to modify the size of the `AnimatedSprite` node. I inspected the `RigidBody2D` root node and lo and behold, I found a `scale` property! In fact, every child node of my Mob scene contains a `scale` property.

I assumed that if I modified the `scale` of the root node, it would reflect accordingly on all child nodes instead of having to modify them one by one. I updated the x and y properties of `scale` and everything reduced in size as per my initial assumptions however, a warning also popped up.

<img class="center" src="/img/warning-rigidbody2d.png" alt="An image of the RigidBody2d warning" style="width: 70%;"/>

Usually warnings can be ignored so I decided to just run the game and see if mobs are actually smaller than before. Surprisingly, the mobs remained its original size. A quick google search of this warning taught me that you should not modify the `scale` of a `RigidBody2D` because it will simply revert to the original / default values. This meant that I should instead modify the `AnimatedSprite` and `CollisionShape2D` nodes separately. With this, I have completed my first task. Next, I need to programmatically spawn mobs of random sizes.

### Task 2: Programmatically spawn mobs of random sizes

A simple way to handle dynamic resizing is to have the `scale` multiply by a random number whenever a mob spawns. I chose an arbitrary range of 0.5 and 1 for this random number i.e. the scale of a mob can go from 0.375 to 0.75. Now I need to figure out how to generate a random number between 0.5 and 1. Luckily, the Godot editor has a built-in help feature and I quickly found a function that allows me to achieve the above result. By combining everything together, I am able to successfully spawn mobs of random sizes! The modified script for the Mob scene is as follows:

```gdscript
extends RigidBody2D

export var min_speed = 150
export var max_speed = 250

const ANIMATED_SPRITE_DEFAULT_SCALE = 0.75
const COLLISION_SHAPE_2D_DEFAULT_SCALE = 1
const MIN_SCALE_MULTIPLIER = 0.5
const MAX_SCALE_MULTIPLIER = 1

func _ready():
	# Setting a random animation for each new mob
	var mob_types = $AnimatedSprite.frames.get_animation_names()
	$AnimatedSprite.animation = mob_types[randi() % mob_types.size()]

	# Setting scale of AnimatedSprite and CollisionShape2D nodes
	var scale_multiplier = rand_range(
		MIN_SCALE_MULTIPLIER,
		MAX_SCALE_MULTIPLIER
	)
	var sprite_scale = scale_multiplier * ANIMATED_SPRITE_DEFAULT_SCALE
	var collision_shape_2d_scale = scale_multiplier * COLLISION_SHAPE_2D_DEFAULT_SCALE
	_set_scale($AnimatedSprite, sprite_scale)
	_set_scale($CollisionShape2D, collision_shape_2d_scale)


func _on_VisibilityNotifier2D_screen_exited():
	# Queues the mob instance to be freed.
	# Mobs will delete themselves when they leave the screen.
	queue_free()


func _set_scale(node, value):
	node.scale.x = value
	node.scale.y = value

```

Here is a gif showing mobs being spawned with random sizes:

<img class="center" src="/img/random-mob-size.gif" alt="A gif of mobs spawning with random sizes" style="width: 40%;"/>

## Feature 2: Increasing game difficulty

There are many ways to increase a game's difficulty but I feel that it is somewhat limited to the type of game that you have. For example, if you have an RPG game, you can increase the difficulty of a boss by increasing its damage and health but where is the fun in that! In my opinion, a better way to increase difficulty is to introduce more game mechanics like having the boss become more unpredictable the lower its hp. You are only really limited by your creativity!

There were many things I could do to make the game harder like having different types of mobs with different behaviours, mobs that shoot out stuff that you need to dodge (like a [SHMUP](https://en.wikipedia.org/wiki/Shoot_%27em_up)), mobs that move randomly instead of just in a straight line etc., but I figured that I wanted to do something simple. Since the game is called "Dodge the Creeps", I thought maybe I could just increase the creeps' density. What that means is that the longer you survive, the faster enemies spawn! I do not really know if that is considered fun but it definitely sounds like it will make the game more difficult (maybe too difficult haha)!

The tutorial introduced an interesting way of using `Timer` nodes and its timeout signal to indicate when mobs should spawn and when your score should increase. As an aside, this resembles a lot to event driven programming. Following that train of thought, perhaps I could also have a `MultiplierTimer` that on every timeout reduces the `wait time` property of `MobTimer` ever so slightly.

### Task 3: Implementing a multiplierTimer

Instead of decreasing `wait time` linearly by substracting a fixed constant from it, I felt that perhaps multiplying `wait time` by a number less than 1 is the better approach because it will never be negative nor underflow. 

There are 2 considerations that I want to highlight:

1. You do not want to decrease the `wait time` property on `multiplierTimer` because that has no effect on how fast the mob spawns!
2. I am also making the assumption that you will never be able to get the `multiplierTimer` to reach such a low value in the first place because there will too many creeps to dodge but I guess I should also implement a minimum threshold for `MultiplierTimer` just to err on the side of caution!

I added a `Timer` node as a child node to the Main scene, connected the timeout signal and implemented the logic as described above. The last thing to do was to start and stop the `MultiplierTimer` in the correct places i.e. starting it when the game starts and stopping it when the game ends. The modified script for the Main scene is as follows:

```gdscript
extends Node

# exposes a variable called Mob on the inspector
export (PackedScene) var Mob

var score
const MULTIPLIER = 0.99
const MOB_TIMER_DEFAULT_WAIT_TIME = 0.5

func _ready():
	randomize()

func game_over():
	_stop_timers()
	$HUD.show_game_over()
	get_tree().call_group("mobs", "queue_free")
	$Music.stop()
	$DeathSound.play()
	# Reset MobTimer
	$MobTimer.wait_time = MOB_TIMER_DEFAULT_WAIT_TIME

func new_game():
	score = 0
	$Player.start($StartPosition.position)
	$StartTimer.start()
	$HUD.update_score(score)
	$HUD.show_message("Get Ready")
	$Music.play()

# When the MobTimer counts down to 0, spawn a mob.
func _on_MobTimer_timeout():
	# Choose a random location on Path2D.
	$MobPath/MobSpawnLocation.offset = randi()

	# Create a Mob instance and add it to the scene.
	var mob = Mob.instance()
	add_child(mob)

	# We use Pi because GDScript uses radians, not degrees
	var direction = $MobPath/MobSpawnLocation.rotation + PI / 2

	# Set the mob's position to a random location.
	mob.position = $MobPath/MobSpawnLocation.position

	# Add some randomness to the direction.
	direction += rand_range(-PI / 4, PI / 4)
	mob.rotation = direction

	# Set the velocity (speed & direction).
	mob.linear_velocity = Vector2(rand_range(mob.min_speed, mob.max_speed), 0)
	mob.linear_velocity = mob.linear_velocity.rotated(direction)

# When ScoreTimer counts down to 0, add a score.
func _on_ScoreTimer_timeout():
	score += 1
	$HUD.update_score(score)

# When StartTimer counts down to 0, start!
func _on_StartTimer_timeout():
	$MobTimer.start()
	$ScoreTimer.start()
	$MultiplierTimer.start()

# Reduce MobTimer every time MultiplierTimer times out
func _on_MultiplierTimer_timeout():
	$MobTimer.wait_time = $MobTimer.wait_time * MULTIPLIER

# Stop all timers
func _stop_timers():
	$ScoreTimer.stop()
	$MobTimer.stop()
	$MultiplierTimer.stop()
```

Here is an image of the game with a 0.8 multiplier factor. I could not even last 5 seconds lol:

<img class="center" src="/img/0.8-multiplier.png" alt="An image of the game on 0.8 multiplier" style="width: 40%;"/>

There you have it, Dodge the Creeps! I quite enjoyed this process of building a game and extending it further. It actually took me less time to build these 2 extra features than to write up this post but I think it might be very different in the future! If you want to play the game, head over to [Newgrounds](https://www.newgrounds.com/portal/view/760991). The source code for the game can be found [here](https://github.com/STYJ/Dodge-the-Creeps-enhanced-edition).

I have plans on upgrading the game even further, Dodge the Creeps enhanced edition if you will. There are some ideas that I want to try, with the most complicated being to convert the game into a multiplayer but let's not get ahead of ourselves here haha! Let me see how far I can get with what I currently know and I will update you guys again when the next version of the game goes live! 

Edit: There was actually a small bug in the game! I forgot to reset `MobTimer`'s `wait time` so every time you restart the game, the difficulty continues from the last game whoops! I have since patched the bug and now it is working as intended! I should really test my code next time though haha 😅