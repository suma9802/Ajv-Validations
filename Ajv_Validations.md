# AJV Validation with TypeScript – Complete Study Material (With Explanations)

---

# 1. What is AJV?

**AJV (Another JSON Validator)** is a fast JSON Schema validator for JavaScript and TypeScript.

### Why Do We Need It?

When working with:
- API request validation
- Dynamic forms
- Configuration JSON
- Dashboard widget JSON
- Menu builder JSON
- Backend request validation

We must ensure:
- Required fields exist
- Types are correct
- Structure is correct
- No unwanted extra fields are present

AJV validates JSON data against a defined schema.

---

# 2. Installation

```bash
npm install ajv
npm install ajv-formats
```

If using TypeScript:

```bash
npm install --save-dev typescript
```

---

# 3. Basic Validation Example

```ts
import Ajv from "ajv";

const ajv = new Ajv();

const schema = {
  type: "object",
  properties: {
    name: { type: "string" },
    age: { type: "number" }
  },
  required: ["name", "age"],
  additionalProperties: false
};

const validate = ajv.compile(schema);

const data = { name: "Suma", age: 25 };

const isValid = validate(data);

if (!isValid) {
  console.log(validate.errors);
}
```

---

## Explanation

1. `type: "object"` → Data must be an object.
2. `properties` → Defines allowed properties.
3. `required` → These fields must exist.
4. `additionalProperties: false` → Prevents extra fields.
5. `compile()` → Converts schema into optimized validation function.

Important:
👉 Always compile once and reuse.

---

# 4. JSON Schema Fundamentals

AJV works using **JSON Schema standard**.

---

## 4.1 Primitive Types

```ts
{ type: "string" }
{ type: "number" }
{ type: "integer" }
{ type: "boolean" }
{ type: "null" }
{ type: "array" }
{ type: "object" }
```

### Explanation

AJV strictly checks types.
Example:

```ts
{ type: "number" }
```

❌ `"25"` (string)  
✅ `25` (number)

---

# 5. String Validation

## 5.1 Length Validation

```ts
{
  type: "string",
  minLength: 3,
  maxLength: 10
}
```

Explanation:
- `minLength` ensures minimum characters.
- `maxLength` ensures maximum characters.

---

## 5.2 Pattern (Regex Validation)

```ts
{
  type: "string",
  pattern: "^[A-Za-z]+$"
}
```

Explanation:
Only alphabets allowed.

---

## 5.3 Format Validation

```ts
import addFormats from "ajv-formats";
addFormats(ajv);

{
  type: "string",
  format: "email"
}
```

Common formats:
- email
- uri
- date
- date-time
- uuid

Explanation:
AJV uses predefined format validators.

---

# 6. Number Validation

```ts
{
  type: "number",
  minimum: 0,
  maximum: 100,
  exclusiveMinimum: 0,
  multipleOf: 5
}
```

Explanation:

- `minimum` → inclusive
- `exclusiveMinimum` → strictly greater than
- `multipleOf` → must be divisible

Example:

If multipleOf = 5  
✅ 10  
❌ 12  

---

# 7. Array Validation

## 7.1 Basic Array

```ts
{
  type: "array",
  items: { type: "string" }
}
```

Explanation:
All elements must be strings.

---

## 7.2 Min / Max Items

```ts
{
  type: "array",
  minItems: 1,
  maxItems: 5
}
```

---

## 7.3 Unique Items

```ts
{
  type: "array",
  uniqueItems: true
}
```

Explanation:
Prevents duplicates.

---

# 8. Object Validation

## 8.1 Nested Objects

```ts
{
  type: "object",
  properties: {
    user: {
      type: "object",
      properties: {
        name: { type: "string" }
      },
      required: ["name"]
    }
  }
}
```

Explanation:
Validation works recursively.

---

# 9. Enum Validation

```ts
{
  type: "string",
  enum: ["admin", "user", "guest"]
}
```

Explanation:
Value must be one of listed values.

Useful for:
- Role types
- Status values
- Widget types

---

# 10. oneOf vs anyOf vs allOf

---

## 10.1 oneOf

