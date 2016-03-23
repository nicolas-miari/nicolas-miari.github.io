---
layout: post
title:  "Highlighter"
date:   2016-03-23 17:35:00 +0900
categories: apps 
---

![App Icon](/assets/images/Highlighter-512.png){: .center-image }

Like I mentioned [last time][PrevPost-link], it is a lot of trouble to highlight a small region of
a screen capture image, like this:

![Example](/assets/images/highlighter_example@2x.png){: .center-image }

_(It would be substantially easier if you give up the fuzzy edges around the 
highlighted region, but you still need to 1. Add a new layer, 2. Paint it black,
3. Make it semi-opaque, 4. Select a rectangle and cut it out.)_

So I decided to make a small app that performs all this image processing (overlay 
a semitransparent dimming layer, and cut a hole in it with blurred edges) with 
just one mouse drag. 

The basic functionality is already working, but I still have some polishing (testing) 
to do. Stay tuned!

[PrevPost-link]: http://nicolasmiari.com/graphic/design/2016/03/17/highlighting.html
