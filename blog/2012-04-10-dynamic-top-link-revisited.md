---
title: "dynamic top link revisited"
date: "2012-04-10"
categories: 
  - "web"
tags: 
  - "button"
  - "css-3"
  - "degradation"
  - "dynamic-insert"
  - "javascript"
  - "jquery"
  - "snippets"
  - "tricks"
---

## The starting point

I'm a Jeff Starr fan. Everytime he blogs something about  Wordpress or JavaScript I'm curious to see what he comes up with to make our developer's life easier. Today he has released the code he uses on his newly Wordpress theme [to dynamically display the "got the top" link](http://perishablepress.com/dynamic-top-link/ "Dynamic Go-to-Top Link by Jeff Starr") .

After looking at the code I was frustrated about many aspects of it, in summary:

- If you don't have JavaScript then you get no button;
- All the css code was embedded in the JavaScript so you could not easily adapt  the script to your own design without messing with the script;
- Everytime the resize event was called jQuery was basically re-creating the button;

## The solution

So [I came up with this _improve_ version](http://www.nyamsprod.com/test/dynamictoplink/ "Dynamic Top Link Revisited Demo"). I hope you'll enjoy it, since it fixes all the above problems, adds a little animation thanks to jQuery and CSS animations (yes again :) ) and tries to be more responsive and less intrusive on the webpage.

## How it works

Once You have included the CSS, the JavaScript and the HTML code in your page. The animation kicks start as you load the page. All the animations except from the scrolling back to the top page are manage by CSS. Which leave the author many choices on how he/she wants the link to be rendered.

I've associated the button to the scroll event . This event is only fired in jQuery if the element is scrollable which means that the window height is smaller than the document height :) .

If no Javascript is present the button still works has excepted by remaining visible on the page.

## Suggestions

1. Since 98% of the script is handle through CSS, you can event adapt the button layout according to media queries to workaround more easily the `position:fixed` problems on smartphone for exemple. Use your imagination :)
2. Making a WordPress plugin out of it to ease it's integration... **Done!!** **[Download the Wordpress plugin](http://wordpress.org/extend/plugins/ultimate-back-to-top/ "Download the WordPress Plugin from Wordpress")**

### _Bug Fixes:_

1. I've removed the used of jQuery's `fadeIn` and `fadeOut` and replaced them with `CSS3 transitions`. By doing so, I'm no longer firing continually the fadeIn animation everytime the page is scrolled;
2. Fixed the annoying double click issue;
