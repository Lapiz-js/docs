## components/ui/uiHelpers.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.UI.hash](#Lapiz.UI.hash)
* [Lapiz.UI.mediator.viewMethod](#Lapiz.UI.mediator.viewMethod)
* [attribute:blur](#attribute_blur)
* [attribute:change](#attribute_change)
* [attribute:click](#attribute_click)
* [attribute:display](#attribute_display)
* [attribute:if](#attribute_if)
* [attribute:live](#attribute_live)
* [attribute:q](#attribute_q)
* [attribute:repeat](#attribute_repeat)
* [attribute:resolver](#attribute_resolver)
* [attribute:selectVal](#attribute_selectVal)
* [attribute:submit](#attribute_submit)
* [attribute:view](#attribute_view)
* [mediator:form](#mediator_form)

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

### <a name='attribute_blur'></a>attribute:blur
```javascript
attribute:blur
<htmlNode blur="$ctxFn">...</htmlNode>
```
The given function will be called with the node loses focus.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_change'></a>attribute:change
```javascript
attribute:change
<htmlNode submit="$ctxFn">...</htmlNode>
```
The given function will be called when the change event fires.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_click'></a>attribute:click
```javascript
attribute:click
<htmlNode click="$ctxFn">...</htmlNode>
```
The given function will be called with the node is clicked.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_display'></a>attribute:display
```javascript
attribute:display
<htmlNode display="$ctxFn">...</htmlNode>
```
The given function will be called with the node is first displayed.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_if'></a>attribute:if
```javascript
attribute:if
<htmlNode if="$ctxVal">...</htmlNode>
```
If the attrVal ($ctxVal above) evaluates to false, the node and it's
children are removed. If the attribute is a function it will be invoked
with no arguments and the return value will be evaluated as a boolean

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_live'></a>attribute:live
```javascript
attribute:live
<htmlNode live>...</htmlNode>
<htmlNode live="$val">...</htmlNode>
```
If no attribute is used, it will default to the context.
When the .on.change event fires the template will be updated.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_q'></a>attribute:q
```javascript
attribute:q
```
Quick method for defining class, id and attributes

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_repeat'></a>attribute:repeat
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

### <a name='attribute_resolver'></a>attribute:resolver
```javascript
attribute:resolver
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_selectVal'></a>attribute:selectVal
```javascript
attribute:selectVal
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_submit'></a>attribute:submit
```javascript
attribute:submit
<htmlNode submit="$ctxFn">...</htmlNode>
```
The given function will be called when the submit event fires.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_view'></a>attribute:view
```javascript
attribute:view
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='mediator_form'></a>mediator:form
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
