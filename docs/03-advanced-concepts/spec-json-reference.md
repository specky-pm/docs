---
sidebar_position: 1
---

# The spec.json File Reference

The `spec.json` file is the heart of every Specky component specification. It contains metadata about your component, defines its dependencies, and configures how Specky should handle it. This reference guide provides detailed information about each field in the `spec.json` file.

## Basic Structure

A typical `spec.json` file looks like this:

```json
{
  "name": "user-component",
  "version": "1.2.0",
  "description": "A comprehensive user management component",
  "author": "Jane Developer",
  "license": "MIT",
  "keywords": ["user", "authentication", "profile"],
  "dependencies": {
    "email-validator": "^1.0.0"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/jane-developer/user-component"
  }
}
```

## Required Fields

### name

**Type**: String  
**Required**: Yes

The name of your component specification. This must be unique within the Specky registry.

```json
"name": "user-component"
```

**Rules**:
- Must be lowercase
- Can contain hyphens and underscores
- Cannot start with a dot or underscore
- Cannot contain spaces
- Maximum length: 214 characters

### version

**Type**: String  
**Required**: Yes

The version of your component specification, following [semantic versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

```json
"version": "1.2.0"
```

**Rules**:
- Must follow semantic versioning format: X.Y.Z
- X (MAJOR): Increment for incompatible changes
- Y (MINOR): Increment for new features (backward compatible)
- Z (PATCH): Increment for bug fixes (backward compatible)

### description

**Type**: String  
**Required**: Yes

A brief description of what your component does. This helps others understand the purpose of your component when they find it in the registry.

```json
"description": "A comprehensive user management component with authentication, profile management, and role-based permissions"
```

**Best practices**:
- Keep it concise but informative (under 300 characters)
- Focus on what the component does, not how it's implemented
- Mention key features or capabilities

## Author Information

### author

**Type**: String or Object  
**Required**: No, but recommended

Information about the author of the component specification. Can be a simple string or a more detailed object.

String format:
```json
"author": "Jane Developer <jane@example.com> (https://janedeveloper.com)"
```

Object format:
```json
"author": {
  "name": "Jane Developer",
  "email": "jane@example.com",
  "url": "https://janedeveloper.com"
}
```

### contributors

**Type**: Array of Strings or Objects  
**Required**: No

A list of people who have contributed to the component specification. Uses the same format as the author field.

```json
"contributors": [
  "Alex Smith <alex@example.com>",
  {
    "name": "Sam Johnson",
    "email": "sam@example.com",
    "url": "https://samjohnson.dev"
  }
]
```

## License Information

### license

**Type**: String  
**Required**: No, but recommended

The license under which the component specification is distributed. Use a valid [SPDX license identifier](https://spdx.org/licenses/).

```json
"license": "MIT"
```

Common licenses:
- `"MIT"`: MIT License
- `"Apache-2.0"`: Apache License 2.0
- `"GPL-3.0-only"`: GNU General Public License v3.0 only
- `"BSD-3-Clause"`: BSD 3-Clause License
- `"UNLICENSED"`: Proprietary, not open source

## Categorization

### keywords

**Type**: Array of Strings  
**Required**: No, but recommended

Tags that help others discover your component specification when searching the registry.

```json
"keywords": ["user", "authentication", "profile", "permissions", "roles"]
```

**Best practices**:
- Include terms related to functionality
- Include alternative terms people might search for
- Keep keywords relevant and specific
- Limit to 5-10 keywords

## Dependencies

### dependencies

**Type**: Object  
**Required**: No

Other component specifications that your component depends on. The keys are the names of the dependencies, and the values are version ranges.

```json
"dependencies": {
  "email-validator": "^1.0.0",
  "password-strength": "~2.1.0",
  "user-permissions": "1.0.0"
}
```

**Version range formats**:
- `"^1.2.3"`: Compatible with 1.2.3 up to (but not including) 2.0.0
- `"~1.2.3"`: Compatible with 1.2.3 up to (but not including) 1.3.0
- `"1.2.3"`: Exactly version 1.2.3
- `">=1.2.3"`: Version 1.2.3 or later
- `"1.2.3 - 1.5.0"`: Range between 1.2.3 and 1.5.0 (inclusive)
- `"latest"`: Always use the latest version (not recommended for production)

### devDependencies

**Type**: Object  
**Required**: No

Dependencies that are only needed during development, not when using the component specification.

```json
"devDependencies": {
  "spec-validator": "^2.0.0",
  "documentation-generator": "^1.5.0"
}
```

### peerDependencies

**Type**: Object  
**Required**: No

Dependencies that the consumer of your component specification must provide. These are not automatically installed.

```json
"peerDependencies": {
  "core-component": ">=2.0.0"
}
```

### optionalDependencies

**Type**: Object  
**Required**: No

Dependencies that enhance your component but are not required for it to function.

```json
"optionalDependencies": {
  "analytics-component": "^1.0.0"
}
```

## Repository Information

### repository

**Type**: String or Object  
**Required**: No, but recommended

Information about where the component specification's source code is hosted.

String format (shorthand for GitHub):
```json
"repository": "github:username/repo-name"
```

Object format:
```json
"repository": {
  "type": "git",
  "url": "https://github.com/username/repo-name.git",
  "directory": "packages/component-name"
}
```

### homepage

**Type**: String  
**Required**: No

URL to the component specification's homepage or documentation.

```json
"homepage": "https://user-component.example.com"
```

### bugs

**Type**: String or Object  
**Required**: No

Information about where to report issues with the component specification.

String format:
```json
"bugs": "https://github.com/username/repo-name/issues"
```

Object format:
```json
"bugs": {
  "url": "https://github.com/username/repo-name/issues",
  "email": "bugs@example.com"
}
```

## Component Configuration

### main

**Type**: String  
**Required**: No

The primary entry point to your component specification. By default, this is `component.md`.

```json
"main": "component.md"
```

### files

**Type**: Array of Strings  
**Required**: No

Files to include when publishing the component specification. If not specified, Specky uses a default set of files.

```json
"files": [
  "component.md",
  "datamodel.json",
  "features/*.feature",
  "examples/**/*"
]
```

### specky

**Type**: Object  
**Required**: No

Specky-specific configuration options.

```json
"specky": {
  "validators": {
    "strict": true,
    "datamodel": true
  },
  "visualization": {
    "defaultFormat": "svg",
    "theme": "light"
  }
}
```

## Publishing Configuration

### private

**Type**: Boolean  
**Required**: No

If true, prevents the component specification from being published to the registry.

```json
"private": true
```

### publishConfig

**Type**: Object  
**Required**: No

Configuration options used when publishing to the registry.

```json
"publishConfig": {
  "access": "public",
  "registry": "https://registry.specky.dev",
  "tag": "beta"
}
```

### engines

**Type**: Object  
**Required**: No

Specifies which versions of Specky your component specification is compatible with.

```json
"engines": {
  "specky": ">=1.0.0"
}
```

## Scripts

### scripts

**Type**: Object  
**Required**: No

Custom scripts that can be run with `spm run <script-name>`.

```json
"scripts": {
  "validate": "spm validate --strict",
  "test": "spm test",
  "docs": "spm docs --output ./docs"
}
```

## Example of a Complete spec.json

Here's an example of a comprehensive `spec.json` file using many of the available fields:

```json
{
  "name": "user-component",
  "version": "1.2.0",
  "description": "A comprehensive user management component",
  "author": {
    "name": "Jane Developer",
    "email": "jane@example.com",
    "url": "https://janedeveloper.com"
  },
  "contributors": [
    "Alex Smith <alex@example.com>",
    {
      "name": "Sam Johnson",
      "email": "sam@example.com"
    }
  ],
  "license": "MIT",
  "keywords": ["user", "authentication", "profile", "permissions"],
  "main": "component.md",
  "files": [
    "component.md",
    "datamodel.json",
    "features/*.feature",
    "examples/**/*"
  ],
  "dependencies": {
    "email-validator": "^1.0.0",
    "password-strength": "~2.1.0"
  },
  "devDependencies": {
    "spec-validator": "^2.0.0"
  },
  "peerDependencies": {
    "core-component": ">=2.0.0"
  },
  "optionalDependencies": {
    "analytics-component": "^1.0.0"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/jane-developer/user-component.git"
  },
  "homepage": "https://user-component.example.com",
  "bugs": {
    "url": "https://github.com/jane-developer/user-component/issues",
    "email": "bugs@example.com"
  },
  "specky": {
    "validators": {
      "strict": true,
      "datamodel": true
    },
    "visualization": {
      "defaultFormat": "svg",
      "theme": "light"
    }
  },
  "publishConfig": {
    "access": "public",
    "tag": "latest"
  },
  "engines": {
    "specky": ">=1.0.0"
  },
  "scripts": {
    "validate": "spm validate --strict",
    "test": "spm test",
    "docs": "spm docs --output ./docs"
  }
}
```

## Best Practices

1. **Keep it minimal**: Include only the fields you need
2. **Be descriptive**: Provide clear and helpful information
3. **Use semantic versioning**: Follow versioning conventions
4. **Specify dependencies precisely**: Use version ranges appropriately
5. **Include documentation links**: Help users find more information
6. **Validate your spec.json**: Use `spm validate` to check for errors

## Next Steps

Now that you understand the `spec.json` file structure, you might want to explore:

- [Component.md Reference](./component-md-reference.md) - Learn about the main component description file
- [Datamodel.json Reference](./datamodel-json-reference.md) - Understand how to define data models
- [Advanced Dependency Management](./advanced-dependencies.md) - Master complex dependency scenarios