---
sidebar_position: 2
---

# Install and Manage Specifications

One of the key benefits of Specky is the ability to reuse component specifications across projects. This guide will show you how to install and manage specifications from the Specky registry.

## Understanding Dependencies

In Specky, dependencies are other component specifications that your project relies on. For example, if you're building an e-commerce application, you might depend on a "product-component" and a "shopping-cart-component".

## Installing Specifications

### Basic Installation

To install a specification from the Specky registry, use the `spm install` command followed by the specification name:

```bash
spm install product-component
```

This command downloads the latest version of the "product-component" specification and adds it to your project.

### Installing a Specific Version

If you need a specific version of a specification, you can specify it using the `@` symbol:

```bash
spm install product-component@1.2.0
```

### Installing Multiple Specifications

You can install multiple specifications at once by listing them:

```bash
spm install product-component shopping-cart-component user-component
```

### Saving Dependencies

By default, installed specifications are added to your project's `spec.json` file as dependencies. You can see this in the `dependencies` section:

```json
{
  "name": "my-ecommerce-app",
  "version": "0.1.0",
  "description": "E-commerce application",
  "dependencies": {
    "product-component": "^1.2.0",
    "shopping-cart-component": "^2.0.0",
    "user-component": "^1.0.0"
  }
}
```

### Installation Options

The `spm install` command has several useful options:

- `--save` or `-S`: Add the specification to dependencies (default)
- `--no-save`: Install without adding to dependencies
- `--exact` or `-E`: Install the exact version (without ^ or ~ version range)

Example:

```bash
spm install product-component --save --exact
```

This installs the product-component as a dependency with an exact version.

## Listing Installed Specifications

To see what specifications are installed in your project, use the `spm list` command:

```bash
spm list
```

This displays a tree of all installed specifications and their dependencies.

To show only the top-level specifications (without their dependencies), use:

```bash
spm list --depth=0
```

## Removing Specifications

To remove a specification from your project, use the `spm uninstall` command:

```bash
spm uninstall product-component
```

This removes the specification from your project and updates the `spec.json` file.

## Understanding Version Ranges

Specky uses semantic versioning (semver) similar to npm. In your `spec.json` file, you might see version numbers with special characters:

- `^1.2.0`: Compatible with 1.2.0 up to (but not including) 2.0.0
- `~1.2.0`: Compatible with 1.2.0 up to (but not including) 1.3.0
- `1.2.0`: Exactly version 1.2.0
- `*` or `latest`: The latest version available

## Installing from spec.json

If you clone a project that already has a `spec.json` file with dependencies, you can install all the dependencies at once by running:

```bash
spm install
```

This reads the `spec.json` file and installs all the specifications listed in the dependencies.

## Working with Local Specifications

### Linking Local Specifications

// FIXME: do we really need this feature?

During development, you might want to work on multiple specifications at the same time. You can use the `spm link` command to create symbolic links between projects:

1. In the directory of the specification you want to link:

```bash
spm link
```

2. In the project where you want to use the linked specification:

```bash
spm link specification-name
```

This creates a symbolic link instead of installing from the registry, allowing you to make changes to the specification and immediately see the effects in your project.

## Best Practices for Managing Dependencies

1. **Keep dependencies up to date**: Regularly update your dependencies to get the latest features and bug fixes.
2. **Use version ranges wisely**: Use `^` for most dependencies to get compatible updates, but use exact versions for critical dependencies.
3. **Document dependencies**: Include information about key dependencies in your README.md file.
4. **Audit dependencies**: Regularly run `spm audit` to check for issues in your dependencies.

## Next Steps

Now that you know how to install and manage specifications, you can:
- [Update your specifications](./update-specifications.md)
- [Search for specifications](./search-specifications.md) in the registry
- [Validate your specifications](../creating-component-specs/validate-specifications)