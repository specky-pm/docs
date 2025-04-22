---
sidebar_position: 2
---

# Create a Component Specification

Component specifications are at the heart of Specky. They define the functional requirements of your application components in a language-agnostic way. This guide will show you how to create your first component specification.

## What is a Component Specification?

A component specification describes what a component should do, not how it should be implemented. This allows developers to implement the component in any programming language or framework while ensuring it meets the functional requirements.

## Creating a Basic Component Specification

In your Specky project directory, create a new component specification using the `spm create` command:

```bash
spm create user-component
```

This creates a new directory in the `components` folder with the basic structure for a component specification:

```
components/user-component/
├── spec.json           # Component metadata
├── component.md        # Component description
├── datamodel.json      # (Optional) Data model
└── features/           # (Optional) Gherkin feature specifications
```

## Defining Component Metadata

The `spec.json` file contains metadata about your component. Open it and customize the information:

```json
{
  "name": "user-component",
  "version": "0.1.0",
  "description": "User management component",
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {}
}
```

## Writing the Component Description

The `component.md` file is where you describe your component in detail. This is the main part of your specification and should be written in a way that an LLM (Large Language Model) can understand its purpose and functionality.

Here's an example of what a user component description might look like:

```markdown
# User Component

## Overview
The User Component handles user management functionality including registration, authentication, profile management, and user permissions.

## Core Functionality

### User Registration
- Allow new users to create an account
- Validate email addresses
- Enforce password strength requirements
- Prevent duplicate accounts

### Authentication
- Authenticate users with email/password
- Support password reset functionality
- Implement session management
- Support remember-me functionality

### Profile Management
- Allow users to view and edit their profile information
- Support profile picture upload
- Manage user preferences

### User Permissions
- Define user roles (e.g., admin, regular user)
- Control access to features based on user roles
- Allow role assignment and management
```

## Adding a Data Model (Optional)

If your component has specific data entities, you can define them in the `datamodel.json` file:

```json
{
  "entities": [
    {
      "name": "User",
      "attributes": [
        {
          "name": "id",
          "type": "string",
          "description": "Unique identifier for the user"
        },
        {
          "name": "email",
          "type": "string",
          "description": "User's email address"
        },
        {
          "name": "passwordHash",
          "type": "string",
          "description": "Hashed password"
        },
        {
          "name": "firstName",
          "type": "string",
          "description": "User's first name"
        },
        {
          "name": "lastName",
          "type": "string",
          "description": "User's last name"
        },
        {
          "name": "role",
          "type": "string",
          "description": "User's role (admin, user, etc.)"
        }
      ]
    }
  ]
}
```

## Adding Feature Tests (Optional)

You can add Gherkin feature specifications to define tests for your component. Create a file in the `features` directory, for example `features/registration.feature`:

```gherkin
Feature: User Registration
  As a new user
  I want to create an account
  So that I can access the system

  Scenario: Successful registration
    Given I am on the registration page
    When I enter valid registration details
    And I submit the registration form
    Then a new user account should be created
    And I should be logged in automatically

  Scenario: Registration with existing email
    Given I am on the registration page
    When I enter an email that is already registered
    And I submit the registration form
    Then I should see an error message
    And no new account should be created
```

## Best Practices for Component Specifications

1. **Focus on what, not how**: Describe what the component should do, not how it should be implemented.
2. **Be clear and specific**: Use clear language to describe functionality.
3. **Use examples**: Provide examples to illustrate complex requirements.
4. **Keep it language-agnostic**: Avoid references to specific programming languages or frameworks.
5. **Consider edge cases**: Document how the component should handle errors and edge cases.

## Next Steps

Now that you've created your first component specification, you can:
- [Validate your specification](./validate-specifications.md)
- [Publish your specification](./publish-specifications.md) to share it with others
- [Install existing specifications](./install-specifications.md) to use as dependencies