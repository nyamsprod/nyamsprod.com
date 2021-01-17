---
layout: post
title: "Firefox and Page Screenschot"
date: "2013-07-17"
categories: 
  - "web"
tags: 
  - "developpers-tools"
  - "firefox"
  - "screenshot"
---

Here's a little trick that comes very handy when you need to make a quick webpage screenshot to send to someone.

1. Fire up Firefox developers tools by hitting `(Shift+F2)`
2. Enter the following command : `(screenshot --selector .hentry myfile.png)`

And voila! Firefox just created a png file called `myfile.png` which is a screenshot of the area occupied by the first _.hentry_ element found in the page if any exists. The selector parameter uses `document.querySelector` to help you refine the area you really want to shot.

Of course, if you are interested in taking the whole page in a single screenshot just drop the selector argument. Of note, there are many others options that comes handy too with this powerful screenshot utility command. For instance you can delay the screenshot capture if for instance your page layout changes based on CSS or JavaScript interaction.
