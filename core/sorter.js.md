## Lapiz/core/sorter.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.Sort](#Lapiz.Sort)
  * [Lapiz.Sort.gt](#Lapiz.Sort.gt)
  * [Lapiz.Sort.locationOf](#Lapiz.Sort.locationOf)
* [sort.Accessor](#sort.Accessor)
* [sort.Filter](#sort.Filter)
* [sort.Range](#sort.Range)
* [sort.Sort](#sort.Sort)
* [sort.each](#sort.each)
* [sort.func](#sort.func)
* [sort.has](#sort.has)
* [sort.keys](#sort.keys)
* [sort.kill](#sort.kill)
* [sort.length](#sort.length)
* [sort.on](#sort.on)
  * [sort.on.change](#sort.on.change)
  * [sort.on.insert](#sort.on.insert)
  * [sort.on.remove](#sort.on.remove)
* [sortFunction](#sortFunction)
  * [sortFunction.range](#sortFunction.range)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "Sorter"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.Sort'></a>Lapiz.Sort
```javascript
Lapiz.Sort(accessor, sorterFunc(keyA, keyB, accessor))
Lapiz.Sort(accessor, fieldName)
Lapiz.Sort(accessor)
```
Lapiz.Sort is an accessor that when sort.each or sort.keys is called, they
will be in the sorted order. If a sorterFunction is provided, that will be
used to sort the accessor, if a fieldName is provided, the values on that
field will be used. If nothing is given, the accessor will be sorted by
key.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Sort.gt'></a>Lapiz.Sort.gt
```javascript
Lapiz.Sort.gt(key, index, fn, accessor)
Lapiz.Sort.gt(key, index, fn, accessor, start, end)
```
This is used by the sorter to sort it's contents. It is left exposed
because a generic bisecting search is useful in many context. It assumes
that the accessor is sorted. It returns the position in index of the first
key that is greater than the val in the accessor.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Sort.locationOf'></a>Lapiz.Sort.locationOf
```javascript
Lapiz.Sort.locationOf(val, index, fn, accessor)
Lapiz.Sort.locationOf(val, index, fn, accessor, start, end)
```
This is used by the sorter to sort it's contents. It is left exposed
because a generic bisecting search is useful in many context. It assumes
that the accessor is sorted. It returns the position in index of the first
key that is greater than or equal to val in the accessor.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.Accessor'></a>sort.Accessor
```javascript
sort.Accessor
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.Filter'></a>sort.Filter
```javascript
sort.Filter(accessor, filterFunc(key, accessor) )
sort.Filter(accessor, field, val)
```
It is possible to create a filter on a sorter, but it is not recommended.
The sorting operations do not stack so this just passes the events
through unnecessary layers of events. Better to create a filter on the
sorters accessor.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.Range'></a>sort.Range
```javascript
sort.Range(val)
sort.Range(start, stop)
```
Returns all values either equal to val (by the sorter compare function)
or between start and stop (start inclusive, stop exclusive). The result
is returned as a Dictionary, but it is not wired in to update.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.Sort'></a>sort.Sort
```javascript
sort.Sort(accessor, sorterFunc(keyA, keyB, accessor))
sort.Sort(accessor, fieldName)
sort.Sort(accessor)
```
It is possible to create a sorter on a sorter, but it is not recommended.
The sorting operations do not stack so this just passes the events
through unnecessary layers of events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.each'></a>sort.each
```javascript
sort.each( function(val, key, sorter) )
```
Iterates over the collection in order

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.func'></a>sort.func
```javascript
sort.func(sorterFunction)
sort.func = sorterFunction
sort.func(field)
sort.func = field
```
Assign a new function or field to sort by;

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.has'></a>sort.has
```javascript
sort.has(key)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.keys'></a>sort.keys
```javascript
sort.keys
```
Read-only property. The keys will be in the order that the sorter has
arranged them.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.kill'></a>sort.kill
```javascript
sort.kill()
```
After calling kill, a Sorter is no longer live. It will not receive
updates and can more easily be garbage collected (because it's
parent accessor no longer has any references to it).

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.length'></a>sort.length
```javascript
sort.length
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sort.on'></a>sort.on
```javascript
sort.on
```
Namespace for event registration

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='sort.on.change'></a>sort.on.change
```javascript
sort.on.change(fn)
sort.on.change = fn
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='sort.on.insert'></a>sort.on.insert
```javascript
sort.on.insert(fn)
sort.on.insert = fn
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='sort.on.remove'></a>sort.on.remove
```javascript
sort.on.remove(fn)
sort.on.remove = fn
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='sortFunction'></a>sortFunction
```javascript
sortFunction(keyA, keyB, accessor)
```
When the sort function is called it will be given two keys and an
accessor. If the value associated with keyA should come after the value
associated with keyB, return a value greater than 0. If the values are
equal return 0 and if keyB should come after keyA, return a value less
than 0.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='sortFunction.range'></a>sortFunction.range
```javascript
sortFunction.range(keyA, valB, accessor)
```
In order to be able to select a range, there must be a way to compare
an object in the accessor to a value. To provide this to the sorter,
it must be attached to the sortfunction as .range. If this is provided
to the sorter, the .range method will be available on the sorter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>