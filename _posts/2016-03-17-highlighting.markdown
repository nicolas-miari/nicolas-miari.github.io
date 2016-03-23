---
layout: post
title:  "Highlighting a Region of Interest in an Image"
date:   2016-03-17 14:10:00 +0900
categories: graphic design 
---

Every now and then I need to post an image highlighting a certain subregion of 
it. For example, a UI element that the reader should tap/click, an area of 
interest, etc., like this one:

![05](/assets/images/highlighting/r05@2x.png){: .center-image }

_(I want to show the user where the "Visible at launch" checkbox is)_


The way I end up making such images is as follows:

1. Capture the screen (e.g. using [Grab][Grab-Link]), and open the resulting 
image in an image editor application (for example, [Pixelmator][Pixelmator-Link]):

    ![01](/assets/images/highlighting/original@2x.png){: .center-image }

2. Add a new layer on top of the original image, and paint it black. Make it 
semitransparent by setting the opacity to -for example- fifty percent. We will 
call this the _dimming layer_, for obvious reasons:

    ![02](/assets/images/highlighting/w02@2x.png){: .center-image }

3. Using the "Rectangular Marquee" or "Elliptical Marquee" tool, the select the 
area of interest that you wish to highlight. Then, select the dimming layer and 
hit 'delete'. This will open a "hole" will in the dimming layer:

    ![03](/assets/images/highlighting/w03@2x.png){: .center-image }

4. Finally, apply a gaussian blur filter to the dimming layer, so as to soften 
the edges of the selected region and create a "spotlight" effect:

    ![04](/assets/images/highlighting/w04@2x.png){: .center-image }

As you can see, there is a problem with this naïve approach: The outer edges of 
the dimming layer get blurred too, and it looks untidy and distracting.

This happens because blurring is just a fancy way of averaging the color and 
opacity values of neighbouring pixels; the image editor does not have any values
for the hypothetical pixels 'outside' the image's bounds, so it simply assumes 
"Fully transaprent". 

To fix this, we need a way to tell the blur filter that -for all intents and
purposes- the black semitrasnparent layer extends "all the way". 

So, we use **_this_** workflow instead:

1. Capture the screen using Grab.
2. Open the captured region in an image editor:

    ![00](/assets/images/highlighting/original@2x.png){: .center-image }

3. **Enlarge** the canvas in both dimensions, by a value strictly greater than the
blur radius you intend to use later:

    ![01](/assets/images/highlighting/r01@2x.png){: .center-image }

_(I typically use 100 pixels in both dimensions, 
because it makes it easy to remember the original size. It is comfortably larger 
than the blur radii of my preference: between 10 and 15 pixels)_

4. Add a new layer on top of the original image, and paint it black. Make it 
semitransparent by setting the opacity to -for example- fifty percent:

    ![02](/assets/images/highlighting/r02@2x.png){: .center-image }

5. Using the "Rectangular Marquee" or "Elliptical Marquee" tool, the select the 
area of interest that you wish to highlight. Then, select the dimming layer and 
hit 'delete'. This will open a "hole" will in the dimming layer:

    ![03](/assets/images/highlighting/r03@2x.png){: .center-image }


6. Apply the gaussian blur filter to the dimming layer, to soften the
edges of the selected region and create a "spotlight" effect:

    ![04](/assets/images/highlighting/r04@2x.png){: .center-image }

7. **Restore** the canvas to its original size:

    ![05](/assets/images/highlighting/r05@2x.png){: .center-image }

As you can see, now the resulting image looks as expected (only the "hole" in the
dimming layer has soft edges).

Admittedly, it is quite a pain to do this each time. That is why [I am making a
small utility app that performs all these steps for you][HighlighterPost-Link]; stay tuned!

[Grab-Link]: https://en.wikipedia.org/wiki/Grab_(software)
[Pixelmator-Link]: http://www.pixelmator.com/mac/
[HighlighterPost-Link]: http://nicolasmiari.com/apps/2016/03/23/Highlighter.html

