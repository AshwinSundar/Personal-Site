+++
linkTitle = "Square One"
shortTitle = "Square One"
title = "Back to Square One"
draft = false
genres = ["other"]
date = 2022-08-01
+++

The original version of this website was written using GatsbyJS, a headless CMS engine that's all the rage right now in the world of web development. After a few weeks, I learned that it was tremendously overkill for a personal website with maybe a few dozen pages (including all my blog posts). Most importantly though, GatsbyJS is bloated with dependencies that take forever for me troubleshoot when all I want to do is add support for MathML.

The zipped, compressed, ready-to-deploy GatsbyJS package is 18.6 MEGABYTES. For a couple dozen pages. It's nuts. I'm a little scared of looking at how big the uncompressed source code is . . ._waiting for Mac Finder to calculate size_ . . . 1.03 GIGABYTES for 62 THOUSAND items??? Are you kidding me??? How many NPM modules do I need to run this tiny site???

I got fed up with learning what I consider non-value-add information about a fad-ish website-building engine, and decided to go back to basics.

I threw it all away. I got a bit overzealous, and threw away Javascript too. That's right - this site is written entirely in HTML and CSS. That's it. This decision was driven partially about seeking the most minimal toolset possible (which I believe I have achieved), and also by my disdain for the anti-intellectual patterns present in Javascript and the community. But who knows, maybe I'll bring back Javascript. Or maybe I'll hook this site up to Rust + WebAssembly, a side project I've wanted to pursue for a while now anyways.

I also plan to working in software development for a while, and will likely own this website for decades of my working lifetime. I want something that's future-proof. I can guarantee that exactly 0 of the popular frameworks today will be popular (or even exist) in 10-20 years. Who knows what will be popular then. I don't care, to be honest. And I don't have to, because HTML and CSS are here forever.

Update: August 26th, 2022
After a couple of weeks of working on other projects, I revisited my personal site to write a new blog post. And WOW it just felt second-nature to enter the code base and figure out what to do, even though I had completely forgotten about the architecture I built (2 weeks is a long time in my head). When I build stuff from the ground up, I always am wary of my poor free recall ability, and leave myself breadcrumbs as I work on things. In the case of this site, I left PLENTY of breadcrumbs, so it was a breeze to pick things up and keep working.

I contrast this with using GatsbyJS, which was I built this site on originally before tearing it down to the ground. Granted, this might be true for any framework that I'm somewhat green to. Which is pretty much every framework, because web development just doesn't stop changing.

As a multidisciplinary software engineer I'm not always working in the same field. At my first job I was working in infrastructure tooling at a medical device company. In my current job I'm a consultant who gets move around projects every 6 months or so. I started out on a web development project, but now I'm in an embedded project, which means I'm not going to keep up with the web dev world for several months at least. Things will definitely change in that time, because that's just the nature of the twitchy field.

Anyway I'm a minimalist developer so I get the most pride out of removing unnecessary code, more so than writing new code.
