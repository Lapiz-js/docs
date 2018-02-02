## core/object.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Cls](#Lapiz.Cls)
* [Lapiz.on.Cls](#Lapiz.on.Cls)
* [classDef](#classDef)
  * [classDef.constructor](#classDef.constructor)
  * [classDef.getter](#classDef.getter)
  * [classDef.meth](#classDef.meth)
  * [classDef.properties](#classDef.properties)
* [obj](#obj)
  * [obj.attr](#obj.attr)
  * [obj.event](#obj.event)
  * [obj.fire](#obj.fire)
    * [obj.fire.change](#obj.fire.change)
    * [obj.fire.remove](#obj.fire.remove)
  * [obj.meth](#obj.meth)
  * [obj.properties](#obj.properties)
  * [obj.pub](#obj.pub)
    * [obj.pub.on](#obj.pub.on)
      * [obj.pub.on.change](#obj.pub.on.change)
      * [obj.pub.on.remove](#obj.pub.on.remove)
  * [obj.setMany](#obj.setMany)

### <a name='Lapiz.Cls'></a>Lapiz.Cls
```javascript
Lapiz.Cls( fn(classDef) )
```
Used to define a Lapiz Class. The function passed in will receive a
classDef object as both the 'this' object as well as the first argument.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.on.Cls'></a>Lapiz.on.Cls
```javascript
Lapiz.on.Cls(fn)
Lapiz.on.Cls = fn
```
Event registration, event will fire whenever a new Lapiz class is defined.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='classDef'></a>classDef
```javascript
classDef
```
A class definition is the object used to define a Lapiz Class.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='classDef.constructor'></a>classDef.constructor
```javascript
classDef.constructor(constructor)
```
Defines the constructor for a class.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='classDef.getter'></a>classDef.getter
```javascript
classDef.getter(namedFn)
classDef.getter(name, fn)
```
Defines a getter on the class. Getter are late-bound:

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='classDef.meth'></a>classDef.meth
```javascript
classDef.meth(namedFn)
classDef.meth(name, fn)
```
Defines a method on the class. Methods are late-bound:
```javascript
  var Person = Lapiz.Cls(function(cls){
    cls.meth(function foo(){
      return "FOO"+this.pub.name;
    });
  });

  var adam = Person();
  adam.name = "Adam";
  adam.foo(); // returns "FOOAdam"
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='classDef.properties'></a>classDef.properties
```javascript
classDef.properties(props, vals)
```
Defines properties on a class

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='obj'></a>obj
```javascript
obj = Lapiz.Obj(proto)
```
Returns a Lapiz Object. The returned value is the private scope. The
prototype that is passed in will be attached to the public scope.
Generally, Obj should not be invoked directly, but through Cls.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.attr'></a>obj.attr
```javascript
obj.attr  
```
A map holding the private attribute scope of an object. This is where the
underlying values for properties are stored.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.event'></a>obj.event
```javascript
obj.event(name)
```
Creates an event on an object. It automatically wires it up so that the
register function is obj.pub.on[name] and the fire event is obj.fire[name].

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.fire'></a>obj.fire
```javascript
obj.fire
```
A map holding the fire controls for the object events.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj.fire.change'></a>obj.fire.change
```javascript
obj.fire.change
```
Fires the change event. It will automatically fire when properties
change.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj.fire.remove'></a>obj.fire.remove
```javascript
obj.fire.remove
```
This should be called if you want to remove an object. It is build in,
but nothing is wired up to fire it automatically. It is your
responsibility to call it when you want the object deleted

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.meth'></a>obj.meth
```javascript
obj.meth(obj, namedFunc)
obj.meth(obj, name, function)
```
Sets properties on the public scopes and stores the attributes in
priv.attr.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.properties'></a>obj.properties
```javascript
obj.properties(props, vals)
```
Sets properties on the public scopes and stores the attributes in
priv.attr.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.pub'></a>obj.pub
```javascript
obj.pub
```
The public scope of a Lapiz Object. All the properties will be exposed
here as well as any public methods.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj.pub.on'></a>obj.pub.on
```javascript
obj.pub.on
```
A map holding the register methods for object event listeners.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

###### <a name='obj.pub.on.change'></a>obj.pub.on.change
```javascript
obj.pub.on.change
```
Fires when the object's properties change

<sub><sup>[&uarr;Top](#__top)</sup></sub>

###### <a name='obj.pub.on.remove'></a>obj.pub.on.remove
```javascript
obj.pub.on.remove
```
Fires when an object is being deleted. If you are holding a collection of
objects, you should remove the object when this fires to prevent memory
leaks or holding onto objects that are considered dead.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj.setMany'></a>obj.setMany
```javascript
obj.setMany(props)
```
Takes a key/value collection (generally a Map or a JavaScript object) and
sets those properties in the object.
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
  this.meth(this.setMany);
}).pub;
obj.setMany({
  "id":12,
  "role": "admin"
});
```
After setMany is done, the change event will fire once and array of all
the keys that were changed will be passed in.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
