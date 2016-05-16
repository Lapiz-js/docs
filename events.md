## Events

Events rely on the [Observer Pattern](https://en.wikipedia.org/wiki/Observer_pattern) and are at the heart of many Lapiz features.

[Home](./index.md)
* [Lapiz.Event()](#event)
  * [Event Structure](#structure)
  * [event.register(fn)](#register)
  * [event.register.deregister(fn)](#deregister)
  * [event.fire(args...)](#fire)
  * [event.enabled](#enabled)
  * [event.length](#length)
* [Lapiz.SingleEvent()](#singleEvent)
* [Lapiz.Event.linkProperty(obj, name, evt)](#linkProperty)


### <a name="event"></a> Lapiz.Event()

```javascript
var event = Lapiz.Event();
e.register(function(val){
  console.log(val);
});
var fn2 = function(val){
  alert(val);
};
e.register = fn2;
e.fire("Test 1"); //will log "Test 1" to the console and pop up an alert
e.register.deregister(fn2);
e.fire("Test 2"); //will log "Test 2" to the console
```

#### <a name="structure"></a> Event Structure
* register
  * deregister
* fire
  * enabled
  * length

It is useful to think of register as the public portion and fire as the private portion.

#### <a name="register"></a> event.register(fn)
The event.register method takes a function. All registered functions will be called when the event fires.

#### <a name="deregister"></a> event.register.deregister(fn)
The event.register.deregister method takes a function. If that function has been registered with the event, it will be removed.

#### <a name="fire"></a> event.fire(args...)
The event.fire method will call all functions that have been registered with the event. The arguments that are passed into fire will be passed into the registered functions.

#### <a name="enabled"></a> event.enabled
The event.enabled is a boolean that can be set to enable or disable the fire method. If event.fire.enable is false, even if event.fire is called, it will not call the registered functions.

#### <a name="length"></a> event.length
The event.length is a read-only property that returns the number of functions registered with the event.

### <a name="singleEvent"></a> Lapiz.SingleEvent()
A single event is an instance that will only fire once. Registering a function after the event has fired will result in the function being immedatly invoked with the arguments that were used when the event fired.

### <a name="linkProperty"></a> Lapiz.Event.linkProperty(obj, name, evt)
This is a helper function for linking an event to an object. It will be linked like a setter method:
```js
var e = Lapiz.Event();
var map = Lapiz.Map();
Lapiz.Event.linkProperty(map, "foo", e);
// These two are the same
map.foo(function(){...});
map.foo = function(){...};

// To deregister
map.foo.deregister(fn);
```