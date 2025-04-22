---
sidebar_position: 9
---

# Configuration Management

Specky offers various configuration options to customize its behavior to your needs. This guide will show you how to manage Specky configuration settings for both your user profile and individual projects.

## Why Configure Specky?

Configuring Specky allows you to:
- Customize default behaviors
- Set up authentication for publishing
- Define project-specific settings
- Optimize performance for your environment
- Integrate with your workflow and tools

## Configuration Levels

Specky has three levels of configuration, in order of precedence:

1. **Command-line options**: Highest priority, applies only to the current command
2. **Project configuration**: Stored in `.speckyrc` or `spec.json` in your project
3. **User configuration**: Stored in `~/.speckyrc` or `~/.config/specky/config`

Settings at a higher level override those at lower levels.

## Viewing Current Configuration

To see your current configuration settings:

```bash
spm config list
```

This shows all settings from all configuration levels, with information about where each setting is defined.

## Setting Configuration Values

### Basic Configuration

To set a configuration value:

```bash
spm config set registry https://registry.specky.dev
```

This sets the `registry` setting to the specified URL.

### Project vs. User Configuration

By default, `spm config set` changes your user configuration. To set a project-specific configuration:

```bash
spm config set registry https://registry.specky.dev --location=project
```

To explicitly set a user configuration:

```bash
spm config set registry https://registry.specky.dev --location=user
```

### Removing Configuration Values

To remove a configuration value:

```bash
spm config delete registry
```

## Common Configuration Settings

### Registry Settings

```bash
# Set the registry URL
spm config set registry https://registry.specky.dev

# Set authentication for the registry
spm config set //registry.specky.dev/:_authToken YOUR_AUTH_TOKEN
```

### Default Settings

```bash
# Set default author information
spm config set init.author.name "Your Name"
spm config set init.author.email "your.email@example.com"
spm config set init.author.url "https://your-website.com"
spm config set init.license "MIT"

# Set default version when creating new specifications
spm config set init.version "0.1.0"
```

### Proxy Settings

```bash
# Set HTTP proxy
spm config set proxy http://proxy.example.com:8080

# Set HTTPS proxy
spm config set https-proxy http://proxy.example.com:8080
```

### Cache Settings

```bash
# Set cache location
spm config set cache /path/to/custom/cache

# Set cache expiration (in seconds)
spm config set cache-max 86400

# Clear the cache
spm cache clean
```

## Configuration File Format

You can also edit configuration files directly. They use JSON format:

### User Configuration (~/.speckyrc)

```json
{
  "registry": "https://registry.specky.dev",
  "init": {
    "author": {
      "name": "Your Name",
      "email": "your.email@example.com",
      "url": "https://your-website.com"
    },
    "license": "MIT",
    "version": "0.1.0"
  },
  "save-exact": false,
  "color": true
}
```

### Project Configuration (.speckyrc in project root)

```json
{
  "registry": "https://company-registry.example.com",
  "save-exact": true,
  "strict-validation": true
}
```

## Environment Variables

You can also use environment variables to configure Specky. These take precedence over configuration files:

```bash
# Set the registry URL
export SPECKY_REGISTRY=https://registry.specky.dev

# Set authentication token
export SPECKY_AUTH_TOKEN=your-auth-token

# Run a command using these settings
spm install user-component
```

Common environment variables:
- `SPECKY_REGISTRY`: Registry URL
- `SPECKY_AUTH_TOKEN`: Authentication token
- `SPECKY_PROXY`: HTTP proxy
- `SPECKY_HTTPS_PROXY`: HTTPS proxy
- `SPECKY_CACHE`: Cache directory
- `SPECKY_COLOR`: Enable/disable color output (true/false)

## Project-Specific Configuration

You can add Specky configuration directly to your `spec.json` file under the `specky` key:

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "My Specky project",
  "specky": {
    "registry": "https://registry.specky.dev",
    "save-exact": true,
    "strict-validation": true
  }
}
```

## Configuration Profiles

For different environments or workflows, you can use configuration profiles:

```bash
# Create a profile
spm config set --profile=work registry https://work-registry.example.com

# Use a profile for a command
spm --profile=work install user-component
```

## Validation Configuration

You can customize validation behavior:

```bash
# Set strict validation by default
spm config set strict-validation true

# Configure which validators to use
spm config set validators.datamodel true
spm config set validators.features false
```

## Visualization Configuration

Customize visualization defaults:

```bash
# Set default visualization format
spm config set viz.format svg

# Set default visualization theme
spm config set viz.theme dark

# Set default visualization depth
spm config set viz.depth 2
```

## Security Configuration

Configure security-related settings:

```bash
# Enable audit checks on install
spm config set audit true

# Set minimum acceptable specification rating
spm config set min-rating 3
```

## Sharing Configuration

For team projects, you can share configuration:

1. Create a `.speckyrc` file in your project
2. Add it to version control
3. Document any required user-level configuration

## Best Practices for Configuration

1. **Use project configuration** for project-specific settings
2. **Use user configuration** for personal preferences
3. **Document required configuration** in your README
4. **Version control project configuration** but not user configuration
5. **Use profiles** for different environments (work, personal, etc.)

## Troubleshooting Configuration

If you encounter issues with configuration:

1. Check which configuration is being used: `spm config list`
2. Temporarily override with command-line options
3. Reset to defaults: `spm config reset`
4. Check for environment variables that might be overriding settings

## Next Steps

Now that you know how to configure Specky, you can:
- Customize your Specky environment to match your workflow
- Set up project-specific configurations for your team
- Explore advanced features enabled through configuration