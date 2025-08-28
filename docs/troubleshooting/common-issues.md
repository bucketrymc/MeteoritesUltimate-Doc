# Common Issues & Solutions

This guide covers the most frequently encountered issues with MeteoritesUltimate and their solutions.

## Installation Issues

### ❌ Plugin Not Loading

**Symptoms:**
- Plugin doesn't appear in `/plugins` list
- No startup messages in console
- Commands not recognized

**Common Causes & Solutions:**

**1. Incompatible Server Version**
```
Solution: Ensure you're using Minecraft 1.21+ with compatible server software
✅ Paper (recommended)
✅ Spigot  
✅ Purpur
❌ Craftbukkit (limited compatibility)
```

**2. Corrupted JAR File**
```bash
# Check file integrity
ls -la plugins/MeteoritesUltimate.jar
# Should show reasonable file size (>1MB typically)

# Re-download if size is suspiciously small or 0 bytes
```

**3. Java Version Issues**
```
Error: "Unsupported class file version"
Solution: Upgrade to Java 17+ for Minecraft 1.21
```

**4. File Permission Issues**
```bash
# Linux/Mac: Fix permissions
chmod 644 plugins/MeteoritesUltimate.jar
chown minecraft:minecraft plugins/MeteoritesUltimate.jar

# Windows: Run server as administrator or check file permissions
```

### ❌ Configuration Generation Failure

**Symptoms:**
- Plugin loads but no config.yml created
- Default config missing sections

**Solutions:**

**1. Folder Permission Issues**
```bash
# Create plugin folder manually if needed
mkdir plugins/MeteoritesUltimate
chmod 755 plugins/MeteoritesUltimate

# Generate default config
/mu reload
```

**2. Disk Space Issues**
```bash
# Check available disk space
df -h
# Ensure at least 100MB free for plugin operation
```

## Configuration Issues

### ❌ YAML Syntax Errors

**Symptoms:**
- Plugin fails to load after config changes
- Console shows "YamlException" or parsing errors
- Configuration reverts to defaults

**Common YAML Mistakes:**

**1. Incorrect Indentation**
```yaml
# ❌ Wrong - mixed spaces and tabs
meteorites:
	iron_meteorite:
    enabled: true

# ✅ Correct - consistent 2-space indentation  
meteorites:
  iron_meteorite:
    enabled: true
```

**2. Missing Colons or Spaces**
```yaml
# ❌ Wrong - missing space after colon
enabled:true

# ✅ Correct - space required after colon
enabled: true
```

**3. Incorrect String Formatting**
```yaml
# ❌ Wrong - special characters without quotes
display-name: &6Golden Apple & More

# ✅ Correct - quotes around strings with special chars
display-name: "&6Golden Apple & More"
```

**Quick YAML Validation:**
```bash
# Use online YAML validator or command-line tools
yamllint config.yml  # If available on your system
```

### ❌ Invalid Configuration Values

**Symptoms:**
- Plugin loads but features don't work
- Console warnings about invalid values
- Unexpected behavior

**Common Issues & Solutions:**

**1. Invalid World Names**
```yaml
# ❌ Wrong - world doesn't exist
random-meteorite-world: nonexistent_world

# ✅ Correct - use exact world folder name
random-meteorite-world: world
```

**2. Out-of-Range Values**
```yaml
# ❌ Wrong - values outside valid ranges
meteorite-speed: 50.0          # Max is 5.0
random-meteorite-interval: 5   # Min is 10

# ✅ Correct - within valid ranges  
meteorite-speed: 3.0           # 0.1 - 5.0
random-meteorite-interval: 300 # 10 - 86400
```

**3. Invalid Material Names**
```yaml
# ❌ Wrong - invalid material
core-block:
  INVALID_BLOCK: 100

# ✅ Correct - valid Bukkit material
core-block:
  IRON_BLOCK: 100
```

### ❌ Permission Configuration Issues

