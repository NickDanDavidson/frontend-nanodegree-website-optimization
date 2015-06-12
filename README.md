#Nick Davidson's Website Optimization Project
---------------------------------------------

##About the Project

First I was given a webpage that needed improvement. I used knowledge about the Critical Rendering Path to optimize the page for performance and loading speed. Then I was given a fake pizza business site that was experiencing scrolling "jank." I used knowledge about how browsers render webpages to optimize the scrolling animation to better than 60 frames per second.

##Steps to run project successfully

###PageSpeed

- Open the [live page](https://nickdandavidson.github.io/frontend-nanodegree-website-optimization) in your favorite browser.

- Then in a separate browser tab, go to [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) and type in the same URL that you used to open the live page. This should show my PageSpeed Insights scores.

###Pizza.html

- Open the [pizza page](https://nickdandavidson.github.io/frontend-nanodegree-website-optimization/views/pizza.html) in your browser.

- Open DevTools and navigate to the Timeline.

- Switch on Profile JS and Paint.

- Press the record button at the top left, scroll a bit, then press the record button again to view the record.

- Once you have reviewed the scrolling records, find the pizza resize button, press the record button again, click the resize button a few times, then press the record button again to view the record.


##Optimizations I made

###Optimizations to index.html

- Added media=“print” to print.css link

- Resized and compressed pizzeria.jpg using GraphicsMagick (improved speed tremendously!)

- Resized and compressed profilepic.jpg using GraphicsMagick

- Made the analytics JS files async

- Added WebFontLoader JS to use Google Fonts instead of adding render-blocking CSS that is not optimized

- Made WFL JS async (huge performance boost on mobile making JS async and delivering fonts thru WFL)

- Inlined all CSS (only thing left to optimize after others) - got mobile score over 90

- Removed unnecessary and unused CSS rules

###Optimizations to views/js/main.js

- I changed instances of document.querySelector to document.getElementById and document.querySelectorAll to document.getElementsByClassName

- I removed the determineDx function and replaced it with a switch case in the changePizzaSizes function, which uses a %-based new width

- I moved querying elements outside of for loops, especially if the element need only be queried once

- I changed the calculations for the left property and phase of each pizza outside the for loop and stored their unique values in arrays instead of using modulo operations (not sure if this really matters, but it was mentioned as a possible scripting bottleneck in the office hours)

- I made comments wherever I made optimizations

- I also added a will-change: transform rule to the .mover class to force each moving pizza into its own layer. This cut the painting time down significantly
