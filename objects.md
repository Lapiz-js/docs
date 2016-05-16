## Objects and Classes

Lapiz supports objects and classes that are event driven. This means that we can listen for new objects of a specific class or when specific objects change or are deleted.

[Home](./index.md)
* [Lapiz.Event()](#event)

### Lapiz.argDict()
This is one of the few "magic methods" in Lapiz. When called from within a function, it returns the arguments names and values as a key/value object. The name is a little misleading, the result is a JavaScript object, not a Lapiz.Dictionary.

```javascript
function foo(x,y,z){
  var args = Lapiz.argDict();
  console.log(args);
}
foo('do','re','mi'); // logs {'x':'do', 'y':'re', 'z':'mi'}
```

### Lapiz.Object(constructor)
Creates a Lapiz object. A Lapiz object is a structure that supports public and private methods and attributes, properties, methods and events. If a constructor function is provided, it will be invoked with the "this" value set to the object.

```javascript
var obj1 = Lapiz.Object();
objs1.foo = "bar";

var obj2 = Lapiz.Object(function(){
  this.foo = "bar";
});
```

#### Object Structure
A Lapiz object is considered to be it's own 'private' namespace. Within that structure is 'pub', the public namespace.

* pub: public namespace
  * on: event registration namespace
    * change: registration method for the object change event
    * delete: registration method for the object delete event
* properties(props, values): create properties in pub
* attr: namespace for property attributes
* event(name): creates an event, adds register to pub.on and fire to fire
* fire: event fire namespace
  * change: fire method for the object change event
  * delete: fire method for the object delete event
* setMany(vals): takes a javascript object as a key/val pair and assignes any properties that match the keys
* getter(fn): creates a getter method in pub
* method(fn): creates a method in pub

#### Example Code
```javascript
var Foo = Lapiz.Object(function(){
  this.properties({
    "id": "int",
    "name": "string",
  },{
    "id": 12,
    "name": "Adam"
  });

  var self = this.pub;
  this.method(function sayHi(){
    console.log("Hi, " + self.name);
  });
}).pub;

Foo.sayHi(); // logs "Hi, Adam"
Foo.on.change(function(x){
  console.log(x.id);
});
Foo.id = "25.5"; // sets id to 25 and fires Foo change event, logging 25 to the console
Foo.name = "Bob"; // also fires the change event, logging 25 to the console
Foo.sayHi(); // logs "Hi, Bob"
```

#### object.properties(props, values)
Properties are one of the key features to Lapiz objects. A property has a setter function and generally a getter function too. There is a corresponding attribute in attr. And when the property is set, the object change event is fired.
```javascript
var Foo = Lapiz.Object(function(){
  this.properties({
    "name": "string",
  },{
    "name": "Adam"
  });
}).pub;
console.log(Foo.name); //Adam

//similar construction done manually
var Bar = {};
Bar.pub = {}
Bar.attr = {
  "name": "Adam",
};
var change = Lapiz.Event();
Bar.pub.on = {
  "change": change.register
};
Bar.fire = {
  "change": change.fire
};
Object.defineProperty(Bar.pub, "name", {
  "get": function(){
    return Bar.attr.name;
  },
  "set": function(val){
    Bar.attr.name = Lapiz.parse.string(val);
    Bar.fire.change(Bar);
  }
});
console.log(Bar.pub.name); //Adam
```

The properties are defined as a set of key value pairs. The value can be a function which will be used as the setter and the getter will just return the attribute value. The value can be a string, in which case the function from Lapiz.parse with that name will be used. The "get" and "set" properties can also be defined manually.
```javascript
var Foo = Lapiz.Object(function(){
  var self = this;
  this.properties({
    "name": "string",
    "id": function(val){
      return Math.abs(Lapiz.parse.int(val));
    }
    "active":{
      "get": function(){
        return (self.attr.active) ? "T" : "F";
      },
      "set": function(val){
        if (val === "toggle"){
          return !self.attr.active;
        }
        return Lapiz.parse.bool(val);
      }
    },
    "setOnly":{
      "set": "int",
      "get": null
    }
  });
});
```

### Lapiz.Class(constructor, customObj)
Generally developers will not directly instanciate Lapiz Objects, but will define a Lapiz class.

```javascript
var Person = Lapiz.Class(function(id, name, active){
  this.properties({
    "id": "int",
    "name": "string",
    "active": "bool"
  }, Lapiz.argDict());
  return this.pub;
});

Person.on.create(function(person){
  console.log(person.name);
});
var adam = Person(1, "Adam", true); // logs "Adam" to console
var stephen = Person(2, "Stephen", false); // logs "Stephen" to console
var lauren = Person(3, "Lauren", true); // logs "Lauren" to console
```