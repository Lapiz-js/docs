## core/index.js<a name="__top"></a><span style="float:right; font-size:60%">[Home](index.md)</sub>

* [Lapiz.Index](#Lapiz.Index)
* [indexedClass.Filter](#indexedClass.Filter)
* [indexedClass.Sort](#indexedClass.Sort)
* [indexedClass.all](#indexedClass.all)
* [indexedClass.each](#indexedClass.each)
* [indexedClass.get](#indexedClass.get)
* [indexedClass.has](#indexedClass.has)
* [indexedClass.keys](#indexedClass.keys)
* [indexedClass.remove](#indexedClass.remove)

### <a name='Lapiz.Index'></a>Lapiz.Index <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Index(lapizClass)
Lapiz.Index(lapizClass, primaryFunc)
Lapiz.Index(lapizClass, primaryField)
Lapiz.Index(lapizClass, primary, domain)
```
Adds an index to a class. If class.on.change and class.on.delete exist,
the index will use these to keep itself up to date.

Index needs a primary key. Any to entries with the same primary key are
considered equivalent and one will overwrite the other. By default, Index
assumes a primary property of "id". To use another field, pass in a string
as primaryField. To generate a primary key from the data in the object,
pass in a function as primaryFunc.

By default, the Index methods will be attached directly to the class. If
this would cause a namespace collision, a string can be provided as a
domain and all methods will be attached in that namespace.

### <a name='indexedClass.Filter'></a>indexedClass.Filter <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.Filter(filterFunc)
indexedClass.Filter(filterField, val)
```

### <a name='indexedClass.Sort'></a>indexedClass.Sort <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.Sort(sortFunc)
indexedClass.Sort(sortField)
```

### <a name='indexedClass.all'></a>indexedClass.all <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.all
```

### <a name='indexedClass.each'></a>indexedClass.each <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.each( function(key, val))
```

### <a name='indexedClass.get'></a>indexedClass.get <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.get(primaryKey)
indexedClass.get(field, val)
```

### <a name='indexedClass.has'></a>indexedClass.has <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.has(key)
```

### <a name='indexedClass.keys'></a>indexedClass.keys <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.keys
```

### <a name='indexedClass.remove'></a>indexedClass.remove <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
indexedClass.remove(key)
```
