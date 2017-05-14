# simplify-json
easy-to-use toolkit to handle JSON objects in node.js that lets you work with string paths.
Originally build to alter mongoose models in an automated way. Please note that this is still under development.

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
  - [`noCircular(json)`](#nocircularjson)

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

### `empty(json)`
Returns true if json is empty, false otherwise.
```js
empty({}) === true;
empty(myJSON) === false;
```
No alias.

### `size(json)`
Returns the number of keys in json, including subkeys. If json has a circular dependency, it returns undefined.
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
Changes the value of a nested key using string syntax for path. Returns true if new value was set, false if key was not found.
```js
var result = modifyNested(myJSON, "foo.fooMore.fooMost", "bye!");

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooMost === "bye!";
```
alias is modify(json, path, value).

### `removeNested(json, path)`
Removes a nested key using string syntax for path. Returns the value of the removed entry or undefined if key was not found.
```js
var removedItem = removeNested(myJSON, "foo.fooMore.fooMass");

// effect on myJSON if removedItem !== undefined:
myJSON.foo.fooMore === { fooMost: "hey!" };
```
alias is remove(json, path, value).

### `findNested(json, key)`
Returns an array of all values that have "key" as key. If nothing was found, array is empty.
```js
var matches = removeNested(myJSON, "foo");

matches ===
[ { fooMore: { fooMost: 'hey!', fooMass: 'bye!', foo: true },
    foo: { fooYou: 'no' },
    fooArray: [ 1, 2, 3, 5 ] },
  true,
  { fooYou: 'no' } ];
```
alias is find(json, key).
### `pushInNestedArray(json, path, item)`
Pushes item into a nested array in json. Returns true if item was succesfully inserted into array, false if key was not found or key is not an array.
```js
var result = pushInNestedArray(myJSON, "foo.fooMore.fooArray", 4);

// effect on myJSON if result === true:
myJSON.foo.fooMore.fooArray === [ 1,2,3,5,4 ];
```
alias is pushArray(json, path, item).
### `removeInNestedArray(json, path, item)`
Removes item in a nested array in json. Returns the value of the removed entry or undefined if key was not found, if key is not an array or if the array does not contain the item.
```js
var removedItem = removeInNestedArray(myJSON, "foo.fooMore.fooArray", 3);

// effect on myJSON if result !== undefined:
myJSON.foo.fooMore.fooArray === [ 1,2,5,4 ];
```
alias is removeArray(json, path, item).

### `noCircular(json)`
Checks json for circular dependency. Returns false if json has a circular dependency, true if not.
```js
noCircular(myJSON) === true;
```
No alias.
