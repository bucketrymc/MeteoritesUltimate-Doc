# Configuration Overview

MeteoritesUltimate offers extensive configuration options through its `config.yml` file. This section provides a comprehensive guide to customizing every aspect of the plugin.

## Configuration File Structure

The main configuration file is located at:
```
plugins/MeteoritesUltimate/config.yml
```

The configuration is organized into several main sections:

### 📋 Main Sections

1. **[General Settings](#general-settings)** - Basic plugin behavior
2. **[World Configuration](#world-configuration)** - World-specific settings
3. **[Random Meteorites](#random-meteorites)** - Automatic spawning configuration
4. **[Protection Systems](#protection-systems)** - Integration with protection plugins
5. **[Meteorite Definitions](#meteorite-definitions)** - Individual meteorite type configurations
6. **[Guardian Configuration](#guardian-configuration)** - Guardian boss settings
7. **[Treasure System](#treasure-system)** - Treasure generation and protection
8. **[Visual Effects](#visual-effects)** - Particles and visual settings
9. **[Messages](#messages)** - All plugin messages and text
10. **[Statistics](#statistics)** - Data tracking and storage

## General Settings

Basic plugin behavior configuration:

```yaml
# Debug mode - shows additional information in console
debug-mode: false

# Default meteorite speed (0.1 - 5.0)
meteorite-speed: 2.0

# Player scaling for guardians
player-scaling:
  enabled: true
  radius: 50                # Detection radius for nearby players
  health-per-player: 1.2    # 20% more health per player
  damage-per-player: 1.1    # 10% more damage per player  
  max-players: 5            # Cap scaling at 5 players
```

### Debug Mode
Enable debug mode to see detailed console output:
- Meteorite spawn information
- Guardian health calculations
- Performance metrics
- Configuration loading details

### Meteorite Speed
Controls how fast meteorites fall:
- **0.1-1.0**: Slow, dramatic fall
- **1.1-2.5**: Normal speed (recommended)
- **2.6-5.0**: Fast impact

### Player Scaling
Automatically adjusts guardian difficulty based on nearby players:
- **Enabled**: Guardians become stronger with more players nearby
- **Radius**: How far to look for players (blocks)
- **Health/Damage per player**: Multiplier increases per additional player
- **Max players**: Cap scaling to prevent overpowered guardians

## World Configuration

Customize world names and display settings:

```yaml
# World display names in messages
world-names:
  world: "Overworld"
  world_nether: "Nether"
  world_the_end: "End"
  # Add custom world names:
  creative: "Creative World"
  skyblock: "SkyBlock"
```

**Best Practices**:
- Use descriptive names that players will recognize
- Keep names consistent with your server's theme
- Avoid overly long names (they appear in chat messages)

## Random Meteorites

Configure automatic meteorite spawning:

```yaml
enable-random-meteorites: true
random-meteorite-interval: 300      # 5 minutes in seconds
random-meteorite-world: world       # Target world name
random-meteorite-spawn-height: 150  # Height to spawn above ground

# Spawn area boundaries
random-meteorite-min-spawn-x-coord: -1000
random-meteorite-max-spawn-x-coord: 1000
random-meteorite-min-spawn-z-coord: -1000  
random-meteorite-max-spawn-z-coord: 1000
```

### Interval Guidelines

| Server Size | Recommended Interval | Players/Meteorite |
|-------------|---------------------|-------------------|
| Small (1-10) | 180-300 seconds | High frequency |
| Medium (11-30) | 300-600 seconds | Balanced |
| Large (31-50) | 600-900 seconds | Moderate |
| Massive (50+) | 900-1800 seconds | Conservative |

### Spawn Area Configuration
- **Coordinates**: Define rectangular spawn boundaries
- **Height**: Higher values create more dramatic impacts
- **World**: Must match exact world name from your server

## Protection Systems

Integration with protection plugins:

```yaml
# WorldGuard Integration
enable-worldguard-safe-zones: false
worldguard-safe-zone-buffer: 50
worldguard-safe-zone-names:
  - spawn
  - safezone
  
# GriefPrevention Integration  
enable-griefprevention-safe-zones: false
griefprevention-safe-zone-buffer: 50

# Lands Integration
enable-lands-safe-zones: false
lands-safe-zone-buffer: 50
protect-all-lands: false
lands-safe-zone-names:
  - "AdminBase"
  - "SafeZone"
```

### Protection Types

1. **WorldGuard**: Protects regions by name
2. **GriefPrevention**: Protects all claims automatically
3. **Lands**: Advanced protection with permission checking

### Buffer Zones
Buffer zones prevent meteorites from spawning too close to protected areas:
- **Small servers**: 25-50 block buffer
- **Large servers**: 50-100 block buffer

## Configuration Best Practices

### Performance Optimization

```yaml
# For better performance
meteorite-particle-interval: 5     # Reduce particle frequency
clean-up-meteorite-blocks-interval: 600  # More frequent cleanup
debug-mode: false                  # Disable unless troubleshooting
```

### Gameplay Balance

```yaml
# Balanced gameplay settings
random-meteorite-interval: 300     # 5 minute intervals
treasure-spawn-chance: 75.0        # 75% chance for treasure
player-scaling:
  enabled: true                    # Scale difficulty with players
  max-players: 5                   # Prevent extreme scaling
```

### Server Safety

```yaml
# Safety settings
enable-worldguard-safe-zones: true    # Protect important areas
worldguard-safe-zone-names:
  - spawn
  - admin
  - shops
treasure-protection:
  type: both                          # Maximum protection
```

## Configuration Validation

MeteoritesUltimate automatically validates configuration:

### Common Validation Errors
- **Invalid world names**: Must match server worlds exactly
- **Out-of-range values**: Coordinates, percentages, intervals
- **Missing sections**: Required configuration sections
- **Invalid YAML syntax**: Indentation, special characters

### Error Handling
- **Invalid values**: Reset to defaults with console warning
- **Missing sections**: Generated automatically
- **Syntax errors**: Plugin fails to load with detailed error message

## Hot Reloading

Reload configuration without server restart:

```bash
/mu reload           # Reload all configurations
/mu reload config    # Reload basic settings only
/mu reload meteorites # Reload meteorite definitions only
/mu reload guardians # Reload guardian settings only
```

### What Reloads
- ✅ Meteorite spawn chances and settings
- ✅ Guardian health and damage values
- ✅ Protection system settings
- ✅ Message customizations
- ✅ Visual effect settings

### What Requires Restart
- ❌ Database connection changes
- ❌ Integration plugin dependencies
- ❌ Core plugin features enable/disable

## Configuration Backup

**Automatic Backups**: Plugin creates automatic backups:
- `config.yml.backup` - Created before each reload
- Located in plugin folder
- Restore by renaming to `config.yml`

**Manual Backups**: Recommended before major changes:
```bash
# Linux/Mac
cp config.yml config-backup-$(date +%Y%m%d).yml

# Windows
copy config.yml config-backup-20240828.yml
```

## Next Steps

Explore specific configuration areas:
- [Basic Settings](basic-settings.md) - Essential configuration options
- [Meteorite Configuration](meteorites.md) - Detailed meteorite customization
- [Guardian Configuration](guardians.md) - Guardian boss setup
- [Protection Settings](protection.md) - World protection configuration
- [Advanced Options](advanced.md) - Expert-level customization

## Configuration Examples

### Small Creative Server
```yaml
enable-random-meteorites: true
random-meteorite-interval: 120     # 2 minutes - frequent spawning
treasure-spawn-chance: 100.0       # Always spawn treasure
player-scaling:
  enabled: false                   # No scaling needed
enable-worldguard-safe-zones: true # Protect builds
```

### Survival PvP Server
```yaml
enable-random-meteorites: true  
random-meteorite-interval: 600     # 10 minutes - strategic timing
treasure-protection:
  type: both                       # Maximum protection
player-scaling:
  enabled: true
  max-players: 10                  # Higher scaling for PvP
```

### Economy Server
```yaml
treasure-spawn-chance: 50.0        # 50% chance - creates scarcity
guardian-spawn-on-impact: true     # Immediate challenge
treasure-show-coordinates: false   # Hidden treasure locations
```