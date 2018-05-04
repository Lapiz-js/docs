## Lapiz/core/grouper.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.Group](#Lapiz.Group)
* [group](#group)
  * [group.Accessor](#group.Accessor)
  * [group.Add](#group.Add)
  * [group.Filter](#group.Filter)
  * [group.Remove](#group.Remove)
  * [group.Sort](#group.Sort)
  * [group._cls](#group._cls)
  * [group.each](#group.each)
  * [group.has](#group.has)
  * [group.keys](#group.keys)
  * [group.kill](#group.kill)
  * [group.length](#group.length)
  * [group.on](#group.on)
    * [group.on.change](#group.on.change)
    * [group.on.insert](#group.on.insert)
    * [group.on.remove](#group.on.remove)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "Group"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.Group'></a>Lapiz.Group
```javascript
Lapiz.Group(accessor)
```
Creates a sub-group of values from an accessor.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='group'></a>group
```javascript
group(key)
```
Returns the value associated with key, if it exists in the group

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Accessor'></a>group.Accessor
```javascript
group.Accessor
```
Returns a reference to self

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Add'></a>group.Add
```javascript
group.Add(key)
```
If the key exists in the accessor, it is added to the group.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Filter'></a>group.Filter
```javascript
group.Filter(filterFunction)
group.Filter(field, val)
```
Returns a filter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Remove'></a>group.Remove
```javascript
group.Remove(key)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Sort'></a>group.Sort
```javascript
group.Sort(sorterFunction)
group.Sort(fieldName)
```
Returns a Sorter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group._cls'></a>group._cls
```javascript
group._cls
```
Return Lapiz.Group

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.each'></a>group.each
```javascript
group.each(fn)
```
Iterates over the collection and calls fn(val, key) on each member.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.has'></a>group.has
```javascript
group.has(key)
```
Returns a bool indicating if the group contains the key

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.keys'></a>group.keys
```javascript
group.keys
```
Returns an array of keys

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.kill'></a>group.kill
```javascript
group.kill()
```
After calling kill, a Filter is no longer live. It will not receive
updates and can more easily be garbage collected (because it's
parent accessor no longer has any references to it).

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.length'></a>group.length
```javascript
group.length
```
Read-only property that returns the length

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.on'></a>group.on
```javascript
group.on
```
Namespace for group events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='group.on.change'></a>group.on.change
```javascript
group.on.change( function(key, accessor) )
group.on.change = function(key, accessor)
```
Registration of change event which fires when a new value is assigned to
an existing key

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='group.on.insert'></a>group.on.insert
```javascript
group.on.insert( function(key, accessor) )
group.on.insert = function(key, accessor)
```
Registration for insert event which fires when a new value is added to
the group

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='group.on.remove'></a>group.on.remove
```javascript
group.on.remove( function(key, val, accessor) )
group.on.remove = function(key, val, accessor)
```
Registration for remove event which fires when a value is removed

<sub><sup>[&uarr;Top](#__top)</sup></sub>