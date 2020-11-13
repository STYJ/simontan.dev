---
title: Dodge the Creeps - enhanced edition
date: 2020-09-06
tags:
  - learn in public
  - projects
  - game dev
layout: layouts/post.njk
---

_Simon: I'm still trying to figure out the best way to do these game dev logs because technical articles might not be everyones' cup of tea so do feedback to me if you find certain styles of writing more enjoyable to read!_

Time for an update again! In my [first game dev log](../my-first-game), I shared about my initial foray into game development and built a game called "Dodge the Creeps". I tried to add my own twist to the game by implementing the following:

- mobs spawning in different sizes
- mobs spawn faster the longer you live

I was pretty proud of myself and wanted to share this achievement with my relatives and friends so I published the game on Newgrounds. What came next was definitely a surprise - feedback from a few members of the Newgrounds community on how to improve the game! The feedback were mostly around how the game feels too similar to the tutorial and that I should add my own personal twist to it. I went back to the drawing board to think about out how I can enhance it further and decided on the following (in no particular order):

- Settings menu
- Difficulty multiplier for score
- Multiple lives
- Spawn rate to sync with BGM
- High score
- New mobs
- New controller scheme

For each feature, I will share more about my thoughts, what I learnt, what I did not like / have enough time to try and how I plan on improving.

# Features

## Settings Menu

<img class="center" src="/img/settings.png" alt="An image of the settings menu" style="width: 40%;"/>

Unlike your conventional settings menu, my menu allows you to modify the game's difficulty by altering some of its core game mechanics. I learnt to create the menu by completing some of the UI tutorials found [here](https://docs.godotengine.org/en/stable/getting_started/step_by_step/index.html). These tutorials cover commonly used control nodes for designing interfaces and how to use them.

I really like the `container` node as they remind me of CSS grid layouts. For those who are unfamiliar with this, the biggest benefit for using containers is that it allows you to build responsive UIs that can automatically resize to accommodate different screen dimensions. That said, if your game has a fixed screen size then I feel like it might not be worth the effort to get the containers set up because it is like over engineering a solution compared to simply repositioning a child node's position.

I tried to use what I thought were the most appropriate node for each component but somehow it feels like I am not doing it the right way... 🤔 I guess a possible explanation for this feeling is that I do not have enough experience making menus so I just have to make more menus. I also tried to modify the theme to update the design of the `button` node but that failed as well so I will need to go and learn that too!

