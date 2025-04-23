---
sidebar_position: 3
---

# The datamodel.json File Reference

The `datamodel.json` file is an optional but powerful part of your Specky component specification. It defines the data structures, entities, and relationships that your component uses. This reference guide explains how to structure and write an effective `datamodel.json` file.

## Purpose of datamodel.json

The `datamodel.json` file serves several important purposes:

1. **Defines data structures**: Documents the entities and attributes your component works with
2. **Establishes relationships**: Shows how different entities relate to each other
3. **Provides validation**: Sets constraints and validation rules for data
4. **Enables visualization**: Allows tools to generate entity-relationship diagrams
5. **Guides implementation**: Helps developers understand the data model when implementing

## Basic Structure

A typical `datamodel.json` file has this structure:

```json
{
  "entities": [
    {
      "name": "User",
      "description": "Represents a user in the system",
      "attributes": [
        {
          "name": "id",
          "type": "string",
          "description": "Unique identifier for the user",
          "required": true
        },
        {
          "name": "email",
          "type": "string",
          "description": "User's email address",
          "required": true,
          "unique": true
        }
      ]
    }
  ],
  "relationships": [
    {
      "name": "UserHasProfile",
      "source": "User",
      "target": "Profile",
      "type": "one-to-one",
      "description": "Each user has one profile"
    }
  ]
}
```

Let's explore each section in detail.

## Entities

The `entities` array defines the main data structures in your component.

### Entity Definition

Each entity represents a distinct concept or object in your domain:

```json
{
  "name": "User",
  "description": "Represents a user in the system",
  "attributes": [
    // attributes go here
  ]
}
```

**Required fields**:
- `name`: The name of the entity (PascalCase is recommended)
- `attributes`: Array of attributes that define the entity's properties

**Optional fields**:
- `description`: A clear explanation of what the entity represents
- `examples`: Example instances of the entity
- `tags`: Keywords to categorize the entity

### Attributes

Attributes define the properties of an entity:

```json
{
  "name": "email",
  "type": "string",
  "description": "User's email address",
  "required": true,
  "unique": true,
  "format": "email",
  "example": "user@example.com"
}
```

**Required fields**:
- `name`: The name of the attribute (camelCase is recommended)
- `type`: The data type of the attribute

**Optional fields**:
- `description`: Explanation of what the attribute represents
- `required`: Boolean indicating if the attribute must have a value
- `unique`: Boolean indicating if values must be unique across all instances
- `default`: Default value if none is provided
- `example`: Example value for the attribute
- `format`: Specific format for the type (e.g., "email", "date-time")
- `minLength`/`maxLength`: For strings, the min/max allowed length
- `minimum`/`maximum`: For numbers, the min/max allowed value
- `enum`: Array of allowed values
- `pattern`: Regular expression pattern the value must match

### Supported Data Types

The `type` field supports these common data types:

- `string`: Text values
- `number`: Numeric values (integers or decimals)
- `integer`: Whole number values
- `boolean`: True/false values
- `array`: List of values
- `object`: Complex nested structure
- `date`: Date values
- `datetime`: Date and time values
- `binary`: Binary data
- `reference`: Reference to another entity

For arrays, you can specify the item type:

```json
{
  "name": "tags",
  "type": "array",
  "items": {
    "type": "string"
  },
  "description": "Tags associated with the user"
}
```

For objects, you can define nested attributes:

```json
{
  "name": "address",
  "type": "object",
  "description": "User's address",
  "properties": {
    "street": {
      "type": "string",
      "description": "Street address"
    },
    "city": {
      "type": "string",
      "description": "City name"
    },
    "zipCode": {
      "type": "string",
      "description": "Postal code"
    }
  }
}
```

For references to other entities:

```json
{
  "name": "createdBy",
  "type": "reference",
  "entity": "User",
  "description": "User who created this record"
}
```

## Relationships

The `relationships` array defines how entities are connected to each other.

### Relationship Definition

Each relationship describes a connection between two entities:

```json
{
  "name": "UserHasProfile",
  "source": "User",
  "target": "Profile",
  "type": "one-to-one",
  "description": "Each user has one profile",
  "sourceAttribute": "profile",
  "targetAttribute": "user",
  "required": true
}
```

