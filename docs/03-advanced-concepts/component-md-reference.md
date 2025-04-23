---
sidebar_position: 2
---

# The component.md File Reference

The `component.md` file is the core of your Specky component specification. While the `spec.json` file contains metadata, the `component.md` file contains the actual functional requirements and detailed description of your component. This reference guide explains how to structure and write an effective `component.md` file.

## Purpose of component.md

The `component.md` file serves several important purposes:

1. **Describes functionality**: Details what the component should do
2. **Defines requirements**: Specifies functional requirements in a language-agnostic way
3. **Guides implementation**: Provides enough detail for developers to implement the component
4. **Enables AI understanding**: Written in a way that LLMs can understand and process

## Basic Structure

A well-structured `component.md` file typically includes these sections:

```markdown
# Component Name

## Overview
Brief description of the component's purpose and scope.

## Core Functionality
Detailed description of the main features and capabilities.

## User Interactions
How users interact with the component.

## Data Management
How the component handles data.

## Integration Points
How the component interacts with other components.

## Edge Cases and Error Handling
How the component handles unusual situations and errors.

## Constraints and Limitations
Any known constraints or limitations.

## Examples
Example scenarios to illustrate usage.
```

Let's explore each section in detail.

## Required Sections

### Component Name

Start with a clear, descriptive title that matches your component name in `spec.json`.

```markdown
# User Authentication Component
```

### Overview

Provide a concise summary of what the component does and its purpose in the system.

```markdown
## Overview

The User Authentication Component handles all aspects of user authentication including registration, login, logout, password management, and session handling. It provides secure, reliable authentication services that can be integrated with any application requiring user identity verification.
```

**Best practices**:
- Keep it concise (2-4 sentences)
- Focus on the "what" and "why"
- Mention the primary value the component provides
- Avoid implementation details

### Core Functionality

Detail the main features and capabilities of the component. This is typically the most substantial section.

```markdown
## Core Functionality

### User Registration
- Collect essential user information (email, password, name)
- Validate email format and uniqueness
- Enforce password strength requirements
- Generate and store secure password hashes
- Send verification emails to confirm user identity
- Create new user accounts upon successful verification

### Authentication
- Verify user credentials against stored information
- Generate secure session tokens upon successful authentication
- Implement rate limiting to prevent brute force attacks
- Support remember-me functionality for persistent sessions
- Track login attempts and lock accounts after suspicious activity

### Password Management
- Allow users to reset forgotten passwords
- Enforce password change policies (expiration, history)
- Support secure password updates
- Implement multi-factor authentication options
```

**Best practices**:
- Organize with clear subheadings
- Use bullet points for clarity
- Focus on functional requirements, not implementation
- Be specific about what the component must do
- Include validation and security requirements

## Recommended Sections

### User Interactions

Describe how users interact with the component, including user flows and experience considerations.

```markdown
## User Interactions

### Registration Flow
1. User navigates to registration page
2. User enters email, password, and profile information
3. System validates input in real-time
4. User submits registration form
5. System sends verification email
6. User clicks verification link
7. Account is activated and user is directed to login

### Login Flow
1. User navigates to login page
2. User enters credentials
3. System validates credentials
4. On success, user is redirected to the application
5. On failure, appropriate error message is displayed
```

### Data Management

Explain how the component manages data, including what data is stored and how it's processed.

```markdown
## Data Management

### User Data
The component stores the following user information:
- Unique identifier
- Email address (unique)
- Password hash (never the plain password)
- Account status (active, pending, locked)
- Registration date
- Last login timestamp
- Failed login attempts

### Data Retention
- Active accounts: Data retained until account deletion
- Inactive accounts: Data archived after 12 months of inactivity
- Deleted accounts: Personal data removed, anonymized usage data retained

### Data Security
- All passwords must be hashed using industry-standard algorithms
- Personal information must be encrypted at rest
- Authentication tokens must be securely generated and validated
```

### Integration Points

Describe how the component interacts with other components or systems.

