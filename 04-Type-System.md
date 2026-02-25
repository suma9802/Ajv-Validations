# Type System Documentation

## Overview
The type system in AJV provides various options to validate data structures against defined schemas. Understanding these types is crucial for successful validation.

## Basic Types
- `string`: Represents text data.
  - Example:
    ```
    {
      "name": "John Doe"
    }
    ```

- `number`: Represents numeric data.
  - Example:
    ```
    {
      "age": 30
    }
    ```

- `boolean`: Represents a true/false value.
  - Example:
    ```
    {
      "isActive": true
    }
    ```

## Complex Types
- `object`: Represents a collection of key-value pairs.
  - Example:
    ```
    {
      "user": {
        "name": "Jane Doe",
        "age": 25
      }
    }
    ```

- `array`: Represents a list of values.
  - Example:
    ```
    {
      "items": ["item1", "item2", "item3"]
    }
    ```

## Type Combinations
You can combine types using `anyOf`, `allOf`, and `oneOf` to create more complex validation rules.

- `anyOf`: At least one of the specified schemas must be valid.
  - Example:
    ```
    {
      "type": "object",
      "properties": {
        "value": {
          "anyOf": [
            {"type": "string"},
            {"type": "number"}
          ]
        }
      }
    }
    ```

## Conclusion
Understanding the type system of AJV allows for effective data validation. Use the examples above to get started with creating your own schemas!