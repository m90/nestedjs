NestedJS
========

API
----

NestedJS has two unique APIs.
The first of them is the base class `NestedSetModel`, which maintains
the hierachy of the set model.

The latter is `NestedSetNodeModel`, which maintains it's own model based
off it's parent `NestedSetModel` and properties required for a nested set
item: `left` and `right`. 

NestedSetModel
----

**constructor(`array` model)**

The constructor takes a single argument, which is a collection of sets
expressed as a single array.

The constructor sorts the collection by left nodes ascending.
This is done to optimize child lookups, as it only has to match
a smaller portion of the tree.

__Take note that utliple root nodes are not supported at this time.__

**Example**
```javascript
var model = new NestedSetModel(my_array);
```
----

**find(`object` partial, `boolean` strict)**

__See: compareNodes(`object` a, `object` b, `boolean` strict)__

The find method acts as expected. It retrieves nodes in the tree that
match a predefined object partial.

If the `strict` paramater is passed with a boolean value of true, the
method will return only exact matches by keys and values.
It does not validate that the object's prototype.

If the `strict` parameter is not passed, or passed as a boolean false,
it will return partial matches.

__Take note that the method will return only the first matched node.__

**Example**
```javascript
var results = model.find({ title: 'test' });
// results will be an instance of NestedSetNodeModel
```

----

NestedSetNodeModel
----

**constructor(`object` node, `NestedSetModel` model)**

Creates a new instance of a node within the nested set.
If caches all properties.

**Example**
```javascript
var node = new NestedSetNodeModel({ left: 1, right: 1}, model);
```

----

**parents()**

This method will return all parents as an array for any particular node.

**Example**
```javascript
var parents = model.find({ left: 6 }).parents();
```

----

**children()**

This method will return all children as an array for any particular node.

**Example**
```javascript
var children = model.find({ left: 6 }).children();
```

----

**isParent()**

Returns a boolean value based on whether the node is a parent in the tree.
__Note: This is an inversion of `isLeaf()`.__

**Example**
```javascript
var isParent = model.find({ left: 6 }).isParent();
```

----

**isChild()**

Returns a boolean value based on whether the node is a child in the tree.

**Example**
```javascript
var isChild = model.find({ left: 6 }).isChild();
```

----

**isLeaf()**

Returns a boolean value based on whether the node is a leaf node in the tree.

**Example**
```javascript
var isLeaf = model.find({ left: 6 }).isLeaf();
```