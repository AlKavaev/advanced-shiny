# Simple AJAX system for Shiny apps (JS -> R -> JS communication)

Sometimes it's useful to be able to call an R function from JavaScript and use the return value from R back in JavaScript. This sort of communication is usually done with AJAX in JavaScript. This app shows how to implement a simple and ultra lightweight AJAX-like system in Shiny, to be able to call functions in R.

Using this system is easy:  
1. Include `api.js` in your Shiny app's UI  
2. Include `api.R` in your Shiny app's server  
3. In your R code: define the functions that you want to be able to call from JavaScript. Each function must have a name beginning with `api.` and take a single argument which is a list of the parameters passed from JavaScript. This function should return a list (can be an empty list), which will be passed to the callback function in JavaScript (if a callback was provided).   
4. In your JavaScript code: make a call to `api.call(params)`, where `params` is an object that contains all the parameters as key-value pairs. You must specify the `_method` parameter -- this is the R function that will get called. For example, if in R you defined a function `api.myfunc` then you can call it in JavaScript with `api.call('_method' : 'myfunc')` (notice that the prefix `api.` is ommitted). You can optionally provide `_callback` and `_failureCallback` functions which can be called when the R function completes or when it throws an error. You can also add any other arbitrary parameters, and they will be available to you in the R function.

This may sound a bit complicated, but if you take a look at the source code of the sample app you'll see it's actually pretty simple to use.