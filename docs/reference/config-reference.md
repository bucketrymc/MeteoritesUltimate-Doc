# Configuration Reference

Complete reference for all configuration options in MeteoritesUltimate's `config.yml` file.

## General Settings

### Basic Configuration
```yaml
debug-mode: false                 # Enable debug console output
meteorite-speed: 2.0             # Default falling speed (0.1-5.0)
```

**debug-mode**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Enables detailed console logging for troubleshooting
- **Impact**: Performance overhead when enabled

**meteorite-speed**
- **Type**: Float
- **Range**: 0.1 - 5.0
- **Default**: 2.0
- **Description**: Controls default falling speed for meteorites

### Player Scaling System
```yaml
player-scaling:
  enabled: true                  # Enable dynamic difficulty scaling
  radius: 50                     # Detection radius in blocks
  health-per-player: 1.2         # Health multiplier per player
  damage-per-player: 1.1         # Damage multiplier per player
  max-players: 5                 # Maximum players for scaling
```

**player-scaling.enabled**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Enables automatic guardian difficulty scaling

**player-scaling.radius**
- **Type**: Integer
- **Range**: 10 - 200
- **Default**: 50
- **Description**: Radius to search for players around guardian spawn

**player-scaling.health-per-player**
- **Type**: Float  
- **Range**: 1.0 - 3.0
- **Default**: 1.2
- **Description**: Health increase per additional player (20% increase)

**player-scaling.damage-per-player**
- **Type**: Float
- **Range**: 1.0 - 2.0  
- **Default**: 1.1
- **Description**: Damage increase per additional player (10% increase)

**player-scaling.max-players**
- **Type**: Integer
- **Range**: 1 - 20
- **Default**: 5
- **Description**: Maximum players counted for scaling (prevents overpowered guardians)

## World Configuration

### World Display Names
```yaml
world-names:
  world: "Overworld"             # Display name for 'world'
  world_nether: "Nether"         # Display name for 'world_nether'
  world_the_end: "End"           # Display name for 'world_the_end'
  # custom_world: "Custom Name"  # Add custom worlds
```

**world-names**
- **Type**: Key-Value mapping
- **Description**: Customizes world names in player messages
- **Note**: Keys must match exact world folder names

## Random Meteorite System

### Basic Settings
```yaml
enable-random-meteorites: true   # Enable automatic spawning
random-meteorite-interval: 300   # Spawn interval in seconds
random-meteorite-world: world    # Target world name
random-meteorite-spawn-height: 150 # Spawn height above ground
```

**enable-random-meteorites**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Master switch for automatic meteorite spawning

**random-meteorite-interval**
- **Type**: Integer
- **Range**: 10 - 86400
- **Default**: 300
- **Description**: Time between automatic spawns in seconds

**random-meteorite-world**
- **Type**: String
- **Default**: `world`
- **Description**: World name for automatic spawning (must exist)

**random-meteorite-spawn-height**
- **Type**: Integer
- **Range**: 50 - 320
- **Default**: 150
- **Description**: Height above ground level to spawn meteorites

### Spawn Area Boundaries
```yaml
random-meteorite-min-spawn-x-coord: -1000  # Western boundary
random-meteorite-max-spawn-x-coord: 1000   # Eastern boundary  
random-meteorite-min-spawn-z-coord: -1000  # Northern boundary
random-meteorite-max-spawn-z-coord: 1000   # Southern boundary
```

**Coordinate Boundaries**
- **Type**: Integer
- **Range**: -29999999 to 29999999
- **Default**: ±1000
- **Description**: Defines rectangular spawn area boundaries

## MythicMobs Integration

### Fallback Configuration
```yaml
mythicmobs-fallback:
  enabled: true                           # Enable fallback system
  netherite_overlord: netherite_brute    # MythicMob -> Vanilla mapping
  sculk_abomination: sculk_warden
  prismarine_leviathan: ocean_guardian
  celestial_warden: diamond_skeleton
  void_emperor: end_wraith
```