```ts
{
  oneOf: [
    { type: "string" },
    { type: "number" }
  ]
}
```

Explanation:
Exactly ONE must match.

---

## 10.2 anyOf

At least one must match.

---

## 10.3 allOf

All conditions must match.

Useful for:
- Extending schemas
- Combining validation rules

---

# 11. Conditional Validation (if / then / else)

```ts
{
  type: "object",
  properties: {
    role: { type: "string" },
    adminCode: { type: "string" }
  },
  if: {
    properties: { role: { const: "admin" } }
  },
  then: {
    required: ["adminCode"]
  }
}
```

Explanation:
If role is "admin", then adminCode becomes mandatory.

Very powerful for dynamic forms.

---

# 12. Using TypeScript with AJV (IMPORTANT)

This is best practice.

---

## Step 1: Define Interface

```ts
interface User {
  name: string;
  age: number;
}
```

---

## Step 2: Use JSONSchemaType

```ts
import Ajv, { JSONSchemaType } from "ajv";

const schema: JSONSchemaType<User> = {
  type: "object",
  properties: {
    name: { type: "string" },
    age: { type: "number" }
  },
  required: ["name", "age"],
  additionalProperties: false
};
```

---

### Why This Is Important

Now TypeScript ensures:

- Schema matches interface
- No missing required fields
- No extra properties
- Type safety

This is extremely useful in large apps.

---

# 13. $ref (Reusable Schemas)

Instead of duplicating schema, reuse it.

```ts
const addressSchema = {
  $id: "address",
  type: "object",
  properties: {
    city: { type: "string" }
  },
  required: ["city"]
};

ajv.addSchema(addressSchema);

const userSchema = {
  type: "object",
  properties: {
    address: { $ref: "address" }
  }
};
```

Explanation:
Reusable components like:
- address
- pagination
- metadata
- widget schema

---

# 14. Custom Keywords

```ts
ajv.addKeyword({
  keyword: "isEven",
  type: "number",
  validate: (_, data) => data % 2 === 0
});
```

Explanation:
Allows creating custom validation logic.

---

# 15. Strict Mode

```ts
const ajv = new Ajv({
  strict: true
});
```

Explanation:
Prevents:
- Unknown keywords
- Invalid schemas
- Silent mistakes

Always enable in production.

---

# 16. Validation Errors

```ts
if (!validate(data)) {
  console.log(validate.errors);
}
```

Error structure:

```ts
[
  {
    instancePath: "/age",
    keyword: "minimum",
    message: "must be >= 18"
  }
]
```

Important fields:
- instancePath → where error occurred
- keyword → which rule failed
- message → human readable

---

# 17. Performance Best Practices

- Compile schema once
- Do not create AJV instance inside functions repeatedly
- Reuse validator
- Enable strict mode
- Use standalone code for large scale apps

---

# 18. Real-World Example (API Validation)

```ts
interface LoginRequest {
  email: string;
  password: string;
}

const schema: JSONSchemaType<LoginRequest> = {
  type: "object",
  properties: {
    email: { type: "string", format: "email" },
    password: { type: "string", minLength: 6 }
  },
  required: ["email", "password"],
  additionalProperties: false
};
```

Explanation:
- Validates login request
- Ensures proper email format
- Ensures password length

---

# 19. How This Helps in Your Projects

Since you're building:
- Dynamic JSON dashboards
- Menu builder JSON
- Widget configurations

AJV can validate:
- Widget schema
- Menu structure
- Template JSON
- Form definitions
- Drill-down hierarchy config

Before rendering UI, validate JSON.

---

# 20. Learning Roadmap

1. Master basic JSON Schema
2. Practice simple validations
3. Learn TypeScript integration
4. Learn conditional validation
5. Learn schema reuse
6. Build middleware validation
7. Apply in real project

---

# Conclusion

AJV + TypeScript gives:

✔ Runtime validation  
✔ Compile-time type safety  
✔ Schema-based architecture  
✔ Production-level data safety  

Mastering AJV will make you strong in:
- Backend validation
- Schema-driven UI
- Large enterprise apps
- Dynamic systems
