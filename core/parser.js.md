## core/parser.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.parse](#Lapiz.parse)
  * [Lapiz.parse.array](#Lapiz.parse.array)
  * [Lapiz.parse.bool](#Lapiz.parse.bool)
  * [Lapiz.parse.int](#Lapiz.parse.int)
  * [Lapiz.parse.number](#Lapiz.parse.number)
  * [Lapiz.parse.string](#Lapiz.parse.string)

### <a name='Lapiz.parse'></a>Lapiz.parse
```javascript
Lapiz.parse
```
Namespace for parser methods. This namespace is left open
so that it can be extended, particularly for use with defining
object properties.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.parse.array'></a>Lapiz.parse.array
```javascript
Lapiz.parse.array(parser)
```
This takes a parser or a string (which will be resolved agains Lapiz.parse)
and returns an array parser.
```javascript
var arrIntParser = Lapiz.parse.array("int");
console.log(arrIntParser([3.14, "12.34", true]); // [3, 12, 1]
console.log(arrIntParser("22.22"); // [22]
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.parse.bool'></a>Lapiz.parse.bool
```javascript
Lapiz.parse.bool(val)
```
Converts val to a bool

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.parse.int'></a>Lapiz.parse.int
```javascript
Lapiz.parse.int(val)
Lapiz.parse.int(val, rad)
```
If rad is not defined it will default to 10. This is mostly a wrapper
around parseInt, however if val is a boolean it will reurn eitehr 1
or 0.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.parse.number'></a>Lapiz.parse.number
```javascript
Lapiz.parse.number(val)
```
Converts val to a number. This is a wrapper around parseFloat.

<sub><sup>[&uarr;Top](#__top)</sup></sub>

#### <a name='Lapiz.parse.string'></a>Lapiz.parse.string
```javascript
Lapiz.parse.string
```
If val is null or undefined, returns an empty stirng. If val
is a string, it is returned, if it's a number it's converted
to a string. If val is an object that has a .str() method,
that will be used, if it doesn't have .str but it does have
.toString, that will be used. As a last resort it will be
concatted with an empty string.

<sub><sup>[&uarr;Top](#__top)</sup></sub>
