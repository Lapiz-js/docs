## Dictionary

Dictionaries are key/value stores that emit events.

[Home](./index.md)
* [Accessors](#accessors)
* [Lapiz.Dictionary(seed)](#dictionary)
  * [dict.length](#length)
  * [dict.remove(key)](#remove)
  * [dict.has(key)](#has)
  * [dict.each( function(key, val) )](#each)
  * [dict.on](#on)
    * [dict.on.insert( function(key, accessor) )](#insert)
    * [dict.on.change( function(key, accessor) )](#change)
    * [dict.on.remove( function(key, val, accessor) )](#onRemove)
  * [dict.Sort(funcOrField)](#sort)
  * [dict.Filter(filterOrAttr, val)](#filter)

### <a name="accessors"></a> Accessors
Accessors are an abstract intereface. An accessor cannot be constructed, but any object that implements the following interface can be treated as an accessor. The accessor itself should be a function that takes a key and returns a value. It should have the following properties and methods.

* has(key) : returns a boolean indicating if the collection has the specified key
* each( function(key, val) ): iterates over the collection passing each into the given function
* on
  * change( function(key, accessor) ): register method to receive an update when a value changes
  * insert( function(key, accessor) ): register method to receive an update when a key/value is inserted
  * remove( function(key, obj, accessor) ): register method to receive an update when a key/value is removed
* keys : read-only property, returns a list of all keys
* length: read-only property, returns the number of key/values
* Accessor: returns a read-only copy of itself. If the instance is read-only, it can reference itself.

### <a name="dictionary"></a> Lapiz.Dictionary(seed)
Dictionaries allow for the storage of key/value pairs in a container that will emit events as the contents change.

If seed values are specified, they will start as the contents of the dictionary, otherwise the dictionary will start off empty.
```javascript
var emptyDict = Lapiz.Dictionary();
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict("A")); // apple
fruitDict("A", "apricot");
console.log(fruitDict("A")); // apricot
emptyDict(12, "zebra");
console.log(emptyDict(12)); // apricot
```

#### <a name="length"></a> dict.length
A read-only property that returns the length of a dictionary
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.length); // 3
```

#### <a name="remove"></a> dict.remove(key)
The remove method will remove a key from the dictionary.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
fruitDict.remove("B");
console.log(fruitDict.length); // 2
console.log(fruitDict("B")); // undefined
```

#### <a name="has"></a> dict.has(key)
The has method returns a boolean stating if the dictionary has the given key.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.has("B")); // true
console.log(fruitDict.has(12)); // false
```

#### <a name="each"></a> dict.each( function(key, val) )
The each method takes a function and calls it for each key/value in the collection. The function will be called with two arguments, the key and the corresponding value. If any invocation of the function returns True, that will signal the each loop to break. The order is not guarenteed.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
fruitDict(function(key, val){
  console.log(key, val);
  return key === "A";
});
```

#### <a name="keys"></a> dict.keys
A read-only property that will return the keys as an array.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.keys); // ["C", "A", "B"] in some order
```

#### <a name="on"></a> dict.on
This is the namespace that hold the event registration

##### <a name="insert"></a> dict.on.insert( function(key, accessor) )
The dict.on.insert method registers an observer that will be called when a value is inserted. Note that the second argument is an accessor, so it cannot modify the contents of dictionary.
```javascript
var dict = Lapiz.Dictionary();
function fn(key, acc){
  console.log(key, acc(key));
}
dict.on.insert = fn;
dict(32, "Adam"); // will output 32 "Adam" to the console
dict.on.insert.deregister(fn);
dict(12, "zebra"); // nothing will output to console
dict.on.insert(fn);
dict(314, "100 pi"); // will output 314 "100 pi" to the console
```

##### <a name="change"></a> dict.on.change( function(key, accessor) )
The dict.on.change method registers an observer that will be called when a value is changed. Note that the second argument is an accessor, so it cannot modify the contents of dictionary.
```javascript
var dict = Lapiz.Dictionary();
function fn(key, acc){
  console.log(key, acc(key));
}
dict.on.change = fn;
dict(32, "Adam"); // will not log anything
dict(32, "Alex"); // will output 32 "Alex" to the console
```

Not shown, but dict.on.change also can be called as a function and has a deregister method.

##### <a name="onRemove"></a> dict.on.remove( function(key, val, accessor) )
The dict.on.remove method registers an observer that will be called when a value is removed. Note that the third argument is an accessor, so it cannot modify the contents of dictionary. Also note that this has a different function signature than insert and change.
```javascript
var dict = Lapiz.Dictionary();
function fn(key, val, acc){
  console.log(key, val, acc.has(key));
}
dict.on.remove = fn;
dict(32, "Adam"); // will not log anything
dict(32, "Alex"); // will not log anything
dict.remove(32); // will output 32 "Alex" false to the console
```

Not shown, but dict.on.change also can be called as a function and has a deregister method.

#### <a name="sort"></a> dict.Sort(funcOrField)
Creates a Sorter that takes the dictionary as input.

#### <a name="filter"></a> dict.Filter(filterOrAttr, val)
Creates a Filter that takes the dictionary as input.