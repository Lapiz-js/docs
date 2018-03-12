## Lapiz/core/dependency.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Dependency](#Lapiz.Dependency)
  * [Lapiz.Dependency.Factory](#Lapiz.Dependency.Factory)
  * [Lapiz.Dependency.Reference](#Lapiz.Dependency.Reference)
  * [Lapiz.Dependency.Service](#Lapiz.Dependency.Service)
  * [Lapiz.Dependency.has](#Lapiz.Dependency.has)
  * [Lapiz.Dependency.remove](#Lapiz.Dependency.remove)

### <a name='Lapiz.Dependency'></a>Lapiz.Dependency
```javascript
Lapiz.Dependency(name)
```
Returns the dependency associated with name

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Dependency.Factory'></a>Lapiz.Dependency.Factory
```javascript
Lapiz.Dependency.Factory(name, fn)
```
Factory is the most direct of the dependency registrations, it registers
the function directly

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Dependency.Reference'></a>Lapiz.Dependency.Reference
```javascript
Lapiz.Dependency.Reference(name, resource)
```
Wraps the resource in a closure function so that calling
```javascript
Lapiz.Dependency(name)
```
will return the resource.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Dependency.Service'></a>Lapiz.Dependency.Service
```javascript
Lapiz.Dependency.Service(name, constructor)
```
Service will register the constructor in manor so that calling
```javascript
Lapiz.Dependency(name)(args...)
```
on a service is the same as calling
```javascript
new constructor(args...)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Dependency.has'></a>Lapiz.Dependency.has
```javascript
Lapiz.Dependency.has(name)
```
Returns a boolean indicating if there is a resource registered corresonding
to name.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Dependency.remove'></a>Lapiz.Dependency.remove
```javascript
Lapiz.Dependency.remove(name)
```
Removes a dependency

<sub><sup>[&uarr;Top](#__top)</sup></sub>