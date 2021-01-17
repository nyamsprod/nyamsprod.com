---
layout: post
title: "introduction to window.postMessage"
date: "2012-06-08"
categories: 
  - "web"
tags: 
  - "api"
  - "html5"
  - "iframe"
  - "javascript"
  - "postmessage"
  - "security"
---

## The problem

Imagine you have one page (A) with an iframe (B) in it and you want an action taking place on B to have an impact on A. **This will always work if A and B are on the same domain, but once they are on 2 differents domains it does not work anymore for security reasons**.

## The solution

We are going to use the `postMessage` API. Luckily for us, **this API is available in all modern browser including IE8+.** Below You'll find an example on how to implement this API using jQuery.

## The code

My page is hosted on `http://www.nyamsprod.com` domain but my iframe is hosted on `http://media.tshoboo.com`. In the example I'll trigger the parent `background-color` change from the iframe.

Here's the idea behind the code: the source window (the iframe) sends a message to the target window (the parent window). When the target window receives the message it validates it and, only if it is issued by the correct origin domain, acts depending on the data it contains.

_The only reason I used jQuery is because IE8 does not support W3C Event Model._

_The Code found on the Iframe window (The Source Window)_

_//this should work only if the page is included as an iframe_
if (top != self) {
	jQuery(function($){
		_//Feature detection if PostMessage is not supported on the browser we just ignore everything_
		if (!!window.postMessage) {
			$('.submit').click(function(){
				_//We are using the `parent` object because this iframe is sending the message to its parent //'\*' is used so that the message is broadcasted to any parent who may use it //In a real example do not use '\*' it may become a vector for security problems_
				parent.postMessage(_myMessage_, '\*'); _//myMessage should be define in your function_
			});
		}
	})
}

_The Code found on the parent window (The Targeted Window)_

jQuery(function($){
	$(window).bind('message', function(event){
		var color,
			oEvent = event.originalEvent; _//because jQuery supercharge the DOM event you need to look at event.originalEvent_
		if (_oEvent.origin_ != 'http://media.tshoboo.com') { _// This is for SECURITY NEVER REMOVE THIS_
			return false;
		}
		_//Now you can act on the page depending on the Message received_
		if (color = _oEvent.data_.match(/^\\#\[0-9A-Za-z\]{6})$/)) { _//oEvent.data = myMessage_
			$('html').css({'background-color':color\[0\]});
		}
	});
});

## The Demo

[So now place for the demo](http://www.nyamsprod.com/test/postmessage/ "postMessage API in use"), if you analyze my demo you'll find out that not only does the `iframe` can trigger some changes on its parent but in response the parent also can trigger the same event on the `iframe`.
