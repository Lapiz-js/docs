## components/ui/ui.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.UI](#Lapiz.UI)
  * [Lapiz.UI.CloneView](#Lapiz.UI.CloneView)
  * [Lapiz.UI.View](#Lapiz.UI.View)
  * [Lapiz.UI.attribute](#Lapiz.UI.attribute)
  * [Lapiz.UI.bind](#Lapiz.UI.bind)
  * [Lapiz.UI.id](#Lapiz.UI.id)
  * [Lapiz.UI.mediator](#Lapiz.UI.mediator)
    * [Lapiz.UI.mediator.mediatorName](#Lapiz.UI.mediator.mediatorName)
  * [Lapiz.UI.render](#Lapiz.UI.render)
* [attribute:resolver](#attribute_resolver)
* [l-view](#l-view)

### <a name='Lapiz.UI'></a>Lapiz.UI
```javascript
Lapiz.UI
```
Namespace for the UI methods.

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

#### <a name='Lapiz.UI.attribute'></a>Lapiz.UI.attribute
```javascript
Lapiz.UI.attribute(name, fn)
Lapiz.UI.attribute(name, fn, before)
Lapiz.UI.attribute(attributes)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.bind'></a>Lapiz.UI.bind
```javascript
Lapiz.UI.bind(node, ctx, templator)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.id'></a>Lapiz.UI.id
```javascript
Lapiz.UI.id(elId)
Lapiz.UI.id(elId, doc)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.mediator'></a>Lapiz.UI.mediator
```javascript
Lapiz.UI.mediator(mediatorName,fn)
Lapiz.UI.mediator(mediators)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

##### <a name='Lapiz.UI.mediator.mediatorName'></a>Lapiz.UI.mediator.mediatorName
```javascript
Lapiz.UI.mediator.mediatorName(propertyName, property)
Lapiz.UI.mediator.mediatorName(properties)
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.UI.render'></a>Lapiz.UI.render
```javascript
Lapiz.UI.render(renderString..., ctx);
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='attribute_resolver'></a>attribute:resolver
```javascript
attribute:resolver
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

### <a name='l-view'></a>l-view
```javascript
l-view
```
Used to create a lapiz view:
```javascript
<htmlNode l-view="viewName">...</htmlNode>
```
All nodes in the document with this attribute will be cloned and saved and
the original will be removed from the document.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
