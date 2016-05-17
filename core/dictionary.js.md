## core/dictionary.js<a name="__top"></a><span style="float:right; font-size:60%">[Home](index.md)</sub>

* [Lapiz.Dictioanry](#Lapiz.Dictioanry)
* [dict](#dict)
  * [dict.Accessor](#dict.Accessor)
  * [dict.Filter](#dict.Filter)
  * [dict.Sort](#dict.Sort)
  * [dict.each](#dict.each)
  * [dict.has](#dict.has)
  * [dict.keys](#dict.keys)
  * [dict.length](#dict.length)
  * [dict.on](#dict.on)
    * [dict.on.change](#dict.on.change)
    * [dict.on.insert](#dict.on.insert)
    * [dict.on.remove](#dict.on.remove)
  * [dict.remove](#dict.remove)

### <a name='Lapiz.Dictioanry'></a>Lapiz.Dictioanry <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dictioanry()
Lapiz.Dictioanry(seed)
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

### <a name='dict'></a>dict <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict(key)
dict(key, val)
```
If only key is given, the value currently associated with that key will
be returned. If key and val are both given, val is associated with key
and the proper event (change or insert) will fire.

#### <a name='dict.Accessor'></a>dict.Accessor <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.Accessor
dict.Accessor(key)
```
The accessor is a read-only iterface to the dictionary
* accessor.length
* accessor.keys
* accessor.has(key)
* accessor.each(fn(key, val))
* accessor.on.insert
* accessor.on.change
* accessor.on.remove
* accessor.Sort
* accessor.Filter

#### <a name='dict.Filter'></a>dict.Filter <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.Filter(filterFunction)
dict.Filter(attribute, val)
```
Returns a Filter with the dictionary as the accessor

#### <a name='dict.Sort'></a>dict.Sort <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.Sort(sorterFunction)
dict.Sort(attribute)
```
Returns a Sorter with the dictionary as the accessor

#### <a name='dict.each'></a>dict.each <span style="float:right; font-size:60%">[Top](#__top)</sub>
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

#### <a name='dict.has'></a>dict.has <span style="float:right; font-size:60%">[Top](#__top)</sub>
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

#### <a name='dict.keys'></a>dict.keys <span style="float:right; font-size:60%">[Top](#__top)</sub>
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

#### <a name='dict.length'></a>dict.length <span style="float:right; font-size:60%">[Top](#__top)</sub>
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

#### <a name='dict.on'></a>dict.on <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.on
```
Namespace for dictionary events

##### <a name='dict.on.change'></a>dict.on.change <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.on.change(fn(key, accessor))
```
Event will fire when a new key has a new value associated with it

##### <a name='dict.on.insert'></a>dict.on.insert <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.on.insert(fn(key, accessor))
```
Event will fire when a new key is added to the dictionary

##### <a name='dict.on.remove'></a>dict.on.remove <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
dict.on.remove(fn(key, val, accessor))
```
Event will fire when a key is removed.

#### <a name='dict.remove'></a>dict.remove <span style="float:right; font-size:60%">[Top](#__top)</sub>
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
