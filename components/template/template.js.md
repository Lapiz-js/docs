## Lapiz/components/template/template.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Template](#Lapiz.Template)
  * [Lapiz.Template.Std](#Lapiz.Template.Std)
    * [Lapiz.Template.Std.resolver](#Lapiz.Template.Std.resolver)
    * [Lapiz.Template.Std.templator](#Lapiz.Template.Std.templator)
    * [Lapiz.Template.Std.tokenizer](#Lapiz.Template.Std.tokenizer)
  * [Lapiz.Template.Templator](#Lapiz.Template.Templator)

### <a name='Lapiz.Template'></a>Lapiz.Template
```javascript
Lapiz.Template
```
Namespace for templating

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Template.Std'></a>Lapiz.Template.Std
```javascript
Lapiz.Template.Std
```
Namespace for the standard templators

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.Template.Std.resolver'></a>Lapiz.Template.Std.resolver
```javascript
Lapiz.Template.Std.resolver(token, ctx)
```
takes a token, splits on dot and steps down through the fields.
If at any point it encounters undefined, it will return undefined.

If the token is "$", it will return the ctx.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.Template.Std.templator'></a>Lapiz.Template.Std.templator
```javascript
Lapiz.Template.Std.templator(template, ctx)
```
Standard Lapiz templator. Takes a string template with tokens
that begin with $ and replaces them with the matching value
from the context. Using "$$" as a token will use the exact
ctx value and passing in a template that is exactly one token
will return the matching value from the context, even if that
value is not a string.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
##### <a name='Lapiz.Template.Std.tokenizer'></a>Lapiz.Template.Std.tokenizer
```javascript
Lapiz.Template.Std.tokenizer(template, ctx, resolver)
```
Expects a string for the template. Finds tokens that being
with $. Passes the token (without the leading $) into
resolver and replaces them with the returned value.

If the template is exactly one token, the value from
the resolver will be returned, even if that value is not
a string.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
#### <a name='Lapiz.Template.Templator'></a>Lapiz.Template.Templator
```javascript
Lapiz.Template.Templator(tokenizer, resolver)
```
Returns a templator of the form:
```javascript
templator(template, ctx)
```
which will take a template and a context and return
their product.

<sub><sup>[&uarr;Top](#__top)</sup></sub>