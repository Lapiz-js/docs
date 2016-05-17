## core/dependency.js<a name="__top"></a><span style="float:right; font-size:60%">[Home](index.md)</sub>

* [Lapiz.Dependency](#Lapiz.Dependency)
  * [Lapiz.Dependency.Factory](#Lapiz.Dependency.Factory)
  * [Lapiz.Dependency.Reference](#Lapiz.Dependency.Reference)
  * [Lapiz.Dependency.Service](#Lapiz.Dependency.Service)
  * [Lapiz.Dependency.has](#Lapiz.Dependency.has)
  * [Lapiz.Dependency.remove](#Lapiz.Dependency.remove)

### <a name='Lapiz.Dependency'></a>Lapiz.Dependency <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dependency(name)
```
Returns the dependency associated with name

#### <a name='Lapiz.Dependency.Factory'></a>Lapiz.Dependency.Factory <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dependency.Factory(name, fn)
```
Factory is the most direct of the dependency registrations, it registers
the function directly

#### <a name='Lapiz.Dependency.Reference'></a>Lapiz.Dependency.Reference <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dependency.Reference(name, resource)
```
Wraps the resource in a closure function so that calling
```javascript
Lapiz.Dependency(name)
```
will return the resource.

#### <a name='Lapiz.Dependency.Service'></a>Lapiz.Dependency.Service <span style="float:right; font-size:60%">[Top](#__top)</sub>
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

#### <a name='Lapiz.Dependency.has'></a>Lapiz.Dependency.has <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dependency.has(name)
```
Returns a boolean indicating if there is a resource registered corresonding
to name.

#### <a name='Lapiz.Dependency.remove'></a>Lapiz.Dependency.remove <span style="float:right; font-size:60%">[Top](#__top)</sub>
```javascript
Lapiz.Dependency.remove(name)
```
Removes a dependency