**mythicmobs-fallback.enabled**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Enables automatic fallback to vanilla mobs when MythicMobs unavailable

**Fallback Mappings**
- **Type**: Key-Value mapping
- **Description**: Maps MythicMobs guardian names to vanilla guardian alternatives

## Protection Systems

### WorldGuard Integration
```yaml
enable-worldguard-safe-zones: false      # Enable WorldGuard protection
worldguard-safe-zone-buffer: 50          # Buffer zone in blocks
protect-all-worldguard-zones: false      # Protect all regions
worldguard-safe-zone-names:              # Specific protected regions
  - spawn
  - safezone
```

**enable-worldguard-safe-zones**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Enables WorldGuard region protection

**worldguard-safe-zone-buffer**
- **Type**: Integer
- **Range**: 0 - 500
- **Default**: 50
- **Description**: Additional protection radius around regions

**protect-all-worldguard-zones**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Protects all WorldGuard regions (not recommended for large servers)

**worldguard-safe-zone-names**
- **Type**: List of Strings
- **Description**: Specific region names to protect

### GriefPrevention Integration
```yaml
enable-griefprevention-safe-zones: false # Enable GriefPrevention protection
griefprevention-safe-zone-buffer: 50     # Buffer zone in blocks
```

**enable-griefprevention-safe-zones**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Enables GriefPrevention claim protection

**griefprevention-safe-zone-buffer**
- **Type**: Integer
- **Range**: 0 - 200
- **Default**: 50
- **Description**: Protection radius around claims

### Lands Integration
```yaml
enable-lands-safe-zones: false          # Enable Lands protection
lands-safe-zone-buffer: 50              # Buffer zone in blocks
protect-all-lands: false                # Protect all claims
lands-safe-zone-names: []               # Specific protected lands
```

**enable-lands-safe-zones**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Enables Lands claim protection

**protect-all-lands**
- **Type**: Boolean
- **Default**: `false`
- **Description**: Protects all Lands claims (can block trusted members)

**lands-safe-zone-names**
- **Type**: List of Strings
- **Description**: Specific land names to fully protect

## Meteorite Layer Settings

### Core Block Settings
```yaml
core-settings:
  enable-explosion: true                 # Visual explosion on impact
  explosion-power: 4                     # Explosion strength (visual only)
  explosion-sets-fire: true             # Temporary fire effects
  enable-lighting-strike: true          # Lightning visual effect
  can-hurt-entities: true               # Falling blocks damage entities
  drop-item-when-destroyed: false       # Blocks place vs drop as items
```

**core-settings.enable-explosion**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Visual explosion effect on impact (no block damage)

**core-settings.explosion-power**
- **Type**: Integer
- **Range**: 1 - 10
- **Default**: 4
- **Description**: Explosion visual intensity and knockback strength

**core-settings.can-hurt-entities**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Whether falling meteorite blocks damage entities

### Effects System
```yaml
effects:
  impact_blindness:
    type: "potion"                       # Effect type
    effect: "BLINDNESS"                  # Potion effect name
    duration: 60                         # Duration in ticks
    amplifier: 1                         # Effect strength
    target: "area"                       # Target type
    radius: 50                           # Effect radius
    delay: 0                             # Delay before applying
```

**Effect Types**:
- `"potion"` - Applies potion effects
- `"summon"` - Spawns entities
- `"command"` - Executes commands

**Target Types**:
- `"area"` - All players in radius
- `"player"` - Specific player
- `"all_online"` - All online players

## Treasure System

### Basic Treasure Settings
```yaml
enable-meteorite-treasure: true         # Enable treasure spawning
treasure-spawn-chance: 100.0           # Percentage chance (0-100)
treasure-spawn-centered: false         # Always spawn at core center
treasure-barrel-or-chest: CHEST        # Container type
enable-treasure-guardian: true         # Enable guardian protection
treasure-show-coordinates: true        # Show coordinates in messages
```

