# Modules / draft

------

This specification addresses how modules should be written. The modules are designed for **browser-based** environment:

- Modules are singletons.
- Execution must be lazy.
- Modules may have cyclic dependencies.


## Define

A module is defined with `define` keyword, `define` is a Function, it accepts a function, object, array, and string as the factory.

- **none-function** factory, the exported API is the data of the factory.
- functional factory must only contain three parameters, which are `require`, `exports` and `module`, the exported API is the data on `exports`.


Guarantees should be made by module writers:

1. A module must be encoded in UTF-8.
2. Take care of the global leaks.


## Require

1. `require` is a Function

    1. The `require` function accepts a module identifier.
    2. The module identifier must be a pure string.
    3. `require` returns the exported API of the foreign module.
    4. If requested module cannot be returned, `require` should return null.

2. `require.async` is a Function

    1. The `require.async` function accepts a list of module identifiers and a callback.
    2. The module identifier can be a variable that refers to a pure string.
    3. Callback accepts the number of parameters according to the module identifiers.
    4. If requested module cannot be returned, `require` should return null.

3. `require.resolve` is a function, it accepts a module identifier and return the absolute path of the module.

4. `require.style` is a Function (*Optional*)

    1. The `require.style` accepts string or a variable that refers to a string.
    2. The parameter should be valid css.
    3. `require.style` should render the css.


## Module Context

In a module, it has two variables that related to this module:

- The `module` object is the module itself, it contains the information of the module
- The `exports` object is the exported API of the module.

### Required Interface

1. `module.id`

    The identifier for the module. It may be the uri of the module.

2. `module.uri`

    The full resolved url to the module.

3. `module.dependencies`

    A list of identifiers that required by this module.

4. `module.exports`

    The exported API of this module.

### Optional Interface

1. `module.parent`

    The module that required this one.

2. `module.status`

    An object of the available loading status. It is defined by the loader itself.

3. `module.factory`

    The factory object of the module.

4. `module.require`

    Just like `require`.


## Module Identifier

1. A module identifier is and must be a string.
2. Module identifiers may not have a filename extensions like `.js`.
3. Module identifiers should be dash-joined string, such as `foo-bar`.
4. Module identifiers can be a relative path, like `./foo` and `../bar`.


## Sample Code

**A functional module**:

```javascript
// hello.js
define(function(require, exports, module) {
    module.exports = 'hello'
})

// world.js
define(function(require, exports, module) {
    var hello = require('./hello')

    var speaker = require('speaker')

    exports.speak = function(name) {
        name = name || 'world'
        return speaker.speak(name)
    }
})
```

**A data module**:

```javascript
// object-data.js
define({
    foo: "bar"
});

// array-data.js
define([
    'foo',
    'bar'
]);

// string-data.js
define('foo bar');
```
