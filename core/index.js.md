## core/index.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Index](#Lapiz.Index)
  * [Lapiz.Index.Class](#Lapiz.Index.Class)
  * [Lapiz.Index.defaultPrimary](#Lapiz.Index.defaultPrimary)
* [indexedClass.Filter](#indexedClass.Filter)
* [indexedClass.Sort](#indexedClass.Sort)
* [indexedClass.all](#indexedClass.all)
* [indexedClass.each](#indexedClass.each)
* [indexedClass.get](#indexedClass.get)
* [indexedClass.has](#indexedClass.has)
* [indexedClass.keys](#indexedClass.keys)
* [indexedClass.remove](#indexedClass.remove)

### <a name='Lapiz.Index'></a>Lapiz.Index
```javascript
Lapiz.Index(lapizClass)
Lapiz.Index(lapizClass, primaryFunc)
Lapiz.Index(lapizClass, primaryField)
Lapiz.Index(lapizClass, primary, domain)
```
Adds an index to a class. If class.on.change and class.on.remove exist,
the index will use these to keep itself up to date.

Index needs a primary key. Any to entries with the same primary key are
considered equivalent and one will overwrite the other. By default, Index
assumes a primary property of "id". To use another field, pass in a string
as primaryField. To generate a primary key from the data in the object,
pass in a function as primaryFunc.

By default, the Index methods will be attached directly to the class. If
this would cause a namespace collision, a string can be provided as a
domain and all methods will be attached in that namespace.

The class does not have to be a lapizClass, but it must have a similar
interface. Specifically, it must have cls.on.change and the instances of
the class must have obj.on.change and obj.on.remove.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Index.Class'></a>Lapiz.Index.Class
```javascript
Lapiz.Index.Class(constructor, primaryFunc, domain)
```
Shorthand helper, constructor for an indexed class.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Index.defaultPrimary'></a>Lapiz.Index.defaultPrimary
```javascript
Lapiz.Index.defaultPrimary
```
Sets the default primary key name. It defaults to "id".

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.Filter'></a>indexedClass.Filter
```javascript
indexedClass.Filter(filterFunc)
indexedClass.Filter(filterField, val)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.Sort'></a>indexedClass.Sort
```javascript
indexedClass.Sort(sortFunc)
indexedClass.Sort(sortField)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.all'></a>indexedClass.all
```javascript
indexedClass.all
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.each'></a>indexedClass.each
```javascript
indexedClass.each( function(val, key))
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.get'></a>indexedClass.get
```javascript
indexedClass.get(primaryKey)
indexedClass.get(field, val)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.has'></a>indexedClass.has
```javascript
indexedClass.has(key)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.keys'></a>indexedClass.keys
```javascript
indexedClass.keys
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='indexedClass.remove'></a>indexedClass.remove
```javascript
indexedClass.remove(key)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
