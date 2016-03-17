---
layout: post
title:  "Highlighting a Region of an Image"
date:   2016-03-17 14:10:00 +0900
categories: apps 
---

Every now and then I need to post an image highlighting a certain region in it -a UI 
element that the reader should tap/click, an area of interest, etc., like this one:

![05](/assets/images/highlighting/r05@2x.png){: .center-image }


The way I end up making such images is as follows:

1. Capture the screen (e.g. using [Grab][Grab-Link]).
2. Open the captured region in an image editor (say, [Pixelmator][Pixelmator-Link]):

![01](/assets/images/highlighting/original@2x.png){: .center-image }

3. Add a new layer on top of the original image, and paint it black. Make it 
semitransparent by setting the opacity to -say- 50 percent:

![02](/assets/images/highlighting/w02@2x.png){: .center-image }

4. Select the area of interest that you wish to highlight, and hit "delete":

![02](/assets/images/highlighting/w03@2x.png){: .center-image }

5. Apply the gaussian blur filter to the semitransparent layer, to soften the
edges of the selected region and create a "spotlight" effect:

![02](/assets/images/highlighting/w04@2x.png){: .center-image }

As you can see, there is a problem with this naïve approach: The outer edges of 
the semitransparent layer get blurred too.

This happens because blurring is just a fancy way of averaging the color and 
opacity values of neighbouring pixels; the image editor can not make any
assumptions about what lies 'beyond' the canvas' boundaries.

To fix this, we instead proceed as follows:

1. Capture the screen using Grab.
2. Open the captured region in an image editor:

![00](/assets/images/highlighting/original@2x.png){: .center-image }

3. Enlarge the canvas in both dimensions, by a value strictly greater than the
blur radius you intend to use. (I typically use 100 pixels in both dimensions, 
because it makes it easy to remember the original size):

![01](/assets/images/highlighting/r01@2x.png){: .center-image }

4. Add a new layer on top of the original image, and paint it black. Make it 
semitransparent by setting the opacity to -say- 50 percent:

![02](/assets/images/highlighting/r02@2x.png){: .center-image }

5. Select the area of interest that you wish to highlight, and hit "delete":

![03](/assets/images/highlighting/r03@2x.png){: .center-image }


6. Apply the gaussian blur filter to the semitransparent layer, to soften the
edges of the selected region and create a "spotlight" effect:

![04](/assets/images/highlighting/r04@2x.png){: .center-image }

7. Restore the canvas to its original size:

![05](/assets/images/highlighting/r05@2x.png){: .center-image }

As you can see, now the resulting image looks as expected (only the "hole" in the
dimming layer has soft edges).

Admittedly, it is quite a pain to do this each time. That is why I am making a
small utility app that performs all these steps for you; stay tuned!

[Grab-Link]: https://en.wikipedia.org/wiki/Grab_(software)
[Pixelmator-Link]: http://www.pixelmator.com/mac/
