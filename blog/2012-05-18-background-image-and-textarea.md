---
title: "Background Image and Textarea"
date: "2012-05-18"
categories: 
  - "web"
tags: 
  - "background"
  - "background-size"
  - "border-image"
  - "css3"
  - "gecko"
  - "image"
  - "internet-explorer"
  - "opera"
  - "resize"
  - "textarea"
  - "webkit"
---

Using a single background image on a `textarea` to change its presentation is no so trivial after all. Modern browser engine (Gecko and Webkit, for now) allow `textarea` to be resize by the user. This resize that I've already talk about in another post can easily break your design if you don't adapt your CSS . Here's a technique that I use to mitigate the new behaviour in modern browser.

To start with, here is a simple rule that should work on any browser (IE8+).

textarea {
	-moz-box-sizing:border-box;
	box-sizing:border-box;
	width:276px;
	height:172px;
	padding:20px;
	overflow:auto;
	border:none;
	background:#fff url(background.png) no-repeat center scroll;
}

The problem with this rule is that in modern browsers you can resize the `textarea` tag as you wish, which means that on resize my image design will break since the background image will not adapt to the resized `textarea`.

## using CSS3 resize property

If you don't want your user to break your design by resizing the `textarea` the simplest solution it's to disallow the resize through CSS. this solution is simple, effective and backward compatible. The only problem with this solution is that you remove a very handy functionality from your website only because you don't know how to work with it :( .

textarea {
	-moz-box-sizing:border-box;
	box-sizing:border-box;
	width:276px;
	height:172px;
	padding:20px;
	overflow:auto;
	border:none;
	background:#fff url(background.png) no-repeat center scroll;
	**_\-moz-resize:none; resize:none;_**
}

## using CSS3 Background module

My first attempt to find a simple solution to my problem was to use the CSS3 property: [background-size](https://developer.mozilla.org/en/CSS/background-size "Background-size on the MDN website"). Which means that I just had to add a new property to my rule.

textarea {
	-moz-box-sizing:border-box;
	box-sizing:border-box;
	width:276px;
	height:172px;
	padding:20px;
	overflow:auto;
	border:none;
	background:#fff url(background.png) no-repeat center scroll;
	**_background-size:100% 100%;_**
}

In doing so, I know that my image will _automagically_ adapt to the `textarea` resize. But I've introduced a new problem, the image ratio is never preserved which means that on resize, the image can be deformed and the result is not quite what I wanted. So even if this solution works and is backward compatible, the result is not great. So my suggestion is to avoid this technique. You may try to work around the problem using the min/max-height properties as well as the min/max-width property to further [style the textarea in modern browser.](http://www.nyamsprod.com/blog/2011/styling-textarea-tag/ "Re-styling the textarea tag in recent browsers") But the loss of ratio is too important to be overlooked.

## Using CSS3 Border module

Since I was not happy with this method, I tried another approach by using the CSS3 border module property: [border-image](https://developer.mozilla.org/en/CSS/border-image "Border-image on the MDN website"). With this property, the image is sliced and repeated on the tag border [following some specific rules](http://css-tricks.com/understanding-border-image/ "Border-image explained"). So whenever you resize the `textarea`, the image ratio remains intact and you finally get the resulting effect you wanted. You may think that everything is fine ... but wait , this is CSS3 we're talking about.

textarea {
	width:276px;
	height:172px;
	overflow:auto;
	border-width:5x;
	border-type:solid;
	border-color:transparent;
	**_\-webkit-border-image:url(textarea.png) 5 repeat;_**
	**_\-moz-border-image:url(textarea.png) 5 repeat;_**
	**_\-ms-border-image:url(textarea.png) 5 repeat;_**
	**_\-o-border-image:url(textarea.png) 5 repeat;_**
	**_border-image:url(textarea.png) 5 repeat;_**
	**_background-color:#fff;_**
}

Some points to consider:

- I used the border module not the background module so we do not use the `background-image` property.
- Since the border-image is relatively new [it is not supported on IE browsers](http://caniuse.com/#search=border-image "When can I use border-image"). Which means that on old browser and in IE, you'll see no background image and no border either, so we need to create a fallback solution.

## Modernizr to the rescue

To try to mitigate these issues, I had to rely on the excellent [javascript framework modernizr](http://www.modernizr.com "is an open-source JavaScript library that helps you build the next generation of HTML5 and CSS3-powered websites.") which can detect browser support for the `border-image` property. With modernizr help, I only switch to the modern border module way only when possible. So When IE support the `border-image` property it will _automagically_ switch to the border image module way.

## Always read the Spec

After reading again the specification for the border-image property, in turns out that you can achieve a backward compatibility rendering without Javascript :) . The border-image has a value called fill which specify the following :

> fill (optional)
> 
> If the "fill" keyword is present, the middle part of the border-image is preserved, and drawn as the background-image of the image.

So by using this `fill` value in border-image supporting browser we draw the image middle part above the declared `background-image`. By doing so we can specify both rules and gain a fallback behaviour :) .

.full {
	-moz-box-sizing:border-box;
	box-sizing:border-box;
	width:276px; height:172px; overflow:auto;
	background:#fff url(pattern.png) no-repeat center scroll;
	border:20px solid transparent;
    /\* Early Implementations the default behaviour was fill and/or fill was not supported \*/
    -webkit-border-image:url(pattern.png) 20 repeat;
       -moz-border-image:url(pattern.png) 20 repeat;
         -o-border-image:url(pattern.png) 20 repeat;
    /\* new implementation: fill must be specified \*/
    -webkit-border-image:url(pattern.png) 20 fill repeat;
       -moz-border-image:url(pattern.png) 20 fill repeat;
         -o-border-image:url(pattern.png) 20 fill repeat;
    /\* standard specification \*/
            border-image:url(pattern.png) 20 fill repeat;
}

## Caveats

- First, you need to have your JavaScript activated to make this solution works. Always keep this in mind.
- Second, if IE start supporting the `textarea` resize attribute without supporting the `border-image` CSS property, my Solution won't work since the two could be implemented separatly in a browser.
- Because we're using 2 different css modules, the scrollbar position changes depending on the solution used. You may view theses changes when comparing my test page rendering in Opera.

To summarize my findings I've created a [test page with all the techniques explained](http://www.nyamsprod.com/test/textarea/ "Styling Textarea with a backgroudn Image") here with some comments to explain what I did. Feel free to use and abuse this page :) .
