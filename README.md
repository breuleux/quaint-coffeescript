
quaint-coffeescript
===================

Allows inline CoffeeScript code in Quaint markup.

Expressions in curly brackets will be evaluated in CoffeeScript.

## Usage

### Command-line

```bash
$ npm install quaint-coffeescript
$ quaint -p coffeescript file.q
```

### Quaint

```
plugins :: coffeescript

2 + 2 is {2 + 2}
```

### JavaScript

```javascript
var quaint = require("quaint");
var qcs = require("quaint-coffeescript");

var q = quaint(qcs);

q.toHTML("2 + 3 = {2 + 3}")
// ==> "2 + 3 = 5"
```

## Functionality

In embedded CoffeeScript, you can use the `h` function to create HTML
elements programmatically:

```javascript
q.toHTML("{h 'a.cls#id', href: 'there', 'A', 'B'}")
// ==> '<a href="there" id="id" class="cls">AB</a>'

q.toHTML("{[(h "b", i * i) for i in [1, 2, 3]]}")
// ==> "<b>1</b><b>4</b><b>9</b>"
```

## Options

### `sandbox`

An object to use as the global object for `eval`. All the properties
you set on that object will be available as top level variables in
scripts.

### `vm`

The module to use for the virtualization (defaults to the standard
`vm` module, so you usally won't have to set it).

The module must implement these two methods:

* **vm.createContext(sandbox)**: "contextify" the object, i.e. make it
  into a proper environment for the evaluator. If you implement your
  own, you return the sandbox itself, or a copy.

* **vm.runInContext(code, sandbox)**: evaluate the code in the sandbox
    returned by `createContext`.
