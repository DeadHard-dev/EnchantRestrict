# 📚 EnchantRestrictor

A highly performant, advanced Minecraft Spigot/Paper server plugin offering dynamic restriction, control, and audit mapping of enchantment matrices across the server's economy. Designed from the ground up to prevent server inflation, manage powerful enchantment paths, and log player activities with unparalleled precision.

---

## ✨ Core Features

*   **Modular Administration GUI Panel (`/enchantrestrict gui`)**: A visual control center to hot-reload config files, toggle safety modes, alter behavior policies, and manage banned enchantment lists dynamically in-game.
*   **Enchantment Table Interception**: Intercepts enchantment table rolls in real-time. Automatically checks permissions and applies configured mitigation pathways:
    *   `REMOVE`: Silently excludes and strips forbidden enchantments from the roll.
    *   `REPLACE_BY_CLEAN`: Completely wipes all enchantments and clears the item's magical metadata if a blocked enchantment is rolled.
*   **Villager Trade Interceptions**: Block, replace, or adapt trading loops dynamically. Supports multiple actions if a villager lists a blocked book or item:
    *   `REPLACE`: Swaps forbidden scrolls with safe, useful *Unbreaking* alternatives.
    *   `REMOVE_TRADE`: Securely purges the targeted trade option entirely from the villager's inventory.
    *   `HIGH_PRICE`: Astronomically inflates the emerald cost by a configurable price multiplier.
    *   `CLEAR_BOOK`: Sanitizes trading, turning the restricted enchanted book item into a standard blank book.
*   **Admin Apply & Remover Scrolls System**: Forge customizable high-authority Admin Scrolls using a visual Scroll Generator interface. Custom level scales run from 1 to 255 (a level of 0 acts as a **Remover Scroll** to strip the specified enchantment when applied).
*   **Asynchronous Audit Logs (Local SQLite / Central MySQL)**: Built-in asynchronous database integration hooks. Keeps clean persistent records of player infractions, blocked table rolls, and rejected villager trades without causing any tick-rate or main-thread locking.
*   **Premium Audio Sound Matrix (`sound.yml`)**: Fully custom auditory mapping files. Alter, amplify, or mute sound effects (volume, pitch) for distinct plugin actions, interface clicks, and event triggers.
*   **Dynamic Language Engine & HEX Formatting**: Change language files on-the-fly. Natively supports RGB hex color format (`&#RRGGBB` and Adventure tags) for striking chat overlays.

---

## 🛠 Command Reference & Commands

All administrative subcommands require the **`enchantrestrictor.admin`** permission. Auto-complete suggests commands dynamically.

| Command | Description | Example |
| :--- | :--- | :--- |
| `/enchantrestrict gui` | Opens the Visual Admin Interface (Control Panel, Rule Matrix, Level Picker). | `/enchantrestrict gui` |
| `/enchantrestrict list` | Lists all currently restricted enchantments for Tables and Trades. | `/enchantrestrict list` |
| `/enchantrestrict reload` | Hot-reloads configuration profiles, audio files, and translation matrices. | `/enchantrestrict reload` |
| `/enchantrestrict toggle <table/trade>` | Toggles specific filter compartments on/off instantly. | `/enchantrestrict toggle table` |
| `/enchantrestrict add <table/trade> <enchant>` | Appends a vanilla enchantment key to the ban list. | `/enchantrestrict add trade mending` |
| `/enchantrestrict remove <table/trade> <enchant>` | Lifts restrictions of a specific enchantment. | `/enchantrestrict remove table infinity` |
| `/enchantrestrict give [player] [enchant] [level]` | Gives an Admin Scroll (use level 0 for a Remover Scroll). | `/enchantrestrict give Notch sharp 5` |
| `/enchantrestrict clear [player] [enchant]` | Hard-clears and purges specific enchantments from player items. | `/enchantrestrict clear Notch knockback` |

---

## 🎨 Creative In-Game GUI

EnchantRestrictor provides a beautifully tactile UI. Running `/enchantrestrict gui` triggers a customized opening visual chime and opens a layered, interactive chest screen:

1.  **Administrative Controls Panel**:
    *   Toggle table protection, villager filters, or bypass options.
    *   Adjust table actions (REMOVE / REPLACE_BY_CLEAN) and villager action policies.
    *   Reload config files with a single click.
2.  **Modular Rule Matrix Editor**:
    *   Displays all registered vanilla enchantments as magical enchanted books.
    *   **Left-Click** a book to toggle its Enchantment Table Ban.
    *   **Right-Click** a book to toggle its Villager Trade Ban.

---

## 🔐 Permission Nodes

### Administrative Node
*   **`enchantrestrictor.admin`**: Permission to run admin commands, access standard visual panels, receive debug listings, and perform manual bypasses.

### Interactive Bypass Permissions
Set `general.enable-permissions: true` in `config.yml` to authorize bypass mechanics for groups or individuals:

| Permission Node | Authorized Bypass Action |
| :--- | :--- |
| `enchantrestrictor.bypass.table` | Bypass all Enchantment Table restrictions. |
| `enchantrestrictor.bypass.table.<enchantment>` | Bypass a specific Enchantment Table rule (e.g., `enchantrestrictor.bypass.table.mending`). |
| `enchantrestrictor.bypass.trade` | Bypass all Villager Trade restrictions. |
| `enchantrestrictor.bypass.trade.<enchantment>` | Bypass a specific Villager Trade rule (e.g., `enchantrestrictor.bypass.trade.efficiency`). |

---

## ⚙️ Configuration Manual

### `config.yml` (Core Engine Settings)
Configure general options and pathways:
```yaml
general:
  # Toggle visual magic visual particle spawns around active inventories
  use-particles: true
  # Toggle general custom sound effects matrix
  use-sounds: true
  # Check and enforce bypass permission rules
  enable-permissions: true
  # Enable deep tracing details in the server console
  debug: false
```

### Database Integration
Configure file-based or centralized storage profiles securely under the database block:
```yaml
database:
  # Supported types: "SQLITE" (packaged local file) or "MYSQL" (central database)
  type: "SQLITE"
  mysql:
    host: "localhost"
    port: 3306
    database: "enchantrestrictor"
    username: "root"
    password: ""
```

---

## 🌈 Styling & Localization support

The plugin supports diverse color schemes:
1.  **Hex Color Code**: `&#FF5555` / `&#12FF34`
2.  **Adventure Formatting**: `<color:#FF5555>Sparks</color>` or `<gold>&b&l`
3.  **Legacy Colors**: Standard formatting such as `&c`, `&a`, `&f`.

Localized language sheets are ready-to-use in:
*   `messages_en.yml` (English)
*   `messages_ru.yml` (Russian)

---
