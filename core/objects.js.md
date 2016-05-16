## core/objects.js

* [Lapiz.Class](#Lapiz.Class)
* [Lapiz.Object](#Lapiz.Object)
* [Lapiz.argDict](#Lapiz.argDict)
* [Lapiz.on.class](#Lapiz.on.class)
* [object.attr](#object.attr)
* [object.event](#object.event)
* [object.fire](#object.fire)
* [object.getter](#object.getter)
* [object.method](#object.method)
* [object.properties](#object.properties)
* [object.pub](#object.pub)
* [object.pub.on](#object.pub.on)
* [object.pub.on.change](#object.pub.on.change)
* [object.pub.on.delete](#object.pub.on.delete)
* [object.setMany](#object.setMany)
### <a name='Lapiz.Class'></a>Lapiz.Class
```javascript
Lapiz.Class(constructor)
Lapiz.Class(constructor, useCustom)
```

### <a name='Lapiz.Object'></a>Lapiz.Object
```javascript
Lapiz.Object();
Lapiz.Object(constructor);
```

### <a name='Lapiz.argDict'></a>Lapiz.argDict
```javascript
Lapiz.argDict()
```
This is one of the few "magic methods" in Lapiz. When called from within a
function, it returns the arguments names and values as a key/value object.
The name is a little misleading, the result is a JavaScript object, not a
Lapiz.Dictionary.
```javascript
function foo(x,y,z){
  var args = Lapiz.argDict();
  console.log(args);
}
foo('do','re','mi'); // logs {'x':'do', 'y':'re', 'z':'mi'}
```

### <a name='Lapiz.on.class'></a>Lapiz.on.class
```javascript
Lapiz.on.class(fn)
Lapiz.on.class = fn
```
Event registration, event will fire whenever a new Lapiz class is defined.

### <a name='object.attr'></a>object.attr
```javascript
object.attr
```
Namespace for attribute values

### <a name='object.event'></a>object.event
```javascript
object.event(name)
```
Creates an event and places the registration method in object.pub.on and
the fire method in object.fire
```javascript
var obj = Lapiz.Object();
obj.event("foo");
obj.pub.on.foo = function(val){ console.log(val);};
obj.fire.foo("bar"); // this will fire foo logging "bar" to the console
```

### <a name='object.fire'></a>object.fire
```javascript
object.fire
```
Namespace for event fire methods

### <a name='object.getter'></a>object.getter
```javascript
object.getter(getterFn)
```
Creates a getter property in the public namespace.

### <a name='object.method'></a>object.method
```javascript
object.method(fn)
```
Creates a method in the public namespace.

### <a name='object.properties'></a>object.properties
```javascript
object.properties(properties)
object.properties(properties, values)
```

### <a name='object.pub'></a>object.pub
```javascript
object.pub
```
The public namespace on the object

### <a name='object.pub.on'></a>object.pub.on
```javascript
object.pub.on
```
Namespace for event registrations

### <a name='object.pub.on.change'></a>object.pub.on.change
```javascript
object.pub.on.change
object.fire.change
```
The change event will fire when ever a property is set.

### <a name='object.pub.on.delete'></a>object.pub.on.delete
```javascript
object.pub.on.delete
object.fire.delete
```
The delete event should be fired if the object is going to be deleted.

### <a name='object.setMany'></a>object.setMany
```javascript
object.setMany(collection)
```
Takes a key/value collection (generally a JavaScript object) and sets
any properties that match the keys.

