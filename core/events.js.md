## core/events.js<a name="__top"></a><span style="float:right; font-size:60%">[Home](index.md)</sub>

* [Lapiz.Event](#Lapiz.Event)
  * [Lapiz.Event.linkProperty](#Lapiz.Event.linkProperty)
* [Lapiz.SingleEvent](#Lapiz.SingleEvent)
* [event.fire](#event.fire)
  * [event.fire.enabled](#event.fire.enabled)
  * [event.fire.length](#event.fire.length)
* [event.register](#event.register)
  * [event.register.deregister](#event.register.deregister)
* [singleEvent.fire](#singleEvent.fire)
  * [singleEvent.fire.enabled](#singleEvent.fire.enabled)
* [singleEvent.register](#singleEvent.register)
  * [singleEvent.register.deregister](#singleEvent.register.deregister)

### <a name='Lapiz.Event'></a>Lapiz.Event <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Event()
```
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

#### <a name='Lapiz.Event.linkProperty'></a>Lapiz.Event.linkProperty <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Event.linkProperty(obj, name, evt)
```
This is a helper function for linking an event to an object. It will be
linked like a setter method:
```javascript
var e = Lapiz.Event();
var map = Lapiz.Map();
Lapiz.Event.linkProperty(map, "foo", e);
// These two are the same
map.foo(function(){...});
map.foo = function(){...};

// To deregister
map.foo.deregister(fn);
```

### <a name='Lapiz.SingleEvent'></a>Lapiz.SingleEvent <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.SingleEvent()
```
A single event is an instance that will only fire once. Registering a
function after the event has fired will result in the function being
immedatly invoked with the arguments that were used when the event fired.

### <a name='event.fire'></a>event.fire <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
event.fire(args...)
```
The event.fire method will call all functions that have been registered
with the event. The arguments that are passed into fire will be passed
into the registered functions.

#### <a name='event.fire.enabled'></a>event.fire.enabled <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
event.fire.enabled
event.fire.enabled = x
```
The event.enabled is a boolean that can be set to enable or disable the
fire method. If event.fire.enable is false, even if event.fire is called,
it will not call the registered functions.

#### <a name='event.fire.length'></a>event.fire.length <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
event.fire.length
```
The event.length is a read-only property that returns the number of
functions registered with the event.

### <a name='event.register'></a>event.register <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
event.register(fn)
event.register = fn
```
The event.register method takes a function. All registered functions will
be called when the event fires.

#### <a name='event.register.deregister'></a>event.register.deregister <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
event.register.deregister(fn)
event.register.deregister = fn
```
The event.register.deregister method takes a function. If that function
has been registered with the event, it will be removed.

### <a name='singleEvent.fire'></a>singleEvent.fire <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
singleEvent.fire
```

#### <a name='singleEvent.fire.enabled'></a>singleEvent.fire.enabled <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
singleEvent.fire.enabled
```

### <a name='singleEvent.register'></a>singleEvent.register <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
singleEvent.register
```

#### <a name='singleEvent.register.deregister'></a>singleEvent.register.deregister <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
singleEvent.register.deregister
```
