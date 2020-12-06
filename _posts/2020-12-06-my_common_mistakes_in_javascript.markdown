---
layout: post
title:      "My Common Mistakes in JavaScript"
date:       2020-12-06 16:06:51 -0500
permalink:  my_common_mistakes_in_javascript
---

## So Many Parentheses
Making the transition from Rails to JavaScript was challenging at time.  Although there are many shared concepts, the syntax proved to be maddening occasionally.  I want to share two particular instances in the hopes that I can help others avoid similar struggles.

The first omission happened in my fetch requests.  Fetch requests are foundational of the inner workings of Javascript. The flow goes something like this:

1. Use the fetch method `.fetch()`
2. Pass in a URL in the form of a string `.fetch('exampleURL.com/data-source')`
3. Use the then method to return the response in JSON (JavaScript Object Notation) `.fetch('exampleURL.com/data-source').then(resp => resp.json())`
4. Use another then method to manipulate that data within the document `.fetch('exampleURL.com/data-source').then(resp => resp.json()).then((data) => data.forEach((object) => new Object(object)))`

If you forget the parentheses after `.json`, you will get strange "undefined" errors from JavaScript.  Unfortunately, JS did not win any awards for giving helpful error messages. Just remember that `.json()` is a method that returns a promise, and it MUST have a pair of parentheses attached to the end.

## The Empty String
When you are working with an object in Rails, such as an array, you can "clear it out" by calling the function `.clear`.  Not only is it easy to remember, it clearly suggests what it will do.  However, there will be times when you need to reset or clear out your innerHTML.  I encountered this is Dog Fetch CEO Lab, and it came up again in my project.  When I rendered new images, they were appearing below the previously rendered images.  Trying to call `example.innerHTLM.clear` will not work.  Instead, you will need to set it to an empty string: `example.innterHTML = ""`. This isn't as intuitive as Rails, but Javascript never promised it would be.

