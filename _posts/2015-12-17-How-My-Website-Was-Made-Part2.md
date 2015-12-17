---
layout: post
title: How My Website Was Made (Part 2)
---
This is part two of '[How my main website was made]'(https://rigellute.github.io/blog/How-My-Website-Was-Made/), which will cover the tools I used and why I chose them.

Aside from the standard HTML5 and CSS, the main tools I used were:

1. Bootstrap
2. jQuery
3. Greensock Animation Platform
4. ScrollMagic

#### 2.1
I love Bootstrap. It provides a solid framework for building fully responsive websites, which massively speeds up production time. I don't use it for every project (sometimes it is overkill), but I felt it suited the design I wanted early on. 

For optimization, I could go through the stylesheets and remove the unused classes. However, if I intend to expand the webpage in the future, many of those classes will likely be used.

#### 2.2
jQuery adds so much to vanilla javascript and I much prefer using it when writing javascript. The main benefit is the simple selector ($), but also the built in functions are extremely helpful – there is no need to reinvent the wheel every time you want to add simple functionality to the page (they are also highly optimized out the bag).

#### 2.3
Here we come to a JavaScript library that is gaining tremendous attention, and for good reason. The Greensock Animation Platform (GSAP) allows developers to control DOM elements with such precision, performance, control, and device/browser compatibility that it is a game changer. 

I use GSAP to change the CSS properties of DOM elements. For example, the loading animation at the start draws the SVG heptagon. This is achieved by calculating the length of the SVG path property  and animating the strokedashArray and strokedashOffset properties to 0.

To animate in the rest of the content, I create a 'timeline' and add 'tweens' (animation instructions) that animate from opacity:0, sometimes combining new x or y coordinates to change the element's position. 

More about GSAP in section three of this mini series. I will also write a tutorial on how to use GSAP.

#### 2.4
ScrollMagic is a scrolling library that allows us to effectively trigger GSAP animations based on the scrollbar position. Again, the performance is very good, and works across devices (for the most part). 

Using GSAP and ScrollMagic, I add a level of interactivity to an otherwise static page. The goal is to increase user engagement without trying to bamboozle the user with too much. A point to always remember is that the best animations are subtle, and complement the message or intended impact of the webpage.
- - -
I have carefully chosen to use these tools as they meet the requirements of high performance, compatibility, and creative freedom.

I have experimented extensively with skrollr.js, which works well but is no longer maintained (and there are problems with mobile scrolling). In addition, GSAP and ScrollMagic offer much greater degrees of creative freedom and performance. 

The next section explores some problems I ran into in the making of my webpage, and how I solved them. 
