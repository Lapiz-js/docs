## Parse

A collection of type parsers.

[Home](./index.md)
* [Lapiz.parse.int(val, rad)](#int)
* [Lapiz.parse.string(val)](#string)
* [Lapiz.parse.bool(val)](#bool)
* [Lapiz.parse.number(val)](#number)
* [Lapiz.parse.object(val)](#object)
* [Lapiz.parse.array(parser)](#array)

### <a name="int"></a> Lapiz.parse.int(val, rad)
Takes in a value and returns an integer. If parsing fails, a value of NaN will be returned. If rad is not specified it will default to 10. This is slighly different that the behavior of parseInt. On some browsers "022" will be interpreted as octal and "0xAB" will be interpreted as hex. Both 'undefined' and 'null' will return NaN.
```javascript
var x = Lapiz.parse.int("22");
console.log(x); // 22 as int
```

This also differs from parseInt in that a boolean true will return 1 and a boolean false will return 0.

### <a name="string"></a> Lapiz.parse.string(val)
Takes in a value and returns a string. If the provided value has a .str() method, that will be used (first) and if it has a .toString method, that will be used (if .str does not exist).
```javascript
var x = Lapiz.parse.int(22);
console.log(x); // "22" as string
```

### <a name="bool"></a> Lapiz.parse.bool(val)
Takes in a value and returns a boolean value.
```javascript
var x = Lapiz.parse.bool(1);
console.log(x); // true
```

### <a name="number"></a> Lapiz.parse.number(val)
Takes in a value and returns a number. This is a wrapper around parseFloat.
```javascript
var x = Lapiz.parse.number("   3.14 ignore trailing");
console.log(x); // 3.14
```

### <a name="object"></a> Lapiz.parse.object(val)
Not actually a parser, it's a pass-through function. It will return what ever value it is given as it is given. Occasionally useful in defining Lapiz.Object properties.

### <a name="array"></a> Lapiz.parse.array(parser)
Takes a type parser in and returns a parser that will cast an entire array to that type. If the returned parser is given a single value it will parse return it as an array of the correct type.
```javascript
var intArrParser = Lapiz.parse.array( Lapiz.parse.int );
console.log( intArrParser( [3.14, "22", true] ) ); //[3, 22, 1]
console.log( intArrParser( "123.4" ) ); //[123]