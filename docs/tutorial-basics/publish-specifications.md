---
sidebar_position: 5
---

# Publish Specifications

Once you've created and validated your component specifications, you can share them with the community by publishing them to the Specky registry. This guide will walk you through the process of publishing your specifications.

## Why Publish Specifications?

Publishing your specifications allows:
- Other developers to discover and use your work
- Collaboration on component requirements
- Standardization of common components
- Building a portfolio of your specification work

## Prerequisites for Publishing

Before publishing, make sure:
1. You have [created a specification](./create-specification.md)
2. Your specification has been [validated](./validate-specifications.md) and is error-free
3. You have a Specky account (see below)

## Creating a Specky Account

To publish specifications, you need a Specky account:

```bash
spm login
```

This will prompt you to enter your username and password, or create a new account if you don't have one.

## Preparing Your Specification for Publication

### Update Metadata

Ensure your `spec.json` file contains accurate and complete information:

```json
{
  "name": "user-component",
  "version": "1.0.0",
  "description": "A comprehensive user management component",
  "author": "Your Name",
  "license": "MIT",
  "keywords": ["user", "authentication", "registration"],
  "repository": {
    "type": "git",
    "url": "https://github.com/yourusername/user-component"
  }
}
```

Important fields include:
- `name`: A unique name for your specification
- `version`: Following semantic versioning (major.minor.patch)
- `description`: A clear, concise description
- `keywords`: Terms that help others find your specification
- `license`: The license under which you're sharing your work

### Create a README

While not required, it's good practice to include a README.md file in your specification with:
- An overview of the component
- Examples of how to use the specification
- Any special considerations
- Contact information for questions or contributions

## Publishing Your Specification

Once your specification is ready, you can publish it with:

```bash
spm publish
```

This command:
1. Performs a final validation
2. Packages your specification
3. Uploads it to the Specky registry
4. Makes it available for others to install

### Publishing Options

The `spm publish` command has several useful options:

#### Access Control

By default, specifications are published with public access. For private specifications:

```bash
spm publish --access=restricted
```

:::note
Private specifications require a paid Specky account.
:::

#### Tags

You can publish with specific tags:

```bash
spm publish --tag=beta
```

Common tags include:
- `latest` (default)
- `beta`
- `alpha`
- `next`

This allows users to install specific versions:

```bash
spm install user-component@beta
```

#### Dry Run

To see what would happen without actually publishing:

```bash
spm publish --dry-run
```

This is useful for checking what files would be included in your package.

## Managing Published Specifications

### Listing Your Publications

To see all specifications you've published:

```bash
spm profile
```

### Updating a Published Specification

To update a published specification:

1. Make your changes
2. Update the version in `spec.json` following semantic versioning:
   - Increment the patch version (1.0.0 → 1.0.1) for bug fixes
   - Increment the minor version (1.0.0 → 1.1.0) for new features
   - Increment the major version (1.0.0 → 2.0.0) for breaking changes
3. Publish again:

```bash
spm publish
```

### Deprecating a Specification

If a specification is no longer maintained or has been replaced:

```bash
spm deprecate user-component "Use auth-component instead"
```

### Removing a Specification

In rare cases, you might need to remove a specification completely:

```bash
spm unpublish user-component
```

:::warning
Unpublishing should be used sparingly, as it can break projects that depend on your specification. It's usually better to deprecate instead.
:::

## Best Practices for Publishing

1. **Validate thoroughly**: Always validate before publishing
2. **Follow semantic versioning**: Use version numbers meaningfully
3. **Write clear documentation**: Help others understand your specification
4. **Be responsive**: Monitor issues and questions about your specifications
5. **Consider backwards compatibility**: Try not to break existing users

## Specification Visibility

Specifications can have different visibility levels:

- **Public**: Available to everyone (default)
- **Restricted**: Available only to you and specified collaborators
- **Organization**: Available to members of your organization

To publish to an organization:

```bash
spm publish --access=public --scope=@your-org
```

## Next Steps

Now that you've published your specification, you can:
- [Search for other specifications](./search-specifications.md) to use in your projects
- [Visualize relationships](./visualize-relationships.md) between your components
- [Update your specifications](./update-specifications.md) as requirements evolve