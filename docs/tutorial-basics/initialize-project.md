---
sidebar_position: 1
---

# Initialize a Specky Project

Getting started with Specky is quick and easy. This guide will walk you through creating your first component specification project.

## What is a Specky Project?

A Specky project is a collection of component specifications that define the functional requirements of your application components. These specifications can be shared, reused, and implemented in any programming language or framework.

## Prerequisites

Before you begin, make sure you have:
- Installed the Specky-Package-Manager (spm) using the instructions in the [Getting Started guide](../intro.md)
- A terminal or command prompt open

## Creating Your First Project

To create a new Specky project, use the `spm init` command:

```bash
spm init my-first-project
```

This command creates a new directory with the name you specified (in this case, "my-first-project") and sets up the basic structure for your Specky project.

Navigate to your new project directory:

```bash
cd my-first-project
```

## Understanding the Project Structure

After initializing a project, you'll see the following structure:

```
my-first-project/
├── spec.json           # Project metadata and dependencies
├── components/         # Directory for your component specifications
└── README.md           # Project documentation
```

### The spec.json File

The `spec.json` file contains metadata about your project and its dependencies. It's similar to a package.json file in npm projects. Here's what a basic spec.json looks like:

```json
{
  "name": "my-first-project",
  "version": "0.1.0",
  "description": "My first Specky project",
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {}
}
```

You can edit this file to add more information about your project.

## Next Steps

Now that you've initialized your Specky project, you're ready to:
- [Create your first component specification](./create-specification.md)
- [Install existing specifications](./install-specifications.md)

:::tip
Use `spm help init` to see all available options for the init command.
:::