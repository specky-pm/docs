---
sidebar_position: 4
---

# Update Specifications

Keeping your specifications up to date is important for maintaining compatibility and getting the latest features. This guide will show you how to update specifications in your Specky projects.

## Why Update Specifications?

Updating specifications helps you:
- Get the latest features and improvements
- Fix bugs and issues in existing specifications
- Maintain compatibility with other components
- Follow evolving best practices and standards

## Checking for Updates

To see if any of your specifications have updates available, use:

```bash
spm outdated
```

This command checks the registry for newer versions of your installed specifications and displays a list of what can be updated:

```
Package               Current    Wanted    Latest    Location
user-component        1.2.0      1.2.3     2.0.0     dependencies
product-component     1.0.0      1.0.5     1.0.5     dependencies
payment-component     2.1.0      2.1.0     3.0.0     dependencies
```

The output shows:
- **Current**: The version you have installed
- **Wanted**: The maximum version that satisfies your version range in spec.json
- **Latest**: The very latest version in the registry
- **Location**: Where the dependency is specified (dependencies or devDependencies)

## Understanding Version Numbers

Specky uses semantic versioning (semver) with three numbers: `MAJOR.MINOR.PATCH`

- **PATCH** (1.0.0 → 1.0.1): Bug fixes and minor improvements
- **MINOR** (1.0.0 → 1.1.0): New features in a backward-compatible manner
- **MAJOR** (1.0.0 → 2.0.0): Breaking changes that might require adjustments

## Basic Update

To update all specifications to their latest compatible versions (based on your spec.json):

```bash
spm update
```

This updates packages within the version constraints in your spec.json file. For example, if you have `"user-component": "^1.2.0"`, it will update to the latest 1.x.x version but not to 2.0.0.

## Updating Specific Specifications

To update a specific specification:

```bash
spm update user-component
```

You can update multiple specifications at once:

```bash
spm update user-component product-component
```

## Updating to Specific Versions

To update to a specific version:

```bash
spm install user-component@1.3.0
```

This replaces your current version with the specified one.

## Updating to Latest Versions

To update a specification to the latest version, even if it's a major version change:

```bash
spm install user-component@latest
```

:::caution
Major version updates may include breaking changes. Always check the changelog or release notes before updating to a major new version.
:::

## Update Strategies

### Safe Updates

For production systems, a conservative approach is best:

```bash
spm update --depth=0
```

This only updates direct dependencies and only within your version constraints.

### Development Updates

During development, you might want to be more aggressive:

```bash
spm update --latest
```

This updates all specifications to their latest versions, regardless of version constraints in your spec.json.

## Handling Breaking Changes

When updating to a new major version:

1. **Read the changelog**: Look for breaking changes
2. **Check the migration guide**: Many specifications provide guides for major updates
3. **Update incrementally**: Update one specification at a time
4. **Validate after updating**: Run `spm validate` to ensure everything still works
5. **Test thoroughly**: Make sure your project still works with the updated specifications

## Updating Your Own Specifications

When updating specifications you've created:

1. Make your changes to the specification
2. Update the version in spec.json following semantic versioning:
   - Increment the patch version for bug fixes
   - Increment the minor version for new features
   - Increment the major version for breaking changes
3. Update the changelog to document your changes
4. Validate the specification: `spm validate`
5. Publish the updated specification: `spm publish`

## Automatic Updates

For projects with many dependencies, you can set up automatic update checks:

```bash
spm outdated --json > outdated.json
```

This outputs the outdated packages in JSON format, which you can use in scripts or CI/CD pipelines.

## Rollback Updates

If an update causes problems, you can roll back to the previous version:

```bash
spm install user-component@1.2.0
```

Replace `1.2.0` with the version you want to roll back to.

## Update Notifications

Specky can notify you about updates when you run commands:

```bash
spm config set update-notifier true
```

With this enabled, Specky will check for updates to your dependencies and notify you when they're available.

## Best Practices for Updates

1. **Update regularly**: Frequent small updates are easier than infrequent large ones
2. **Use version ranges wisely**: 
   - `^1.2.0`: Accept minor and patch updates (recommended for most cases)
   - `~1.2.0`: Accept only patch updates (more conservative)
   - `1.2.0`: Accept no updates (very conservative)
3. **Keep a changelog**: Document what changes in each version of your specifications
4. **Test after updating**: Always validate and test after updating specifications
5. **Update dependencies in batches**: Group related specifications when updating

## Next Steps

Now that you know how to update specifications, you can:
- [Manage configuration](./configuration-management.md) to customize your update preferences
- [Validate your specifications](./validate-specifications.md) after updates
- [Visualize relationships](./visualize-relationships.md) to understand the impact of updates