**enable-meteorite-treasure**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Master switch for treasure system

**treasure-spawn-chance**
- **Type**: Float
- **Range**: 0.0 - 100.0
- **Default**: 100.0
- **Description**: Percentage chance for treasure to spawn

**treasure-barrel-or-chest**
- **Type**: String
- **Values**: `CHEST`, `BARREL`
- **Default**: `CHEST`
- **Description**: Type of container for treasures

### Global Treasure Protection
```yaml
treasure-protection:
  type: none                            # Protection type
  container:
    material: OBSIDIAN                  # Barrier block material
    thickness: 1                        # Barrier thickness (1-3)
    breakable: true                     # Can players break barrier
    break-time: 10                      # Mining fatigue duration
    unbreakable-message: 'Cannot break!' # Message when hitting barrier
    all-broken-message: 'Barrier down!' # Message when barrier destroyed
  guardian-lock:
    lock-message: 'Defeat guardian!'    # Message when locked
    unlock-message: 'Unlocked!'        # Message when unlocked
    unlock-effects: true                # Particle effects on unlock
```

**Protection Types**:
- `none` - No protection
- `container` - Physical barrier around treasure
- `guardian-lock` - Must defeat guardian first
- `both` - Both protections active

**Container Protection**:
- Creates crater-shaped barriers around treasures
- Thickness 1-3 creates different crater sizes
- Breakable barriers have mining fatigue effect

### Guardian Spawn Settings
```yaml
guardian-spawn-on-impact: false        # Spawn guardian on impact vs chest open
```

**guardian-spawn-on-impact**
- **Type**: Boolean
- **Default**: `false`
- **Description**: When `true`, guardian spawns immediately on impact; when `false`, spawns when chest is opened

## Particle Effects

### Basic Particle Settings
```yaml
enable-meteorite-particles: true       # Enable particle effects
meteorite-particle-interval: 2         # Particle spawn interval in ticks
```

**enable-meteorite-particles**
- **Type**: Boolean
- **Default**: `true`
- **Description**: Master switch for all particle effects

**meteorite-particle-interval**
- **Type**: Integer
- **Range**: 1 - 20
- **Default**: 2
- **Description**: Ticks between particle spawns (lower = more particles)

## Cleanup System

### Block Cleanup Settings
```yaml
clean-command:
  max-radius: 200                       # Maximum cleanup radius
  confirm-threshold: 50                 # Radius requiring confirmation
  confirm-timeout: 30                   # Confirmation timeout in seconds
```

**clean-command.max-radius**
- **Type**: Integer
- **Range**: 10 - 1000
- **Default**: 200
- **Description**: Maximum allowed radius for `/mu clean` command

**clean-command.confirm-threshold**
- **Type**: Integer
- **Default**: 50
- **Description**: Radius above which confirmation is required

## Meteorite Definitions

### Basic Meteorite Structure
```yaml
meteorites:
  iron_meteorite:                       # Unique meteorite identifier
    enabled: true                       # Enable this meteorite type
    chance: 22                          # Spawn weight (relative to others)
    chat-message: 'Iron meteorite!'     # Announcement message
    meteorite-speed: 2.0               # Override default speed
    outer-layer-size: 3                 # Outer layer radius
    inner-layer-size: 2                 # Inner layer radius  
    enable-inner-layer: true           # Enable inner layer
    clean-up-meteorite-blocks-interval: 600 # Cleanup time in seconds
```

**Meteorite Properties**:
- `enabled` - Include in random spawning
- `chance` - Spawn weight (higher = more common)
- `meteorite-speed` - Override global speed setting
- `outer-layer-size` - Size of outer shell (1-10)
- `inner-layer-size` - Size of inner core (1-outer_size)
- `clean-up-meteorite-blocks-interval` - Auto-cleanup time

