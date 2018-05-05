## Lapiz/core/dictionary.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.Dictionary](#Lapiz.Dictionary)
* [dict](#dict)
  * [dict.Accessor](#dict.Accessor)
  * [dict.Filter](#dict.Filter)
  * [dict.Sort](#dict.Sort)
  * [dict._cls](#dict._cls)
  * [dict.each](#dict.each)
  * [dict.has](#dict.has)
  * [dict.keys](#dict.keys)
  * [dict.length](#dict.length)
  * [dict.on](#dict.on)
    * [dict.on.change](#dict.on.change)
    * [dict.on.insert](#dict.on.insert)
    * [dict.on.remove](#dict.on.remove)
  * [dict.remove](#dict.remove)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "Dictionary"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.Dictionary'></a>Lapiz.Dictionary
```javascript
Lapiz.Dictionary()
Lapiz.Dictionary(seed)
```
Dictionaries allow for the storage of key/value pairs in a container that
will emit events as the contents change.

If seed values are specified, they will start as the contents of the
dictionary, otherwise the dictionary will start off empty.
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

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='dict'></a>dict
```javascript
dict(key)
dict(key, val)
```
If only key is given, the value currently associated with that key will
be returned. If key and val are both given, val is associated with key
and the proper event (change or insert) will fire. For chaining, the
val is returned when dict is called as a setter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.Accessor'></a>dict.Accessor
```javascript
dict.Accessor
dict.Accessor(key)
```
The accessor is a read-only interface to the dictionary

* accessor.length
* accessor.keys
* accessor.has(key)
* accessor.each(fn(val, key))
* accessor.on.insert
* accessor.on.change
* accessor.on.remove
* accessor.Sort
* accessor.Filter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.Filter'></a>dict.Filter
```javascript
dict.Filter(filterFunction)
dict.Filter(attribute, val)
```
Returns a Filter with the dictionary as the accessor

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.Sort'></a>dict.Sort
```javascript
dict.Sort(sorterFunction)
dict.Sort(attribute)
```
Returns a Sorter with the dictionary as the accessor

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict._cls'></a>dict._cls
```javascript
dict._cls
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.each'></a>dict.each
```javascript
dict.each(fn(key, val))
```
The each method takes a function and calls it for each key/value in the
collection. The function will be called with two arguments, the key and
the corresponding value. If any invocation of the function returns True,
that will signal the each loop to break. The order is not guarenteed.
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

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.has'></a>dict.has
```javascript
dict.has(key)
```
The has method returns a boolean stating if the dictionary has the given
key.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.has("B")); // true
console.log(fruitDict.has(12)); // false
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.keys'></a>dict.keys
```javascript
dict.keys
```
A read-only property that will return the keys as an array.
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.keys); // ["C", "A", "B"] in some order
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.length'></a>dict.length
```javascript
dict.length
```
A read-only property that returns the length of a dictionary
```javascript
var fruitDict = Lapiz.Dictionary({
  "A": "apple",
  "B": "banana",
  "C": "cantaloupe"
});
console.log(fruitDict.length); // 3
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.on'></a>dict.on
```javascript
dict.on
```
Namespace for dictionary events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='dict.on.change'></a>dict.on.change
```javascript
dict.on.change(fn(key, accessor, oldVal))
```
Event will fire when a new key has a new value associated with it.

One poentential "gotcha":
```javascript
var d = Dict();
d.on.change = function(key, acc){
  console.log(key, acc(key));
};
//assume person is a Lapiz Class
d(5, Person(5, "Adam", "admin")); // does not fire change, as it's an insert
d(5).role = "editor"; // this will fire person.on.change, but not dict.on.change
d(5, Person(5, "Bob", "editor")); // this will fire dict.on.change
```
To create a change listener for a class on a dict (or other accessor)

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='dict.on.insert'></a>dict.on.insert
```javascript
dict.on.insert(fn(key, accessor))
```
Event will fire when a new key is added to the dictionary

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='dict.on.remove'></a>dict.on.remove
```javascript
dict.on.remove(fn(key, accessor, oldVal))
```
Event will fire when a key is removed.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='dict.remove'></a>dict.remove
```javascript
dict.remove(key)
```
The remove method will remove a key from the dictionary and the remove
event will fire.
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

<sub><sup>[&uarr;Top](#__top)</sup></sub>