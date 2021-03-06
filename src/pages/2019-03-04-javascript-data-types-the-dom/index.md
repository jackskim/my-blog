---
path: "/javascript-data-types-the-dom/"
date: "2019-03-04"
title: "JavaScript Data Types & The DOM"
tags: ['javaScript']
excerpt: "About 60% done with Gordon's Practical JavaScript Course now. Today's lessons were quite useful and covered JS data types and the DOM."
---

# Javascript Data Types & The DOM

About 60% done with Gordon's Practical JavaScript Course now.

Today's lessons were quite useful and covered JS data types and the DOM.

**Notes:**

There are two categories of data types in JS:

1. Objects (can be as complex as you want)
  * E.g. Objects, Arrays, Functions, 

2. Primitives (building blocks of JS) 
  * String
  * Number
  * Boolean
  * Undefined _// value that hasn&#8217;t been set_
  * Null _// &#8216;nothing&#8217;_

*If it's not a primitive, it's an object.*

**Primitive Comparisons vs Object Comparisons:**

When you create an object in JS, it actually creates a unique location in memory.

When comparing primitives, JS is comparing the values.  
When comparing objects, JS is comparing the references (memory addresses).


![primitives vs objects](../../assets/primitives_vs_objects.png "Primitives vs
Objects")

*For objects, JS doesn&#8217;t care that the values look the same, it&#8217;s irrelevant &#8211; what it actually cares about is if the addresses are the same*

When primitives are assigned to a variable, the value is stored.  
When objects are assigned to a variable, the reference/memory address is stored.

**What is the DOM?**

The DOM is what the browser understands the HTML document to be. The browser will use the information in your HTML to build an understanding of this document looks like. The browser's interpretation of your HTML is the DOM tree.

<u>Event Listeners</u>

Event listeners listen for specified &#8216;events&#8217; (eg. mouse click) and runs the specified event handler function each time the event occurs  
  
If you have DOM interactions in your JS file, you need to put your `<script>` tag right before the closing `</body>` tag.