**Symptoms:**
- Players can't use commands they should have access to
- "You don't have permission" errors
- GUI not accessible

**Solutions:**

**1. Check Permission Plugin Syntax**
```yaml
# LuckPerms example
/lp user Tommy permission set meteoritesultimate.admin true

# GroupManager example  
/mangaddp Tommy meteoritesultimate.admin

# PermissionsEX example
/pex user Tommy add meteoritesultimate.admin
```

**2. Verify Permission Inheritance**
```yaml
# Ensure parent permissions include children
meteoritesultimate.admin:
  children:
    meteoritesultimate.default: true
    meteoritesultimate.shoot: true
    # ... other permissions
```

**3. Check Default Permissions**
```yaml
# In plugin.yml (automatically configured)
permissions:
  meteoritesultimate.gui.view:
    default: true  # Auto-granted to all players
  meteoritesultimate.admin:
    default: op    # Auto-granted to ops
```

## Gameplay Issues

### ❌ Meteorites Not Spawning

**Symptoms:**
- No automatic meteorite spawning
- Manual spawning works but random doesn't
- No spawn announcements

**Diagnostic Steps:**

**1. Check System Status**
```bash
/mu                    # View status display
/mu start              # Ensure random spawning is active
```

**2. Verify Configuration**
```yaml
# Check these settings
enable-random-meteorites: true     # Must be true
random-meteorite-interval: 300     # Reasonable interval
random-meteorite-world: world      # Valid world name
```

**3. Check Console for Errors**
```
Look for messages like:
[MeteoritesUltimate] World 'worldname' not found
[MeteoritesUltimate] No valid spawn location found
[MeteoritesUltimate] Protected area prevented spawn
```

**Common Solutions:**

**1. World Name Mismatch**
```bash
# List available worlds
/mv list     # If using Multiverse
/worlds      # If available
ls world*/   # Check server folders

# Update config with exact world name
random-meteorite-world: "correct_world_name"
```

**2. Spawn Area Too Restrictive**
```yaml
# Expand spawn boundaries
random-meteorite-min-spawn-x-coord: -2000
random-meteorite-max-spawn-x-coord: 2000
random-meteorite-min-spawn-z-coord: -2000
random-meteorite-max-spawn-z-coord: 2000
```

**3. Protection Plugins Blocking Spawns**
```yaml
# Temporarily disable to test
enable-worldguard-safe-zones: false
enable-griefprevention-safe-zones: false  
enable-lands-safe-zones: false
```

### ❌ Guardians Not Spawning

**Symptoms:**
- Treasures appear but no guardians
- Guardian spawn commands fail
- No guardian death rewards

**Diagnostic Steps:**

**1. Test Guardian Spawning**
```bash
/mu guardian rusty_zombie    # Test specific guardian
/mu debug                    # Enable debug output
```

**2. Check Guardian Configuration**
```yaml
# Ensure guardians are enabled
enable-treasure-guardian: true

# Check individual guardian settings
possible-guardians:
  rusty_zombie:
    enabled: true             # Must be true
    chance: 40               # Reasonable spawn weight
```

**3. Verify Entity Spawning**
```bash
# Check server mob spawning limits
/gamerule doMobSpawning true
/gamerule mobGriefing true   # May affect some guardian features
```

**Common Solutions:**

**1. MythicMobs Integration Issues**
```yaml
# Enable fallback system
mythicmobs-fallback:
  enabled: true

# Check MythicMobs plugin status
/mm mobs list              # List available MythicMobs
/plugins                   # Ensure MythicMobs is loaded
```

**2. Health/Damage Calculation Problems**
```bash
# Console will show debug info like:
[MeteoritesUltimate] Guardian base health: 40
[MeteoritesUltimate] Players nearby: 2
[MeteoritesUltimate] Final health: 96 (40 * 1.2 * 2)
```

**3. Location/Spawn Issues**
```
Error: "Invalid spawn location for guardian"
Solution: Ensure spawn area has sufficient space (3x3x3 minimum)
```

