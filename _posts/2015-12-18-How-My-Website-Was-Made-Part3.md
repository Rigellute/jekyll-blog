---
layout: post
title: How My Website Was Made (Part 3)
---
This is part three of [How my main website](https://rigellute.github.io/blog/How-My-Website-Was-Made/) was made and will explore some of the problems I ran in to when making my main website, including how I overcame them. 

After creating my initial mockup, I made the mistake of moving full-steam-ahead with the animations based on the desktop. I crafted complex timelines with responsive offsets that worked well for screens above `1024px` (desktops).

I relied on bootstrap to take care of the mobile version, though this was not nearly enough. For example, as I am using an SVG file for my logo, there were alignment issues on mobiles and tablets. Another problem consisted in the heights of the sections; set to `100vh` on desktop works well but means content spills over on mobile. Fortunately, these problems were a simple fix using CSS media queries. 

But things got really messy after creating initial scrolling animations. For example, on the desktop version I animate the portfolio section's title and image from left and right respectively, pushing them beyond the viewport. On mobile, this causes the width of the page to spill over the viewport (meaning you can scroll right and left). This is a problem as you could scroll beyond what I want you to see, missing some of the content and animations. 

To make things worse, certain devices did not like some animations. For example, some android devices simply refused to scroll. The old advice is to disable all animations for touch devices, but I wanted to push it and try to get them working. 

In the end, the solution to these JavaScript issues was to create a number of JavaScript media queries. I essentially made two different scrolling sequences for touch devices and desktop devices.

This is where Modernizr.js came in extremely handy. The loading animation at the start exists independently of the scroll bar and contains the large SVG logo, so to solve problems I used a simple if-else statement that determines touch devices:

``` javascript
if (!Modernizr.touch) {
// GSAP tweens for non-touch devices
} else {
// touch devices
}
```
For the scrolling animations I used an ordinary JavaScript media query based on device width to separate desktop and mobile devices:

``` javascript
if (window.matchMedia("(min-width: 89em)").matches) {
// large screens and up
} else {
// small screens
}
```

The mobile overflow issue couldn’t be solved using CSS `overflow: hidden`, instead I had to just animate everything in from the left. As expected there were more problems unique to smaller devices, and this media query solved most of them.

However, it turns out this wasn't enough. After solving most of the device size issues, I then had to combat the peculiarities of different device operating systems. 

Only having iOS devices on hand to test on, I could ensure functionality for those device. When it came to Android, some devices worked as expected (galaxy S6), whilst others (galaxy tab) refused to even scroll. 

With no errors being thrown, I decided my only option was to disable ScrollMagic for non-iOS. Unlike with iOS, not all Android devices are sufficiently powerful enough to offer a decent user experience with the scrolling animations. Not to knock Android devices, but they serve almost all areas of the market, from low-end to high-end. Meaning some devices work well while others do not. 

So to guarantee usability for Android, I wrote this little script to query the device OS using Modernizr:

``` javascript
    //Add Modernizr test
    Modernizr.addTest('isios', function () {
        return navigator.userAgent.match(/(iPad|iPhone|iPod)/g) ? true : false;
    });
```
and inserted an else if into my main scrolling media query:

``` javascript
else if (Modernizr.isios) {
// animations for iOS
} else {
	// disable scrollMagic
}
```

After all this device separation, the site works well on iOS devices. For Android, it has been tested on a Galaxy S6, Galaxy Tab and Google Nexus. Of course, I would relish the opportunity to test on more devices, but I currently don't have access to them – this is an important reason behind why playing it safe and disabling the scrolling animations is prudent. The CSS and HTML should work on almost all but the most antiquated browsers.

### Conclusion

I have learnt an enormous amount building my main page. As with many things, much of what I learnt I had already known, at least to some extent, but had not fully understood. New projects nearly always provide new perspectives to recurring challenges, and these new perspectives lead to new problem solving skills. The result of which ultimately improves your overall ability as a developer.

 Here is a summary of important points:

* Always create a simple responsive website first. And then add complexity later.
* Play it safe and don't overcomplicate the site interactivity, especially for mobile devices.
* Optimize code and take advantage of things like GPU acceleration for high performance rendering.
* Adhering to coding standards and use Javascript comments.
* The importance of testing: test test test. Although this WILL lead to one's head hitting the table over and over.
* Know the peculiarities of different devices and operating systems.
* Choose the correct tools for the job—Not only saves time, but opens up higher levels of creativity.  
