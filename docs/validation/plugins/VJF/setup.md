## Enabling Vanilla Javascript Validation Functions (VJF)

When enabling the `VJF` plugin, you can optionally enhance it using [chriso/validator.js](https://github.com/chriso/validator.js).

#### Install `chriso/validator.js` Package (optional)
`chriso/validator.js` it's not included in the package, so you have to install it manually.

```bash
npm install --save validator
```

#### Define a plugins object

Minimal setup:

```javascript
import vjf from 'mobx-react-form/lib/validators/VJF';

const plugins = {
  vjf: vjf()
};
```

Using `chriso/validator.js`:

```javascript
import vjf from 'mobx-react-form/lib/validators/VJF';
import validator from 'validator';

const plugins = {
  vjf: vjf(validator)
};
```

%accordion% **VERSION < 1.37** %accordion%

No need to import the plugin function:

```javascript
import validator from 'validator';

const plugins = {
  vjf: validator
};
```

%/accordion%

#### Create the form passing the `plugins` object

```javascript
new Form({ ... }, { plugins });
```

#### Using the `chriso/validator.js` functions

You can now access the `validator` package in your custom function.

```javascript
export function isEmail({ field, validator }) {
  const isValid = validator.isEmail(field.value); // <<---
  return [isValid, `The ${field.label} should be an email address.`];
}
```

The function takes in input an object with the following props:

* the `form` instance
* the `field` instance
* the `validator` instance

Check out how to define [Custom VJF Validation Function](extend.md)