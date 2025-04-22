---
sidebar_position: 7
---

# Search for Specifications

Finding the right component specifications for your project is easy with Specky's search capabilities. This guide will show you how to effectively search for and discover specifications in the Specky registry.

## Why Search for Specifications?

Searching for existing specifications allows you to:
- Reuse well-designed components instead of starting from scratch
- Find industry-standard specifications for common functionality
- Discover components that might integrate with your existing specifications
- Learn from how others have structured their specifications

## Basic Search

To search for specifications in the Specky registry, use the `spm search` command followed by your search terms:

```bash
spm search user authentication
```

This returns a list of specifications that match your search terms, showing:
- Specification name
- Latest version
- Description
- Author
- Download count
- Rating

Example output:

```
SEARCH RESULTS FOR "user authentication"

user-auth-component@2.1.0
A comprehensive user authentication component with registration, login, and password reset
by auth-experts (★★★★☆) Downloads: 12.5k

simple-auth@1.3.2
Lightweight authentication component for small applications
by webdev-tools (★★★★★) Downloads: 8.3k

user-management@3.0.1
Complete user management including authentication, profiles, and permissions
by enterprise-specs (★★★★☆) Downloads: 5.7k

Found 15 packages (showing top 3)
```

## Refining Your Search

### Filtering by Tags

You can filter your search results by tags:

```bash
spm search authentication --tag=security
```

This returns only specifications tagged with "security".

### Filtering by Author

To see specifications from a specific author:

```bash
spm search --author=auth-experts
```

### Sorting Results

You can sort search results in different ways:

```bash
spm search authentication --sort=downloads
```

Sorting options include:
- `relevance` (default)
- `downloads` (popularity)
- `recent` (recently updated)
- `rating` (highest rated)

### Limiting Results

To control the number of results displayed:

```bash
spm search authentication --limit=5
```

## Advanced Search

### Using Search Operators

Specky search supports advanced operators:

```bash
spm search "user AND authentication NOT oauth"
```

Supported operators:
- `AND`: Both terms must be present
- `OR`: Either term can be present
- `NOT`: Exclude results with this term
- `"exact phrase"`: Match this exact phrase

### Searching in Specific Fields

You can target your search to specific fields:

```bash
spm search name:auth description:secure
```

Searchable fields include:
- `name`: Specification name
- `description`: Specification description
- `keywords`: Tags and keywords
- `author`: Author name
- `dependencies`: Dependency names

## Viewing Specification Details

Once you've found an interesting specification, you can get more details:

```bash
spm info user-auth-component
```

This shows comprehensive information about the specification:

```
user-auth-component@2.1.0

Description: A comprehensive user authentication component with registration, login, and password reset

Author: auth-experts
License: MIT
Published: 2 months ago
Downloads: 12.5k (last month)
Rating: ★★★★☆ (42 ratings)

Keywords: authentication, user, login, registration, security

Dependencies:
- email-validator@1.2.0
- password-strength@2.0.1

Used by: 342 specifications

Homepage: https://github.com/auth-experts/user-auth-component
```

## Exploring Popular Specifications

To discover popular specifications without a specific search term:

```bash
spm search --sort=downloads --limit=10
```

This shows the top 10 most downloaded specifications.

## Finding Related Specifications

To find specifications related to one you're already using:

```bash
spm related user-auth-component
```

This shows specifications that are often used together with the specified one.

## Searching Locally

To search among your locally installed specifications:

```bash
spm list --search=auth
```

This searches through specifications installed in your current project.

## Browsing Categories

Specky organizes specifications into categories for easier browsing:

```bash
spm browse
```

This opens the Specky registry in your browser, where you can navigate through categories like:
- Authentication & Security
- Data Management
- User Interface
- Communication
- Business Logic

## Search Best Practices

1. **Start broad, then narrow**: Begin with general terms, then add filters
2. **Check ratings and downloads**: Higher numbers usually indicate better quality
3. **Look at dependencies**: Check what other specifications it relies on
4. **Read the documentation**: Always review the component.md before installing
5. **Consider maintenance**: Check when it was last updated

## Finding Specification Examples

To find example implementations of a specification:

```bash
spm examples user-auth-component
```

This shows projects that have implemented the specification in different languages or frameworks.

## Next Steps

Now that you know how to search for specifications, you can:
- [Install specifications](./install-specifications.md) you've found
- [Update specifications](./update-specifications.md) to newer versions
- [Manage configuration](./configuration-management.md) to customize your Specky experience