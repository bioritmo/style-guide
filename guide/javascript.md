# JavaScript

#### Use 2 spaces for indentation, no tabs.
#### Always declare your variables at the top of the function to avoid [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting) problems.
#### Use single variable definition.

#### Don't prefix jQuery cached selector variables with ```$```

```js
var target = $('.my-class'),
    offset = target.offset(),
    height = target.outerHeight(),
    width  = target.outerWidth();
```

#### Use ```CamelCase``` and ```mixedCase``` for naming stuff.

```js
// Avoid this
[1, 2, 3].map(function(value, index, array) {
  return value + 1;
});

// Prefer this
[1, 2, 3].map(function(value) {
  return value + 1;
});
```

#### Avoid global scope lookup. Access top level variables and functions explictly through the ```window``` object or inject the required namespace in an [IIFE](http://en.wikipedia.org/wiki/Immediately-invoked_function_expression):

```js
// Avoid this
someGlobalFunction();

// Prefer this
window.someGlobalFunction();

// Avoid this
(function() {
  var localValue = globalStuff.value + 5;
})();

// Prefer this
(function(globalStuff) {
  var localValue = globalStuff.value + 5;
})(window.globalStuff);
```
