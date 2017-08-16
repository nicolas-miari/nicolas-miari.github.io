---
layout: post
title:  "Developing a Game Engine, Part I: The Genesis"
date:   2017-08-16 10:53:00 +0900
categories: development 
---

### Background

In 2011 I was working at a small shop that specializes in content creation and 
manangement of their own IP assets. At some point I was given an incredible 
amount of creative freedom and set to develop my own idea of a 2D game.

I had my own sprite library I had been polishing since 2010 and soon found out 
that I also needed I tilemap editor (I didn't want to use an existing tool: in line
with my ideology of creating my own sprite library from scratch, I wanted a custom
tilemap engine that was compatible with it).

It worked but it was buggy and feature limitted; I could live with it for the 
short period of time it took to develop the nine stages of the very simple game, 
but it was too much to ask other people to use it (or even myself, in the long 
run). 

The game didn't do well, but after I left the job the good folks at the company 
ceded the rights to the app to me (it was my brainchild after all: not just the 
code but the whole idea and visual design too. Also, it wasn't IP good enough 
that they could monetize. I'm not the guy who invented Pokémon or anything). In 
the end, the custom sound library I was using broke with one of the iOS updates 
(it seemed to rely on a bug that got fixed, apparently!) and I removed it from 
sale.

I promised to myself that I would recreate the map editor from scratch, 
one day, update my game with support for modern devices, re-release it, and move
on to develop further games.

I have been trying since, but at each turn I found myself facing design 
that I could not solve. I wanted my map editor to have the capability of 
"testing" and tuning each map in real time, during development (without having 
to export it and import into the game project each time), but on the other hand 
I didn't want the editor to know too much about the game in order to keep it 
generic and versatile.

### The Turning Point

Last night I couldn't sleep and set to think about what I'm rally trying to do
with my (stagnant) personal project. I decided to change my mentality and 
develop a full-fledged game editor.

A game-agnostic map editor that can also "test run" the maps being created is an
impossibility. Instead, I will draw some very generic constraints of what 
constitutes a tilemap-based game, and design my game editor around that. It will 
be basically a game template with lots of options to configure.

The bonus is that most of the logic will be coded once, into the engine 
framework, and each particular game I develop after that will consist of custom 
assets and settings of the engine. Kind of like Unity3d or Unreal Engine, but 
tailored to my own goals.

_Next: [Part 2][Next-Post-Link]._

[Next-Post-Link]: http://nicolasmiari.com/development/2017/08/17/GameEngine_2.html