**Required fields**:
- `name`: Unique name for the relationship (PascalCase is recommended)
- `source`: The name of the source entity
- `target`: The name of the target entity
- `type`: The type of relationship

**Optional fields**:
- `description`: Explanation of what the relationship represents
- `sourceAttribute`: The attribute name on the source entity that references the target
- `targetAttribute`: The attribute name on the target entity that references the source
- `required`: Boolean indicating if the relationship is required

### Relationship Types

The `type` field supports these relationship types:

- `one-to-one`: Each source entity is related to at most one target entity, and vice versa
- `one-to-many`: Each source entity is related to multiple target entities
- `many-to-one`: Multiple source entities are related to one target entity
- `many-to-many`: Multiple source entities are related to multiple target entities

## Enumerations

The `enums` array defines sets of predefined values:

```json
{
  "enums": [
    {
      "name": "UserRole",
      "description": "Possible roles a user can have",
      "values": [
        {
          "name": "ADMIN",
          "description": "Administrator with full access"
        },
        {
          "name": "USER",
          "description": "Regular user with limited access"
        },
        {
          "name": "GUEST",
          "description": "Guest user with minimal access"
        }
      ]
    }
  ]
}
```

You can then reference these enums in your attributes:

```json
{
  "name": "role",
  "type": "enum",
  "enum": "UserRole",
  "description": "The user's role in the system",
  "default": "USER"
}
```

## Validation Rules

You can define additional validation rules for attributes:

```json
{
  "name": "password",
  "type": "string",
  "description": "User's password",
  "required": true,
  "minLength": 8,
  "maxLength": 100,
  "pattern": "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@$!%*?&])[A-Za-z\\d@$!%*?&]{8,}$",
  "validationMessage": "Password must contain at least one uppercase letter, one lowercase letter, one number, and one special character"
}
```

Common validation rules include:

- For strings: `minLength`, `maxLength`, `pattern`, `format`
- For numbers: `minimum`, `maximum`, `multipleOf`
- For arrays: `minItems`, `maxItems`, `uniqueItems`
- For all types: `enum`, `required`, `default`

## Complete Example

Here's a more comprehensive example of a `datamodel.json` file for a user management component:

