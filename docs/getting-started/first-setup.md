# First Setup

After installing MeteoritesUltimate, follow this guide to configure the plugin for your server's needs.

## Initial Configuration

### 1. Access the Configuration

The main configuration file is located at:
```
plugins/MeteoritesUltimate/config.yml
```

**Important**: Always stop your server before editing configuration files!

### 2. Basic Settings

Configure these essential settings first:

```yaml
# Enable/disable debug information
debug-mode: false

# Default meteorite falling speed (0.1 - 5.0)
meteorite-speed: 2.0

# Random meteorite spawning
enable-random-meteorites: true
random-meteorite-interval: 300  # 5 minutes in seconds
random-meteorite-world: world   # Your main world name
```

### 3. World Configuration

Update world settings to match your server:

```yaml
# Customize world display names in messages
world-names:
  world: "Overworld"
  world_nether: "Nether" 
  world_the_end: "End"
  # Add your custom worlds:
  # skyworld: "Sky Dimension"
  # creative: "Creative World"

# Random meteorite spawn area
random-meteorite-spawn-height: 150
random-meteorite-min-spawn-x-coord: -1000
random-meteorite-max-spawn-x-coord: 1000  
random-meteorite-min-spawn-z-coord: -1000
random-meteorite-max-spawn-z-coord: 1000
```

## Feature Configuration

### Enable Core Features

Choose which features to enable:

```yaml
# Treasure system
enable-meteorite-treasure: true
treasure-spawn-chance: 100.0

# Guardian protection
enable-treasure-guardian: true

# Visual effects
enable-meteorite-particles: true
meteorite-particle-interval: 2

# Show treasure coordinates in chat
treasure-show-coordinates: true
```

### Configure Protection

Set up protection systems based on your server's needs:

```yaml
# Global treasure protection (can be overridden per meteorite)
treasure-protection:
  type: none  # Options: none, container, guardian-lock, both
```

Available protection types:
- **none**: No protection
- **container**: Physical barrier around treasure
- **guardian-lock**: Must defeat guardian to access treasure  
- **both**: Both container and guardian protection

## Permission Setup

### Basic Permission Structure

Grant permissions based on roles:

```yaml
# For server administrators
meteoritesultimate.admin:
  description: Full access to all features
  default: op
  children:
    meteoritesultimate.shoot: true
    meteoritesultimate.reload: true
    meteoritesultimate.gui.admin: true

# For players
meteoritesultimate.default:
  description: Basic player access
  default: true
  children:
    meteoritesultimate.gui.view: true
    meteoritesultimate.gui.stats: true
```

### Essential Permissions

**For Admins**:
- `meteoritesultimate.admin` - Full access
- `meteoritesultimate.gui.admin` - Full GUI access

**For Moderators**:
- `meteoritesultimate.shoot` - Spawn meteorites manually
- `meteoritesultimate.start` / `meteoritesultimate.stop` - Control random spawning

**For Players**:
- `meteoritesultimate.gui.view` - View GUIs (auto-granted)
- `meteoritesultimate.gui.stats` - View statistics

## Integration Setup

### WorldGuard Integration

If you use WorldGuard:

```yaml
enable-worldguard-safe-zones: true
worldguard-safe-zone-buffer: 50
worldguard-safe-zone-names:
  - spawn
  - safezone
  - protected
```

### Lands Integration

If you use Lands:

```yaml
enable-lands-safe-zones: true  
lands-safe-zone-buffer: 50
protect-all-lands: false  # Set true to protect all claims
lands-safe-zone-names:    # Specifically protected lands
  - "AdminBase"
  - "SafeZone"
```

### PlaceholderAPI Setup

MeteoritesUltimate provides 16 placeholders automatically when PlaceholderAPI is installed:

- `%meteorites_next_spawn_formatted%` - Time until next meteorite
- `%meteorites_status%` - Current plugin status  
- `%meteorites_total_spawned%` - Total meteorites spawned
- And 13 more! See [PlaceholderAPI Integration](../integrations/placeholderapi.md)

## Testing Your Setup

### 1. Test Basic Functionality

Start your server and run:

```
/mu
```

You should see the status display with:
- Plugin version
- Current settings
- Active meteorites count

### 2. Test Manual Spawning

Spawn a test meteorite:

```
/mu shoot iron_meteorite
```

This will spawn an iron meteorite at your target location.

### 3. Test Random Spawning

Enable automatic spawning:

```
/mu start
```

Meteorites will now spawn automatically based on your interval setting.

### 4. Access the GUI

Open the management interface:

```
/mu gui
```

Navigate through the menus to familiarize yourself with the interface.

## Initial Customization

### Adjust Meteorite Rarities

Modify spawn chances in `config.yml`:

```yaml
meteorites:
  iron_meteorite:
    chance: 22  # 22% chance
  diamond_meteorite:
    chance: 8   # 8% chance
  sculk_meteorite:
    chance: 2   # 2% chance (rare)
```

### Configure Guardian Difficulty

Adjust guardian health and damage:

```yaml
possible-guardians:
  rusty_zombie:
    guardian-health: 40        # Lower for easier fights
    guardian-attack-damage: 6
  sculk_warden:
    guardian-health: 500       # Higher for boss fights
    guardian-attack-damage: 45
```

## Performance Optimization

### For Large Servers

```yaml
# Reduce particle intensity
meteorite-particle-interval: 5  # Default: 2

# Increase cleanup intervals  
clean-up-meteorite-blocks-interval: 1200  # 20 minutes

# Limit protection checks
treasure-protection:
  type: guardian-lock  # Less resource intensive than container
```

### For Small Servers

```yaml
# Increase visual effects
meteorite-particle-interval: 1

# More frequent spawning
random-meteorite-interval: 180  # 3 minutes

# Full protection
treasure-protection:
  type: both
```

## Common First-Setup Issues

### Meteorites Not Spawning

**Check**:
1. `enable-random-meteorites: true`
2. World name matches your server world
3. `/mu start` has been run
4. No console errors

### Permission Errors

**Solutions**:
1. Grant yourself `meteoritesultimate.admin`
2. Check permission plugin syntax
3. Reload permissions or restart server

### GUI Not Opening

**Check**:
1. Player has `meteoritesultimate.gui.view` permission
2. No console errors when using `/mu gui`
3. Server memory isn't exhausted

## Next Steps

Once basic setup is complete:

1. [Customize meteorite types](../configuration/meteorites.md)
2. [Configure guardians](../configuration/guardians.md)  
3. [Set up treasures](../configuration/treasures.md)
4. [Configure integrations](../integrations/overview.md)
5. [Learn all commands](../commands/overview.md)

## Getting Help

Need assistance with setup?

- Check the [Configuration Reference](../reference/config-reference.md)
- Review [Common Issues](../troubleshooting/common-issues.md)
- Join our Discord community
- Create an issue on GitHub