# PlaceholderAPI Integration

MeteoritesUltimate provides comprehensive PlaceholderAPI integration with 16 unique placeholders that can be used in other plugins like scoreboards, chat formatting, holograms, and more.

## Prerequisites

### Required Plugins
- **PlaceholderAPI** v2.11.x or higher
- **MeteoritesUltimate** v1.0.0 or higher

### Installation
1. Install PlaceholderAPI on your server
2. Install MeteoritesUltimate
3. Restart your server
4. Placeholders are automatically registered

### Verification
Check if placeholders are working:
```bash
/papi parse me %meteorites_status%
# Should return current plugin status
```

## Available Placeholders

### ⏰ Timing & Spawn Information

#### `%meteorites_next_spawn_seconds%`
Returns seconds until next meteorite spawn.
- **Type**: Integer
- **Example**: `245` (4 minutes 5 seconds remaining)
- **Use Case**: Countdown timers in scoreboards

#### `%meteorites_next_spawn_formatted%`
Returns formatted time until next spawn.
- **Type**: String  
- **Example**: `"5m 30s"` or `"2h 15m"`
- **Use Case**: User-friendly time displays

#### `%meteorites_next_spawn_timer%`
Returns time in MM:SS format.
- **Type**: String
- **Example**: `"05:30"` (5 minutes 30 seconds)
- **Use Case**: Digital clock displays

#### `%meteorites_next_spawn_progress%`
Returns spawn progress as percentage (0-100).
- **Type**: Integer
- **Example**: `67` (67% complete)
- **Use Case**: Progress bars and completion tracking

#### `%meteorites_next_spawn_bar%`
Returns visual progress bar with colors.
- **Type**: String
- **Example**: `"████████████░░░░░░░░ 60%"`
- **Use Case**: Visual progress displays in chat/scoreboards

### 📊 Last Meteorite Information

#### `%meteorites_last_type%`
Returns type of last spawned meteorite.
- **Type**: String
- **Example**: `"Diamond Meteorite"` or `"None"`
- **Use Case**: Recent activity displays

#### `%meteorites_last_time%`
Returns time since last meteorite spawned.
- **Type**: String
- **Example**: `"5m 30s ago"` or `"Never"`
- **Use Case**: Activity tracking

### 📈 Statistics

#### `%meteorites_total_spawned%`
Returns total meteorites spawned this session.
- **Type**: Integer
- **Example**: `156`
- **Use Case**: Server statistics, achievements

#### `%meteorites_enabled_count%`
Returns number of enabled meteorite types.
- **Type**: Integer
- **Example**: `11` (all types enabled)
- **Use Case**: Configuration status display

#### `%meteorites_guardian_count%`
Returns number of enabled guardian types.
- **Type**: Integer
- **Example**: `12` (all guardians enabled)
- **Use Case**: Feature availability display

### ⚙️ Configuration Information

#### `%meteorites_spawn_interval%`
Returns configured spawn interval (formatted).
- **Type**: String
- **Example**: `"5m 0s"` (300 seconds)
- **Use Case**: Server settings display

#### `%meteorites_spawn_world%`
Returns configured spawn world name.
- **Type**: String
- **Example**: `"Overworld"` (uses world-names from config)
- **Use Case**: Location information

#### `%meteorites_spawn_height%`
Returns configured spawn height.
- **Type**: Integer
- **Example**: `150`
- **Use Case**: Technical information display

### 🔄 Status Information

#### `%meteorites_is_active%`
Returns whether random spawning is active.
- **Type**: String
- **Values**: `"true"` or `"false"`
- **Use Case**: Conditional displays, API integration

#### `%meteorites_status%`
Returns colored status indicator.
- **Type**: String (with color codes)
- **Examples**: 
  - `"§aSpawning"` (active with green color)
  - `"§cDisabled"` (inactive with red color)
  - `"§eInactive"` (stopped with yellow color)
- **Use Case**: Status displays with color coding

## Usage Examples

### Scoreboard Integration

Using **DeluxeScoreboard** or similar plugins:

```yaml
# scoreboard.yml
lines:
  - "&6&lMETEORITE TRACKER"
  - ""
  - "&7Status: %meteorites_status%"
  - "&7Next Spawn: &f%meteorites_next_spawn_formatted%"
  - "%meteorites_next_spawn_bar%"
  - ""
  - "&7Last Type: &f%meteorites_last_type%"
  - "&7Total Spawned: &f%meteorites_total_spawned%"
```

### Chat Format Integration

Using **ChatFormatter** or similar plugins:

```yaml
# Format with meteorite info in tab list
tab-format: "&7[&6☄&7] &f{player} &8- &7Next: %meteorites_next_spawn_formatted%"

# Chat prefix showing status
chat-format: "%meteorites_status% &7{player}&f: {message}"
```

### Hologram Displays

Using **HolographicDisplays**:

