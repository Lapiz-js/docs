## Lapiz/core/grouper.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [.ModuleName](#.ModuleName)
* [Lapiz.Group](#Lapiz.Group)
* [Lapiz.GroupBy](#Lapiz.GroupBy)
* [group](#group)
  * [group.Accessor](#group.Accessor)
  * [group.Add](#group.Add)
  * [group.Change](#group.Change)
  * [group.Filter](#group.Filter)
  * [group.GroupBy](#group.GroupBy)
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
* [groupBy](#groupBy)
  * [groupBy.ForceRescan](#groupBy.ForceRescan)
  * [groupBy._cls](#groupBy._cls)
  * [groupBy.has](#groupBy.has)
  * [groupBy.keys](#groupBy.keys)
  * [groupBy.length](#groupBy.length)
* [settings](#settings)
  * [settings.DoNotListen](#settings.DoNotListen)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "Group"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "GroupBy"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.Group'></a>Lapiz.Group
```javascript
Lapiz.Group(accessor, settings)
```
Creates a sub-group of values from an accessor. This is essentially an
actively managed filter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.GroupBy'></a>Lapiz.GroupBy
```javascript
Lapiz.GroupBy(accessor, field)
Lapiz.GroupBy(accessor, groupKeyFn(key, accessor) )
```
Creates a set of sub-groups from an accessor. While not limited to this, it
is particularly useful in representing one-to-many relationships. The
accessor containing all the instances of the child class can be grouped by
their parent key.

The same thing could be accomplished with Filters, one per parent. The
advantage of this is that it is more efficient. Using filters, when a child
is added, removed or changed, each Filter instance will be invoked to
handle the event - O(N) where N is the number of Filters which is the
number of parent keys. With this, the event is handled once and on the
groups that need to be notified of the change are. This is O(1) regardless
of the number of parent keys.

Undefined group keys will not be used, they will just be skipped and not
belong to any group.

The second argument can be a group key function. This needs to return a
string that represents the group key. This can be used to normalize values,
group by multiple fields or replace undefined with a string value so that
those values are grouped.

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
group.Accessor(key)
```
The accessor is a read-only iterface to the group

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
#### <a name='group.Add'></a>group.Add
```javascript
group.Add(key)
```
If the key exists in the accessor, it is added to the group.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Change'></a>group.Change
```javascript
group.Change(key, oldVal)
```
Fires the change event.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Filter'></a>group.Filter
```javascript
group.Filter(filterFunction)
group.Filter(field, val)
```
Returns a filter.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.GroupBy'></a>group.GroupBy
```javascript
group.GroupBy(attribute)
group.GroupBy(groupByFunction)
```
Returns a GroupBy with the group as the accessor

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='group.Remove'></a>group.Remove
```javascript
group.Remove(key)
group.Remove(key, oldVal)
```
Removes the key. The oldVal parameter is only needed if the Group is not
listening on it's underlying Accessor and the value has been removed.

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
### <a name='groupBy'></a>groupBy
```javascript
groupBy(key)
```
Returns the group associated with key, if it exists.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='groupBy.ForceRescan'></a>groupBy.ForceRescan
```javascript
groupBy.ForceRescan()
```
Rescans all values from parent access and fires insert and remove events

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='groupBy._cls'></a>groupBy._cls
```javascript
groupBy._cls
```
Return Lapiz.GroupBy

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='groupBy.has'></a>groupBy.has
```javascript
groupBy.has(key)
```
Returns a bool indicating if the groupBy contains a group for the key

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='groupBy.keys'></a>groupBy.keys
```javascript
groupBy.keys
```
Returns an array of the keys.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='groupBy.length'></a>groupBy.length
```javascript
groupBy.length
```
Read-only property that returns the length

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='settings'></a>settings
```javascript
settings
```
Settings to change the behavior of the group

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='settings.DoNotListen'></a>settings.DoNotListen
```javascript
settings.DoNotListen
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>