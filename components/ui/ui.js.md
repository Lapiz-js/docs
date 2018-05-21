## Lapiz/components/ui/ui.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [.ModuleName](#.ModuleName)
* [Lapiz.UI](#Lapiz.UI)
  * [Lapiz.UI.Children](#Lapiz.UI.Children)
  * [Lapiz.UI.CloneView](#Lapiz.UI.CloneView)
  * [Lapiz.UI.View](#Lapiz.UI.View)
  * [Lapiz.UI.appendChild](#Lapiz.UI.appendChild)
  * [Lapiz.UI.attribute](#Lapiz.UI.attribute)
  * [Lapiz.UI.bind](#Lapiz.UI.bind)
  * [Lapiz.UI.bindState](#Lapiz.UI.bindState)
    * [Lapiz.UI.bindState.after](#Lapiz.UI.bindState.after)
    * [Lapiz.UI.bindState.ctx](#Lapiz.UI.bindState.ctx)
    * [Lapiz.UI.bindState.firstPass](#Lapiz.UI.bindState.firstPass)
    * [Lapiz.UI.bindState.parent](#Lapiz.UI.bindState.parent)
    * [Lapiz.UI.bindState.proceed](#Lapiz.UI.bindState.proceed)
    * [Lapiz.UI.bindState.templator](#Lapiz.UI.bindState.templator)
  * [Lapiz.UI.empty](#Lapiz.UI.empty)
  * [Lapiz.UI.getStyle](#Lapiz.UI.getStyle)
  * [Lapiz.UI.id](#Lapiz.UI.id)
  * [Lapiz.UI.insertAfter](#Lapiz.UI.insertAfter)
  * [Lapiz.UI.mediator](#Lapiz.UI.mediator)
    * [Lapiz.UI.mediator.mediatorName](#Lapiz.UI.mediator.mediatorName)
  * [Lapiz.UI.on.add](#Lapiz.UI.on.add)
  * [Lapiz.UI.on.loaded](#Lapiz.UI.on.loaded)
  * [Lapiz.UI.on.move](#Lapiz.UI.on.move)
  * [Lapiz.UI.on.remove](#Lapiz.UI.on.remove)
  * [Lapiz.UI.render](#Lapiz.UI.render)
* [attribute](#attribute)
  * [attribute:l-view](#attribute_l-view)
* [tag](#tag)
  * [tag:comment:bind](#tag_comment_bind)
  * [tag:l-view](#tag_l-view)
  * [tag:render](#tag_render)

### <a name='.ModuleName'></a>.ModuleName
```javascript
.ModuleName "UI"
```
In addition to the documentation, the examples folder will provide a lot of
guidance in using this module.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='Lapiz.UI'></a>Lapiz.UI
```javascript
Lapiz.UI
```
Namespace for the UI methods.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.Children'></a>Lapiz.UI.Children
```javascript
Lapiz.UI.Children(node)
Lapiz.UI.Children(selectorStr)
```
Gets all the children of the node as an array, including textnodes, which
the built-in node.children will leave out. Node can also be a document
fragment. If a selectorStr is used, it will be run against document.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.CloneView'></a>Lapiz.UI.CloneView
```javascript
Lapiz.UI.CloneView(name)
```
Returns an html Node that is a clone of the View.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.View'></a>Lapiz.UI.View
```javascript
Lapiz.UI.View(name, viewStr)
```
Adds a view that can be rendered or cloned.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.appendChild'></a>Lapiz.UI.appendChild
```javascript
Lapiz.UI.appendChild(child)
Lapiz.UI.appendChild(child, parent)
Lapiz.UI.appendChild(childStr)
Lapiz.UI.appendChild(childStr, parent)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.attribute'></a>Lapiz.UI.attribute
```javascript
Lapiz.UI.attribute(name, fn(node, ctx, attrVal) )
Lapiz.UI.attribute(name, fn(node, ctx, attrVal), before)
Lapiz.UI.attribute(attributes)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.bind'></a>Lapiz.UI.bind
```javascript
Lapiz.UI.bind(node, ctx, templator)
Lapiz.UI.bind(node)
```
Binds a context and node together using the templator. If no templator is
given, it will inheirit a templator from it's parent, if no parent is
present it will use the standard templator. Generally, it is better to call
Lapiz.UI.render than Lapiz.UI.bind.

If ctx and templator are undefined, the ctx and templator will be
inheirited - they will be whatever they would have been.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.bindState'></a>Lapiz.UI.bindState
```javascript
Lapiz.UI.bindState
```
The bind state helps coordinate binding a template and a context. It is
available to the attributes during the binding process so they can direct
aspects of the bind process.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.after'></a>Lapiz.UI.bindState.after
```javascript
Lapiz.UI.bindState.after(fn);
```
Adds a function that will be called after all attributes and child nodes
have been handled.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.ctx'></a>Lapiz.UI.bindState.ctx
```javascript
Lapiz.UI.bindState.ctx
```
Initially, this is set to the ctx that is resolved for the binding
operationg. If it is changed by attribute, that will become the context

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.firstPass'></a>Lapiz.UI.bindState.firstPass
```javascript
Lapiz.UI.bindState.firstPass
```
The bind operation may run several times during the life span of a node
for various update operations. This property will indicate if this is the
first pass binding.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.parent'></a>Lapiz.UI.bindState.parent
```javascript
Lapiz.UI.bindState.parent
```
The bindstate of the parent node.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.proceed'></a>Lapiz.UI.bindState.proceed
```javascript
Lapiz.UI.bindState.proceed
```
If an attribute set this to false, no further attributes will be bound
and the child nodes will not be processed. This is useful if an attribute
is removing a node.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.bindState.templator'></a>Lapiz.UI.bindState.templator
```javascript
Lapiz.UI.bindState.templator
```
The templator that will be used

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.empty'></a>Lapiz.UI.empty
```javascript
Lapiz.UI.empty(node)
Lapiz.UI.empty(nodeId)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.getStyle'></a>Lapiz.UI.getStyle
```javascript
Lapiz.UI.getStyle(node, property)
Lapiz.UI.getStyle(selectorString, property)
Lapiz.UI.getStyle(nodeOrStr, property, doc)
Lapiz.UI.getStyle(nodeOrStr, property, doc, docView)
Lapiz.UI.getStyle(nodeOrStr, property, doc, docView, pseudoElt)
```
Returns the computed style for the node. If a string is passed in for node
the node will be found with doc.querySelector. For defaults, doc will
document, docView will be 'defaultView' and pseudoElt will be null.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.id'></a>Lapiz.UI.id
```javascript
Lapiz.UI.id(elId)
Lapiz.UI.id(elId, doc)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.insertAfter'></a>Lapiz.UI.insertAfter
```javascript
Lapiz.UI.insertAfter(newNode, afterElement)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.mediator'></a>Lapiz.UI.mediator
```javascript
Lapiz.UI.mediator(mediatorName,fn)
Lapiz.UI.mediator(namedMediatorFn)
```
Mediators are a pattern to provide reusable code. Mediators can only be
used as an attribute value and always follow the pattern of two words
seperated by a period, or more exactly:
```javascript
/^(\w+)\.(\w+)$/
```
Abstractly, if we have
```javascript
<N A="M.F">...</N>
```
and
```javascript
Lapiz.UI.attribute(A, fn_A);
Lapiz.UI.mediator(M, fn_M);
Lapiz.UI.mediator.M(F, val_F);
Lapiz.UI.render("view > target", C); //view includes the segmetn above
```
Then we will invoke the follwing logic:
```javascript
fn_A(N, C, fn_M(N, C, val_F));
```

A good example of the usefulness of this pattern is the form mediator.
```javascript
Lapiz.UI.mediator.form(formHandlerName, formHandlerFunction(formData));
```
The form mediator abstracts away the logic of pulling the values from named
elements within the form into a key/value Map so that the
formHandlreFunction can focus on what should be done with the data. It
produces clean html:
```javascript
<form submit="form.newPerson">...</form>
```

```javascript
Lapiz.UI.mediator.form("newPerson", function(newPersonData){...});
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.UI.mediator.mediatorName'></a>Lapiz.UI.mediator.mediatorName
```javascript
Lapiz.UI.mediator.mediatorName(propertyName, property)
Lapiz.UI.mediator.mediatorName(properties)
```
Defines a mediator property. If 

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.on.add'></a>Lapiz.UI.on.add
```javascript
Lapiz.UI.on.add(node, fn)
```
When the node is added to the document, fn will be called.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.on.loaded'></a>Lapiz.UI.on.loaded
```javascript
Lapiz.UI.on.loaded(fn())
Lapiz.UI.on.loaded = fn()
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.on.move'></a>Lapiz.UI.on.move
```javascript
Lapiz.UI.on.move(node, fn)
```
When the node is moved with in the document, fn will be called.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.on.remove'></a>Lapiz.UI.on.remove
```javascript
Lapiz.UI.on.remove(node, fn)
```
When the node is removed from the document, fn will be called.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.UI.render'></a>Lapiz.UI.render
```javascript
Lapiz.UI.render(renderString..., ctx)
renderString: "viewName > target"
renderString append: "viewName >> target"  
```
The renderString has three parts. The first part is the view name. The
second part is either ">" which will replace the contents of the target or
">>" which will append to the target. The target is a CSS querySelector,
but it will on render to the first match.

When using multiple renderStrings, the first render string will select a
target in the document, all other render strings will select a target in
the view. Using "viewName>>" with no selector indicates that it should
append to the view, not a node within the view, but will not work for the
first renderString.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='attribute'></a>attribute
```javascript
attribute
```
An HTML attribute

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='attribute_l-view'></a>attribute:l-view
```javascript
attribute:l-view
<htmlNode l-view="viewName">...</htmlNode>
```
Used to create a lapiz view:
All nodes in the document with this attribute will be cloned and saved and
the original will be removed from the document.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
### <a name='tag'></a>tag
```javascript
tag
```
An html tag

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='tag_comment_bind'></a>tag:comment:bind
```javascript
tag:comment:bind(ctx)
```
This is kind of a hack (but only a little one). By attaching a bind
function to a comment node, that will be invoked during any bind pass.
This allows logic to be added without adding tags that will render.
A use case if an attribute removes the tag it was originally associated
with, but may need to restore it on a later bind pass.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='tag_l-view'></a>tag:l-view
```javascript
tag:l-view
<l-view name="viewName">...</l-view>  
```
Any node with the l-view tag will also be cloned as a view, but only the
children will be cloned, the node itself will be ommited, therefor
attributes like 'with' will not work. The node must have a name attribute.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='tag_render'></a>tag:render
```javascript
tag:render
<render name="viewName"></render>
```
Inserts a sub view. Contents of render will be wiped. The viewName
can be dynamic, the result of either a tempator value or a mediator.
Currently, the render tag will ignore all attributes.

<sub><sup>[&uarr;Top](#__top)</sup></sub>