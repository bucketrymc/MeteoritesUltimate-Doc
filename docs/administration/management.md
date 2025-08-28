# Server Management

This guide covers essential server management tasks for MeteoritesUltimate administrators, including monitoring, maintenance, and optimization.

## Daily Management Tasks

### 📊 Status Monitoring

Check plugin status regularly:

```bash
/mu                    # View general status
/mu stats              # View detailed statistics  
/mu list               # List active meteorites
/mu types              # Check meteorite configuration
```

**Key Metrics to Monitor**:
- Active meteorite count (should be reasonable)
- Total spawned vs server uptime ratio
- Guardian spawn success rate
- Treasure discovery frequency

### 🧹 Maintenance Commands

Regular cleanup prevents server bloat:

```bash
/mu clean 50           # Clean 50-block radius around you
/mu clear-invalid      # Remove invalid location data
/mu stats reset        # Reset statistics (monthly/quarterly)
```

**Cleanup Schedule**:
- **Daily**: Check active meteorite count
- **Weekly**: Run `/mu clear-invalid` 
- **Monthly**: Clean up old meteorite blocks in unused areas
- **Quarterly**: Reset statistics if needed

## Performance Management

### Resource Monitoring

Monitor server performance impact:

```yaml
# Enable performance monitoring
debug-mode: true
```

**Console Indicators**:
- `[MeteoritesUltimate] Performance: Normal` - Good
- `[MeteoritesUltimate] Performance: High Load` - Review settings
- `[MeteoritesUltimate] Performance: Critical` - Immediate action needed

### Optimization Settings

For high-performance servers:

```yaml
# Reduce visual effects
meteorite-particle-interval: 5
enable-meteorite-particles: false

# Increase cleanup frequency
clean-up-meteorite-blocks-interval: 300

# Reduce spawn frequency
random-meteorite-interval: 900

# Limit guardian effects
persistent-particles:
  enabled: false
```

### Memory Management

Monitor memory usage:

```bash
/mu debug              # Toggle detailed logging
# Check console for memory warnings
```

**Memory Optimization**:
- Regularly clean up old meteorite locations
- Limit active meteorites (max 5-10 for large servers)
- Reduce particle effects in high-population areas
- Use shorter cleanup intervals

## Player Management

### Permission Administration

Manage player access efficiently:

```yaml
# Staff permissions
staff:
  permissions:
    - meteoritesultimate.shoot
    - meteoritesultimate.start
    - meteoritesultimate.stop
    - meteoritesultimate.gui.admin

# VIP permissions  
vip:
  permissions:
    - meteoritesultimate.gui.view
    - meteoritesultimate.gui.stats
    - meteoritesultimate.compass
```

### Event Management

Control meteorite events for special occasions:

```bash
# Special events
/mu interval 60        # Increase frequency for events
/mu shoot netherite_meteorite Tommy  # Target specific players

# Maintenance mode
/mu stop               # Stop random spawning
/mu clean 200 confirm  # Clean large areas
```

## Monitoring & Alerts

### Performance Alerts

Set up monitoring for:

1. **High CPU Usage**: Too many active meteorites
2. **Memory Leaks**: Increasing memory over time
3. **TPS Drops**: Correlated with meteorite events
4. **Error Rates**: Configuration or integration issues

### Log Analysis

Important log patterns to watch:

```
[MeteoritesUltimate] Invalid coordinates detected  # Location validation
[MeteoritesUltimate] Failed to spawn guardian      # Guardian issues  
[MeteoritesUltimate] Protection check failed       # Integration problems
[MeteoritesUltimate] Configuration error          # Config validation
```

## Database Management

### Statistics Database

Manage the statistics database:

```bash
/mu stats              # View current statistics
/mu stats reset        # Reset all statistics
```

**Database Files**:
- `statistics.yml` - Main statistics storage
- `config.yml` - Configuration backup
- Automatic backups in `backups/` folder

### Backup Strategy

**Automated Backups**:
```yaml
# Plugin automatically backs up:
# - config.yml (before each reload)
# - statistics.yml (daily)
# - Location data (on server shutdown)
```

**Manual Backup Script**:
```bash
#!/bin/bash
# backup-meteorites.sh
DATE=$(date +%Y%m%d)
cp plugins/MeteoritesUltimate/config.yml "backups/config-$DATE.yml"
cp plugins/MeteoritesUltimate/statistics.yml "backups/statistics-$DATE.yml"
```

## Troubleshooting Workflows

### Performance Issues

1. **Check Active Meteorites**:
   ```bash
   /mu list
   # If >10 active, clean up old ones
   /mu clean 100
   ```

