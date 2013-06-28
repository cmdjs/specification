# Common Module Definition / draft

------

This specification addresses how modules should be written in order to be interoperable in **browser-based** environment. By implication, this specification defines the minimum features that a module system must provide in order to support interoperable modules.

- Modules are singletons.
- New free variables within the module scope should not be introduced.
- Execution must be lazy.



## Module Definition

A module is defined with `define` keyword, which is a function.

```js
define(factory);
```

1. The `define` function accepts a single argument, the module factory.
1. The `factory` may be a function or other valid values.
1. If `factory` is a function, the first three parameters of the function, if specified, must be "require", "exports", and "module", in that order.
1. If `factory` is not a function, then the module's exports are set to that object.



## Module Context

In a module, there are three free variables: `require`, `exports` and `module`.

```js
define(function(require, exports, module) {

  // The module code goes here

});
```


### The `require` Function

1. `require` is a function

    1. `require` accepts a module identifier.
    1. `require` returns the exported API of the foreign module.
    1. If requested module cannot be returned, `require` should return null.

1. `require.async` is a function

    1. `require.async` accepts a list of module identifiers and a optional callback function.
    1. The callback function receives module exports as function arguments, listed in the same order as the order in the first argument.
    1. If requested module cannot be returned, the callback should receive null correspondingly.



### The `exports` Object

In a module, there is a free variable called "exports", that is an object that the module may add its API to as it executes.


### The `module` Object

1. `module.uri`

    The full resolved uri to the module.

1. `module.dependencies`

    A list of module identifiers that required by the module.

1. `module.exports`

    The exported API of the module. It is the same as `exports` object.



## Module Identifier

1. A module identifier is and must be a **literal** string.
2. Module identifiers may not have a filename extensions like `.js`.
3. Module identifiers should be dash-joined string, such as `foo-bar`.
4. Module identifiers can be a relative path, like `./foo` and `../bar`.



## Sample Code


**A typical sample**

math.js
```js
define(function(require, exports, module) {
  exports.add = function() {
    var sum = 0, i = 0, args = arguments, l = args.length;
    while (i < l) {
      sum += args[i++];
    }
    return sum;
  };
});
```

increment.js
```js
define(function(require, exports, module) {
  var add = require('math').add;
  exports.increment = function(val) {
    return add(val, 1);
  };
});
```

program.js
```js
define(function(require, exports, module) {
  var inc = require('increment').increment;
  var a = 1;
  inc(a); // 2

  module.id == "program";
});
```


**Wrapped modules with non-function factory**

object-data.js
```js
define({
    foo: "bar"
});
```

array-data.js
```js
define([
    'foo',
    'bar'
]);
```

string-data.js
```
define('foo bar');
```
