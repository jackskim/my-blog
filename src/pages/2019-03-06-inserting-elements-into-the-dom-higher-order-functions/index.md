---
path: "/inserting-elements-into-the-dom-higher-order-functions"
date: "2019-03-06"
title: "Inserting Elements into the DOM & Higher Order Functions"
tags: ['javaScript']
excerpt: "Today's Practical JavaScript lessons covered inserting elements into the DOM and higher order functions." 
---

# Inserting Elements into the DOM & Higher Order Functions

Today&#8217;s Practical JavaScript lessons covered inserting elements into the DOM and higher order functions. I barely remembered some of these methods so it was a great refresher.

**Notes:**

`document.createElement([tagname])`creates a HTML element

`document.querySelector([selector])`selects the first DOM element that matches the selector

`.appendChild([childElement])`inserts a child element into the specified element

`Element.innerHTML`gets all the inner HTML of the element (it can also be reassigned)

`Element.textContent`allows you to get / set the text content of the element

While following along with the lessons today, I couldn&#8217;t get my program working correctly. Rather than getting frustrated and struggling to figure out what I did wrong, I applied yesterday&#8217;s lesson (on the debugger). With the help of the debugger, I quickly found out it was due to a typo, fixed it, and carried on.

Higher order functions:  
&#8211; Functions that accept other functions  
&#8211; Enhance the behavior of other functions

Callback functions:  
&#8211; The functions that are passed into higher order functions

A couple of examples of higher order functions:  
`setTimeout([callbackFunction], [# of ms])`

`Array.forEach([callbackFunction])`

Tip: When inspecting an element in chrome, you can reference the selected HTML element with `$0` in the console.

84% done with PJS now!
