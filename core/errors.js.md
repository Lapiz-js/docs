## core/errors.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Err](#Lapiz.Err)
  * [Lapiz.Err.logTo](#Lapiz.Err.logTo)
  * [Lapiz.Err.throw](#Lapiz.Err.throw)
* [Lapiz.on.error](#Lapiz.on.error)

### <a name='Lapiz.Err'></a>Lapiz.Err
```javascript
Lapiz.Err
```
Namespace for error handling.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Err.logTo'></a>Lapiz.Err.logTo
```javascript
Lapiz.Err.logTo = logger
```
The logger passed in must have logger.log method. It is meant to work with
the console object:
```javascript
Lapiz.Err.logTo = console
```
But a custom logger can also be used.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.Err.throw'></a>Lapiz.Err.throw
```javascript
Lapiz.Err.throw(Error)
Lapiz.Err.throw(errString)
```
Sends the event to any errHandlers, then throws the event. Note that the
error handlers cannot catch the error.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.on.error'></a>Lapiz.on.error
```javascript
Lapiz.on.error( errHandler(err) )
Lapiz.on.error = errHandler(err)
```
Register an error handler to listen for errors thrown with Lapiz.Err.throw

<sub><sup>[&uarr;Top](#__top)</sup></sub>
