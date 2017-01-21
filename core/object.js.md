## core/object.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.on.Cls](#Lapiz.on.Cls)
* [classDef](#classDef)
  * [classDef.constructor](#classDef.constructor)
  * [classDef.meth](#classDef.meth)
  * [classDef.properties](#classDef.properties)
* [obj2](#obj2)
  * [obj2.attr](#obj2.attr)
  * [obj2.event](#obj2.event)
  * [obj2.fire](#obj2.fire)
    * [obj2.fire.change](#obj2.fire.change)
    * [obj2.fire.delete](#obj2.fire.delete)
  * [obj2.meth](#obj2.meth)
  * [obj2.properties](#obj2.properties)
  * [obj2.pub](#obj2.pub)
    * [obj2.pub.on](#obj2.pub.on)
      * [obj2.pub.on.change](#obj2.pub.on.change)
      * [obj2.pub.on.delete](#obj2.pub.on.delete)
  * [obj2.setMany](#obj2.setMany)

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

#### <a name='classDef.meth'></a>classDef.meth
```javascript
classDef.meth(namedFn)
classDef.meth(name, fn)
```
Defines the constructor for a class

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='classDef.properties'></a>classDef.properties
```javascript
classDef.properties(props, vals)
```
Defines properties on a class

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='obj2'></a>obj2
```javascript
obj2 = Lapiz.Obj(proto)
```
Returns a Lapiz Object. The returned value is the private scope. The
prototype that is passed in will be attached to the public scope.
Generally, Obj should not be invoked directly, but through Cls.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.attr'></a>obj2.attr
```javascript
obj2.attr  
```
A map holding the private attribute scope of an object. This is where the
underlying values for properties are stored.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.event'></a>obj2.event
```javascript
obj2.event(name)
```
Creates an event on an object. It automatically wires it up so that the
register function is obj.pub.on[name] and the fire event is obj.fire[name].

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.fire'></a>obj2.fire
```javascript
obj2.fire
```
A map holding the fire controls for the object events.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj2.fire.change'></a>obj2.fire.change
```javascript
obj2.fire.change
```
Fires the change event. It will automatically fire when properties
change.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj2.fire.delete'></a>obj2.fire.delete
```javascript
obj2.fire.delete
```
This should be called if you want to remove an object. It is build in,
but nothing is wired up to fire it automatically. It is your
responsibility to call it when you want the object deleted

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.meth'></a>obj2.meth
```javascript
obj2.meth(obj, namedFunc)
obj2.meth(obj, name, function)
```
Sets properties on the public scopes and stores the attributes in
priv.attr.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.properties'></a>obj2.properties
```javascript
obj2.properties(props, vals)
```
Sets properties on the public scopes and stores the attributes in
priv.attr.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.pub'></a>obj2.pub
```javascript
obj2.pub
```
The public scope of a Lapiz Object. All the properties will be exposed
here as well as any public methods.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='obj2.pub.on'></a>obj2.pub.on
```javascript
obj2.pub.on
```
A map holding the register methods for object event listeners.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

###### <a name='obj2.pub.on.change'></a>obj2.pub.on.change
```javascript
obj2.pub.on.change
```
Fires when the object's properties change

<sub><sup>[&uarr;Top](#__top)</sup></sub>

###### <a name='obj2.pub.on.delete'></a>obj2.pub.on.delete
```javascript
obj2.pub.on.delete
```
Fires when an object is being deleted. If you are holding a collection of
objects, you should remove the object when this fires to prevent memory
leaks or holding onto objects that are considered dead.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='obj2.setMany'></a>obj2.setMany
```javascript
obj2.setMany(props)
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
