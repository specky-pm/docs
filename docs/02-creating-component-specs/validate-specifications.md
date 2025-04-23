---
sidebar_position: 4
---

# Validate Specifications

Validation is a crucial step in the component specification process. It ensures that your specifications are well-formed, complete, and follow best practices. This guide will show you how to validate your specifications using Specky.

## Why Validate Specifications?

Validating your specifications helps you:
- Catch errors and inconsistencies early
- Ensure all required information is present
- Follow best practices for component specifications
- Prepare your specifications for sharing with others

## Basic Validation

To validate a component specification, navigate to your project directory and run:

```bash
spm validate
```

This command checks all component specifications in your project against the Specky schema and reports any issues it finds.

If you want to validate a specific component, you can specify its name:

```bash
spm validate user-component
```

## Understanding Validation Results

When you run the validation command, you'll see output similar to this:

```
Validating user-component...

✓ spec.json: Valid
✓ component.md: Valid
✓ datamodel.json: Valid
✓ features/registration.feature: Valid

Validation complete: All files are valid!
```

If there are issues, you'll see error messages explaining what's wrong:

```
Validating user-component...

✓ spec.json: Valid
✗ component.md: Missing required section "Core Functionality"
✓ datamodel.json: Valid
✗ features/registration.feature: Invalid Gherkin syntax at line 12

Validation failed: 2 issues found.
```

## Validation Levels

Specky offers different validation levels to suit your needs:

### Standard Validation

The default validation checks for basic correctness and completeness:

```bash
spm validate
```

### Strict Validation

Strict validation enforces additional best practices and style guidelines:

```bash
spm validate --strict
```

This might check for things like:
- Consistent terminology
- Comprehensive documentation
- Complete test coverage
- Proper formatting

### Auto-fixing Issues

Some validation issues can be automatically fixed:

```bash
spm validate --fix
```

This attempts to fix common issues like:
- Formatting problems
- Missing sections with default templates
- Simple structural issues

:::caution
Always review auto-fixes carefully, as they might not always match your intentions.
:::

## What Gets Validated

Specky validates several aspects of your component specifications:

### spec.json Validation

- Checks for required fields (name, version, etc.)
- Validates semantic versioning
- Verifies dependency references

### component.md Validation

- Checks for required sections
- Validates structure and formatting
- Ensures comprehensive documentation

### datamodel.json Validation

- Validates JSON schema
- Checks entity definitions
- Verifies attribute types and relationships

### features/*.feature Validation

- Validates Gherkin syntax
- Checks for complete scenarios
- Ensures proper feature descriptions

## Common Validation Issues and Solutions

### Missing Required Fields

**Issue**: `spec.json is missing required field "version"`

**Solution**: Add the missing field to your spec.json file:
```json
{
  "name": "user-component",
  "version": "0.1.0",  // Added version field
  "description": "User management component"
}
```

### Incomplete Documentation

**Issue**: `component.md is missing required section "Core Functionality"`

**Solution**: Add the missing section to your component.md file:
```markdown
# User Component

## Overview
...

## Core Functionality
- User registration
- Authentication
- Profile management
```

### Invalid Gherkin Syntax

**Issue**: `Invalid Gherkin syntax at line 12`

**Solution**: Fix the syntax in your feature file:
```gherkin
# Before
Scenario: Registration
Given I am on the registration page
When I enter valid details
I submit the form  # Missing And/Then keyword

# After
Scenario: Registration
Given I am on the registration page
When I enter valid details
And I submit the form  # Fixed with proper keyword
```

## Continuous Validation

For larger projects, it's a good practice to validate specifications regularly:

1. **During development**: Validate as you work to catch issues early
2. **Before commits**: Validate before committing changes
3. **In CI/CD pipelines**: Add validation to your continuous integration process

## Next Steps

Now that you know how to validate your specifications, you can:
- [Publish your specifications](./publish-specifications.md) to share them with others
- [Visualize relationships](./visualize-relationships.md) between your components
- [Update your specifications](./update-specifications.md) to fix any issues