### ❌ Treasure System Problems

**Symptoms:**
- No treasure chests spawning
- Empty treasure chests
- Protection not working

**Common Issues & Solutions:**

**1. Treasure Spawn Configuration**
```yaml
# Check treasure settings
enable-meteorite-treasure: true    # Must be enabled
treasure-spawn-chance: 100.0       # 100% for testing
treasure-spawn-centered: false     # Try both settings
```

**2. Treasure Content Issues**
```yaml
# Ensure treasure items are properly configured
treasure-content:
  meteorite_iron:
    enabled: true                   # Must be enabled
    chance: 60                      # Reasonable weight
    item-type: IRON_INGOT          # Valid material
    amount: 8                       # Valid quantity (1-64)
```

**3. Protection System Problems**
```yaml
# Test different protection modes
treasure-protection:
  type: none        # No protection for testing
  # type: container # Physical barrier
  # type: guardian-lock # Guardian required
  # type: both      # Both protections
```

## Performance Issues

### ❌ Server Lag During Meteorite Events

**Symptoms:**
- TPS drops when meteorites spawn
- Players experience lag during impacts
- Long delays in meteorite physics

**Performance Optimization:**

**1. Reduce Particle Effects**
```yaml
# Lower particle frequency
meteorite-particle-interval: 10    # Higher = less frequent
enable-meteorite-particles: false  # Disable entirely if needed

# Reduce guardian particle effects
persistent-particles:
  enabled: false                    # Disable persistent effects
```

**2. Optimize Spawn Rates**
```yaml
# Increase intervals for large servers
random-meteorite-interval: 600     # 10 minutes instead of 5

# Reduce meteorite complexity
outer-layer-size: 2                # Smaller meteorites
inner-layer-size: 1
```

**3. Faster Cleanup**
```yaml
# More aggressive cleanup
clean-up-meteorite-blocks-interval: 300  # 5 minutes instead of 10
```

**4. Limit Active Meteorites**
```bash
# Regular maintenance
/mu list                           # Check active count
/mu clean 100                      # Clean up if too many (>5)
```

### ❌ Memory Usage Issues

**Symptoms:**
- Gradual memory increase over time
- "Out of memory" errors
- Server crashes during meteorite events

**Memory Management Solutions:**

**1. Regular Cleanup**
```bash
# Weekly maintenance
/mu clear-invalid                  # Remove invalid locations
/mu clean 200 confirm              # Clean old meteorites
/mu stats reset                    # Reset statistics monthly
```

**2. Configuration Optimization**
```yaml
# Reduce memory footprint
debug-mode: false                  # Disable debug logging
meteorite-particle-interval: 5    # Reduce particle frequency
```

**3. Monitor Statistics**
```bash
/mu stats                          # Check for unusual patterns
# Look for:
# - Extremely high spawn counts
# - Rapid increase in guardian spawns
# - Excessive active meteorite locations
```

## Integration Issues

### ❌ PlaceholderAPI Not Working

**Symptoms:**
- Placeholders show as literal text
- Incorrect values in placeholders
- Scoreboards/holograms not updating

**Solutions:**

**1. Verify Installation**
```bash
/plugins                           # Check PlaceholderAPI is loaded
/papi reload                       # Reload PlaceholderAPI
/papi parse me %meteorites_status% # Test placeholder
```

**2. Check Integration Status**
```
Console should show on startup:
[MeteoritesUltimate] ✓ PlaceholderAPI integration enabled!
[MeteoritesUltimate] Available placeholders: next_spawn_seconds, ...
```

**3. Restart Server**
```bash
# Sometimes integration requires full restart
stop
# Start server
/papi list                         # Should show "MeteoritesUltimate" in list
```

### ❌ Protection Plugin Conflicts

**Symptoms:**
- Meteorites spawn in protected areas
- Manual spawning blocked everywhere
- Inconsistent protection behavior

**Solutions:**

