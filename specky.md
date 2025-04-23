# Introduction

In this new age of AI driven agentic coding, requirements are more important than ever. But writing good requirements is time consuming and, for those who are not subject matter experts, extremely difficult, requiring a lot of research and learning, before specification can begin! There needs to be a way for developers to share component specifications, just like they do with libraries. That's where Specky comes in.

Specky is a tool for creating, sharing and downloading component specifications to be used when building applications. The Specky-Package-Manager (spm) is a command line tool that enables developers to easily work with 3rd party specifications as if they were project dependencies. It works in a similar way to NPM and we've copied a lot of NPM features to make it easy for developers to get up and running. If you've used NPM, you'll find a lot of the tools and processes very familiar.

# Component Specs

At the core of Specky you'll find **component specifications**. When we say **component** we're refering to an application component for example the "user component" or "customer component", that represents all the functionality belonging to those concepts.

## What's in a Component Spec?

Component specs should ONLY contain functional requirements. Why? See the next section for an explanation.

Component specs contain the following assets:
- spec.json: contains metadata about the component such as name, version, author, license etc.
- datamodel.json (optional): models any entities that the component may rely on
- component.md: describes the component in detail so that an LLM can understand it's purpose and how it functions
- features/*.feature (optional): gherkin feature specifications that outline tests to verify the component is working correctly

## What's not in Component Spec?

Your component spec should not depend on any specific:
- programming language e.g. Python, Java, Go, Rust
- programming framework or library e.g. Spring, NextJS, Rails
- deployment environment e.g. AWS, Azure
- tools like Databases (e.g. MongoDB, Postgres), Communication protocols (REST, gRPC),

Why? Because architecture choices may differ, depending on non-functional requirements and business or technical constraints. One developer might be building a hobby project and is fine with using python to implement their project. Another developer might be building a high-performance application and wants to use Rust. If you make architectural choices for your users, you're limiting who can use your specification.

Do NOT include implementation logic in your specification. If you want to share an implementation, create and share a library! In the case of requirements, we're only concerned with what should happen, not how. By prescribing how a specific feature is to be implemented, you're again limiting the usefulness of your specification. It might make sense to describe how to implement some feature in a low level language like C, but that function may already exist in python.

The goal here is to maximise the usefulness of requirements so that they can be applied in as many areas as possible. A well written specification can be just as easily implemented as a REST API, a User Interface or a function library.

# Specky Commands

The Specky-Package-Manager CLI (spm) has the following commands. You will find these very similar to NPM.

`spm app [name]` - Initialize a new Spekcy project. Creates a basic directory structure with template files.

`spm install [spec]` - Download and install a component specification from the registry. Alias: `spm i`
  - `spm install [spec]@[version]` - Install a specific version of a component specification
  - `spm install [spec] --save` - Install and add to dependencies in spec.json
  - `spm install --production` - Install only production dependencies

`spm uninstall [spec]` - Remove a component specification. Alias: `spm un`, `spm remove`

`spm update [spec]` - Update a component specification to the latest version

`spm list` - List installed component specifications. Alias: `spm ls`
  - `spm list --depth=0` - Show only top-level specifications
  - `spm list --json` - Output in JSON format

`spm search [query]` - Search for component specifications in the registry

`spm publish` - Publish a component specification to the registry
  - `spm publish --access=public` - Publish with public access
  - `spm publish --tag=[tag]` - Publish with a specific tag

`spm pack` - Create a tarball from a component specification

`spm version [major|minor|patch]` - Increment the version of a component specification

`spm validate` - Validate the current component specification against schema
  - `spm validate --fix` - Attempt to fix validation issues automatically
  - `spm validate --strict` - Enforce stricter validation rules

`spm test` - Run tests for the component specification using the features/*.feature files

`spm docs` - Generate documentation from the component specification

`spm viz` - Visualize component relationships and dependencies
  - `spm viz --format=svg` - Output visualization in SVG format
  - `spm viz --depth=2` - Limit visualization to specified depth
  - `spm viz --focus=[component]` - Focus visualization on a specific component

`spm link` - Create a symbolic link to a component specification for local development

`spm audit` - Check for issues in component specifications

`spm deprecate [spec][@version] [message]` - Deprecate a component specification version

`spm help [command]` - Display help information for a command

