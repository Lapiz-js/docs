## Filter

Filters take in an object that implements the Accessor interface and provides a filtered subset. Filter itself fulfills the Accessor interface. Filter is an event listener, so it will always reflect the values in the accessor it is filtering.

[Home](./index.md)
* [Lapiz.Event()](#event)

### Constructors

#### Lapiz.Filter(accessor, filterFunction(key, accessor) )
When the filter is created, each key will be passed in to the filterFunction along with a reference to the accessor. The filterFunction should return a boolean indicating if the key corresponds to a value that falls within the filter.

#### Lapiz.Filter(accessor, field, value)
This construction is useful when the accessor values are objects. The filter can select all objects where the specified field matches the specified value.

#### accessor.Filter(filterFunction) or accessor.Filter(field, value)
All Lapiz accessors provide a method for generating a filter. This is not strictly part of the accessor interface.

### Example
```javascript
var people = Dictionary({
  1: {
    name: "Adam",
    role: "admin",
    active: true
  },
  2: {
    name: "Stephen",
    role: "admin",
    active: false
  },
  3: {
    name: "Lauren",
    role: "editor",
    active: true
  }
});
var active = people.Filter("active", true);
active.each(function(key, val){
  console.log(key, val); //this will print records for Adam and Lauren because they are both active
});

function log(key, acc){
  console.log(key, acc[key]);
}
active.on.change = log;
active.on.insert = log;
active.on.delete = function(key, val, acc){
  console.log(key, val);
};

var stephen = people.get(2);
stephen.active = true; //this does not trigger an event
people(2, stephen); // this does and will output a record for stephen
```