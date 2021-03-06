## Lapiz/components/ui/uiHelpers.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.UI.hash](#Lapiz.UI.hash)
* [Lapiz.UI.mediator](#Lapiz.UI.mediator)
  * [Lapiz.UI.mediator.form](#Lapiz.UI.mediator.form)
  * [Lapiz.UI.mediator.viewMethod](#Lapiz.UI.mediator.viewMethod)
* [attribute:blur](#attribute_blur)
* [attribute:change](#attribute_change)
* [attribute:click](#attribute_click)
* [attribute:display](#attribute_display)
* [attribute:focus](#attribute_focus)
* [attribute:hash](#attribute_hash)
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
* [attribute:with](#attribute_with)
* [mediator:resolver](#mediator_resolver)
* [mediator:templator](#mediator_templator)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "DefaultUIHelpers"
```
This module contains a set of default UI tools. It's important to note that
this module is seperate from the UI module, so it shows the extent of what
is possible without access to the internals of the UI mdoule. In addition to
the documentation, the examples folder will provide a lot of guidance in
using this module.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.UI.hash'></a>Lapiz.UI.hash
```javascript
Lapiz.UI.hash(hash, fn)
Lapiz.UI.hash(namedFn)
Lapiz.UI.hash(hash, renderArgs...)
Lapiz.UI.hash([argSet...])
```
Registers a hash handler. When the hash in the url changes to match the
given hash the function will be called or the renderString will be passed
into render. A hash will be split on "/" as "hash/arg1/arg2/...".

When passing in an array, each element should either be a named function
or an array of arguments.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.UI.mediator'></a>Lapiz.UI.mediator
```javascript
Lapiz.UI.mediator
```
Mediators are a way to attach generic logic to a view. See
[more](ui.js.md#Lapiz.UI.mediator)

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.mediator.form'></a>Lapiz.UI.mediator.form
```javascript
Lapiz.UI.mediator.form
```
```javascript
<form>
  ...
  <button click="form.formHandler">Go!</button>
</form>
```
```javascript
Lapiz.UI.mediator.form("formHandler", fn(formData, formNode, ctx));
```
The form mediator will search up the node tree until it finds
a form node. All elements with a name will be added to the
formData. If more than one element has the same name, the value will be
returned as a list.

Checkboxes and radio buttons will return a boolean by default indicating
if they are checked. But if they have a value attribute, they will use that
and only include the value if they are checked.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.mediator.viewMethod'></a>Lapiz.UI.mediator.viewMethod
```javascript
Lapiz.UI.mediator.viewMethod(viewMethodName, func(node, ctx, args...))
Lapiz.UI.mediator.viewMethod(namedFunc(node, ctx, args...))
Lapiz.UI.mediator.viewMethod({"viewMethodName":funcs(node, ctx, args...)...})
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
Causes this element to receive focus when a view is rendered

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='attribute_hash'></a>attribute:hash
```javascript
attribute:hash
```
Just a shorthand for adding hash links so
```javascript
<a hash="foo">Foo</a>
```
becomes
```javascript
<a href="#foo">Foo</a>
```

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
removals. To keep the contents up to date, also use live.

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
or
```javascript
Lapiz.UI.mediator.view("foo", function(node, ctx){
  return {
    view: "someview > #string",
    ctx: {"another": "context"}
  };
});
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='attribute_with'></a>attribute:with
```javascript
attribute:with
<tag with="$SubCtx">...</tag>
```
Set the render context. This changes the render context for the node and
all children of the node. Can be combined with the render tag for reusable
sub-views.

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