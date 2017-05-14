# simplify-json
easy-to-use toolkit to handle JSON objects in node.js that lets you work with string paths.
I originally build this to handle mongoose models in an automated way. Please note that this is still under development.

NOTE: THIS MODULE COMES WITH ABSOLUTELY NO WARANTY. USE AT YOUR OWN RISK.

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

- [simplify-json](#simplify-json)
  - [`empty(json)`](#emptyjson)
  - [`size(json)`](#sizejson)
  - [`getNested(json, path)`](#getnestedjson-path)
  - [`modifyNested(json, path, value)`](#modifynestedjson-path-value)
  - [`removenested(json, path)`](#removenestedjson-path)
  - [`findnested(json, key)`](#findnestedjson-key)
  - [`pushInNestedArray(json, path, item)`](#pushinnestedarrayjson-path-item)
  - [`removeInNestedArray(json, path, item)`](#removeinnestedarrayjson-path-item)

```js
var myJSON = {
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
No alias.
### `empty(json)`
Returns true if json is empty, false otherwise.
```js
empty({}) === true;
empty(myJSON) === false;
```
No alias.
### `size(json)`
Returns the number of keys in json, including subkeys.
```js
size(myJSON) === 8;
```
No alias.
### `getNested(json, path)`
Returns the value of a nested key using string syntax for path.
```js
getNested(myJSON, "foo.fooMore.fooMost"); // returns "hey!"
getNested(myJSON, "foo.fooMore.fooNo"); // returns undefined
getNested(myJSON, ""); // returns myJSON object
```
alias is get(json, path).
### `modifyNested(json, path, value)`
Changes the value of a nested key using string syntax for path.
```js
var result = modifyNested(myJSON, "foo.fooMore.fooMost", "bye!"); // returns true if new value was set,
false if key not found.

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooMost === "bye!";
```
alias is modify(json, path, value).
### `removeNested(json, path)`
Removes a nested key using string syntax for path.
```js
var removedItem = removeNested(myJSON, "foo.fooMore.fooMass"); // returns removed value if key was removed,
undefined if key not found.

// effect on myJSON if removedItem !== undefined:
myJSON.foo.fooMore === { fooMost: "hey!" };
```
alias is remove(json, path, value).
### `findNested(json, key)`
Returns an array of all values that have "key" as key.
```js
var matches = removeNested(myJSON, "foo"); // if nothing is found, array is empty.

matches ===
[ { fooMore: { fooMost: 'hey!', fooMass: 'bye!', foo: true },
    foo: { fooYou: 'no' },
    fooArray: [ 1, 2, 3, 5 ] },
  true,
  { fooYou: 'no' } ];
```
alias is find(json, key).
### `pushInNestedArray(json, path, item)`
Pushes item into a nested array in json.
```js
var result = pushInNestedArray(myJSON, "foo.fooMore.fooArray", 4); // returns true if item was inserted
into array, false if key not found or key is no array.

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooArray === [ 1,2,3,5,4 ];
```
alias is pushArray(json, path, item).
### `removeInNestedArray(json, path, item)`
Removes item in a nested array in json.
```js
var removedItem = removeInNestedArray(myJSON, "foo.fooMore.fooArray", 3); // returns removed value if item was
removed from array, false if key not found or key is no array or array does not containt item.

// effect on myJSON if result !== undefined:
myJSON.foo.fooMore.fooArray === [ 1,2,5,4 ];
```
alias is removeArray(json, path, item).

### function stringifyNoCircular(json)
Converts a JSON object to a string, omitting circular references in it.
```

```
