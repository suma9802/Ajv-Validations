# Schema Keywords and Validation Rules

This document provides a comprehensive overview of the schema keywords, validation rules, and type-specific constraints used in JSON validation as per the JSON Schema specification.

## 1. Basics of JSON Schema
JSON Schema is a powerful tool for validating the structure of JSON data. It allows developers to define a schema that outlines the expected format and types of data.

## 2. Common Schema Keywords
### 2.1. `$schema`
Indicates the schema version being used.

### 2.2. `type`
Specifies the data type (e.g., object, array, string, number, boolean, null).

### 2.3. `properties`
Defines the properties of an object.

### 2.4. `required`
Lists the properties that must be present in the object.

### 2.5. `items`
Specifies the type of items in an array.

## 3. Validation Rules
### 3.1. `maximum` and `minimum`
Used with numbers to specify maximum and minimum values.

### 3.2. `maxLength` and `minLength`
Set limits on the length of strings.

### 3.3. `pattern`
Defines a regular expression that a string must comply with.

### 3.4. `enum`
Specifies a set of allowed values for a field.

## 4. Type-Specific Constraints
### 4.1. For Strings
- **`format`**: Specifies semantic type (e.g., date-time, email, URI).

### 4.2. For Numbers
- **`multipleOf`**: Ensures the number is a multiple of another number.

### 4.3. For Arrays
- **`uniqueItems`**: Ensures all items in the array are unique.

## 5. Advanced Features
### 5.1. `allOf`, `anyOf`, `oneOf`, `not`
These keywords facilitate complex validation logic by combining multiple schemas.

### 5.2. `if`, `then`, `else`
Conditional schemas for more dynamic validations.

## Conclusion
Understanding these schema keywords and validation rules is essential for effective data validation in JSON. Adhering to the structure defined by a schema helps ensure the integrity and correctness of the data being processed in applications.