```markdown
## Integration Points

### External Authentication Providers
- Support for OAuth 2.0 integration with major providers
- Standardized interface for adding custom authentication providers
- Mapping between external provider data and internal user model

### Notification System
- Sends registration confirmation emails
- Delivers password reset links
- Alerts users about suspicious login attempts
- Notifies about account changes

### Authorization System
- Provides authenticated user identity to authorization systems
- Supports role-based access control integration
- Maintains user session information for authorization decisions
```

### Edge Cases and Error Handling

Detail how the component should handle unusual situations and errors.

```markdown
## Edge Cases and Error Handling

### Account Recovery
- Process for recovering access when email is inaccessible
- Handling of accounts with suspicious activity
- Procedure for administratively resetting accounts

### Concurrent Sessions
- How to handle multiple simultaneous logins
- Session invalidation across devices
- Conflict resolution for concurrent profile updates

### System Failures
- Behavior during database unavailability
- Handling of email delivery failures
- Fallback authentication methods when primary method fails
```

### Constraints and Limitations

Document any known constraints or limitations of the component.

```markdown
## Constraints and Limitations

- Maximum of 10 failed login attempts before temporary lockout
- Password reset links expire after 24 hours
- Email verification required before full account access
- Session tokens valid for maximum of 30 days
- Username changes limited to once per 30 days
```

### Examples

Provide example scenarios to illustrate how the component should be used.

```markdown
## Examples

### Standard Registration and Login

This example illustrates a typical user registration and login process:

1. New user registers with email: user@example.com
2. System validates email format and confirms it's not already registered
3. System sends verification email to user@example.com
4. User clicks verification link
5. User account is activated
6. User logs in with verified credentials
7. System generates session token and authenticates user

### Password Reset Flow

This example shows the password reset process:

1. User clicks "Forgot Password" link
2. User enters email address
3. System sends password reset link (valid for 24 hours)
4. User clicks link and enters new password
5. System validates password strength
6. System updates password hash and invalidates old sessions
7. User logs in with new password
```

## Optional Sections

### Glossary

Define key terms used throughout the specification.

```markdown
## Glossary

- **Authentication**: The process of verifying a user's identity
- **Authorization**: The process of determining what actions a user can perform
- **Multi-factor Authentication (MFA)**: Authentication using two or more verification methods
- **Session**: A period of interaction between a user and the application
- **Token**: A digital credential used to authenticate a user
```

### Performance Requirements

Specify any performance expectations for the component.

```markdown
## Performance Requirements

- Authentication requests must complete within 500ms under normal load
- System must support at least 100 concurrent authentication requests
- Password hashing must use algorithms that balance security and performance
- Registration process must handle at least 10 new users per second
```

### Compliance Requirements

Document any regulatory or compliance requirements.

```markdown
## Compliance Requirements

- Must comply with GDPR for EU users
- Must support CCPA data deletion requests
- Must maintain audit logs for all authentication events
- Must implement appropriate measures for PII protection
```

## Writing Style Guidelines

To ensure your `component.md` file is effective and useful:

### Be Clear and Specific

```markdown
// Good
The system must validate email addresses using standard format validation and verify uniqueness in the database.

// Not as good
The system should check emails.
```

### Focus on What, Not How

```markdown
// Good
The component must securely store passwords using industry-standard hashing algorithms.

// Not as good
The component must use bcrypt with a work factor of 12 to hash passwords in a PostgreSQL database.
```

### Use Consistent Terminology

```markdown
// Good (consistent use of "user", "authenticate")
Users must authenticate with email and password.
The system validates user credentials.

// Not as good (mixing "user", "account", "login", "authenticate")
Users must login with email and password.
The system checks account credentials.
```

### Use Active Voice

```markdown
// Good
The system sends a verification email.

// Not as good
A verification email is sent by the system.
```

### Organize Hierarchically

Use headings and subheadings to create a clear structure:

```markdown
## Core Functionality

### User Registration
- Feature 1
- Feature 2

### Authentication
- Feature 1
- Feature 2
```

