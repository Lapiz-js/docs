## Module Loader

[Home](./index.md)

The module loader is useful when building Lapiz modules. Lapiz is intended to be extended.

The first argument is the name of the module as a string. This is only used for dependancy management, it is not used to name or attach any values. The last argument is the module function. An optional middle argument is an array of dependancies. When the module function is loaded, Lapiz will be passed as an argument. This lets the module use a shorthand, generally $L.

```javascript
Lapiz.Module("Foo", ["Events"], function($L){
  $L.set($L, "foo", "bar");
});
```
This will wait for the Events module to be loaded, then invoke the function and register that the Foo module has been loaded, if it has any dependancies.