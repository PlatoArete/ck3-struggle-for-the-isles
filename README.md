# Struggle for The Isles

A comprehensive Crusader Kings III mod focused on the 867 start date, bringing depth and historical flavor to the struggle for dominance across the British Isles.

## Overview

**Struggle for The Isles** transforms the British Isles (Britannia, Isle of Man, Orkney, and the Hebrides) into a dynamic theater of conflict, culture, and faith. Experience the clash between Anglo-Saxon kingdoms, Celtic realms, and Norse invaders through a custom Struggle system with meaningful choices and multiple paths to victory.

## Key Features (Planned)

### Political Systems
- **Custom Struggle System** with three phases: Invasion → Consolidation → Hegemony
- **Multiple Resolutions**: Form a Hegemon Empire OR peaceful Confederation of the Isles
- **Unity of the Isles**: Legitimacy system tracking your realm's stability and influence (0-100 scale)
- **Confederation Mechanics**: Rule as High King of High Kings with council votes and stability challenges

### Religion Paths
- **Roman Dominance**: Catholic supremacy with papal benefits
- **Insular Resurgence**: Revived Insular Christianity with unique head and holy order
- **Norse Victorious**: Raiding economy with sea-king syncretism options
- **Old Gods Stir**: Revive Goidelic, Brythonic, or Hellenic paganism
- **Syncretic Faith**: Forge the tolerant "Faith of the Isles" blending traditions

### Culture Systems
- **Melting Pot Culture**: Unified "Isles" culture with communal ethos
- **Hegemon's Divergence**: Imperial culture variants (English/Norse/Gaelic)
- **Cultural Acceptance** mechanics tied to Unity system

### Regional Building Chains
- **Burhs** (Anglo-Saxon): Timber → Stone → Royal Burh with defensive auras
- **Dúns** (Celtic): Hill → Stone → Royal Dún / Fortified Monastery
- **Longphorts** (Norse): Coastal bases → Fortified → Sea-King's Haven

### Military & Levies
- **Fyrd System** (Anglo-Saxon): Lower numbers, higher morale and home defense
- **Ceithernn** (Celtic): Mobile forces with terrain advantages
- **Leidang** (Norse): Naval focus with raid bonuses
- **Unique MaA**: Huscarls, Gallóglaigh, Hersir's Huscarls, Warriors of the Isles

### Court & Retainers
- **High Reeve**: Control and tax bonuses
- **Ollamh/Court Bard**: Prestige and cultural acceptance
- **Hersir**: Raid income optimization
- **Law-Speaker**: Realm stability and tyranny reduction
- **Sea-Marshal**: Naval superiority

## Development Status

**Current Phase**: Foundation & Setup
**Version**: 0.1.0 (Pre-Alpha)
**Game Version**: CK3 1.17.*

This mod is in early development. Core systems are being designed and scaffolded. No gameplay features are currently implemented.

### Roadmap

**MVP (Minimum Viable Product)**
- Struggle skeleton with phase modifiers
- One political resolution (Hegemon)
- One building chain (Burhs)
- Fyrd levy system + Huscarls MaA
- Basic Unity value tracking
- 10-12 core events

**v1.0 - Full Release**
- All building chains and levy systems
- All religious paths including syncretic options
- Cultural resolutions
- Unity UI bar with threshold events
- Confederation system
- ~40-60 events

**v2.0 - Polish & Flavor**
- Additional Old Gods variants
- Artifacts and special buildings
- Law trees and hybrid governments
- Custom UI art and icons
- Achievement support

## Installation

### For Players (When Released)

1. Subscribe via Steam Workshop (link TBD)
2. Enable "Struggle for The Isles" in the CK3 launcher
3. Start a new game in 867 as any ruler in the British Isles

### For Developers

1. Clone this repository
2. Create a symlink from your Paradox mods folder to the repo:
   ```bash
   # Windows (run as admin)
   mklink /D "%USERPROFILE%\Documents\Paradox Interactive\Crusader Kings III\mod\ck3-struggle-for-the-isles" "path\to\repo"

   # Linux/macOS
   ln -s /path/to/repo ~/.local/share/Paradox\ Interactive/Crusader\ Kings\ III/mod/ck3-struggle-for-the-isles
   ```
3. Create a `.mod` file in your mods directory:
   ```
   name="Struggle for The Isles"
   path="mod/ck3-struggle-for-the-isles"
   supported_version="1.17.*"
   ```
4. Install **CK3Tiger** VS Code extension for validation

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Development environment setup
- Coding standards and style guide
- Naming conventions (`isles_` namespace)
- Testing checklist
- PR workflow

**Key Principles:**
- Additive design (no vanilla file replacement)
- Namespace all content with `isles_` prefix
- Localization required for all player-facing content
- Scope to Britannia region for performance

## Compatibility

- **Game Version**: 1.17.* (current stable)
- **Other Mods**: Designed to be compatible with most mods due to additive approach
- **DLC**: No DLC required, but compatible with all official content
- **Ironman**: Will support achievement-compatible gameplay (when released)

## Technical Details

- **Language**: Paradox Script (CK3)
- **File Encoding**: UTF-8 with LF line endings
- **Indentation**: 2 spaces, no tabs
- **Validation**: CK3Tiger linting

## License

[MIT License](LICENSE)

## Credits

Design and development by the Struggle for The Isles team.

Special thanks to the Crusader Kings III modding community for tools, documentation, and support.

---

**Status**: 🔨 In Development | **Version**: 0.1.0 | **CK3**: 1.17.*
