---
layout: post
title:  "DinnerJacket.framework"
date:   2016-10-11 19:33:00 +0900
categories: development 
---

![Frameworks Icon](/assets/images/FrameworkIcon.png){: .center-image }


There's recently a trend to give open source libraries and frameworks **fancy names** that have nothing to do with the software's functionality; for example: [Alamofire](https://github.com/Alamofire/Alamofire), [Freddy](https://github.com/bignerdranch/Freddy)[^1], and [Starscream](https://github.com/daltoniam/starscream) (to name a few ones that are prominent in the "cocoasphere").

I started developing my very own **sprite library** for iOS back in 2010, and although I do not work on it very often, I keep improving it and over the years and it has gone through several incarnations (and names).

Back then, I had just finished my first iPhone game [^2], using the (then popular) open source library known as [Cocos2d-iPhone](http://cocos2d-objc.org).
The game was a simple 3D puzzler, but the 3D requirements were so minimal that I just needed to write some custom OpenGL ES 1.1 code on top of the library's existing functionality (unlike SpriteKit, cocos-2d iPhone provides direct access to the OpenGL ES layer for performing custom drawing other than 2D sprites).

Cocos2d is a great library and very easy to use; but there were a few things that bugged me about it. At that moment, Apple and other smartphone manufacturers were transitioning to GPUs with a programmable pipeline (i.e., shaders), but the current version of Cocos2d was stuck in the older, fixed-pipeline version of OpenGL ES (1.1).
Although the geometry of my game was minimal, I still wanted to be able to experiment with fancy visual effects in order to
enhance the player's experience. The programmable pipeline-ready 2.0 API was there for anyone to use, but the people developing Cocos2d just hadn't had time to make the transition yet.

Secondly, even though I am a computer graphics major, back then the last graphics programming I had done was learning some Direct Draw at a previous job, and before that, immediate-mode desktop OpenGL in the early 00's at college. In the constantly evolving mobile arena of modern times, I really felt left behind. I needed to learn the present-day graphics programming idioms and techniques.

Finally, it was **somebody else's code**. I am not an advocate of reinventing the wheel every time (especially when the available options are so plenty and so good), but there are exceptions.

In this particular case, I felt I would rather be someone with enough technical skills to **build his own sprite library from scratch**, than just another programmer who knows how to **use** somebody else's library.

Fast forward to today, and iOS has made great strides. OpenGL ES, as of version 3.0, has converged closer towards its desktop counterpart. And regarding my "library", what used to be a folder with source files copied and pasted from one project to another (and all the version control madness that entails), is now a dynamic framework whose source code I can keep in one place.

Following the trend mentioned at the beginning of the article, I have re-christened the code base to **_Dinner Jacket_**. The name merely reflects something that I like (evening dress), and has absolutely nothing to do with the library's capabilities.

Although the days of OpenGL (and Objective-C) seem to be numbered, I owe to my library a big, final update to modern standards before I move on to other projects. Also, there is a small trail of games I developed mostly in my spare time, over the years, that broke on way or another on subsequent OS updates and I was forced to pull from the AppStore. I owe those games a remake and a relaunch.

But after that is done, I will port the framework to the Metal API, and at the same time rewrite it in Swift.

#### _Update (2017 Oct 11)_
I have officially abandoned development of DinnerJacket and moved to my next project library, redesigned from scratch with Swift and Metal in mind (some design ideas were inherited, though). The new project is still private, but I will be writing blog posts on its design and architexture.

In the mean time, DinnerJacket is now **open source** and the (first and) final release is available on [GitHub](https://github.com/nicolas-miari/DinnerJacket), for reference and demonstration purposes.

[^1]: To be fair, this one is sort of a pun.
[^2]: As is usually the case with someone who can not make time to keep his personal projects up to date, it is currently removed from sale until I can modernize it.