```json
{
  "entities": [
    {
      "name": "User",
      "description": "Represents a user in the system",
      "attributes": [
        {
          "name": "id",
          "type": "string",
          "description": "Unique identifier for the user",
          "required": true,
          "unique": true
        },
        {
          "name": "email",
          "type": "string",
          "description": "User's email address",
          "required": true,
          "unique": true,
          "format": "email"
        },
        {
          "name": "passwordHash",
          "type": "string",
          "description": "Hashed password",
          "required": true
        },
        {
          "name": "firstName",
          "type": "string",
          "description": "User's first name",
          "required": true
        },
        {
          "name": "lastName",
          "type": "string",
          "description": "User's last name",
          "required": true
        },
        {
          "name": "role",
          "type": "enum",
          "enum": "UserRole",
          "description": "User's role in the system",
          "default": "USER"
        },
        {
          "name": "status",
          "type": "enum",
          "enum": "UserStatus",
          "description": "Current status of the user account",
          "default": "PENDING"
        },
        {
          "name": "lastLoginAt",
          "type": "datetime",
          "description": "Timestamp of the last successful login",
          "required": false
        },
        {
          "name": "createdAt",
          "type": "datetime",
          "description": "Timestamp when the user was created",
          "required": true
        }
      ]
    },
    {
      "name": "Profile",
      "description": "Extended information about a user",
      "attributes": [
        {
          "name": "id",
          "type": "string",
          "description": "Unique identifier for the profile",
          "required": true,
          "unique": true
        },
        {
          "name": "bio",
          "type": "string",
          "description": "User's biography",
          "required": false,
          "maxLength": 1000
        },
        {
          "name": "avatarUrl",
          "type": "string",
          "description": "URL to the user's avatar image",
          "required": false,
          "format": "uri"
        },
        {
          "name": "phoneNumber",
          "type": "string",
          "description": "User's phone number",
          "required": false,
          "pattern": "^\\+?[0-9]{10,15}$"
        },
        {
          "name": "address",
          "type": "object",
          "description": "User's address",
          "required": false,
          "properties": {
            "street": {
              "type": "string",
              "description": "Street address"
            },
            "city": {
              "type": "string",
              "description": "City name"
            },
            "state": {
              "type": "string",
              "description": "State or province"
            },
            "zipCode": {
              "type": "string",
              "description": "Postal code"
            },
            "country": {
              "type": "string",
              "description": "Country name"
            }
          }
        }
      ]
    },
    {
      "name": "Session",
      "description": "User session information",
      "attributes": [
        {
          "name": "id",
          "type": "string",
          "description": "Unique identifier for the session",
          "required": true,
          "unique": true
        },
        {
          "name": "token",
          "type": "string",
          "description": "Session token",
          "required": true
        },
        {
          "name": "expiresAt",
          "type": "datetime",
          "description": "Expiration timestamp",
          "required": true
        },
        {
          "name": "ipAddress",
          "type": "string",
          "description": "IP address of the client",
          "required": true
        },
        {
          "name": "userAgent",
          "type": "string",
          "description": "User agent of the client",
          "required": true
        },
        {
          "name": "createdAt",
          "type": "datetime",
          "description": "Timestamp when the session was created",
          "required": true
        }
      ]
    }
  ],
  "relationships": [
    {
      "name": "UserHasProfile",
      "source": "User",
      "target": "Profile",
      "type": "one-to-one",
      "description": "Each user has one profile",
      "sourceAttribute": "profile",
      "targetAttribute": "user",
      "required": true
    },
    {
      "name": "UserHasSessions",
      "source": "User",
      "target": "Session",
      "type": "one-to-many",
      "description": "Each user can have multiple sessions",
      "sourceAttribute": "sessions",
      "targetAttribute": "user",
      "required": false
    }
  ],
  "enums": [
    {
      "name": "UserRole",
      "description": "Possible roles a user can have",
      "values": [
        {
          "name": "ADMIN",
          "description": "Administrator with full access"
        },
        {
          "name": "USER",
          "description": "Regular user with limited access"
        },
        {
          "name": "GUEST",
          "description": "Guest user with minimal access"
        }
      ]
    },
    {
      "name": "UserStatus",
      "description": "Possible statuses for a user account",
      "values": [
        {
          "name": "ACTIVE",
          "description": "Account is active and usable"
        },
        {
          "name": "PENDING",
          "description": "Account is created but not yet verified"
        },
        {
          "name": "LOCKED",
          "description": "Account is temporarily locked"
        },
        {
          "name": "DISABLED",
          "description": "Account is disabled by an administrator"
        }
      ]
    }
  ]
}
```

## Best Practices

### Naming Conventions

- **Entities**: Use PascalCase singular nouns (e.g., `User`, `Product`)
- **Attributes**: Use camelCase (e.g., `firstName`, `emailAddress`)
- **Relationships**: Use descriptive names that indicate the connection (e.g., `UserHasProfile`)
- **Enums**: Use PascalCase for enum names, UPPER_CASE for enum values

### Documentation

- Provide clear descriptions for all entities, attributes, and relationships
- Include examples where helpful
- Document validation rules and constraints

### Structure

- Group related entities together
- Order attributes logically (e.g., id first, timestamps last)
- Use consistent patterns across similar entities

### Validation

- Define appropriate validation rules for each attribute
- Use standard formats where applicable (e.g., email, URI)
- Set reasonable constraints (min/max values, lengths)

## Validating Your datamodel.json

Use the Specky validation tools to check your `datamodel.json` file:

```bash
spm validate --focus=datamodel.json
```

This will check for:
- Valid JSON structure
- Required fields
- Consistent naming
- Valid relationships
- Proper type definitions

## Visualizing Your Data Model

Specky provides tools to visualize your data model:

```bash
spm viz --model --format=svg --output=datamodel.svg
```

This generates an entity-relationship diagram based on your `datamodel.json` file.

## Next Steps

Now that you understand how to create an effective `datamodel.json` file, you might want to explore:

- [Gherkin Features Reference](./gherkin-features-reference.md) - Learn how to write feature tests
- [Advanced Data Modeling](./advanced-data-modeling.md) - Explore complex data modeling techniques
- [Component Integration Patterns](./component-integration-patterns.md) - Understand how components share data