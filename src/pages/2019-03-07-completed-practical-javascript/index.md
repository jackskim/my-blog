---
path: "/completed-practical-javascript"
date: "2019-03-07"
title: "Completed Practical Javascript"
tags: ['javascript']
excerpt: "Today I learned about DOM manipulation via JS and the different cases of the `this` keyword."
---

# Completed Practical JavaScript

Today I learned about DOM manipulation via JS and the different cases of the `this` keyword.

**Notes:**

You can get/set classes of elements with `.className`

When you add an event listener to an element, an event object is passed to the callback function. The event object has many useful properties on it such as:  
- `.target` which shows you which element triggered the event  
- `.parentNode`which shows you the parent element of the target  
  
`parseInt()` is a built in method which converts numerical strings into numbers

*DOM event delegation is a mechanism of responding to ui-events via a single common parent rather than each child, through the magic of event bubbling (aka event propagation)* (E.g. adding an event listener to a `<ul>` element rather than adding one to each child `<li>` element)

The `this` keyword can be thought of as a special variable that changes depending on the situation.

Case 1: In a regular function, (or if you&#8217;re not in a function at all) `this` points to the `window`object

Case 2: When a function is called as a method, `this` points to the object that&#8217;s on the left side of the dot

Case 3: In a function that&#8217;s being called as a constructor, `this`points to the object that the constructor is creating.

Case 4: When you explicitly set the value of `this` manually using `.bind`, `.apply` or `.call`, it&#8217;s all up to you. (.bind, .apply. and .call are methods on functions where `this` is set to the first argument passed).

Finally completed Practical JavaScript. To be honest I barely remembered some of the DOM and `this` keyword information so it was a great refresher. Looking forward to the premium material!

P.S. Also applied to Lambda School. Will do my best to get accepted!
