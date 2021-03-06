# Functions

Functions will always:

- Functions will only do one thing.
    - You will know a function is only doing one thing when you cannot possibly extract another meaningful function from within it.
- Functions will be assorted into service classes based upon the type of business logic being performed.
- Functions will have descriptive names.
- Functions will declare their return types.
- Function variables will be typed.
- Functions will avoid accepting raw values whenever possible.
- Try to limit functions to two or three variables, beyond that consider passing objects instead.
- Command and Query Separation. A function that returns `void` must have a side effect.
- When writing `try` blocks:
    - The only thing within the function will be the try block.
    - Only one function will be written within the try block.
- Comments will only be used as a last resort. Descriptive variable and function names are preferred.

If a function must intake a raw value create a variable instead.

```php
// Poor
$this->saveEntry($entry, true);

// Better
$doValidation = true;
$this->saveEntry($entry, $doValidation);

// Even Better
$this->saveAndValidateEntry($entry);
$this->saveEntry($entry);

// Best
if ($entry->validate()){
    $entry->save();
}
```

## Why create variables?

When authoring code you fully understand what the boolean variable does. However, when returning to code several months later or trying to understand other developer's code a raw boolean variable can be confusing and forces developers to search out the function when trying to understand what the boolean does. Code readability is more important than the negligible performance hit of declaring an extra variable. Although the *"best"* solution would be to provide a robust set of tiny functions that don't use parameters and have highly descriptive names.

## Examples

### Example One

```php
private function getFileContents(string $path) : string
{
    $output = "";
    if (file_exists($path))
    {
        $output = file_get_contents($path);
    }
    return $output;
}

public function getCriticalCss(array $files) : string
{
    $output = "";
    foreach ($files as $file)
    {
        $path = $_SERVER["DOCUMENT_ROOT"] . "/assets/" . rtrim($file, ".css") . ".css";
        $output .= $this->getFileContents($path);
    }
    return $output;
}
```

### Example Two

```php
// Poor
$params = $request->getBodyParams();
$fields = $this->setParamAsArray($params, "productGroup");
$fields = $this->setParamAsArray($fields, "laminate");
$fields = $this->setParamAsArray($fields, "score");
$entry->setFieldValues($fields);

// Better
$params = $request->getBodyParams();
$fields = $this->convertValuesToArrays($params, ["productGroup", "laminate", "score"]);
$entry->setFieldValues($fields);

private function convertValuesToArrays(array $data, mixed $keys): array
{
    $keys = (array)$keys;
    foreach ($keys as $key){
        if (isset($data[$key])){
            $data[$key] = (array)$data[$key];
        }
    }
    return $data;
}
```