### Block Composition
```yaml
core-block:
  IRON_BLOCK: 100                      # 100% iron blocks in core

inner-layer-blocks:
  IRON_ORE: 50                         # 50% iron ore
  DEEPSLATE_IRON_ORE: 30               # 30% deepslate iron ore
  RAW_IRON_BLOCK: 20                   # 20% raw iron blocks

outer-layer-blocks:
  STONE: 40                            # 40% stone
  DEEPSLATE: 30                        # 30% deepslate
  COBBLESTONE: 20                      # 20% cobblestone
  TUFF: 10                             # 10% tuff
```

**Block Weights**:
- Numbers represent relative probability
- Must total any value (percentages calculated automatically)
- Use valid Material names from Bukkit API

## Guardian Definitions

### Basic Guardian Structure
```yaml
possible-guardians:
  rusty_zombie:                        # Unique guardian identifier
    enabled: true                      # Enable this guardian
    chance: 40                         # Spawn weight
    guardian-mob-type: ZOMBIE          # Bukkit entity type
    guardian-display-name: 'Rusty Guardian' # Custom name
    guardian-health: 40                # Health points
    guardian-attack-damage: 6          # Damage per attack
    guardian-movement-speed: 0.28      # Movement speed multiplier
    guardian-spawn-sound: ENTITY_ZOMBIE_AMBIENT # Spawn sound
    player-message: 'Guardian emerges!' # Spawn message
```

**Guardian Properties**:
- `guardian-mob-type` - Valid Bukkit EntityType
- `guardian-health` - Health points (default mob health * this value)
- `guardian-attack-damage` - Damage value
- `guardian-movement-speed` - Speed multiplier (0.1-2.0)

### Guardian Equipment
```yaml
enable-guardian-equipment: true       # Enable custom equipment
guardian-equipment:
  main-hand: IRON_SWORD              # Weapon
  helmet: IRON_HELMET                # Head armor
  chestplate: IRON_CHESTPLATE        # Chest armor  
  leggings: CHAINMAIL_LEGGINGS       # Leg armor
  boots: CHAINMAIL_BOOTS             # Foot armor
```

### Guardian Particle Effects
```yaml
tier-particles: common                # Simple preset effects
# OR
spawn-particles:                     # Custom particle system
  smoke_effect:
    type: LARGE_SMOKE                # Particle type
    count: 25                        # Number of particles
    spread: {x: 0.5, y: 0.5, z: 0.5} # Particle spread
    speed: 0.05                      # Particle speed

persistent-particles:                # Ongoing particle effects
  enabled: true                      # Enable persistent effects
  interval-ticks: 60                 # Particle interval
  duration-seconds: -1               # Duration (-1 = permanent)
  intensity: 0.2                     # Effect intensity (0.1-1.0)
```

**Particle Tiers**:
- `common` - Simple smoke effects
- `rare` - Soul and flame particles
- `epic` - Soul fire and enchant particles
- `legendary` - End rod and dragon breath particles

### Guardian Effects System
```yaml
effects:
  copper_slowness:                   # Effect identifier
    type: "potion"                   # Effect type
    effect: "SLOWNESS"               # Potion effect
    duration: 60                     # Duration in ticks
    amplifier: 1                     # Effect level (0-based)
    target: "area"                   # Target type
    radius: 10                       # Effect radius
    delay: 20                        # Spawn delay in ticks
```

### MythicMobs Guardians
```yaml
netherite_overlord:                  # Guardian identifier
  enabled: true                      # Enable this guardian
  chance: 8                          # Spawn weight
  mythic-mob: NetheriteOverlord      # MythicMobs internal name
  mythic-mob-level: 1                # MythicMobs level
  guardian-display-name: 'Overlord'  # Display name
  guardian-spawn-sound: ENTITY_WITHER_SPAWN # Spawn sound
  player-message: 'Overlord awakens!' # Spawn message
  death-commands:                    # Commands on death
    - "give %player% netherite_ingot 1"
  meteorite-spawns:                  # Compatible meteorites
    - netherite
```