```
/hd create MeteoriteStatus
/hd addline MeteoriteStatus &6&l☄ METEORITE STATUS ☄
/hd addline MeteoriteStatus &7Status: %meteorites_status%
/hd addline MeteoriteStatus &7Next: &f%meteorites_next_spawn_formatted%
/hd addline MeteoriteStatus %meteorites_next_spawn_bar%
/hd addline MeteoriteStatus &7Spawned: &f%meteorites_total_spawned%
```

### Action Bar Updates

Using **ActionBarAPI**:

```yaml
# config.yml
action-bar:
  message: "&6☄ Next meteorite: %meteorites_next_spawn_formatted% %meteorites_next_spawn_bar%"
  interval: 20  # Update every second
```

### Boss Bar Integration

Using **BossBarAPI**:

```yaml
# Display countdown as boss bar
boss-bar:
  title: "&6Next Meteorite: %meteorites_next_spawn_formatted%"
  progress: "%meteorites_next_spawn_progress%"
  color: YELLOW
  style: SOLID
```

## Advanced Usage

### Conditional Displays

Many plugins support conditional placeholder display:

```yaml
# Show different message based on status
conditional-message: 
  - condition: "%meteorites_is_active%" == "true"
    message: "&aMeteorites active! Next: %meteorites_next_spawn_formatted%"
  - condition: "%meteorites_is_active%" == "false"  
    message: "&cMeteorites disabled"
```

### Mathematical Operations

Using **PlaceholderAPI** math expansion:

```yaml
# Calculate minutes until next spawn
minutes-remaining: "%math_{meteorites_next_spawn_seconds}/60%"

# Progress as decimal
progress-decimal: "%math_{meteorites_next_spawn_progress}/100%"
```

### Animation Support

Create animated displays with formatting:

```yaml
# Animated progress bar (using plugin features)
animated-bar:
  frames:
    - "%meteorites_next_spawn_bar%"
    - "§a%meteorites_next_spawn_bar%"
    - "§e%meteorites_next_spawn_bar%"
  interval: 1000  # Change every second
```

## Troubleshooting

### Placeholder Not Working

**Symptoms**: Shows placeholder text instead of values

**Solutions**:
1. Verify PlaceholderAPI is installed and running
2. Check MeteoritesUltimate loaded correctly
3. Test with `/papi parse me %meteorites_status%`
4. Restart server if integration failed

### Incorrect Values

**Symptoms**: Placeholder returns wrong or outdated values

**Solutions**:
1. Ensure random meteorites are properly configured
2. Check if meteorite spawning is active (`/mu start`)
3. Verify configuration reload: `/mu reload`
4. Check console for integration errors

### Performance Issues

**Symptoms**: Server lag when using many placeholders

**Solutions**:
1. Limit placeholder update frequency in other plugins
2. Use caching in scoreboard/hologram plugins
3. Avoid using complex placeholders in high-frequency updates
4. Consider using fewer placeholders simultaneously

## Best Practices

### Performance Optimization
- Use placeholders with appropriate update intervals
- Cache values in plugins that support it
- Avoid using all 16 placeholders simultaneously
- Test performance impact with your player count

### Display Design
- Use color codes for better visual appeal
- Combine multiple placeholders for rich information
- Consider player screen space and readability
- Test displays on different screen resolutions

### Update Intervals
Recommended update frequencies:
- **Status information**: Every 5-10 seconds
- **Countdown timers**: Every 1-2 seconds  
- **Statistics**: Every 30-60 seconds
- **Configuration info**: Static (no updates needed)

## Integration Examples

### Popular Plugin Combinations

#### **DeluxeScoreboard + MeteoritesUltimate**
```yaml
# Perfect for survival servers
scoreboard.yml:
  title: "&6&lSERVER STATUS"
  lines:
    - "&7Meteorite: %meteorites_status%"
    - "&7Next: %meteorites_next_spawn_formatted%"
    - "%meteorites_next_spawn_bar%"
```

#### **TAB + MeteoritesUltimate**  
```yaml
# Great for tab list information
header: |
  &6&l☄ METEORITE SERVER ☄
  &7Status: %meteorites_status%
  &7Next: %meteorites_next_spawn_formatted%
```

#### **ChatFormatter + MeteoritesUltimate**
```yaml
# Add meteorite info to chat
formats:
  default: "&7[%meteorites_status%&7] &f{player}&8: &7{message}"
```

## API Information

### Update Frequency
Placeholders are updated:
- **Every second**: Countdown timers and progress
- **On event**: Status changes, statistics updates
- **On configuration reload**: Settings and counts

### Data Sources
Placeholders pull data from:
- Plugin configuration files
- Runtime statistics tracking
- Integration with PlaceholderAPI core
- Real-time calculation for countdowns

## Support

### Getting Help
- Test placeholders with `/papi parse me %placeholder%`
- Check console for integration errors
- Verify both plugins are latest versions
- Report issues with specific placeholder examples

### Reporting Issues
Include in bug reports:
- PlaceholderAPI version
- MeteoritesUltimate version  
- Specific placeholder not working
- Expected vs actual output
- Console error messages