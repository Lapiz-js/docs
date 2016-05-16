## Collections Helpers

The Collections helpers module provides a number of tools for working with arrays, objects and maps (key/value with no prototype).

[Home](./index.md)
* [Lapiz.remove(array, element, start)](#remove)
* [Lapiz.each(collection, func)](#each)
* [Lapiz.set(obj, name, value)](#set)
* [Lapiz.Map()](#map)
  * [Lapiz.Map.method(obj, method)](#method)
  * [Lapiz.Map.prop(obj, name, desc)](#prop)
  * [Lapiz.Map.getter(object, getter)](#getter)
  * [Lapiz.Map.setterGetter(obj, name, setter, getter)](#setterGetter)
* [Lapiz.Namespace(constructor)](#namespace)
* [Lapiz.ArrayConverter(accessor)](#arrayConverter)

### <a name="remove"></a> Lapiz.remove(array, element, start)
Removes the one instance of the given element from the array. If start is not specified, it will be the first instance, otherwise it will be the first instance at or after start.
```javascript
var arr = [3,1,4,1,5,9];
Lapiz.remove(arr,1);
console.log(arr); //[3,4,1,5,9]
```

### <a name="each"></a> Lapiz.each(collection, func)
Iterates over the collection, calling func(key, val) for each item in the collection. If the collection is an array, key will be the index. If func returns true (or an equivalent value) the Lapiz.each will return the current key allowing each to act as a search.

```javascript
var arr = [3,1,4,1,5,9];
Lapiz.each(arr, function(key,val){
  console.log(key, val);
});
var gt4 = Lapiz.each(arr, function(key,val){return val > 4;});

var kv = {
  "A":"apple",
  "B":"banana",
  "C":"cantaloupe"
};
Lapiz.each(kv, function(key,val){
  console.log(key, val);
});
```

### <a name="set"></a> Lapiz.set(obj, name, value)
Defines a fixed property on an object. This is a wrapper around:
```javascript
Object.defineProperty(obj, name, {value:value});
```

This can be a useful technique to create properties that cannot be overridden
```javascript
var x = {};
x.foo = function(){...};
/* somewhere else */
x.foo = 12; //the method is now gone

var y = {};
Lapiz.set(y, "foo", function{...});
y.foo = 12; //this will not override the method
```

### <a name="map"></a> Lapiz.Map()
Returns a key value store that inherits no properties or methods. Useful to bypass calling "hasOwnProperty". This is just a wrapper around Object.create(null);

Lapiz.Map also servers as a namespace for the following helper methods. They can be called on any object. They all use Object.defineProperty to create a proptery that cannot be overridden.

#### <a name="method"></a> Lapiz.Map.method(obj, method)
Attaches a method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.Map.method(x, function foo(){...});
x.foo(); //calls foo
```

#### Lapiz.Map.setterMethod(obj, method)
Attaches a setter method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.Map.method(x, function foo(val){...});

//these two calls are equivalent
x.foo("bar");
x.foo = "bar";
```

#### <a name="prop"></a> Lapiz.Map.prop(obj, name, desc)
Just a wrapper around Object.defineProperty

#### <a name="getter"></a> Lapiz.Map.getter(object, getter)
Attaches a getter method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
var ctr = 0;
Lapiz.Map.getter(x, function foo(){
  var c = ctr;
  ctr +=1;
  return c;
});
console.log(x.foo); //0
console.log(x.foo); //1
```

#### <a name="setterGetter"></a> Lapiz.Map.setterGetter(obj, name, setter, getter)
Creates a setter/getter property via a closure. A setter function is required, if no getter is provided, the value will be returned. This is the reason the method is named setterGetter rather than the more traditional arrangement of "getterSetter" because the arguments are arranged so that the first 3 are required and the last is optional.

```javascript
var x = Lapiz.Map();
Lapiz.Map.setterGetter(x, "foo", function(i){return parseInt(i);});

x.foo = "12";
console.log(x.foo); // will log 12 as an int
```

The value 'this' is always set to a special setterInterface for the setter method. This can be used to cancel the set operation;

```javascript
var x = Lapiz.Map();
Lapiz.Map.setterGetter(x, "foo", function(i){
  i = parseInt(i);
  this.set = !isNaN(i);
  return i;
});

x.foo = "12";
console.log(x.foo); // will log 12 as an int
x.foo = "hello";
console.log(x.foo); // value will still be 12
```

### <a name="namespace"></a> Lapiz.Namespace(constructor)
Namespace is a closure around all of the Map methods (plus Lapiz.set). It provides syntactic sugar so that the obj argument doesn't need to be supplied each time.

* set(name, value)
* prop(name, desc)
* method(fn)
* setterMethod(fn)
* getter(fn)
* setterGetter(name, setter, getter)
* .namespace : the object of the namespace

The constructor is optional. If not given the outer layer of the namespace is returned.
```javascript
var x = Lapiz.Namespace();
x.set("foo", "bar");
x.method(function sayHello(name){
  console.log("Hello, "+name);
});
console.log(x.namespace.foo); // bar
x.namespace.sayHello("World"); // Hello, World
```

If a constructor is provided, it will be invoked with "this" as the outer layer of the namespace and will return in the inner namespace.
```javascript
var x = Lapiz.Namespace(function(){
  this.set("foo", "bar");
  this.method(function sayHello(name){
    console.log("Hello, "+name);
  });
});

console.log(x.foo); // bar
x.sayHello("World"); // Hello, World
```

### <a name="arrayConverter"></a> Lapiz.ArrayConverter(accessor)
Takes an [accessor](./dictionary.md#accessor) and provides an array. The events on the accessor will be used to keep the array up to date. However, if the array is modified, the results can be unpredictable. This primarily provided as a tool for interfacing with other libraries and frameworks. Use the accessor interface whenever possible.
