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
Used to define a class. Lapiz.on.class will fire everytime a new class
is created. The returned constructor will also have an on.create method
that will fire everytime a new instance is created.
```javascript
var Person = Lapiz.Class(function(id, name, role, active){
  this.properties({
    "id": "int",
    "name": "string",
    "role": "string",
    "active": "bool"
  }, Lapiz.argDict());
  return this.pub;
});
Person.on.create(function(person){
  console.log(person.name);
});
var adam = Person(12, "Adam", "admin", true); //will fire create event and log "Adam"
```
If the constructor doesn't return anything, the Lapiz object that was
passed in as 'this' will be will be returned as the contructed object.
If the constructor does return a value, that will be used. As in the
example above, returning the public namespace is a common technique.

If the second argument is 'true', a Lapiz object will not be set to 'this',
instead it will be set to what whatever the calling scope is.

### <a name='Lapiz.Object'></a>Lapiz.Object
```javascript
Lapiz.Object();
Lapiz.Object(constructor);
```
Creates a Lapiz Object, a structure per-wired for adding events, properties
and methods. If a constructor is supplied, it will be invoked with 'this' set
to the object.
```javascript
var obj = Lapiz.Object();
obj.properties({
  "name": "string"
});
obj = obj.pub;
obj.name = "test";

var obj2 = Lapiz.Object(function(){
  this.properties({
    "name": "string"
  });
}).pub;
obj2.name = "test 2";
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
```javascript
var obj = Lapiz.Object(function(){
  this.properties({
    "name": "string"
  });
});
obj.pub.name = "test";
console.log(obj.attr.name); // test
obj.attr.name = "bar";
console.log(obj.pub.name); // test
```

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
The properties method is used to attach getter/setter properties to the public
namespace. The attribute that underlies the getter/setter will be attached to
object.attr.

If a setter is defined and no getter is defined, a getter will be generated
that returns the attribute value. If a function is given, that will be used as
the setter, if a string is provided, that will be used to get a setter from
Lapiz.parse.
```javascript
var obj = Lapiz.Object(function(){
  var self = this;
  this.properties({
    "name": "string", // this will use Lapiz.parse.string
    "foo": function(val){
      // this will be the setter for foo
      return parseInt("1"+val);
    },
    "bar": {
      "set": "int",
      "get": function(){
        return "== "+self.attr.bar+" ==";
      }
    },
    "glorp":{
      "set": "bool",
      "get": null, //makes this a set only property
    }
  });
});
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
```javascript
var obj = Lapiz.Object(function(){
  this.properties({
    "id": "int",
    "name": "string",
    "role": "string"
  });
});
obj.setMany({
  "id":12,
  "role": "admin"
});
```
Another technique is to attach setMany to the public interface
```javascript
var obj = Lapiz.Object(function(){
  this.properties({
    "id": "int",
    "name": "string",
    "role": "string"
  });
  this.method(this.setMany);
}).pub;
obj.setMany({
  "id":12,
  "role": "admin"
});
```