## Complete Example

Here's a simplified example of a complete `component.md` file:

```markdown
# User Authentication Component

## Overview

The User Authentication Component handles all aspects of user authentication including registration, login, logout, password management, and session handling. It provides secure, reliable authentication services that can be integrated with any application requiring user identity verification.

## Core Functionality

### User Registration
- Collect essential user information (email, password, name)
- Validate email format and uniqueness
- Enforce password strength requirements
- Generate and store secure password hashes
- Send verification emails to confirm user identity
- Create new user accounts upon successful verification

### Authentication
- Verify user credentials against stored information
- Generate secure session tokens upon successful authentication
- Implement rate limiting to prevent brute force attacks
- Support remember-me functionality for persistent sessions
- Track login attempts and lock accounts after suspicious activity

### Password Management
- Allow users to reset forgotten passwords
- Enforce password change policies (expiration, history)
- Support secure password updates
- Implement multi-factor authentication options

## User Interactions

### Registration Flow
1. User navigates to registration page
2. User enters email, password, and profile information
3. System validates input in real-time
4. User submits registration form
5. System sends verification email
6. User clicks verification link
7. Account is activated and user is directed to login

### Login Flow
1. User navigates to login page
2. User enters credentials
3. System validates credentials
4. On success, user is redirected to the application
5. On failure, appropriate error message is displayed

## Data Management

### User Data
The component stores the following user information:
- Unique identifier
- Email address (unique)
- Password hash (never the plain password)
- Account status (active, pending, locked)
- Registration date
- Last login timestamp
- Failed login attempts

### Data Security
- All passwords must be hashed using industry-standard algorithms
- Personal information must be encrypted at rest
- Authentication tokens must be securely generated and validated

## Integration Points

### External Authentication Providers
- Support for OAuth 2.0 integration with major providers
- Standardized interface for adding custom authentication providers
- Mapping between external provider data and internal user model

### Notification System
- Sends registration confirmation emails
- Delivers password reset links
- Alerts users about suspicious login attempts

## Edge Cases and Error Handling

### Account Recovery
- Process for recovering access when email is inaccessible
- Handling of accounts with suspicious activity
- Procedure for administratively resetting accounts

### System Failures
- Behavior during database unavailability
- Handling of email delivery failures
- Fallback authentication methods when primary method fails

## Constraints and Limitations

- Maximum of 10 failed login attempts before temporary lockout
- Password reset links expire after 24 hours
- Email verification required before full account access
- Session tokens valid for maximum of 30 days

## Examples

### Standard Registration and Login

This example illustrates a typical user registration and login process:

1. New user registers with email: user@example.com
2. System validates email format and confirms it's not already registered
3. System sends verification email to user@example.com
4. User clicks verification link
5. User account is activated
6. User logs in with verified credentials
7. System generates session token and authenticates user
```

## Best Practices

1. **Be comprehensive**: Cover all aspects of the component's functionality
2. **Stay language-agnostic**: Avoid specifying implementation details
3. **Use clear structure**: Organize with consistent headings and formatting
4. **Include examples**: Provide concrete examples to illustrate functionality
5. **Consider AI readability**: Write in a way that's clear for both humans and LLMs
6. **Focus on requirements**: Describe what the component must do, not how it should do it
7. **Update regularly**: Keep the specification in sync with evolving requirements

## Validating Your component.md

Use the Specky validation tools to check your `component.md` file:

```bash
spm validate --focus=component.md
```

This will check for:
- Required sections
- Consistent structure
- Clarity and completeness
- Language-agnostic descriptions

## Next Steps

Now that you understand how to create an effective `component.md` file, you might want to explore:

- [Datamodel.json Reference](./datamodel-json-reference.md) - Learn how to define data models
- [Gherkin Features Reference](./gherkin-features-reference.md) - Understand how to write feature tests
- [Advanced Component Patterns](./advanced-component-patterns.md) - Explore complex component specifications