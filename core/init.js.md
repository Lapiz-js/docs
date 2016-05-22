## core/init.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Module](#Lapiz.Module)
  * [Lapiz.Module.Loaded](#Lapiz.Module.Loaded)
* [Lapiz.assert](#Lapiz.assert)
* [Lapiz.set](#Lapiz.set)
* [Lapiz.typeCheck](#Lapiz.typeCheck)
  * [Lapiz.typeCheck.array](#Lapiz.typeCheck.array)
  * [Lapiz.typeCheck.func](#Lapiz.typeCheck.func)
  * [Lapiz.typeCheck.nested](#Lapiz.typeCheck.nested)
  * [Lapiz.typeCheck.number](#Lapiz.typeCheck.number)
  * [Lapiz.typeCheck.obj](#Lapiz.typeCheck.obj)
  * [Lapiz.typeCheck.string](#Lapiz.typeCheck.string)

### <a name='Lapiz.Module'></a>Lapiz.Module
```javascript
Lapiz.Module(moduleName, moduleFunction(Lapiz))
Lapiz.Module(moduleName, [dependencies...], moduleFunction(Lapiz))
```
The module loader is useful when building Lapiz modules. It will invoke the
moduleFunction and pass in Lapiz when all dependencies have been loaded. The
moduleName is only used for dependency management.
```javascript
Lapiz.Module("Foo", ["Events"], function($L){
  $L.set($L, "foo", "bar");
});
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Module.Loaded'></a>Lapiz.Module.Loaded
```javascript
Lapiz.Module.Loaded
```
Returns all the modules that have been loaded

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.assert'></a>Lapiz.assert
```javascript
Lapiz.assert(bool, err)
```
If bool evaluates to false, an error is thrown with err.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.set'></a>Lapiz.set
```javascript
Lapiz.set(obj, name, value)
```
Defines a fixed propery on an object. Properties defined this way cannot be
overridden.
```javascript
var x = {};
x.foo = function(){...};
//somewhere else
x.foo = 12; //the method is now gone

var y = {};
Lapiz.set(y, "foo", function{...});
y.foo = 12; // this will not override the method
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.typeCheck'></a>Lapiz.typeCheck
```javascript
Lapiz.typeCheck(obj, type)
Lapiz.typeCheck(obj, type, err)
```
Checks if the type of obj matches type. If type is a string, typeof will be
used, if type is a class, instanceof will be used. To throw an error when
the types do not match, specify err as a string. Other wise, typeCheck will
return a boolean indicating if the types matched.
```javascript
Lapiz.typeCheck([], Array); // true
Lapiz.typeCheck("test", "string"); // true
Lapiz.typeCheck("test", Array); // false
Lapiz.typeCheck([], "string", "Expected string"); // throws an error
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.array'></a>Lapiz.typeCheck.array
```javascript
Lapiz.typeCheck.array(obj)
Lapiz.typeCheck.array(obj, err)
```
Checks if the object is a array. If a string is supplied for err, it
will throw err if obj is not an array.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.func'></a>Lapiz.typeCheck.func
```javascript
Lapiz.typeCheck.func(obj)
Lapiz.typeCheck.func(obj, err)
```
Checks if the object is a function. If a string is supplied for err, it
will throw err if obj is not a function.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.nested'></a>Lapiz.typeCheck.nested
```javascript
Lapiz.typeCheck.nested(obj, nestedFields..., typeCheckFunction)
Lapiz.typeCheck.nested(obj, nestedFields..., typeCheckFunctionName)
```
Checks that each nested field exists and that the last field matches the function type.
So this:
```javascript
if (collection.key !== undefined && collection.key.on !== undefined && Lapiz.typeCheck.func(collection.key.on.change)){
```
becomes:
```javascript
if (Lapiz.typeCheck.nested(collection, "key", "on", "change", "func")){
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.number'></a>Lapiz.typeCheck.number
```javascript
Lapiz.typeCheck.number(obj)
Lapiz.typeCheck.number(obj, err)
```
Checks if the object is a number. If a string is supplied for err, it
will throw err if obj is not an number.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.obj'></a>Lapiz.typeCheck.obj
```javascript
Lapiz.typeCheck.obj(obj)
Lapiz.typeCheck.obj(obj, err)
```
Checks if the object is an object. If a string is supplied for err, it
will throw err if obj is not an number. Note that many things like Arrays and
Dates are objects, but numbers strings and functions are not.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.typeCheck.string'></a>Lapiz.typeCheck.string
```javascript
Lapiz.typeCheck.string(obj)
Lapiz.typeCheck.string(obj, err)
```
Checks if the object is a string. If a string is supplied for err, it
will throw err if obj is not an string.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
