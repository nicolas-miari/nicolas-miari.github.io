---
layout: post
title:  "DinnerJacket.framework"
date:   2016-10-11 19:33:00 +0900
categories: development 
---

![Frameworks Icon](/assets/images/FrameworkIcon.png.png){: .center-image }


There's recently a trend in naming shared libraries and frameworks with fancy names that have nothing to do with the software's functionality; for example take Alamofire, Freddy, and Starscream, to name a few in the cocoasphere.

I started developing my own sprite library for iOS back in 2010, and although I do not work on it very often, I keep improving it and over the years, it has gone through several incarnations (and names). 

Back then, I had just finished my first iPhone game, using the popular open-source library known as [Cocos2d-iPhone](http://cocos2d-objc.org). 
The game was simple 3D puzzler, but the 3D requirements were so few that I just needed to write some OpenGL ES 1.1 code to extend the library's functionality. 

Cocos2d is a great library and very easy to use. But there were a few things that bugged me about it. At that moment, Apple and other smartphone manufacturers were transitioning to GPUs with a programmable pipeline (shaders), but the current version of Cocos2d was stuck in the older, fixed-pipeline version of OpenGL ES (1.1).
Although the geometry of my game was minimal, I still wanted to be able to experiment with fancy visual effects to
enhance the user experience. The 2.0 API was there for anyone to use, but the library just hadn't had time to make the transition yet.

Secondly, even though I am a computer graphics major, back then the last graphics programming I had done was learning some Direct Draw at a previous job, and before that, immediate-mode desktop OpenGL in the early 00's at college. In the constantly evolving mobile arena of modern times, I really felt left behind. I needed to learn the present-day graphics programming idioms and techniques.

Finally, it was _somebody else's code_. I am not an advocate of reinventing the wheel every time (especially when the available options are so plenty and so good), but sometimes you just have to. 

In this case, I decided that I'd rather be the guy who can _build_ his own sprite library from scratch, than just another guy who knows how to _use_ somebody else's library.

Fast forward to today, iOS has made great strides, and OpenGL ES, as of version 3.0 has converged closer towards its desktop ancestor. What used to be a folder with source files copied and pasted between different projects (and all the version control madness that entails), is now a dynamic framework whose source code I can keep in one place.

Following the trend mentioned at the beginning, I am renaming the library Dinner Jacket. That name merely reflects something that I like (black tie), and has absolutely nothing to do with the library's characteristics.

Although the days of OpenGL (and Objective-C) seem to be numbered, I owe to my library a big, final update to modern standards before I move on to other projects. Also, there is a small trail of games I developed mostly in my spare time, over the years, that broke on way or another on subsequent OS updates and I was forced to pull from the AppStore. I owe those games a remake and a relaunch.

But after that is done, I will port the framework to the Metal API, and at the same time rewrite it in Swift.

Rest assured, the modernized version already exists as a stub on a private Github repository, and it is called MetalJacket.

