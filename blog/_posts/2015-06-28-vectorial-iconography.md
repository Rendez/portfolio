---
layout: post
title: Vectorial Iconography
---

The day *font icon sets* appeared as a solution, one of the most repeated problems in web development seemed solved almost overnight.

Yes! IE had support for @font-face and .eot files since its 8th version... Say what?!

What had we been doing wrong? The web community spent all the internet boom years inventing super smart tools like Cufon and SIRF, and a long etcetera.

---

### Is this the future in iconland?

I believe the strongest point font-based icons have these days are the broad compatibility across browsers and devices they offer. But, are they the future?

Two years ago at my company, we created SVG sprites as the only needed solution, that's what you get when you drop IE8 support. To my surprise, our designer came to me with his Windows laptop to ask me why did the SVG displayed with CSS backgrounds looked so blurry... "Why is our logo blurry?". After some dueling on Inkscape, I quickly found an [explanation](http://benfrain.com/svg-backgrounds-dont-zoom-correctly-in-internet-explorer-10/).

Meh, we can't reliably use SVG in backgrounds, bye bye SVG sprites... Unless...!

> It seems that putting a dummy SVG tag with width=100% and height=100% make IE11 display all my SVG elements.

Which brings me back to try and understand why we use fonts to represent icons?

We arrive then at [ligatures](https://icomoon.io/#docs/ligatures). We could then call symbols with common terms. Screen readers and search engines see words. Users see symbols. What a great idea? We write our word and we get an icon. Just like emoticons! I really thought for a bit this was THE solution. Ah, and let's not forget the idea to use unicode to call symbols to present our icons as well. A risky option as it seems, let's not [the unicode private area](http://nimbupani.com/markup-free-icon-fonts-with-unicode-range.html). There's yet another solution, unicode-range, for Chrome and Safari only it seems. This defeats the purpose of wide browser compatibility for the font-icon approach.

To be fair, as often in web development, there is not one single solution to tackle one problem.

It was then when I bumped into a very insightful writing from [Thomas Fuchs](http://mir.aculo.us/2014/10/31/icon-fonts-vs-inline-svg/) on the topic. As Pete Hunt fantastically put it in JSConf 2013, [Rethinking Best Practices](https://www.youtube.com/watch?v=x7cQ3mrcKaY), I reminded myself that if anything, we as developers should constantly be defying instead of settling.

When it comes to font icons, there are a couple of critical points I would like to emphasize on, because I believe that they are hard to circumvent:

- There’s blurry rendering on certain browsers.
- Some special headers are required when serving these font files so that our CDN (Amazon CloudFront).
- You can’t easily edit icons, and it’s hard to see what’s been updated in source code control.

### Enter inline SVG, and SVG stacks

What is an icon if not a graphic element, an concise image representing a symbol. We need images, and our best friend SVG is not the de-facto approach to add most images to interfaces.

Let's ask for a few things:

- Cross-browser solution, with PNG fallbacks.
- Easy flow and easy addition of icons to the set.
- Optimization and flexibility.
- Styleable and capable to understanding css animations.
- No flash of unstyled text; quite the opposite: instant loading, and guaranteed rendering.

I would like to share my workflow to make vectorial icons a bliss and first I would like to credit the creators of [grunticon](https://github.com/filamentgroup/grunticon/) for all the insights I've gotten from their workflow. They wrote about their [reasons for switching](http://ianfeather.co.uk/ten-reasons-we-switched-from-an-icon-font-to-svg/), which reinforced my thinking.

To stack icons into one single file, comes in handy the <use> svg element, which allows to refer to any SVG element via its ID attribute.

Generating such stuck for me needs to be as easy as placing a new .svg file into my icons folder.

The markup and css necessary has to be easy, and minimum.

- svg2png, svgstore, svg4everybody, snippet.