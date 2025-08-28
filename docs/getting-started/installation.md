# Installation

## System Requirements

Before installing MeteoritesUltimate, ensure your server meets these requirements:

### Server Requirements
- **Minecraft Version**: 1.21 or higher
- **Server Software**: Spigot, Paper, or compatible fork
- **Java Version**: Java 17 or higher
- **RAM**: At least 2GB free (recommended 4GB+ for optimal performance)
- **Storage**: 50MB+ free space for plugin files and data

### Supported Platforms
- ✅ Paper (Recommended)
- ✅ Spigot
- ✅ Purpur
- ✅ Other Paper/Spigot forks

## Installation Steps

### 1. Download the Plugin

1. Download the latest `MeteoritesUltimate.jar` file
2. Verify the file is not corrupted (check file size and hash if provided)

### 2. Install the Plugin

1. **Stop your server** if it's currently running
2. Navigate to your server's `plugins` folder
3. **Copy** `MeteoritesUltimate.jar` into the `plugins` folder
4. **Start your server**

### 3. Initial Setup

When you start your server for the first time with MeteoritesUltimate:

1. The plugin will create a `MeteoritesUltimate` folder in your `plugins` directory
2. A default `config.yml` file will be generated
3. You'll see startup messages in your console indicating successful initialization

### 4. Verify Installation

Check that the plugin loaded correctly:

```
/mu
```

You should see the MeteoritesUltimate status display showing:
- Plugin version (v1.0.0)
- Current settings
- Available commands

## Post-Installation

### Set Permissions

Configure permissions for your staff and players. See [Permission Nodes](../commands/permissions.md) for details.

Basic permission setup:
```yaml
# For administrators
- meteoritesultimate.admin
- meteoritesultimate.gui.admin

# For moderators  
- meteoritesultimate.shoot
- meteoritesultimate.start
- meteoritesultimate.stop

# For players (auto-granted)
- meteoritesultimate.gui.view
- meteoritesultimate.gui.stats
```

### Configure Basic Settings

Edit the `config.yml` file to customize:
- Random meteorite spawning intervals
- World settings
- Enable/disable features
- Protection integrations

See [First Setup](first-setup.md) for detailed configuration guidance.

## Common Installation Issues

### Plugin Not Loading

**Symptom**: Plugin doesn't appear in `/plugins` list

**Solutions**:
1. Check server console for error messages
2. Verify you're using a compatible server version (1.21+)
3. Ensure the JAR file is not corrupted
4. Check server has sufficient permissions to read plugin files

### Permission Errors

**Symptom**: "You don't have permission" messages

**Solutions**:
1. Grant yourself `meteoritesultimate.admin` permission
2. Check your permission plugin configuration
3. Ensure permissions are properly applied after granting

### Configuration Errors

**Symptom**: Plugin reports configuration warnings or errors

**Solutions**:
1. Delete `config.yml` to regenerate defaults
2. Check YAML syntax (indentation, special characters)
3. Review console messages for specific error details

### Memory Issues

**Symptom**: Server lag or out of memory errors

**Solutions**:
1. Allocate more RAM to your server
2. Reduce meteorite spawn frequency
3. Lower particle effect intensity
4. Disable unused features

## Next Steps

Once installed successfully:

1. [Complete the first setup](first-setup.md)
2. [Configure basic settings](../configuration/basic-settings.md)
3. [Set up permissions](../commands/permissions.md)
4. [Test with the quick start guide](quick-start.md)

## Getting Help

If you encounter issues during installation:

- Check the [Troubleshooting Guide](../troubleshooting/common-issues.md)
- Review server console logs for error messages
- Join our Discord community for support
- Report bugs on our GitHub repository