# simplify-json
easy-to-use toolkit to handle JSON objects in node.js that lets you work with string paths.
I originally build this for my to handle mongoose models in an automated way. Please note that this is still under development and use own your own risk.

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

Provided methods are listed below, each one with exemplary use.

#### function empty(json)
Returns true if json is empty, false otherwise:
```
empty({}) === true;
empty({ foo: "bar" }) === false;
```
#### function getNested(json, path)
Returns the value of a nested key using string syntax for path.
```
getNested({ foo: { fooMore: { fooMost: "hey!" } } }, "foo.fooMore.fooMost") === "hey!";
```
alias is get(json, path)
#### function modifyNested(json, path, value)
Changes the value of a nested key using string syntax for path.
```
let myJSON = { foo: { fooMore: { fooMost: "hey!" } } };
modifyNested(myJSON, "foo.fooMore.fooMost", "bye!");
myJSON === { foo: { fooMore: { fooMost: "bye!" } } };
```
alias is modify(json, path, value)
#### function removeNested(json, path)
Removes a nested key using string syntax for path.
```
let myJSON = { foo: { fooMore: { fooMost: "hey!", fooMass: "bye!" } } };
modifyNested(myJSON, "foo.fooMore.fooMass");
myJSON === { foo: { fooMore: { fooMost: "hey!" } } };
```
alias is remove(json, path, value)
#### function pushInNestedArray(json, path, item)
Pushes item into a nested array in json.
```
let myJSON = { foo: { fooMoreArray: [ "hey!", "bye!" ] } };
modifyNested(myJSON, "foo.fooMoreArray", "wow!");
myJSON === { foo: { fooMoreArray: [ "hey!", "bye!", "wow!" ] } };
```
alias is pushArray(json, path, item)
#### function removeInNestedArray(json, path, item)
Removes item in a nested array in json.
```
let myJSON = { foo: { fooMoreArray: [ "hey!", "bye!" ] } };
modifyNested(myJSON, "foo.fooMoreArray", "bye!");
myJSON === { foo: { fooMoreArray: [ "hey!" ] } };
```
alias is removeArray(json, path, item)
