# 🚀 NanoScripter

**Runtime Kotlin/Java Script Loader für Purpur 1.21**

NanoScripter ermöglicht es dir, Minecraft-Plugins direkt auf dem Server in Kotlin oder Java zu schreiben - **ohne externe Build-Tools, ohne IntelliJ, ohne manuelle Kompilierung!**

---

## ✨ Features

- 🔥 **Runtime-Kompilierung** - Scripts werden direkt auf dem Server kompiliert
- 📝 **Kotlin & Java Support** - Schreibe Plugins in deiner bevorzugten Sprache
- 🎯 **Vollständige Bukkit/Purpur API** - Alle Imports automatisch verfügbar
- 🔄 **Hot-Reload** - Lade Plugins neu ohne Server-Neustart (`/ns reload`)
- 📦 **Plugin-Struktur** - Jeder Ordner = Ein Plugin
- 🎨 **Adventure API** - Moderne Text-Components sofort verfügbar
- ⚡ **Kein IDE nötig** - Schreibe Code direkt auf dem Server

---

## 📥 Installation

1. **Download** die neueste `NanoScripter.jar` aus den [Releases](https://github.com/ItzCubiq/NanoScripter/releases)
2. Lege die JAR in deinen `/plugins` Ordner
3. Starte den Server
4. Fertig! 🎉

---

## 📚 Verwendung

### Plugin-Struktur

Plugins werden im Ordner `/plugins/NanoScripter/` erstellt:

```
plugins/
└── NanoScripter/
    ├── welcomemessage/
    │   └── main.kts
    ├── customcommands/
    │   └── main.kts
    └── antigrief/
        └── main.java
```

### Beispiel: Welcome Message Plugin

Erstelle einen Ordner `/plugins/NanoScripter/welcomemessage/` und darin eine `main.kts`:

```kotlin
class WelcomeListener : Listener {
    @EventHandler
    fun onJoin(event: PlayerJoinEvent) {
        val playerName = event.player.name
        val message = Component.text("§e$playerName §7ist dem Server beigetreten! §a✓")
        event.joinMessage(message)
        
        event.player.sendMessage("§a§lWillkommen §7auf dem Server!")
    }
}

Bukkit.getPluginManager().registerEvents(WelcomeListener(), plugin)
logger.info("Welcome Message Plugin wurde aktiviert")
```

### Beispiel: Custom Command Plugin

```kotlin
class FlyCommand : CommandExecutor {
    override fun onCommand(sender: CommandSender, cmd: Command, label: String, args: Array<String>): Boolean {
        if (sender !is Player) {
            sender.sendMessage("§cNur Spieler können diesen Befehl nutzen!")
            return true
        }
        
        sender.allowFlight = !sender.allowFlight
        sender.sendMessage(if (sender.allowFlight) "§aFly aktiviert!" else "§cFly deaktiviert!")
        return true
    }
}

val command = Bukkit.getPluginCommand("fly")
command?.setExecutor(FlyCommand())
logger.info("Fly Command wurde registriert")
```

### Beispiel: Java Plugin

`/plugins/NanoScripter/javaplugin/main.java`:

```java
class MyListener implements Listener {
    @EventHandler
    public void onBreak(BlockBreakEvent event) {
        Player player = event.getPlayer();
        player.sendMessage("§aDu hast einen Block abgebaut!");
    }
}

Bukkit.getPluginManager().registerEvents(new MyListener(), plugin);
logger.info("Java Plugin wurde aktiviert");
```

---

## 🎮 Commands

| Command | Beschreibung | Permission |
|---------|--------------|------------|
| `/ns` | Zeigt das Hilfe-Menü | - |
| `/ns reload` | Lädt alle Plugins neu | `nanoscripter.reload` |
| `/ns list` | Zeigt alle geladenen Plugins | `nanoscripter.list` |
| `/ns help` | Zeigt das Hilfe-Menü | - |

**Aliases:** `/nanoscripter`, `/ns`

---

## 📖 Verfügbare APIs

Alle folgenden APIs sind **automatisch importiert** und können direkt genutzt werden:

### Bukkit/Spigot/Purpur
- ✅ Events (Player, Block, Entity, Inventory, World, etc.)
- ✅ Commands & TabCompletion
- ✅ Scheduler & Tasks (BukkitRunnable)
- ✅ Inventory & Items (ItemStack, Meta, Recipes)
- ✅ Blocks & BlockData
- ✅ Entities (Player, Mob, Animals, Monster, etc.)
- ✅ Scoreboard & BossBars
- ✅ Permissions
- ✅ Configuration (FileConfiguration)
- ✅ Enchantments & Potions

### Adventure API
- ✅ Component (moderne Text-Components)
- ✅ MiniMessage
- ✅ Titles & ActionBars
- ✅ BossBars
- ✅ Sounds

### Java Standard Library
- ✅ Collections (List, Map, Set, etc.)
- ✅ UUID
- ✅ File I/O
- ✅ Time & Date (LocalDateTime, Duration, etc.)
- ✅ Streams & Lambdas

---

## 🔧 Technische Details

- **Minecraft Version:** Purpur 1.21.10+
- **Java Version:** 21
- **Kotlin Version:** 1.9.22
- **Build Tool:** Maven
- **Dependencies:**
  - Kotlin Compiler Embeddable
  - Purpur API
  - Adventure API

---

## 🛠️ Development

### Projekt builden

```bash
git clone https://github.com/ItzCubiq/NanoScripter.git
cd NanoScripter
mvn clean package
```

Die fertige JAR findest du unter `target/NanoScripter-1.0.0.jar`

### Projekt-Struktur

```
NanoScripter/
├── src/
│   └── main/
│       ├── kotlin/
│       │   └── de/
│       │       └── nanosmp/
│       │           ├── NanoScripter.kt
│       │           ├── ScriptManager.kt
│       │           ├── ScriptPlugin.kt
│       │           ├── loaders/
│       │           │   ├── KotlinScriptLoader.kt
│       │           │   └── JavaScriptLoader.kt
│       │           └── registry/
│       │               ├── CommandRegistry.kt
│       │               └── EventRegistry.kt
│       └── resources/
│           └── plugin.yml
├── pom.xml
└── README.md
```

---

## 📝 Lizenz

Dieses Projekt ist unter der [MIT License](LICENSE) lizenziert.

---

## 🤝 Contributing

Contributions sind willkommen! Erstelle gerne Issues oder Pull Requests.

1. Fork das Projekt
2. Erstelle einen Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit deine Änderungen (`git commit -m 'Add some AmazingFeature'`)
4. Push zum Branch (`git push origin feature/AmazingFeature`)
5. Öffne einen Pull Request

---

## 💡 Ideen für Plugins

- 🏠 Custom Home/Warp System
- ⚔️ Custom Combat System
- 🛡️ Anti-Griefing Tools
- 💰 Economy System
- 🎲 Mini-Games
- 📊 Statistics Tracker
- 🔔 Custom Notifications
- 🎯 Quest System

---

## 📧 Support

Bei Fragen oder Problemen:
- Erstelle ein [Issue](https://github.com/ItzCubiq/NanoScripter/issues)

---

**Made with ❤️ by ItzCubiq**

*Entwickle Minecraft-Plugins so einfach wie nie zuvor!*