On a separate note, there is an open source project on github that provides creators with a template to quickly get started and it comes with a menu! I plan on studying the template to better understand how its developer(s) designed their interfaces. Here is the [link](https://github.com/AnJ95/godot-toolbox-project) to the repo if you want to check it out.

## Difficulty multiplier for score

If you are going to allow your players the option to choose what difficulty they want to play at then it is only fair for those who chose the harder difficulty to be rewarded with more points - the bigger the risk, the bigger the reward!

<img class="center" src="/img/difficulty-multiplier.png" alt="An image of the difficulty multiplier in the settings menu" style="width: 70%;"/>

I think the simplest solution to this is to rely on an extra variable that is multiplied with the default scoring rate (of 1 point per second). This multiplicative factor also has a default value of 1 so if the player chooses not to modify the difficulty then you will still get a rate of 1 score per second.

I think this is also how other games handle difficulty as well. For example, if I am fighting a boss on a higher difficulty then maybe the increased movement speed, the more unpredictable movement patterns and other common features of a higher difficulty boss fight would be turned on because the higher difficulty mode was selected. I particularly like the approach that I used to handle difficulty (especially if the game is simple) because it gives the players more options to choose from instead of difficulty levels with predetermined features. At the end of the day, the goal is to get as high as possible of a score and if it means choosing 3 lives and fixed spawn rate then go for it!

I encountered a strange issue when multiplying an integer with a float. In other programming languages, multiplying an int with a float results in a float. Likewise for division, as long as one of the variable is a float, the resulting value is a float. However, when I used a factor of 2.5 and multiplied it with 1, it showed me a value of 2. Needless to say, dividing 2 with 2.5 results in 0. Not entirely sure what is the cause of this but this can be entirely avoided if I were consistent with the data types of my variables!

## Multiple lives

The first option that players can decide on is whether or not they want to play the game with a single life or multiple lives. Playing with a single life will result in a score multiplier of 4x because with the default multiple lives option, every collision with any mob will clear the entire screen. This gives the player ample breathing room to reorientate and focus for the next onslaught of mobs and during this time, the player is still earning points. Since the player can do this 2 times, it seems fair to reward players who play with a single life more than at least 2x!

What proved really helpful for me when designing and implementing this feature was learning how to use the `tween` node from one of the UI tutorials that I shared earlier. The `tween` node is used for smoothly animating a node's property over time. In this case, I want to animate the player losing a life over a certain amount of time instead of instantly since it looks cooler! The end result looks something like this...

<img class="center" src="/img/lives-animation.gif" alt="A gif showing the animation for lives" style="width: 70%;"/>

The only issue that I have right now is that I do not quite remember what I did because it has been a while from when I made the game to finally getting the time to write this article so more relearning to do! Moreover, I think my `container` nodes were not configured very well because when I played in the single life mode compared to the multiple lives mode, the hearts were not positioned in the same place! I used a band-aid fix for it but a better approach would be to learn to use the container nodes correctly or to make it such that only 1/3 of a life gets removed on each collision.

A tip that I can give for drawing assets to be used in a `TextureProgress` node is to ensure that the image on the inside is smaller than the image on the outside and be center aligned. For example, the outer image (outline of my heart) is of size 50x50 and the actual layer is also of size 50x50. The inner image (the background fill of the heart) is also of size 50x50 but the layer is 40x40 and is center aligned i.e. a margin of 5px in all directions. You just have to make sure that your outline is thick enough to cover over the fill so that you cannot see the background of the game through the heart.

## Spawn rate to sync with BGM

A feature that I implemented as part of an earlier version of the game is an increasing spawn rate for mobs the longer the player is able survive. While I felt that this feature definitely made the game harder, it is not necessarily something that everyone wants to play with so I decided to make it optional and configurable via settings. If you'd like to learn more about how I implemented this, you can read it [here](../my-first-game/#feature-2%3A-increasing-game-difficulty).

While playing around with this feature, I noticed that the beat of the background music did not match the spawn rate of mobs. I recalled that without "Increased Spawn", mobs would spawn more or less in sync with the beat of the music. I think this is intended because these assets are provided with the tutorial. The additional layer of unpredictability did not add to anything to the game so I wanted to remove it. With the use of an online BPM counter and some simple math, I applied a band-aid solution to it by modifying the `pitch_scale` property of the `AudioStreamPlayer` node. This has the unfortunate side effect of a background music with an increasing pitch the longer you survive! Is that a bug or a feature? You decide! Here is a snippet of the implementation for the fix:

```gdscript
func _on_MultiplierTimer_timeout():
  # value of spawn_multiplier is modified through the settings
  # menu when the option "Increased Spawn" is selected.
  # Default value of spawn_multiplier is 1.

  $MobTimer.wait_time = $MobTimer.wait_time * spawn_multiplier
  $Music.pitch_scale = $Music.pitch_scale * (1 / spawn_multiplier)
```

On hindsight, I would not recommend modifying the pitch of the soundtrack but instead to think of a different way to increase the spawn rate of mobs. For example, at the start of a game, 1 mob is spawned whenever the timer node times out. This is increased to 2 after 20 seconds and to 3 after 40 seconds and so on. This approach allows your game's difficulty to increase without modifying the music.

## High score

<img class="center" src="/img/high-score.png" alt="An image of the highscore" style="width: 70%;"/>

A local high score system is a feature that is very simple to implement and should be familiar to those who did coding questions where you need to look for the highest value in an array. Essentially, you have a variable that tracks the maximum score and whenever the game is over, you compare the score of the current game with the maximum score recorded. If it is higher then replace it otherwise do nothing. Simple huh?

That said, it can get a lot more complex when you want to track it across games or compare between players on some global leaderboard. This requires you to persist the score elsewhere e.g. in your database when the player closes the game. This is one of the reasons (albeit an easier one) why making multiplayer games are hard! It becomes more than just how much hardware your players have since you have to deal with infrastructure, networking, security etc.

## New mobs

I also added 2 new mobs to the game. _drum roll_......

Introducing the jellyfish!

<img class="center" src="/img/jellyfish.gif" alt="A gif showing the jellyfish mob" style="width: 40%;"/>

and the ROCKET FISH!

<img class="center" src="/img/rocketfish.gif" alt="A gif showing the rocketfish mob" style="width: 40%;"/>

Growing up, we had to take compulsory art lessons but I was never really a big fan of it. I mean, I even failed the art exam. How do you _fail_ an art exam? Needless to say, I was a little hesistant when I brought up this feature as one of the possible things that I could do to improve the game. I could technically not do it but I feel that if I'm really going to do this whole indie thing then I need to embrace my creative mind. Of course, I left it to the end because I dreaded starting it and as expected, once I started, my brain farted immediately.

I was not sure what kind of mob would fit well with the current mob designs but since they look like jellyfishes, I thought that maybe something related to a jellyfish. Seeing as I do not have an actual jellyfish mob, I thought maybe I should just create a real jellyfish mob and that was how the idea for my first mob was conceived.

The design for the rocketfish mob came about because of a limitation. I was lazy and did not want to create an entirely new node for new enemy types so I decided to reuse the same mob node and a self imposed restriction that came with that is not modifying the shape and size of the `CollisionShape2D` node. I don't think anyone likes to get damaged when they are clearly no within range of getting hit from their point of view.

Going back to the rocketfish design, I thought to myself that a simpler approach would be to design a mob that can fit nicely with the current `CollisionShape2D` node. When you put these requirements together, you are somewhat limited... or at least I was. There are only so many ways you can design the upper half of a jellyfish so I needed to get a bit creative with the bottom half. Since I also have an interest in space, I thought that it might be cool to design a jellyfish that looks like a rocket ship and thus, the rocketfish was born!

Looking back, I think this was a pretty enjoyable experience. It is a change of pace compared to just programming the game's logic and this is also something that I want to be exposed to more often. I even bought a pixel art course on Udemy to learn how to draw pixel art so I will need to get around to doing that eventually!

## New controller scheme

Another feature that I implemented was to introduce a new control scheme. The previous control scheme only works for the keyboard which might be good for some types of games but not for mine. In fact, the folks that I shared my game with were all on their mobile phones when they attempted to play the game and they could not play it!

I decided to redo the control scheme such that the character follows the mouse as you hold down left click. On mobile, this is the equivalent of dragging your finger across your screen. Getting the character to follow the mouse was relatively simple since there were already code samples on the Godot documentation that you can copy and paste. I was also under the impression that the left click event is equivalent to the touch event but when I tried the game on mobile, the character would not move so back to the documentation I went!

Another issue that I faced with this new method is that when the character is directly above the mouse / finger, it goes crazy. It is easier to understand this problem if I showed you a short gif of it.

<img class="center" src="/img/crazy-movement.gif" alt="A gif showing the crazy movement bug" style="width: 40%;"/>

Notice how the character faces in one direction and immediately turns in the opposite direction and back again. This is probably because of how I used my current mouse / finger position to determine the speed and direction of the character. A simple fix for this is to only modify the speed and direction if it is greater than a certain distance from the mouse / finger. This means that there will always be a "gap" between the character and where the mouse / finger is actually at.

An unintended benefit that came to light with this control scheme is that it allows your character to move in substantially more angles and not just in 8 directions (up, down, left, right and the 4 diagonals) so it makes it a lot easier to maneuver the character through tight spots!

# What's next

If you managed to read all the way until here, give yourself a pat on the back and thanks a lot for the support 😊

<img class="center" src="/img/thank-you.gif" alt="A pusheen thank you gif" style="width: 40%;"/>
<a href="https://giphy.com/gifs/sticker-osjgQPWRx3cac">GIPHY</a>

This will probably be my last update to the Dodge the Creep game. Moving forward, I am planning to experiment with making at least 1 game in every genre to better understand what I find fun to create and play and also to dabble with some asset and music creation as well!

Hope you enjoyed the read :)
