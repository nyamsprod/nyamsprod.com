---
title: "Re-styling the textarea tag in recent browsers"
date: "2011-03-21"
categories: 
  - "web"
tags: 
  - "css"
  - "firefox-4"
  - "style"
  - "textarea"
  - "webkit"
---

With [Firefox just around the corner](http://blog.mozilla.com/blog/2011/03/18/check-out-what%E2%80%99s-coming-soon-in-firefox-4-2/), it's time to take a look at some major changes that will go public starting tomorrow and I'm not going to talk about wider WebM supports or speedier web experience but about something everyone will come accros eventually: forms styling.

Firefox is not the first browser to add some fancyness to its forms tag. Opera, and Webkit Browsers already uses new features and new ways to present and/or style forms but styling a `textarea` can become crucial since `textarea` tags are responsible for presenting the main area used to get content from your viewer whether you run a major corporate website, a blog or use a simple contact form.

Webkit before and Firefox now have made their `textarea` resizable by default. But while by default on Webkit the `textearea` can not be shrink more than it's original size on Firefox you can give it any size. So after many googling and experiencing, I've come up with simple rules to allow you to style correctly the textarea tag. So that it takes advantage of these new features without breaking your existing rules and design.

1. First thing first, 99% of the time you'll only want to let the user resize vertically you tag. Letting them resize the tag horizontally can only lead to a design break unless this is what you really want :) . So I encourage you to add this rule to any of your website that hosts a textarea tag. \[source lang="css"\]textarea { -moz-resize:vertical; resize:vertical; }\[/source\]
2. With this information, Webkit will be ok but not Firefox. With Gecko powered browser you need to declare a minimum height for your textarea otherwise the viewer could shrink it more than desired. So you should add to the above rule the information needed. The rule becomes something like this \[source lang="css"\]textarea { -moz-resize:vertical; resize:vertical; min-height:160px; }\[/source\]
3. Now to be complete you way want also to control how far the textarea could be stretch. The user should not be able to stretch the tag more than necessary too. So once again let's add another constraint by adding a maximum height value. The final rule becomes \[source lang="css"\]textarea { -moz-resize:vertical; resize:vertical; min-height:160px; max-height:480px }\[/source\]

Of course, the value I gave can and should be change to match your design but remember, if you don't apply theses changes to all of your existing website using a `textarea`, starting from tomorrow, your `textarea` may end up breaking your wonderful design. If you need a real life example, well just check [the simplybadass css style file](http://nyams.planbweb.com/blog/wp-content/themes/simplybadass/style.css) on this wordpress blog ;)

_PS: someone could argue that I could I just use a rule to disabled completely the textarea resize mechanism, but isn't more fun to just play around with new features than just disabling them and forgetting about them in the process :( ...._

Ok, if this is what you really want the just add this simple line :

\[source lang="css"\]textarea { -moz-resize:no-resize; resize:no-resize; }\[/source\]