2. **Review Configuration**:
   ```bash
   /mu types
   # Check spawn chances sum to reasonable total
   ```

3. **Monitor Resource Usage**:
   ```bash
   /mu debug
   # Enable debug mode and monitor console
   ```

### Configuration Issues

1. **Validate Configuration**:
   ```bash
   /mu reload
   # Check console for validation errors
   ```

2. **Test Individual Features**:
   ```bash
   /mu shoot iron_meteorite    # Test meteorite spawning
   /mu guardian rusty_zombie   # Test guardian spawning
   /mu treasure diamond info   # Test treasure system
   ```

3. **Reset to Defaults**:
   ```bash
   # Backup current config
   cp config.yml config-backup.yml
   rm config.yml
   /mu reload  # Regenerates defaults
   ```

## Integration Management

### Plugin Dependencies

Monitor integration health:

```bash
/plugins  # Check if integration plugins are loaded
/mu reload  # Test integration connections
```

**Integration Status Indicators**:
- PlaceholderAPI: Check `/papi parse me %meteorites_status%`
- WorldGuard: Test meteorite spawning in protected regions
- MythicMobs: Try spawning MythicMobs guardians
- Lands: Test protection in claimed areas

### Version Compatibility

Track compatible versions:

| Integration | Tested Version | Status |
|-------------|---------------|---------|
| PlaceholderAPI | 2.11.x | ✅ Compatible |
| WorldGuard | 7.0.x | ✅ Compatible |
| MythicMobs | 5.0.x | ✅ Compatible |
| Lands | 6.x.x | ✅ Compatible |
| GriefPrevention | 16.x.x | ✅ Compatible |

## Scheduled Maintenance

### Weekly Tasks
- [ ] Check `/mu stats` for unusual patterns
- [ ] Review server logs for MeteoritesUltimate errors
- [ ] Test random meteorite spawning
- [ ] Verify backup files are being created

### Monthly Tasks
- [ ] Clean up old meteorite blocks in inactive areas
- [ ] Review and update meteorite spawn rates
- [ ] Check integration plugin versions for updates
- [ ] Analyze statistics for gameplay balance

### Quarterly Tasks
- [ ] Full configuration review and optimization
- [ ] Reset statistics if needed (`/mu stats reset`)
- [ ] Update plugin to latest version
- [ ] Review and update documentation

## Emergency Procedures

### Plugin Malfunction

1. **Immediate Response**:
   ```bash
   /mu stop               # Stop random spawning
   /mu debug              # Enable debug logging
   ```

2. **Damage Assessment**:
   ```bash
   /mu list               # Check active meteorites
   /mu stats              # Review recent activity
   ```

3. **Recovery**:
   ```bash
   /mu clean 200 confirm  # Clean up if needed
   /mu reload             # Reset configuration
   /mu start              # Resume operations
   ```

### Server Performance Crisis

1. **Immediate Actions**:
   - Stop all meteorite events: `/mu stop`
   - Clean up active meteorites: `/mu clean 100 confirm`
   - Disable particle effects temporarily

2. **Investigation**:
   - Enable debug mode and monitor console
   - Check for resource-intensive configurations
   - Review recent meteorite activity

3. **Resolution**:
   - Optimize configuration for performance
   - Gradually re-enable features
   - Monitor performance metrics

## Best Practices

### Configuration Management
- Always backup before making changes
- Test configuration changes on a staging server first
- Use version control for configuration files
- Document custom configurations and changes

### Player Communication
- Announce scheduled maintenance windows
- Explain any temporary service interruptions
- Provide updates during extended troubleshooting
- Share cool statistics and achievements with players

### Security
- Restrict admin commands to trusted staff only
- Monitor for abuse of teleportation commands
- Log all administrative actions
- Regularly review permission assignments

## Support Resources

### Getting Help
- **Discord Community**: Real-time support and discussion
- **GitHub Issues**: Bug reports and feature requests
- **Documentation**: Comprehensive guides and references
- **Server Logs**: Most issues can be diagnosed from console output

### Reporting Issues
When reporting problems, include:
- Plugin version and server software
- Relevant configuration sections
- Console error messages
- Steps to reproduce the issue
- Server specifications and player count

## Performance Metrics

### Healthy Server Indicators
- Meteorite spawn success rate >95%
- Guardian spawn success rate >90%
- Average cleanup time <5 seconds
- Memory usage stable over time
- No location validation errors

### Warning Signs
- Frequent "invalid coordinates" messages
- Guardian spawn failures
- Increasing memory usage
- Player complaints about lag during meteorite events
- Statistics showing unusual patterns