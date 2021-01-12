# Services

Service functions:

- Functions will declare their return types.
- Function variables will be typed.
- Functions will avoid accepting booleans whenever possible.
- Only one business logic action will be performed per function.
- Functions will be assorted into unique services based upon their business logic.
- Functions will have descriptive names.

If a function must intake a `boolean` you should **not** pass a raw value, instead create a variable.

```php
// Incorrect
$this->saveEntry($entry, true);

// Correct
$doValidation = true;
$this->saveEntry($entry, $doValidation);
```

## Why create variables?

When authoring code you fully understand what the boolean variable does. However, when returning to code several months later or trying to understand other developer's code a raw boolean variable can be confusing and forces developers to search out the function when trying to understand what the boolean does. Code readability is more important than the negligible performance hit of declaring an extra variable.