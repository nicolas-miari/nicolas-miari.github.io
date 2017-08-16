---
layout: post
title:  "Developing a Game Engine Part II: Stage Architecture"
date:   2017-08-17 10:53:00 +0900
categories: development 
---

(Read Part 1 [here][Prev-Post-Link].)

### Stages

So I set to develop a game engine so generic that, just by providing custom 
graphic and sound assets, and tweaking a few settings here and there, it could 
produce the working code for any game I want.

This means that I need to isolate the most general structure shared by all the 
games I expect to develop (i.e., 2D action/puzzle platformers), and work my way 
from there. 

Let's take a moment and think what that is.

__First__, a basic 2D platformer consists of a _series_ of stages. You start at 
stage 1 and proceed until you find the exit, which leads to stage 2. Once you 
complete all stages, you have finished the game.

But is that the most _general_ structure possible? Definitely not: some games 
have a "world map" connecting several "village" stages. With exceptions 
-typically dictated by game progress- you can get to any stage from the world 
map. Once you enter a stage, some games let you "return to 
map" at any moment (typically from the "pause" menu), while others force you to 
complete the current stage first. And even if the game is "linear" 
as in the previous paragraph, the condition to complete a stage can be anything 
from finding an exit, to defeating a boss, or collecting a certain amount of 
items.

So, a game is not a series of stages: it is more of a (potentially directed) 
**network**. In games that include a "world map", the map itself is also a stage 
(with very different rules from the "village" stages). There's even the 
possibility that there are multiple world maps, linked by (for example) bridges 
that become accessible partway through the game, etc.

#### Gates

Each stage can be entered and exited somehow. For this, we need portals or 
gates. A gate is an object placed somewhere within a stage. It can work as 
either an entrance or an exit. When an exit is entered by the player character, 
it transports it to a specific entrance of another stage! That is, each exit 
gate leads to an entrance gate in some stage (entrance stages do nothing when 
entered: they are mere "starting points" for game play on that stage).  

Each stage can have more than one exit: think of the world map we described 
earlier. But it can also have more than one entrance: Each particular "village"
stage, when completed, takes the player character back to the world map, at the 
location of the village's entrance!

#### Cut Scenes

We can generalize the concept of the stage further: What about the "cut scenes"?
You know, those animations that typically happen in between (sometimes within) 
stages, to advance the story? Those can be though of as special cases of stages 
too. The inter-stage cut scenes are just stages where there is no user input and
all the characters are scripted! Of course, scripting and temporary cancellation 
of user input can also happen temporarily within a 'regular' stage, perhaps 
triggered by some action of one of the characters (e.g., stepping on a trap). 

#### Triggers

This bring us to the concept of triggers, which are nothing more than a 
generalization of the exit gates we talked about earlier. A trigger is basically 
a location on a stage (a single tile or a group af adjascent tiles, if it needs 
to be larger) that, when entered, causes some predetermined action to happen. 
The action can be:

- Teleport the player character (and thus, advance the game) to a specific 
location (entrance) of a specific stage,

- Run a script that causes change and/or programmed motion in one or more 
characters or map objects (optionally, disabling user input while at it)

etc.

_Coming next: Part 3._

[Prev-Post-Link]: http://nicolasmiari.com/development/2017/08/16/GameEngine_1.html

