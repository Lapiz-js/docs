## Lapiz/core/collectionsHelper.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.ArrayConverter](#Lapiz.ArrayConverter)
* [Lapiz.Map](#Lapiz.Map)
  * [Lapiz.Map.has](#Lapiz.Map.has)
* [Lapiz.argMap](#Lapiz.argMap)
* [Lapiz.each](#Lapiz.each)
* [Lapiz.getFnName](#Lapiz.getFnName)
* [Lapiz.remove](#Lapiz.remove)
* [Lapiz.set](#Lapiz.set)
  * [Lapiz.set.binder](#Lapiz.set.binder)
  * [Lapiz.set.copyProps](#Lapiz.set.copyProps)
  * [Lapiz.set.getter](#Lapiz.set.getter)
  * [Lapiz.set.getterFactory](#Lapiz.set.getterFactory)
  * [Lapiz.set.meth](#Lapiz.set.meth)
  * [Lapiz.set.prop](#Lapiz.set.prop)
  * [Lapiz.set.setProperties](#Lapiz.set.setProperties)
    * [Lapiz.set.setProperties:fire](#Lapiz.set.setProperties_fire)
    * [Lapiz.set.setProperties:setterInterface](#Lapiz.set.setProperties_setterInterface)
      * [Lapiz.set.setProperties:setterInterface.event](#Lapiz.set.setProperties_setterInterface.event)
      * [Lapiz.set.setProperties:setterInterface.self](#Lapiz.set.setProperties_setterInterface.self)
      * [Lapiz.set.setProperties:setterInterface.set](#Lapiz.set.setProperties_setterInterface.set)
  * [Lapiz.set.setterFactory](#Lapiz.set.setterFactory)
  * [Lapiz.set.setterGetter](#Lapiz.set.setterGetter)
  * [Lapiz.set.setterMethod](#Lapiz.set.setterMethod)
* [namespace](#namespace)
* [namespace](#namespace)
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
#### <a name='Lapiz.Map.has'></a>Lapiz.Map.has
```javascript
Lapiz.Map.has(obj, field)
```
Wrapper around Object.hasOwnProperty, useful for maps.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.argMap'></a>Lapiz.argMap
```javascript
Lapiz.argMap()
Lapiz.argMap(levels)
```
This is one of the few "magic methods" in Lapiz. When called from within a
function, it returns the arguments names and values as a map.
```javascript
function foo(x,y,z){
  var args = Lapiz.argMap();
  console.log(args);
}
foo('do','re','mi'); // logs {'x':'do', 'y':'re', 'z':'mi'}
```
Levels determines how many levels up the stack to go.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.each'></a>Lapiz.each
```javascript
Lapiz.each(collection, fn(val, key, collection))
```
Iterates over the collection, calling func(key, val, collection) for each
item in the collection. If the collection is an array, key will be the
index. If func returns true (or an equivalent value) the Lapiz.each will
return the current key allowing each to act as a search.
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
### <a name='Lapiz.getFnName'></a>Lapiz.getFnName
```javascript
Lapiz.getFnName(fn)
```
Returns the name of a function. Throws an error if the function is
anoymous. Also strips "bound" off the front of bound functions.

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
### <a name='Lapiz.set'></a>Lapiz.set
```javascript
Lapiz.set
```
Defined in init. This is used as a namespace for many helpers in setting
properties.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.binder'></a>Lapiz.set.binder
```javascript
Lapiz.set.binder(proto, namedFn)
Lapiz.set.binder(proto, name, fn)
```
Handles late binding for prototype methods
```javascript
var fooProto = {};
binder(fooProto, function sayHi(){
  console.log("Hi, " + this.name);
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
#### <a name='Lapiz.set.copyProps'></a>Lapiz.set.copyProps
```javascript
Lapiz.set.copyProps(copyTo, copyFrom, props...)
```
Copies the properties from the copyFrom object to the copyTo obj. The
properties should be strings. By default, the property will be copied with
basic assignment. If the property is preceeded by &, it will be copied by
reference.
```javascript
var A = {"x": 12, "y": "foo", z:[]};
var B = {};
Lapiz.set.copyProps(B, A, "x", "&y");
A.x = 314;
console.log(B.x); // 12
B.y = "Test";
console.log(A.y); // Test
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.getter'></a>Lapiz.set.getter
```javascript
Lapiz.set.getter(object, namedGetterFunc() )
Lapiz.set.getter(object, name, getterFunc() )
Lapiz.set.getter(object, [namedGetterFuncs...] )
Lapiz.set.getter(object, {name: getterFunc...} )
```
Attaches a getter method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
var ctr = 0;
Lapiz.set.getter(x, function foo(){
  var c = ctr;
  ctr +=1;
  return c;
});
console.log(x.foo); //0
console.log(x.foo); //1
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.getterFactory'></a>Lapiz.set.getterFactory
```javascript
Lapiz.set.getterFactory(attr, property)
Lapiz.set.getterFactory(attr, func)
```
Used in generating properties on an object or namespace.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.meth'></a>Lapiz.set.meth
```javascript
Lapiz.set.meth(obj, namedFunc)
Lapiz.set.meth(obj, name, function)
Lapiz.set.meth(obj, namedFunc, bind)
Lapiz.set.meth(obj, name, function, bind)
```
Attaches a method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.set.meth(x, function foo(){...});
x.foo(); //calls foo
Lapiz.set.meth(x, "bar", function(){...});
```
Providing a bind value will perminantly set the "this" value inside the
method.
```javascript
var x = Lapiz.Map();
x.name = "Test";
Lapiz.set.meth(x, function foo(){
  console.log(this.name);
}, x);
var y = Lapiz.Map();
y.bar = x.foo;
y.bar(); // calls x.foo with this set to x
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.prop'></a>Lapiz.set.prop
```javascript
Lapiz.set.prop(obj, name, desc)
```
Just a wrapper around Object.defineProperty

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.setProperties'></a>Lapiz.set.setProperties
```javascript
Lapiz.set.setProperties(obj, attr, properties, values, callback)
Lapiz.set.setProperties(obj, attr, properties, values)
Lapiz.set.setProperties(obj, attr, properties, callback)
Lapiz.set.setProperties(obj, attr, properties)
```
Defines properties on an object and puts the underlying value in the
attributes collection. If callback is defined, it will be called whenever
any of the setters is invoked.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.set.setProperties_fire'></a>Lapiz.set.setProperties:fire
```javascript
Lapiz.set.setProperties:fire
```
setting this to false will prevent the fire event, but the value
will still be set to the return value

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.set.setProperties_setterInterface'></a>Lapiz.set.setProperties:setterInterface
```javascript
Lapiz.set.setProperties:setterInterface
```
The 'this' property of a setter will be the setter interface
```javascript
var obj = $L.Map();
var attr = $L.Map();
$L.set.setProperties(obj, attr,{
  "*id": "int",
  "foo": function(val){
    // 'this' is not the setterInterface
    if (val === attr['foo']){
      // can suppress set and fire
      this.set = false;
    }
    if (val === "quite"){
      // can suppress fire (but will still set)
      this.fire = false;
    }
    if ($L.typeCheck.func(val)){
      // can set a callback that will invoked:
      // callback(obj, 'foo', val, oldVal)
      this.callback = val;
    }
  }
})
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
###### <a name='Lapiz.set.setProperties_setterInterface.event'></a>Lapiz.set.setProperties:setterInterface.event
```javascript
Lapiz.set.setProperties:setterInterface.event(obj.pub, val, oldVal)
```
Attaching an event here will cause this event to be fired after the
set operation

<sub><sup>[&uarr;Top](#__top)</sup></sub>
###### <a name='Lapiz.set.setProperties_setterInterface.self'></a>Lapiz.set.setProperties:setterInterface.self
```javascript
Lapiz.set.setProperties:setterInterface.self
```
A reference to the object on which the setting was defined

<sub><sup>[&uarr;Top](#__top)</sup></sub>
###### <a name='Lapiz.set.setProperties_setterInterface.set'></a>Lapiz.set.setProperties:setterInterface.set
```javascript
Lapiz.set.setProperties:setterInterface.set
```
Setting this to false will prevent the set and event fire

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.setterFactory'></a>Lapiz.set.setterFactory
```javascript
Lapiz.set.setterFactory(self, attr, field, func)
Lapiz.set.setterFactory(self, attr, field, func, callback)
```
Used in generating setters for objects or namespaces. It will create the
setterInterface which provides special controls to setters and call the
setter with the interface as "this". If setterInterface.set is true,
the returned value will be set in attr[field]. If callback is defined,
self will be passed into callback

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.set.setterGetter'></a>Lapiz.set.setterGetter
```javascript
Lapiz.set.setterGetter(obj, name, val, setterFunc, getterFunc)
Lapiz.set.setterGetter(obj, name, val, setterFunc)
```
Creates a setter/getter property via a closure. A setter function is
required, if no getter is provided, the value will be returned. This is the
reason the method is named setterGetter rather than the more traditional
arrangement of "getterSetter" because the arguments are arranged so that
the first 4 are required and the last is optional.
```javascript
var x = Lapiz.Map();
Lapiz.set.setterGetter(x, "foo", 12, function(i){return parseInt(i);});
console.log(x.foo); // will log 12 as an int
```
The value 'this' is always set to a special setterInterface for the setter
method. This can be used to cancel the set operation;
```javascript
var x = Lapiz.Map();
Lapiz.set.setterGetter(x, "foo", 0, function(i){
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
#### <a name='Lapiz.set.setterMethod'></a>Lapiz.set.setterMethod
```javascript
Lapiz.set.setterMethod(obj, namedSetterFunc)
Lapiz.set.setterMethod(obj, name, setterFunc)
Lapiz.set.setterMethod(obj, namedSetterFunc, bind)
Lapiz.set.setterMethod(obj, name, setterFunc, bind)
```
Attaches a setter method to an object. The method must be a named function.
```javascript
var x = Lapiz.Map();
Lapiz.set.meth(x, function foo(val){...});

//these two calls are equivalent
x.foo("bar");
x.foo = "bar";
```
If an object is supplied for bind, the "this" value will always be the bind
object, this can be useful if the method will be passed as a value.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='namespace'></a>namespace
```javascript
namespace = Lapiz.Namespace()
namespace = Lapiz.Namespace(constructor)
```
Returns a namespace. If a constructor is given, the inner namespace is
returned, otherwise the namespace wrapper is returned.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='namespace'></a>namespace
```javascript
namespace
```
The "this" object on a Namespace constructor.
```javascript
var foo = Lapiz.Namespace(function(){
  this.properties(...);
  this.meth(...);
  this.set(...);
  // and so forth
});
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.attr'></a>namespace.attr
```javascript
namespace.attr
```
This is where the attributes for properties are stored.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.meth'></a>namespace.meth
```javascript
namespace.meth(namedFn)
namespace.meth(name, fn)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.namespace'></a>namespace.namespace
```javascript
namespace.namespace
```
The inner namespace is where all methods and properties are attached, the
outer wrapper holds the tools for attaching these.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.properties'></a>namespace.properties
```javascript
namespace.properties(props, vals)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.set'></a>namespace.set
```javascript
namespace.set(name, val)
```
Sets the value as a property on the namespace.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='namespace.setterMethod'></a>namespace.setterMethod
```javascript
namespace.setterMethod(namedFn)
namespace.setterMethod(name, fn)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>