## Lapiz/core/filter.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.Filter](#Lapiz.Filter)
* [filter](#filter)
  * [filter.Accessor](#filter.Accessor)
  * [filter.Filter](#filter.Filter)
  * [filter.ForceRescan](#filter.ForceRescan)
  * [filter.Sort](#filter.Sort)
  * [filter._cls](#filter._cls)
  * [filter.each](#filter.each)
  * [filter.func](#filter.func)
    * [filter.func.on.change](#filter.func.on.change)
  * [filter.has](#filter.has)
  * [filter.keys](#filter.keys)
  * [filter.kill](#filter.kill)
  * [filter.length](#filter.length)
  * [filter.on](#filter.on)
    * [filter.on.change](#filter.on.change)
    * [filter.on.insert](#filter.on.insert)
    * [filter.on.remove](#filter.on.remove)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "Filter"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.Filter'></a>Lapiz.Filter
```javascript
Lapiz.Filter(accessor, filterFunc(key, accessor) )
Lapiz.Filter(accessor, field, val)
```
Filters an accessor based on a function or field.

One edge case is that an accessor cannot filter by field
for undefined. To do that, you have to create a function
to check the field.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='filter'></a>filter
```javascript
filter(key)
```
Returns the value associated with key, if it exists in the filter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.Accessor'></a>filter.Accessor
```javascript
filter.Accessor
```
Returns a reference to self

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.Filter'></a>filter.Filter
```javascript
filter.Filter(filterFunction)
filter.Filter(field, val)
```
Returns a filter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.ForceRescan'></a>filter.ForceRescan
```javascript
filter.ForceRescan()
```
Rescans all values from parent access and fires insert and remove events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.Sort'></a>filter.Sort
```javascript
filter.Sort(sorterFunction)
filter.Sort(fieldName)
```
Returns a Sorter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter._cls'></a>filter._cls
```javascript
filter._cls
```
Return Lapiz.Filter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.each'></a>filter.each
```javascript
filter.each(fn)
```
Iterates over the collection and calls fn(val, key) on each member.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.func'></a>filter.func
```javascript
filter.func(filterFunc(key, accessor))
filter.func = filterFunc(key, accessor)
```
Changes the function used for the filter. The insert and remove events
will fire as the members are scanned to check if they comply with the
new members

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='filter.func.on.change'></a>filter.func.on.change
```javascript
filter.func.on.change
```
If the function supplied for filter function has a change event,
then when that event fires, it will force a rescan.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.has'></a>filter.has
```javascript
filter.has(key)
```
Returns a bool indicating if the filter contains the key

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.keys'></a>filter.keys
```javascript
filter.keys
```
Returns an array of keys

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.kill'></a>filter.kill
```javascript
filter.kill()
```
After calling kill, a Filter is no longer live. It will not receive
updates and can more easily be garbage collected (because it's
parent accessor no longer has any references to it).

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.length'></a>filter.length
```javascript
filter.length
```
Read-only property that returns the length

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='filter.on'></a>filter.on
```javascript
filter.on
```
Namespace for filter events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='filter.on.change'></a>filter.on.change
```javascript
filter.on.change( function(key, accessor) )
filter.on.change = function(key, accessor)
```
Registration of change event which fires when a new value is assigned to
an existing key

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='filter.on.insert'></a>filter.on.insert
```javascript
filter.on.insert( function(key, accessor) )
filter.on.insert = function(key, accessor)
```
Registration for insert event which fires when a new value is added to
the filter

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='filter.on.remove'></a>filter.on.remove
```javascript
filter.on.remove( function(key, val, accessor) )
filter.on.remove = function(key, val, accessor)
```
Registration for remove event which fires when a value is removed

<sub><sup>[&uarr;Top](#__top)</sup></sub>