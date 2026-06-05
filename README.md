# MinerCreepers Mod v1.0.0

Mod de Fabric para Minecraft 26.1.2 que añade 11 variantes de creeper que convierten piedra en menas al explotar.

---

## Índice

1. [Tipos de Creeper](#1-tipos-de-creeper)
2. [Mecánicas](#2-mecánicas)
3. [Configuración](#3-configuración)
4. [Build](#4-build)

---

## 1. Tipos de Creeper

### Overworld

| Tipo | Bioma | Peso | Grupo | Mult. Daño | Menas que genera | Drop al matar |
|------|-------|------|-------|-------------|-------------------|---------------|
| Coal Creeper | MOUNTAIN | 15 | 1-2 | 0.5× | coal_ore, deepslate_coal_ore | 1 Coal |
| Iron Creeper | PLAINS | 12 | 1-2 | 0.7× | iron_ore, deepslate_iron_ore | 1 Raw Iron |
| Copper Creeper | BEACH | 12 | 1-2 | 0.7× | copper_ore, deepslate_copper_ore | 1 Raw Copper |
| Gold Creeper | BADLANDS | 8 | 1-2 | 1.0× | gold_ore, deepslate_gold_ore | 1 Raw Gold |
| Redstone Creeper | Cualquier overworld | 8 | 1-2 | 1.0× | redstone_ore, deepslate_redstone_ore | 4 Redstone |
| Lapis Creeper | MOUNTAIN | 7 | 1-2 | 1.2× | lapis_ore, deepslate_lapis_ore | 1 Lapis Lazuli |
| Diamond Creeper | Cualquier overworld | 3 | 1-1 | 2.0× | diamond_ore, deepslate_diamond_ore | 1 Diamond |
| Emerald Creeper | EXTREME_HILLS | 3 | 1-1 | 2.0× | emerald_ore, deepslate_emerald_ore | 1 Emerald |

### Nether

| Tipo | Peso | Grupo | Mult. Daño | Menas que genera | Drop al matar |
|------|------|-------|-------------|-------------------|---------------|
| Quartz Creeper | 10 | 1-3 | 0.8× | nether_quartz_ore | 1 Quartz |
| Nether Gold Creeper | 8 | 1-2 | 1.0× | nether_gold_ore | 2-6 Gold Nuggets |
| Ancient Debris Creeper | 1 | 1-1 | 3.5× | ancient_debris | 1 Ancient Debris |

**Notas:**
- Los creepers del Nether solo convierten netherrack, blackstone y basalto (no piedra/deepslate).
- Los creepers del Overworld solo convierten piedra y deepslate.
- Todos spawnen en oscuridad total (luz 0) como cualquier monstruo.

---

## 2. Mecánicas

### 2.1 Explosión y Conversión de Bloques

Al explotar, el creeper convierte bloques dentro de un radio (configurable, default **3**) a su mena correspondiente:

| Bloque origen | Se convierte a |
|---------------|----------------|
| Stone → | ore_block |
| Deepslate → | deepslate_variant |
| Netherrack → | ore_block (nether types) |
| Blackstone → | ore_block (nether types) |
| Basalt / Smooth Basalt → | ore_block (nether types) |

### 2.2 Raw Block Chance

30% de probabilidad (configurable) de que los bloques de carbón, hierro, cobre y oro se conviertan en su variante de bloque en bruto (coal_block, raw_iron_block, raw_copper_block, raw_gold_block) en lugar de la mena.

### 2.3 Creeper Cargado (Rayos)

Si un miner creeper es alcanzado por un rayo, su explosión se duplica (power 6 en vez de 3). El radio de conversión no cambia.

### 2.4 Encendedor (Flint & Steel)

Funciona como un creeper vanilla: al hacer clic derecho con un encendedor, el creeper se hincha y explota.

### 2.5 Drops al Morir por Jugador

Cada creeper suelta **1** mineral correspondiente solo si muere por un jugador. Si muere por otras causas (caída, fuego, etc.) no suelta el mineral.

### 2.6 Glow por FOV (Contorno Brillante)

Cuando un jugador **mira directamente** a un miner creeper (ángulo de visión ≥ 0.5 y línea de visión directa), el creeper se marca con un contorno brillante del color de su mineral. El glow persiste **3 segundos** (configurable) después de dejar de mirarlo.

### 2.7 Texturas Emisivas (Brillo en Oscuridad)

Cada creeper tiene una textura emisiva (`*_e.png`) que se activa solo en zonas oscuras (luz promedio ≤ 6). Los ojos y detalles brillan en la oscuridad y se ven apagados con luz.

### 2.8 Spawn Eggs

Los 11 creepers tienen sus propios spawn eggs con textura y rareza:
- **COMMON**: coal, iron, copper, gold, redstone, lapis, quartz, nether_gold
- **RARE**: diamond, emerald
- **EPIC**: ancient_debris

### 2.9 Pestaña Creativa

Todos los spawn eggs aparecen en una pestaña creativa propia (`MinerCreepers`).

---

## 3. Configuración

Archivo: `config/minercreepers_config.json` (se genera automáticamente al iniciar el juego).

### 3.1 Generales

```json
{
  "enabled": true,
  "mod_version": "1.0.0",
  "glowing": true,
  "glow_timeout_seconds": 3
}
```

| Opción | Default | Descripción |
|--------|---------|-------------|
| `enabled` | `true` | Activa/desactiva todo el mod |
| `glowing` | `true` | Activa/desactiva el contorno brillante por FOV |
| `glow_timeout_seconds` | `3` | Segundos que dura el glow después de dejar de mirar |

### 3.2 Explosión

```json
"explosion": {
  "convert_stone": true,
  "convert_deepslate": true,
  "convert_netherrack": true,
  "convert_blackstone": true,
  "convert_basalt": true,
  "natural_only": false,
  "radius": 3,
  "raw_block_chance": 0.3,
  "damage_blocks": false
}
```

| Opción | Default | Descripción |
|--------|---------|-------------|
| `convert_stone` | `true` | Convierte piedra a mena |
| `convert_deepslate` | `true` | Convierte deepslate a su variante de mena |
| `convert_netherrack` | `true` | Convierte netherrack a mena (nether) |
| `convert_blackstone` | `true` | Convierte blackstone a mena (nether) |
| `convert_basalt` | `true` | Convierte basalto/basalto liso a mena (nether) |
| `natural_only` | `false` | Solo convierte bloques naturales (no placas de jugador) |
| `radius` | `3` | Radio en bloques de la conversión |
| `raw_block_chance` | `0.3` | Probabilidad (0.0-1.0) de raw block en vez de mena |
| `damage_blocks` | `false` | La explosión rompe bloques como TNT |

### 3.3 Daño

```json
"damage": {
  "enabled": true,
  "base_damage": 49.0,
  "scale_by_rarity": true,
  "damage_players": true,
  "damage_mobs": true,
  "block_damage_reduction": true
}
```

| Opción | Default | Descripción |
|--------|---------|-------------|
| `enabled` | `true` | La explosión hace daño |
| `base_damage` | `49.0` | Daño base (49.0 = vanilla creeper) |
| `scale_by_rarity` | `true` | Multiplica daño por damage_multiplier del tipo |
| `damage_players` | `true` | Daña jugadores |
| `damage_mobs` | `true` | Daña otras criaturas |
| `block_damage_reduction` | `true` | Bloques entre medio reducen daño |

### 3.4 Spawn

```json
"spawn": {
  "biome_specific": true,
  "nether_spawn": true
}
```

| Opción | Default | Descripción |
|--------|---------|-------------|
| `biome_specific` | `true` | Cada tipo spawn solo en su bioma configurado |
| `nether_spawn` | `true` | Los nether creepers spawn en el Nether |

Cada tipo tiene además su propio peso configurable: `weight_coal`, `weight_iron`, `weight_copper`, `weight_gold`, `weight_redstone`, `weight_lapis`, `weight_diamond`, `weight_emerald`, `weight_quartz`, `weight_nether_gold`, `weight_ancient_debris`. Valores por defecto en la [tabla de tipos](#1-tipos-de-creeper).

### 3.5 Debug

```json
"debug": {
  "log_spawn": true,
  "log_explosion": true,
  "verbose": false
}
```

| Opción | Default | Descripción |
|--------|---------|-------------|
| `log_spawn` | `true` | Log al spawnear un miner creeper |
| `log_explosion` | `true` | Log al explotar un miner creeper |
| `verbose` | `false` | Logs detallados en consola |

---

## 4. Build

```bash
./gradlew build
```

El JAR se genera en `build/libs/minercreepers-1.0.0-26.1.2-Fabric.jar`.

**Requisitos:**
- Java ≥ 25
- Fabric Loader ≥ 0.18.5
- Fabric API
- Minecraft 26.1.2
