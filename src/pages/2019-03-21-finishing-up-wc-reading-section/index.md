---
path: "/finishing-up-wc-reading-section"
title: "Finishing Up W&C Reading Section"
date: "2019-03-21"
tags: ['javascript', 'web development']
excerpt: "I spent the last few days continuing to read through the source code for this app ..."
---

# Finishing Up W&C Reading Section

I spent the last few days continuing to read through the source code for this app ([https://glitch.com/~light-vein).](https://glitch.com/~light-vein)

I paused throughout the lessons numerous times to re-trigger different breakpoints in the debugger. There were moments where I got stuck but eventually figured it out through repetition and examination.

Today's exercise was to go through `app.js` line by line and write comments in plain English explaining what's going on.

I'm not fully comfortable with *Handlebars.js* syntax or Chrome local storage yet, so I'll review again tomorrow and finish up the commenting after.

**Random notes:**

When using jQuery, `this` in event handlers refers to the element that the event was triggered on (as a jQuery default). You want to manually set the value using `.bind( )` if you want to set it to a different value.

**Routing** is the process of determining what code to run when a URL is requested. 

Having `/#/` in the URL prevents a page request/refresh

**Templating** is a combination of data and layout, where both are kept separate. It's usually used to format repeating items (eg. generating `<li>` elements from an array of objects)

Almost any app is going to use some templating library, so it&#8217;s a good idea to get used to reading the docs.

Chrome local storage can be accessed via the console under the Application tab under Storage -> Local Storage.

`localStorage` can only store data as strings. Hence the need for `JSON.stringify()` and `JSON.parse()`
