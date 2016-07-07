## core/collectionsHelper.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.ArrayConverter](#Lapiz.ArrayConverter)
* [Lapiz.Map](#Lapiz.Map)
  * [Lapiz.Map.binder](#Lapiz.Map.binder)
  * [Lapiz.Map.copyProps](#Lapiz.Map.copyProps)
  * [Lapiz.Map.getter](#Lapiz.Map.getter)
  * [Lapiz.Map.getterFactory](#Lapiz.Map.getterFactory)
  * [Lapiz.Map.has](#Lapiz.Map.has)
  * [Lapiz.Map.meth](#Lapiz.Map.meth)
  * [Lapiz.Map.prop](#Lapiz.Map.prop)
  * [Lapiz.Map.setProperties](#Lapiz.Map.setProperties)
  * [Lapiz.Map.setterFactory](#Lapiz.Map.setterFactory)
  * [Lapiz.Map.setterGetter](#Lapiz.Map.setterGetter)
  * [Lapiz.Map.setterMethod](#Lapiz.Map.setterMethod)
* [Lapiz.Namespace](#Lapiz.Namespace)
* [Lapiz.each](#Lapiz.each)
* [Lapiz.remove](#Lapiz.remove)
* [lapizObject.properties:fire](#lapizObject.properties_fire)
* [lapizObject.properties:setterInterface](#lapizObject.properties_setterInterface)
  * [lapizObject.properties:setterInterface.event](#lapizObject.properties_setterInterface.event)
  * [lapizObject.properties:setterInterface.set](#lapizObject.properties_setterInterface.set)
* [namespace.attr](#namespace.attr)
* [namespace.meth](#namespace.meth)
* [namespace.namespace](#namespace.namespace)
* [namespace.properties](#namespace.properties)
* [namespace.set](#namespace.set)
* [namespace.setterMethod](#namespace.setterMethod)

### <a name='Lapiz.ArrayConverter'></a>Lapiz.ArrayConverter
```javascript
Lapiz.ArrayConverter(accessor)
```
Takes an accessor and provides an array. The events on the accessor will be
used to keep the array up to date. However, if the array is modified, the
results can be unpredictable. This primarily provided as a tool for
interfacing with other libraries and frameworks. Use the accessor interface
whenever possible.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.Map'></a>Lapiz.Map
```javascript
Lapiz.Map()
```
Returns a key value store that inherits no properties or methods. Useful to
bypass calling "hasOwnProperty". This is just a wrapper around
Object.create(null);

Lapiz.Map also serves as a namespace for the following helper methods.
They can be called on any object. They all use Object.defineProperty to
create a proptery that cannot be overridden.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.binder'></a>Lapiz.Map.binder
```javascript
Lapiz.Map.binder(proto, fn)
```
Handles late binding for prototype methods
```javascript
var fooProto = {};
binder(fooProto, function sayHi(){
  console.log("Hi, "+name);
});
var x = {};
x.__proto__ = fooProto;
var sh = x.sayHi;
x.name = "Adam";
sh(); // Hi, Adam
```
This approach balances two concerns. Without binding, we need to eliminate
the use of 'this' with closures, which can add boilerplate code. But
without leveraging prototypes, we can create a lot of uncessary functions.
With late binding, 'this' will always refer to the original 'this' context,
but bound functions will only be generated when they are called or assigned

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.copyProps'></a>Lapiz.Map.copyProps
```javascript
Lapiz.Map.copyProps(copyTo, copyFrom, props...)
```
Copies the properties from the copyFrom object to the copyTo obj. The
properties should be strings. By default, the property will be copied with
basic assignment. If the property is preceeded by &, it will be copied by
reference.
```javascript
var A = {"x": 12, "y": "foo", z:[]};
var B = {};
Lapiz.Map.copyProps(B, A, "x", "&y");
A.x = 314;
console.log(B.x); // 12
B.y = "Test";
console.log(A.y); // Test
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.getter'></a>Lapiz.Map.getter
```javascript
Lapiz.Map.getter(object, namedGetterFunc() )
Lapiz.Map.getter(object, name, getterFunc() )
Lapiz.Map.getter(object, [namedGetterFuncs...] )
Lapiz.Map.getter(object, {name: getterFunc...} )
```
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

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.getterFactory'></a>Lapiz.Map.getterFactory
```javascript
Lapiz.Map.getterFactory(attr, property)
Lapiz.Map.getterFactory(attr, func)
```
Used in generating properties on an object or namespace.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.has'></a>Lapiz.Map.has
```javascript
Lapiz.Map.has(obj, field)
```
Wrapper around Object.hasOwnProperty, useful for maps.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.meth'></a>Lapiz.Map.meth
```javascript
Lapiz.Map.meth(obj, namedFunc)
Lapiz.Map.meth(obj, name, function)
Lapiz.Map.meth(obj, namedFunc, bind)
Lapiz.Map.meth(obj, name, function, bind)
```
Attaches a method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.Map.meth(x, function foo(){...});
x.foo(); //calls foo
Lapiz.Map.meth(x, "bar", function(){...});
```
Providing a bind value will perminantly set the "this" value inside the
method.
```javascript
var x = Lapiz.Map();
x.name = "Test";
Lapiz.Map.meth(x, function foo(){
  console.log(this.name);
}, x);
var y = Lapiz.Map();
y.bar = x.foo;
y.bar(); // calls x.foo with this set to x
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.prop'></a>Lapiz.Map.prop
```javascript
Lapiz.Map.prop(obj, name, desc)
```
Just a wrapper around Object.defineProperty

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.setProperties'></a>Lapiz.Map.setProperties
```javascript
Lapiz.Map.setProperties(obj, attr, properties, values)
Lapiz.Map.setProperties(obj, attr, properties)
```
Defines properties on an object and puts the underlying value in the
attributes collection.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.setterFactory'></a>Lapiz.Map.setterFactory
```javascript
Lapiz.Map.setterFactory(self, attr, field, func)
Lapiz.Map.setterFactory(self, attr, field, func, callback)
```
Used in generating setters for objects or namespaces. It will create the
setterInterface which provides special controls to setters and call the
setter with the interface as "this". If setterInterface.set is true,
the returned value will be set in attr[field]. If callback is defined,
self will be passed into callback

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.setterGetter'></a>Lapiz.Map.setterGetter
```javascript
Lapiz.Map.setterGetter(obj, name, val, setterFunc, getterFunc)
Lapiz.Map.setterGetter(obj, name, val, setterFunc)
```
Creates a setter/getter property via a closure. A setter function is
required, if no getter is provided, the value will be returned. This is the
reason the method is named setterGetter rather than the more traditional
arrangement of "getterSetter" because the arguments are arranged so that
the first 4 are required and the last is optional.
```javascript
var x = Lapiz.Map();
Lapiz.Map.setterGetter(x, "foo", 12, function(i){return parseInt(i);});
console.log(x.foo); // will log 12 as an int
```
The value 'this' is always set to a special setterInterface for the setter
method. This can be used to cancel the set operation;
```javascript
var x = Lapiz.Map();
Lapiz.Map.setterGetter(x, "foo", 0, function(i){
  i = parseInt(i);
  this.set = !isNaN(i);
  return i;
});

x.foo = "12";
console.log(x.foo); // will log 12 as an int
x.foo = "hello";
console.log(x.foo); // value will still be 12

```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Map.setterMethod'></a>Lapiz.Map.setterMethod
```javascript
Lapiz.Map.setterMethod(obj, namedSetterFunc)
Lapiz.Map.setterMethod(obj, name, setterFunc)
Lapiz.Map.setterMethod(obj, namedSetterFunc, bind)
Lapiz.Map.setterMethod(obj, name, setterFunc, bind)
```
Attaches a setter method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.Map.meth(x, function foo(val){...});

//these two calls are equivalent
x.foo("bar");
x.foo = "bar";
```
If an object is supplied for bind, the "this" value will always be the bind
object, this can be useful if the method will be passed as a value.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.Namespace'></a>Lapiz.Namespace
```javascript
Lapiz.Namespace()
Lapiz.Namespace(constructor)
```
Returns a namespace. If a constructor is given, the inner namespace is
returned, otherwise the namespace wrapper is returned.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.each'></a>Lapiz.each
```javascript
Lapiz.each(collection, fn(val, key, collection))
```
Iterates over the collection, calling func(key, val) for each item in the
collection. If the collection is an array, key will be the index. If func
returns true (or an equivalent value) the Lapiz.each will return the
current key allowing each to act as a search.
```javascript
var arr = [3,1,4,1,5,9];
Lapiz.each(arr, function(val, key){
  console.log(key, val);
});
var gt4 = Lapiz.each(arr, function(val, key){return val > 4;});

var kv = {
  "A":"apple",
  "B":"banana",
  "C":"cantaloupe"
};
Lapiz.each(kv, function(val, key){
  console.log(key, val);
});
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.remove'></a>Lapiz.remove
```javascript
Lapiz.remove(arr, el, start)
Lapiz.remove(arr, el)
```
Removes the one instance of the given element from the array. If start is
not specified, it will be the first instance, otherwise it will be the
first instance at or after start.
```javascript
var arr = [3,1,4,1,5,9];
Lapiz.remove(arr,1);
console.log(arr); //[3,4,1,5,9]
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='lapizObject.properties_fire'></a>lapizObject.properties:fire
```javascript
lapizObject.properties:fire
```
setting this to false will prevent the fire event, but the value
will still be set to the return value

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='lapizObject.properties_setterInterface'></a>lapizObject.properties:setterInterface
```javascript
lapizObject.properties:setterInterface
```
The 'this' property of a setter will be the setter interface

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='lapizObject.properties_setterInterface.event'></a>lapizObject.properties:setterInterface.event
```javascript
lapizObject.properties:setterInterface.event(obj.pub, val, oldVal)
```
Attaching an event here will cause this event to be fired after the
set operation

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='lapizObject.properties_setterInterface.set'></a>lapizObject.properties:setterInterface.set
```javascript
lapizObject.properties:setterInterface.set
```
Setting this to false will prevent the set and event fire

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.attr'></a>namespace.attr
```javascript
namespace.attr
```
This is where the attributes for properties are stored.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.meth'></a>namespace.meth
```javascript
namespace.meth(namedFn)
namespace.meth(name, fn)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.namespace'></a>namespace.namespace
```javascript
namespace.namespace
```
The inner namespace is where all methods and properties are attached, the
outer wrapper holds the tools for attaching these.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.properties'></a>namespace.properties
```javascript
namespace.properties(props, vals)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.set'></a>namespace.set
```javascript
namespace.set(name, val)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='namespace.setterMethod'></a>namespace.setterMethod
```javascript
namespace.setterMethod(namedFn)
namespace.setterMethod(name, fn)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
