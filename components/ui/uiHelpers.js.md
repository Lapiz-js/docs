## components/ui/uiHelpers.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.UI.hash](#Lapiz.UI.hash)
* [Lapiz.UI.mediator](#Lapiz.UI.mediator)
  * [Lapiz.UI.mediator.form](#Lapiz.UI.mediator.form)
  * [Lapiz.UI.mediator.viewMethod](#Lapiz.UI.mediator.viewMethod)
* [attribute:blur](#attribute_blur)
* [attribute:change](#attribute_change)
* [attribute:click](#attribute_click)
* [attribute:display](#attribute_display)
* [attribute:focus](#attribute_focus)
* [attribute:if](#attribute_if)
* [attribute:ifNot](#attribute_ifNot)
* [attribute:isChecked](#attribute_isChecked)
* [attribute:live](#attribute_live)
* [attribute:q](#attribute_q)
* [attribute:repeat](#attribute_repeat)
* [attribute:resolver](#attribute_resolver)
* [attribute:selectVal](#attribute_selectVal)
* [attribute:submit](#attribute_submit)
* [attribute:templator](#attribute_templator)
* [attribute:view](#attribute_view)
* [mediator:resolver](#mediator_resolver)
* [mediator:templator](#mediator_templator)

### <a name='Lapiz.UI.hash'></a>Lapiz.UI.hash
```javascript
Lapiz.UI.hash(hash, fn, ctx)
Lapiz.UI.hash(hash, renderString)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='Lapiz.UI.mediator'></a>Lapiz.UI.mediator
```javascript
Lapiz.UI.mediator
```
Mediators are a way to attach generic logic to a view.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.mediator.form'></a>Lapiz.UI.mediator.form
```javascript
Lapiz.UI.mediator.form("formHandler", fn(formData, formNode, ctx));
```
```javascript
  <form>
    <input ... name="someName" />
    <input ... name="someOtherName" parse="someParser" />
    ...
    <button click="form.formHandler">Go!</button>
  </form>
```
The form mediator will search up the node tree until it finds a form node.
All elements with a name will be added to the formData. If the type is
"checkbox" or "radio", a boolean will be added. For any other type a string
will be added based on n.value unless the tag has a "parse" attribute. If
it does have a parse attribute, that will be used to get a parser from
Lapiz.parse which will be used against the form value.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.mediator.viewMethod'></a>Lapiz.UI.mediator.viewMethod
```javascript
Lapiz.UI.mediator.viewMethod(viewMethodName, func(node, ctx, args...))
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

### <a name='attribute_focus'></a>attribute:focus
```javascript
attribute:focus
```
Causes this element to recieve focus when a view is rendered

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

### <a name='attribute_ifNot'></a>attribute:ifNot
```javascript
attribute:ifNot
<htmlNode ifNot="$ctxVal">...</htmlNode>
```
If the attrVal ($ctxVal above) evaluates to true, the node and it's
children are removed. If the attribute is a function it will be invoked
with no arguments and the return value will be evaluated as a boolean

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_isChecked'></a>attribute:isChecked
```javascript
attribute:isChecked
<htmlNode isChecked="$boolVal">...</htmlNode>
```
Will set the checked attribute. If combined with live, will keep the
checked status up to date.

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
<tag resolver="$resolver">...</tag>
```
Takes the current tokenizer and the tokenizer assigned and creates a new
templator that will be used on all attributes processed after this and all
child nodes. By default, resolver is the first attribute evaluated.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_selectVal'></a>attribute:selectVal
```javascript
attribute:selectVal
```
For a select box, it checks all the child select options and if it finds
one who's value property matches val, it sets it to selected.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_submit'></a>attribute:submit
```javascript
attribute:submit
<htmlNode submit="$ctxFn">...</htmlNode>
```
The given function will be called when the submit event fires.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_templator'></a>attribute:templator
```javascript
attribute:templator
<tag templator="$templator">...</tag>
```
Takes the current tokenizer and the tokenizer assigned and creates a new
templator that will be used on all attributes processed after this and all
child nodes. By default, templator is the second attribute evaluated only
after resolver.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_view'></a>attribute:view
```javascript
attribute:view
```
Renders a view. By default uses the current ctx.
```javascript
<tag click="view.foo">Foo</tag>
```

```javascript
Lapiz.UI.mediator.view("foo", "foo > #main");
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='mediator_resolver'></a>mediator:resolver
```javascript
mediator:resolver
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='mediator_templator'></a>mediator:templator
```javascript
mediator:templator
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
