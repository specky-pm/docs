---
sidebar_position: 1
---

# Getting Started with Specky

Let's discover **Specky-Package-Manager (spm) in less than 5 minutes**.

## What is Specky?

Specky is a tool for creating, sharing, and downloading component specifications to be used when building applications. In this new age of AI-driven agentic coding, requirements are more important than ever. Specky helps developers share component specifications, just like they do with libraries.

## What you'll need

- Basic understanding of component-based architecture
- Familiarity with command-line tools
- A terminal or command prompt

## Install Specky

The Specky-Package-Manager (spm) is a standalone CLI tool that can be installed using various package managers.

### macOS (using Homebrew)

```bash
brew install spm
```

### Linux/Windows

// FIXME
Download the appropriate binary for your system from the [official Specky releases page](https://github.com/specky/releases).

You can verify the installation by running:

```bash
spm --version
```

## Initialize a new component specification

Create a new component specification project using the init command:

```bash
spm init my-component
cd my-component
```

The `spm init` command creates a basic directory structure with template files:
- spec.json: contains metadata about the component
- component.md: describes the component in detail
- datamodel.json (optional): models any entities the component may rely on
- features/ directory: for gherkin feature specifications

## Working with specifications

### Install dependencies

If your component specification depends on other specifications, you can install them:

```bash
spm install user-component --save
```

### Validate your specification

Ensure your specification is valid:

```bash
spm validate
```

### Visualize component relationships

See how your component relates to others:

```bash
spm viz --format=svg
```

### Test your specification

Run tests for your component specification:

```bash
spm test
```

### Generate documentation

Create documentation from your specification:

```bash
spm docs
```

## Next Steps

Now that you've created your first component specification, you can:
- Learn more about [Component Specs](../component-specs) // FIXME 
- Explore the [Specky Commands](../specky-commands) // FIXME 
- Check out [Best Practices](../best-practices) for creating specifications // FIXME
