# Commands Overview

MeteoritesUltimate provides a comprehensive set of commands for managing meteorite events, guardians, treasures, and plugin settings.

## Base Commands

The plugin uses two base commands:
- `/mu` - Short form (recommended)
- `/meteoritesultimate` - Full form

Both commands work identically. This documentation uses `/mu` for brevity.

## Command Categories

### 🚀 Spawning Commands
Commands for spawning meteorites and testing guardians.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu shoot <type>` | Spawn specific meteorite | `meteoritesultimate.shoot` |
| `/mu shootrandom` | Spawn random meteorite | `meteoritesultimate.shootrandom` |
| `/mu guardian <name>` | Test spawn guardian | `meteoritesultimate.admin` |

### ⚙️ Management Commands  
Commands for controlling meteorite events and plugin behavior.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu start` | Start random meteorite spawning | `meteoritesultimate.start` |
| `/mu stop` | Stop random meteorite spawning | `meteoritesultimate.stop` |
| `/mu interval <seconds>` | Change spawn interval | `meteoritesultimate.admin` |
| `/mu reload [type]` | Reload configuration | `meteoritesultimate.reload` |

### 📊 Information Commands
Commands for viewing statistics, locations, and plugin status.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu` | Show status display | `meteoritesultimate.default` |
| `/mu list` | List active meteorites | `meteoritesultimate.admin` |
| `/mu stats [reset]` | View/reset statistics | `meteoritesultimate.admin` |
| `/mu types` | List meteorite types | `meteoritesultimate.admin` |

### 🧭 Navigation Commands
Commands for teleporting and tracking meteorites.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu tp <nearest\|last>` | Teleport to meteorite | `meteoritesultimate.admin` |
| `/mu compass [type]` | Get tracking compass | `meteoritesultimate.default` |

### 🎮 GUI Commands
Commands for accessing the graphical interface.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu gui` | Open main GUI | `meteoritesultimate.gui.view` |

### 🛠️ Utility Commands
Commands for maintenance and testing.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu clean <radius> [confirm]` | Remove meteorite blocks | `meteoritesultimate.admin` |
| `/mu debug` | Toggle debug mode | `meteoritesultimate.debug` |
| `/mu treasure <type> [info]` | Spawn test treasure | `meteoritesultimate.admin` |
| `/mu clear-invalid` | Clear invalid locations | `meteoritesultimate.admin` |

### ❓ Help Commands
Commands for getting help and information.

| Command | Description | Permission |
|---------|-------------|------------|
| `/mu help [page]` | Show command help | `meteoritesultimate.default` |

## Command Syntax

### Basic Usage
```
/mu <command> [required] [optional]
```

### Common Parameters

**Meteorite Types**: Use the exact name from config (without `_meteorite` suffix)
- `iron`, `diamond`, `netherite`, `sculk`, etc.

**Coordinates**: Support both absolute and relative positioning
- Absolute: `/mu shoot iron 100 64 200`
- Relative: `/mu shoot iron ~ ~10 ~` (10 blocks above current position)

**Player Targeting**: Many commands accept player names
- `/mu shoot iron Tommy` (spawn at Tommy's location)

## Permission Inheritance

MeteoritesUltimate uses a hierarchical permission system:

```yaml
meteoritesultimate.admin:
  # Includes ALL permissions below
  children:
    meteoritesultimate.default: true
    meteoritesultimate.reload: true 
    meteoritesultimate.shoot: true
    meteoritesultimate.shootrandom: true
    meteoritesultimate.start: true
    meteoritesultimate.stop: true
    meteoritesultimate.debug: true
    meteoritesultimate.gui.admin: true
```

## Auto-Complete Support

All commands support tab completion:

- **Command names**: Press Tab after `/mu ` to see available commands
- **Meteorite types**: Press Tab after `/mu shoot ` to see meteorite names  
- **Guardian names**: Press Tab after `/mu guardian ` to see guardian names
- **Player names**: Press Tab in commands that accept player targets

## Status Display

Running `/mu` without arguments shows a comprehensive status display:

```
☄ MeteoritesUltimate v1.0.0

▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬
Next Meteorite: 3m 45s
████████████░░░░░░░░ 60%
Last Type: Diamond Meteorite
▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬

Status: ACTIVE
Active Meteorites: 2
Total Spawned: 156
Guardians Spawned: 89
Treasures Found: 67

Type /mu help for commands
```

## Command Safety

### Confirmation Required

Some commands require confirmation for safety:

```bash
/mu clean 100
# Warning: This will clean meteorites in a 100 block radius.
# Type /mu clean 100 confirm to proceed.

/mu clean 100 confirm
# ✓ Removed 1,247 meteorite blocks in radius 100
```

### Location Validation

Commands that affect world locations include safety checks:
- Coordinate bounds validation
- World existence verification  
- Permission area checking (with Lands/WorldGuard integration)

## Console Usage

Most commands work from the server console:

```bash
# Console commands (require coordinate specification)
mu shoot iron 0 100 0
mu start
mu reload
mu stats

# Player-only commands  
mu tp nearest    # Error: Only players can teleport
mu gui          # Error: This command can only be used by players
```

## Error Handling

Commands provide helpful error messages:

```bash
/mu shoot invalidtype
# Error: Meteorite type 'invalidtype' not found!
# Available types: iron, copper, coal, gold, lapis, diamond, emerald, netherite, end, sculk, prismarine

/mu tp nearest
# Error: No active meteorites!

/mu interval 5
# Error: Interval must be between 10 and 86400 seconds!
```

## Performance Considerations

### Command Frequency
- Avoid rapid-fire `/mu shoot` commands (can cause server lag)
- Use `/mu shootrandom` sparingly in automated systems
- Limit `/mu clean` usage to maintenance windows

### Resource-Intensive Commands
- `/mu clean` with large radius values
- `/mu shoot` with complex meteorite configurations
- `/mu gui` with many players simultaneously

## Next Sections

Explore specific command categories:
- [Admin Commands](admin.md) - Full administrative control
- [Player Commands](player.md) - Commands available to players  
- [Permission Nodes](permissions.md) - Complete permission reference
- [Command Examples](examples.md) - Real-world usage examples