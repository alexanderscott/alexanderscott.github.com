Tips for writing effective JavaScript libraries
============================

1.  Wrap in a self-calling anonymous function
2.  Use strict mode
3.  Leverage deferreds for chaining promises
4.  Limit external dependencies and use native JavaScript where possible
5.  Prototype classes instead of `_.extend` where it makes sense
6.  Add AMD compliance by defining and returning a module
7.  Abstract-out configuration & constants, defining them upfront or in a config file
8.  Comment clearly and publish with Docco


1.  Wrap in a self-calling anonymous function
--------------------
 * Polluting the global namespace is a no-no
 * Control your library's functions and variables inside a 'closure'

  (function(){

  ...

  })();


or for a jQuery dependency/plugin

    (function($){

    ...

    })(jQuery);

Learn the power of closures for creating public, private, and privileged members from [Douglas Crockford](http://www.crockford.com/javascript/private.html)


2.  Use strict mode
--------------------
 * Standard for ECMAScript 5, adopted by all modern browsers 
 * Include "use strict"; at the beginning of the file (or beginning of a function to limit the strict scope)
 * Advantages
   * Safer - limited use of eval()
   * No accidental global namespace conflicts
   * Fails loudly - easier to debug





3.  Leverage deferreds for chaining promises
--------------------





4.  Limit external dependencies and use native JavaScript where possible
-------------------
 * Often faster to use native JavaScript functions rather than library equivalent
 * Dependency versions can be difficult to track and cause namespace conflicts (ex/ jQuery and Underscore's noConflict() method)

Some of my favorite native helpers:
 * `property in Object`
 * `Object.hasOwnProperty`
 * `Object.keys`
 * `Object.toFixed`
 * `Object.toJSON` `document.getElementByTagName`
 * `document.getElementById`

and lastly, the good old-fashioned [for loop](http://jsperf.com/fastest-array-loops-in-javascript/24)



5.  Prototype classes instead of `_.extend` where it makes sense
-------------------
(http://www.2ality.com/2012/08/underscore-extend.html)



6.  Add AMD compliance by defining and returning a module
-------------------

    if (typeof define == 'function' && define.amd)
        define(function() { return Spinner })
    else window.Spinner = Spinner




7.  Abstract-out configuration & constants, defining them upfront or in a config file
-------------------
 * Well-written libraries should be abstracted a level where they are situationally-independent
 * Configuration information or constants which vary case-by-case should ideally be removed from library source entirely, or at least referenced from a separate configuration file.
 * Examples of this in Node's `package.json`, or Sencha's `app.json`
 * If included in the source, helps visually to use all capital letters, underscore btw/ words (ex/ PLAYLIST_TRACK_VARIANCE_COEFFICIENT )



8.  Comment clearly and publish with Docco
-------------------
[Github Pages](http://pages.github.com/)

[Docco](http://jashkenas.github.com/docco/)
Examples
[Backbone](http://documentcloud.github.com/backbone/docs/backbone.html)
[Underscore](http://documentcloud.github.com/underscore/docs/underscore.html)

Runner-up: [Groc](http://nevir.github.com/groc/)