**1. Check Integration Status**
```
Console messages on startup:
[MeteoritesUltimate] WorldGuard integration: Enabled
[MeteoritesUltimate] Lands integration: Enabled
```

**2. Test Protection Settings**
```bash
# Test in known protected area
/mu shoot iron_meteorite
# Should see: "Cannot spawn meteorite in protected area!"
```

**3. Review Configuration**
```yaml
# Ensure protection is properly configured
enable-worldguard-safe-zones: true
worldguard-safe-zone-names:
  - spawn          # Must match exact region name
  - safezone       # Case sensitive
```

### ❌ MythicMobs Guardian Issues

**Symptoms:**
- MythicMobs guardians don't spawn
- Fallback to vanilla mobs not working
- Custom skills not functioning

**Solutions:**

**1. Verify MythicMobs Installation**
```bash
/mm version                        # Check MythicMobs version
/mm mobs list                      # List available mobs
/mm mobs info NetheriteOverlord    # Check specific mob exists
```

**2. Test Individual Components**
```bash
/mm mobs spawn NetheriteOverlord 1  # Test MythicMobs directly
/mu guardian netherite_overlord     # Test through MeteoritesUltimate
```

**3. Check Fallback Configuration**
```yaml
# Ensure fallbacks are configured
mythicmobs-fallback:
  enabled: true
  netherite_overlord: netherite_brute  # Valid vanilla guardian
```

## Database/Statistics Issues

### ❌ Statistics Not Saving

**Symptoms:**
- Statistics reset after server restart
- `/mu stats` shows no data
- Statistics not updating

**Solutions:**

**1. Check File Permissions**
```bash
# Ensure plugin can write to its folder
ls -la plugins/MeteoritesUltimate/
chmod 755 plugins/MeteoritesUltimate/
chmod 644 plugins/MeteoritesUltimate/statistics.yml
```

**2. Verify Statistics Database**
```bash
/mu stats                          # Should show current data
# Check for console errors about database access
```

**3. Manual Statistics Reset**
```bash
/mu stats reset                    # Reset and reinitialize
# Plugin will recreate statistics database
```

## Emergency Troubleshooting

### 🚨 Server Crash/Freeze

**If server crashes during meteorite events:**

**1. Immediate Steps**
```bash
# Stop server
pkill java

# Check crash logs  
tail -50 logs/latest.log
tail -50 crash-reports/crash-*.txt
```

**2. Safe Mode Restart**
```bash
# Temporarily disable plugin
mv plugins/MeteoritesUltimate.jar plugins/MeteoritesUltimate.jar.disabled
# Start server to ensure stability
```

**3. Gradual Re-enablement**
```yaml
# Re-enable with minimal configuration
enable-random-meteorites: false
enable-meteorite-particles: false
debug-mode: true
```

### 🚨 Configuration Corruption

**If config becomes corrupted:**

**1. Backup Current Config**
```bash
cp config.yml config-corrupted.yml
```

**2. Restore Default**
```bash
rm config.yml
/mu reload    # Regenerates default config
```

**3. Migrate Settings**
```bash
# Manually copy important settings from backup
# Compare configs and migrate sections carefully
```

## Getting Additional Help

### Information to Collect

When seeking support, provide:

**1. Server Information**
```bash
/version                           # Server version
/plugins                          # Plugin list
java -version                     # Java version
```

**2. Plugin Information**
```bash
/mu                               # Plugin status
/mu debug                         # Enable debug mode
# Reproduce issue and copy console output
```

**3. Configuration**
```yaml
# Share relevant config sections (remove sensitive info)
# Include meteorite and guardian definitions causing issues
```

**4. Error Messages**
```
# Full console error messages
# Any crash reports or stack traces
```

### Support Channels

- **Discord Community**: Real-time help and discussion
- **GitHub Issues**: Bug reports and feature requests  
- **Documentation**: Search existing guides first
- **Server Forums**: Community troubleshooting