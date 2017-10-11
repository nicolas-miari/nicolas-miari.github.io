---
layout: post
title:  "Developing a Game Engine Part III: Stage Structure"
date:   2017-08-18 10:53:00 +0900
categories: development 
---

(Read Part 2 [here][Prev-Post-Link].)

### What's in a Stage

So far we've talked about how stages are linked together and how to get from one
to another. However, we still don't know what the actual stages look like 
internally; let's think about it now.

#### Substructure

At first glance, it feels as if each stage is just a tile map with objects in 
it. These include collectible objects (gems, coins, inventory items, etc.), 
traps, triggers (including exits), NPCs, etc. each placed at a specific 
location of the map grid. But we can do better than this.

In some 2D platformers, action within a stage isn't just continuous scrolling 
along a large map: sometimes the player goes through a "door" that leads to a
different "room", typically immediately. Sort of like linking between stages, 
but within the same stage, and perhaps you can traverse the door back in the 
direction you came from (but not always: think trapdoors). The goal is to make
the stage experience richer by providing different sub-environments, perhaps 
each with its own mood: a unique visual style, or eve a different BGM 
altogether.

So, a stage is (again), a (possibly directed) network of tile maps. This 
generalizes the notion of a __gate__ into a trigger that leads to a specific 
location on another map, possibly in a different stage.

#### Contents


_Coming next: Part 4._

[Prev-Post-Link]: http://nicolasmiari.com/development/2017/08/17/GameEngine_2.html
[Next-Post-Link]: http://nicolasmiari.com/development/2017/08/19/GameEngine_4.html