## Treasure Content Definitions

### Basic Treasure Structure
```yaml
treasure-content:
  meteorite_iron:                    # Unique treasure identifier
    enabled: true                    # Enable this treasure
    chance: 60                       # Spawn weight
    item-type: IRON_INGOT           # Bukkit Material
    amount: 8                        # Item quantity
    display-name: 'Meteorite Iron'  # Custom item name
    lore:                           # Item description
      - 'Iron from space'
      - 'Very valuable'
    meteorite-spawns:               # Compatible meteorites
      - iron
      - coal
      - copper
```

**Treasure Properties**:
- `item-type` - Valid Bukkit Material name
- `amount` - Stack size (1-64 typically)
- `meteorite-spawns` - List of compatible meteorites (empty = universal)

### Enchanted Items
```yaml
cosmic_diamond:
  item-type: DIAMOND
  enchants:                          # Enchantments to apply
    fortune: 1                       # Enchantment: level
    unbreaking: 3
```

### Potion Items
```yaml
strength_potion:
  item-type: POTION
  potion-effects:                    # Potion effects
    - type: STRENGTH                 # Effect type
      duration: 3600                 # Duration in ticks
      amplifier: 2                   # Effect level (0-based)
```

## Particle Effect Definitions

### Basic Particle Structure
```yaml
possible-meteorite-particle-effects:
  cosmic_flame:                      # Unique effect identifier
    enabled: true                    # Enable this effect
    chance: 40                       # Selection weight
    particle-effect: SOUL_FIRE_FLAME # Particle type
    amount: 8                        # Particle count
    spread: 0.8                      # Spread radius
    speed: 0.15                      # Particle speed
    force-visibility: true           # Force render distance
```

**Particle Properties**:
- `particle-effect` - Valid Bukkit Particle type
- `amount` - Number of particles to spawn
- `spread` - Random distribution radius
- `speed` - Initial particle velocity
- `force-visibility` - Render beyond normal distance

## Message Configuration

### Message Structure
```yaml
messages:
  commands:
    prefix: '&8[&6☄&8] &e'          # Command response prefix
    error-prefix: '&8[&6☄&8] &c'    # Error message prefix
    success-prefix: '&8[&6☄&8] &a'  # Success message prefix
    no-permission: 'No permission!' # Permission error message
```

**Color Codes**:
- Use `&` followed by color code (e.g., `&a` for green)
- Use `§` in some contexts (automatically converted)
- Supports all Minecraft color and formatting codes

### Meteorite Messages
```yaml
meteorite-approach:
  announcement: '&e%meteorite% approaching!' # Spawn announcement
  coordinates-display: '&7Location: %x% %y% %z%' # Coordinate display
```

**Placeholders in Messages**:
- `%meteorite%` - Meteorite type name
- `%world%` - World display name
- `%x%`, `%y%`, `%z%` - Coordinates
- `%player%` - Player name
- `%guardian%` - Guardian display name

## Statistics Section

```yaml
statistics:
  total-spawned: 0                   # Total meteorites spawned
  guardians-spawned: 0              # Total guardians spawned
  treasures-opened: 0               # Total treasures found
```

**Note**: These values are automatically managed by the plugin and update in real-time.

## Validation Rules

### Data Type Validation
- **Boolean**: `true` or `false` only
- **Integer**: Whole numbers within specified ranges
- **Float**: Decimal numbers within specified ranges
- **String**: Text values, must be quoted if containing spaces
- **List**: YAML list format with `-` prefix

### Range Validation
The plugin automatically validates:
- Coordinate boundaries (-30M to +30M)
- Percentage values (0-100)
- Time intervals (10-86400 seconds)
- Entity health values (1-2000)
- Particle counts (1-1000)

### Reference Validation
The plugin verifies:
- World names exist on server
- Material names are valid
- Entity types are supported
- Permission nodes are properly formatted
- Sound names are valid