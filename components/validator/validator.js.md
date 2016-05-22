## components/validator/validator.js<a name="__top"></a>

<sub><sup>[&larr;Home](index.md)</sup></sub>

* [Lapiz.Validator](#Lapiz.Validator)

### <a name='Lapiz.Validator'></a>Lapiz.Validator
```javascript
Lapiz.Validator(validationRules)
Lapiz.Validator(validationRules, data)
Lapiz.Validator(validationRules, data, formatFunc)
```
If only validationRules are given, a validator function is returned.
If data is given, the validation rules are run against the data.
```javascript
  var personValidator = Lapiz.Validator({
    "id" : "required"
  });
```

<sub><sup>[&uarr;Top](#__top)</sup></sub>
