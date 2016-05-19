## components/ui/uiHelpers.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.UI.hash](#Lapiz.UI.hash)
* [Lapiz.UI.mediator.viewMethod](#Lapiz.UI.mediator.viewMethod)
* [attribute:blur](#attribute:blur)
* [attribute:change](#attribute:change)
* [attribute:click](#attribute:click)
* [attribute:display](#attribute:display)
* [attribute:if](#attribute:if)
* [attribute:live](#attribute:live)
* [attribute:q](#attribute:q)
* [attribute:repeat](#attribute:repeat)
* [attribute:resolver](#attribute:resolver)
* [attribute:selectVal](#attribute:selectVal)
* [attribute:submit](#attribute:submit)
* [attribute:view](#attribute:view)
* [mediator:form](#mediator:form)

### <a name='Lapiz.UI.hash'></a>Lapiz.UI.hash
```javascript
Lapiz.UI.hash(hash, fn, ctx)
Lapiz.UI.hash(hash, renderString)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.UI.mediator.viewMethod'></a>Lapiz.UI.mediator.viewMethod
```javascript
Lapiz.UI.mediator.viewMethod
```
Useful mediator for attaching generic methods available to views.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:blur'></a>attribute:blur
```javascript
attribute:blur
<htmlNode blur="$ctxFn">...</htmlNode>
```
The given function will be called with the node loses focus.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:change'></a>attribute:change
```javascript
attribute:change
<htmlNode submit="$ctxFn">...</htmlNode>
```
The given function will be called when the change event fires.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:click'></a>attribute:click
```javascript
attribute:click
<htmlNode click="$ctxFn">...</htmlNode>
```
The given function will be called with the node is clicked.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:display'></a>attribute:display
```javascript
attribute:display
<htmlNode display="$ctxFn">...</htmlNode>
```
The given function will be called with the node is first displayed.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:if'></a>attribute:if
```javascript
attribute:if
<htmlNode if="$ctxVal">...</htmlNode>
```
If the attrVal ($ctxVal above) evaluates to false, the node and it's
children are removed. If the attribute is a function it will be invoked
with no arguments and the return value will be evaluated as a boolean

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:live'></a>attribute:live
```javascript
attribute:live
<htmlNode live>...</htmlNode>
<htmlNode live="$val">...</htmlNode>
```
If no attribute is used, it will default to the context.
When the .on.change event fires the template will be updated.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:q'></a>attribute:q
```javascript
attribute:q
```
Quick method for defining class, id and attributes

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:repeat'></a>attribute:repeat
```javascript
attribute:repeat
```
Takes a collection (array, map or accessor) and repeats the node for every
item in the collection.
```javascript
<ul>
  <li repeat="$people>$name</li>
</ul>
```
If the collection has Lapiz event wiring (an accessor such as a Dictionary)
the collection will automatically stay up to date with additions and
removals. To keep thecontents up to date, also use live.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:resolver'></a>attribute:resolver
```javascript
attribute:resolver
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:selectVal'></a>attribute:selectVal
```javascript
attribute:selectVal
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:submit'></a>attribute:submit
```javascript
attribute:submit
<htmlNode submit="$ctxFn">...</htmlNode>
```
The given function will be called when the submit event fires.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute:view'></a>attribute:view
```javascript
attribute:view
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='mediator:form'></a>mediator:form
```javascript
mediator:form
```
```javascript
  <form>
    ...
    <button click="form.formHandler">Go!</button>
  </form>
```
```javascript
Lapiz.UI.mediator.form("formHandler", fn(formData));
```
The form mediator will search up the node tree until it finds
a form node. All elements with a name will be added to the
formData.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
