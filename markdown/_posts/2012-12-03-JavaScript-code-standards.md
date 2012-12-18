---
layout: post
category : software development
tags : [javascript, Node.JS, code standards, client-side, DOM]
---

Below are some general guidelines and best practices for JS, HTML, and CSS.  
Many were gathered from experience and lessons learned (often the hard way).  
The rest will help ensure consistency throughout your web app.

## GENERAL FRONT-END

### Naming conventions
 - Files which represent 'classes' or modules should have first-letter capitalization
    (ex/ `ActivityCollection`)
 - Referenced libraries should also have first-letter capitalization, except for those with symbolic representations like jQuery ($) and Underscore (_)
 - As variables can be functions and vice versa, these should both have first-letter capitalization except for the initial letter
    (ex/ `collectActivity`)

### Semicolons
 - Please **use them** where possible.  Not using semicolons can cause problems with minification.  I'm serious, look it up.

### DOM
 - HTML id tags should be **globally unique **and contain some indication of the element type (
        (ex/ `<button id="activateBtn">`)
 - HTML classes can be used for efficient CSS styling when applied to multiple elements.  This is often a better option than CSS id references.
 - Reference element IDs instead of classes in jQuery selectors when possible.  It's faster.
 - Scope the jQuery selector inside $el views and where applicable
        (ex/ `this.$("#activateBtn").toggle();`)
 - Separate out and defer DOM manipulation functions.  These can be deferred using the jQuery wrapper, `_.defer()`, `$.promise()`, etc.

### Avoid polluting the global namespace###
 - Local variables (variables inside functions used only in that function) should be initialized with var and use 'new'
        (ex/ `var myVar = new MyObject()`)
 - Make JS functions **first-class citizens** where possible.  Use function **parameters **for passing in variables instead of the parent scope.

<pre>
function subtractDates(date1, date2){ 
    var newDate = date1 - date2;  
    return newDate;
}
</pre>
vs.
<pre>
var date1;  var date2;  
function subtractDates(){
    return date1 - date 2;
}
</pre>

 - Garbage-collect views, models, etc. when no longer needed.  This is especially important in Backbone, and forgetting to destroy these can create 'ghosts'
 - Reference this wherever beneficial.  In AJAX there are tricks for doing so:

{% capture text %}...
<pre>
var self = this;              
$.ajax({
    url: 'ajax/test.html',
    success: function(data) {
        $('#result').html(data);
        self.addToLog('Load was performed.');
    }
});
</pre>
...{% endcapture %}
{% include JB/liquid_raw %}

### Practice asynchronous code with callbacks
 - In JS, these are achieved by using a function parameter.
 - Include options parameter with success or error attributes in the callback (think of AJAX calls)
        
{% capture text %}...
function getSomeData(id, callback){
    ... some time-intensive asyc method with callback(result); inside...  
};
...{% capture text %}
{% include JB/liquid_raw %}

### Commenting
 - Own your work - include your name and email in JS file headers, along with date created and a short description.  Even if you only wrote a small portion, you have some working knowledge of its contents if ever there is a problem.  See files in client dir for reference.
 - Functions/variables should be prepended with a short // comment if you think they might be confusing to others or do something funky (all comments are removed during minification anyway, so go wild)
 - Use `//TODO` for writing future tasks to yourself or others
 - Remove all HTML commenting before build

### Double vs Single Quotes
 - HTML element attributes, including those inlined in JS and jQuery selectors, should all be quotations.  This will help prevent escaping and separate from the below:
 - JS string literals should be in single quotes
     * ex/ `var name = 'Alex'`
     * ex/ `html += '<div>';`
 - JSON must have double-quotes (you prob already knew this)

### Remove all logs to console
 - Prior to build if minification does not take care of this - as well as all other debugging code

### Code Re-Use/Referencing
 - Follow the DRY (**Don't Repeat Yourself**) principle
 - Instead of copying and pasting commonly used functions, create a first-class function for them and reference the hell out of it.
 - Important for HTML/DOM:  Separate out into templates which can be re-used by JS views.  HTML cannot be properly minified.
 - Native JS functions are often slow and error-prone.  Use better performing functions if already including a function library such as jQuery or Underscore
     (ex/  `$.each()` for an Array or `_.each()` for a Collection instead of `for(i = 0; i < blah; i++)`)
     (ex/  `_.isUndefined(myVar)`  instead of `if(myVar == undefined)` or `if(myVar.length)`)
 - **Read the source** before including **any** JS plugins.  This will help you understand how to use it, whether to use it if its bloated, make you write better code, and prevent crappy code from entering the codebase.
 - Source libraries should not reside in the same directory as non-source.  **Avoid editing the source** of mature libs, except for removing unneeded &amp; self-contained plugins.  **Override or extend** source functions locally in the project if need-be, its a much safer alternative.

### Length/Size
 - Views should not be over 500 lines of code.  Anything beyond that becomes cumbersome, and shouldn't be loaded all at once for reasons of speed and error-catching
 - Lines of code shouldn't be longer than a normal editor full-screen.  This can be seen often when including inline HTML in long strings.  Do everyone the favor of separating-out the string and concatenate where it makes sense with `+`
 - Use switch (case) statements instead of long or nested `if()`s.
 - Move/remove unused files from the team working directory.  One way to achieve this is with a .gitignore'd sandbox folder.



## BACKBONE.JS , REQUIRE.JS SPECIFIC
 - Data should ideally not be extracted from the DOM.  The binding should be one-way for the most part (with the exception of forms/input data and event triggers)
 - Each individual view, model, collection, router, etc. should have its own require module (thus **its own file**).  This is a requirement (no pun intended) of Require and r.js optimization
 - Use the prototyped eventAggregator sparingly when it's necessary to trigger events between views (its an app global)
 - Validation logic should reside in the Model or Collection instead of the View layer.  A view can then ask its model/collection to return validity.  Safer, more consistent, and DRY.
 - Any external libraries or plugins included must have a path defined in the main.js require config file (must also be shim'ed if it isn't AMD-friendly).



## NODE.JS SPECIFIC
 - Create an npm package.json file for every node module (project).
     - Include name, version, dependencies, engines, and contributors (see existing for reference)
     - Dependencies for published node modules can be added to package.json upon install by using the `--save` argument
     - Maintained package.json enables installation locally or on a remote server by simply run `$ npm install` from project root ('node_modules' should be .gitignore'd)
     - If global module used, link locally
 - Do not write description comments in headers - this should be included in a README.md inside project root along with runtime instructions
 - Determine series/parallel/waterfall needs of processes and code accordingly (async module is particularly helpful for this)
 - Use monitor (CLI) or forever-monitor (programatically) if the node server is required to always be running
 - Include a logs directory and append error callback data to file
 - Reference `__dirname` and relative paths for scalability
 - Use buffers for small amounts of data to be returned all at once (such as status messages).  Use streams for larger data - tapping into stdout and stderr and use out-of-the-box pipes for stdin to stdout
