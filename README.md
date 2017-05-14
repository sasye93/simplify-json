# simplify-json
easy-to-use toolkit to handle JSON objects in node.js that lets you work with string paths.
I originally build this to handle mongoose models in an automated way. Please note that this is still under development and use on your own risk.

## Installation
Install via npm:
```
npm install simplify-json
```
or install via git:
```
$ git clone https://github.com/sasye93/simplify-json
$ cd node-github
$ npm install
```

## Usage

Provided methods are listed below, each one with exemplary use on "myJSON" object.

```
let myJSON = {
  foo: {
    fooMore: {
      fooMost: "hey!",
      fooMass: "bye!",
      foo: true,
    },
    foo: {
      fooYou: "no",
    },
    fooArray: [ 1,2,3,5 ]
  },
};
```
### function isJSON(object)
Returns true if object is a valid json, false if not.
```
isJSON(myJSON) === true;
isJSON("foo") === false;
```
No alias.
### function empty(json)
Returns true if json is empty, false otherwise.
```
empty({}) === true;
empty(myJSON) === false;
```
No alias.
### function size(json)
Returns the number of keys in json, including subkeys.
```
size(myJSON) === 5;
```
No alias.
### function getNested(json, path)
Returns the value of a nested key using string syntax for path.
```
getNested(myJSON, "foo.fooMore.fooMost"); // returns "hey!"
getNested(myJSON, "foo.fooMore.fooNo"); // returns undefined
getNested(myJSON, ""); // returns myJSON
```
alias is get(json, path).
### function modifyNested(json, path, value)
Changes the value of a nested key using string syntax for path.
```
let result = modifyNested(myJSON, "foo.fooMore.fooMost", "bye!"); // returns true if new value was set,
false if key not found.

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooMost === "bye!";
```
alias is modify(json, path, value).
### function removeNested(json, path)
Removes a nested key using string syntax for path.
```
let removedItem = removeNested(myJSON, "foo.fooMore.fooMass"); // returns removed value if key was removed,
undefined if key not found.

// effect on myJSON if removedItem !== undefined:
myJSON.foo.fooMore === { fooMost: "hey!" };
```
alias is remove(json, path, value).
### function findNested(json, key)
Returns an array of all values that have "key" as key.
```
let matches = removeNested(myJSON, "foo.fooMore.fooMass"); // if nothing is found, array is empty.

matches ===
[ { fooMore: { fooMost: 'hey!', fooMass: 'bye!', foo: true },
    foo: { fooYou: 'no' },
    fooArray: [ 1, 2, 3, 5 ] },
  true,
  { fooYou: 'no' } ];
```
alias is find(json, key).
### function pushInNestedArray(json, path, item)
Pushes item into a nested array in json.
```
let result = pushInNestedArray(myJSON, "foo.fooMore.fooArray", 4); // returns true if item was inserted
into array, false if key not found or key is no array.

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooArray === [ 1,2,3,5,4 ];
```
alias is pushArray(json, path, item).
### function removeInNestedArray(json, path, item)
Removes item in a nested array in json.
```
let removedItem = removeInNestedArray(myJSON, "foo.fooMore.fooArray", 3); // returns removed value if item was
removed from array, false if key not found or key is no array or array does not containt item.

// effect on myJSON if result !== undefined:
myJSON.foo.fooMore.fooArray === [ 1,2,5,4 ];
```
alias is removeArray(json, path, item).

### function stringifyNoCircular(json)
Converts a JSON object to a string, omitting circular references in it.
```

```
