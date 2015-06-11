#Nick Davidson's Website Optimization Project
---------------------------------------------

##Steps to run project successfully

I did not know how to get my site onto the public internet except for publishing it or using ngrok to tunnel it locally. So I opted for using ngrok because that seemed the best option.

###PageSpeed

- If you do not have ngrok, it is available as a node module. At your terminal, type npm install ngrok -g (or go here for more details: https://www.npmjs.com/package/ngrok).

- If you do not have ngrok, go here for instructions on how to install it: https://ngrok.com/.

- Once you have ngrok installed, open a local server in my project folder at your terminal: python -m SimpleHTTPServer.

- On a separate tab, type ngrok 8000 (or whatever port your computer is listening on).

- Find the forwarding URL that your ngrok tab displays and type it in your browser's search bar.

- You should arrive at index.html.

- Then in a separate browser tab, go to https://developers.google.com/speed/pagespeed/insights/ and type in the same URL that you used to open index.html. This should show my PageSpeed Insights scores. For comparison, my tests say Mobile: 94/100 and Desktop: 96/100. Please let me know if there is a discrepancy.

###Pizza.html

- Open views/pizza.html in your browser. You do not need to use the ngrok tunnel and local server (I'm sure you know that - sorry for any redundancy).

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