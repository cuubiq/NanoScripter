# NanoScripter

**Runtime Kotlin and Java scripting for Purpur servers.**

NanoScripter allows you to create and run Minecraft plugins directly on your server using Kotlin or Java — without an external IDE, build pipeline, or manual compilation workflow.

Write your code, reload it, and keep developing directly inside your server environment.

## Features

* **Runtime compilation** — Compile scripts directly on the server
* **Kotlin & Java support** — Choose the language you prefer
* **Purpur / Bukkit API access** — Use the APIs available to your server
* **Hot reload** — Reload scripts without restarting the server
* **Plugin-based structure** — Each script directory represents a plugin
* **Adventure API support** — Use modern components, MiniMessage, titles and more
* **No IDE required** — Develop scripts directly on your server
* **Lightweight workflow** — Ideal for prototyping and smaller server projects

## Requirements

* **Minecraft:** Purpur 1.21.10+
* **Java:** 21

## Installation

Download the latest `NanoScripter.jar` from the project's releases and place it into your server's `plugins` directory.

```text
server/
└── plugins/
    └── NanoScripter.jar
```

Start or restart your server.

NanoScripter will automatically create its required directories.

## Getting Started

Scripts are stored inside:

```text
plugins/
└── NanoScripter/
```

Each subdirectory represents an individual script plugin.

For example:

```text
plugins/
└── NanoScripter/
    ├── welcomemessage/
    │   └── main.kts
    ├── customcommands/
    │   └── main.kts
    └── antigrief/
        └── main.java
```

This structure keeps individual scripts isolated and makes them easy to manage.

## Kotlin

Create:

```text
plugins/NanoScripter/welcomemessage/main.kts
```

Example:

```kotlin
class WelcomeListener : Listener {
    @EventHandler
    fun onJoin(event: PlayerJoinEvent) {
        val playerName = event.player.name
        val message = Component.text("$playerName joined the server.")

        event.joinMessage(message)
        event.player.sendMessage("Welcome to the server!")
    }
}

Bukkit.getPluginManager().registerEvents(
    WelcomeListener(),
    plugin
)

logger.info("Welcome Message Plugin enabled")
```

## Commands

Commands can be registered directly from your scripts.

Example:

```kotlin
class FlyCommand : CommandExecutor {
    override fun onCommand(
        sender: CommandSender,
        command: Command,
        label: String,
        args: Array<String>
    ): Boolean {
        if (sender !is Player) {
            sender.sendMessage("Only players can use this command.")
            return true
        }

        sender.allowFlight = !sender.allowFlight

        sender.sendMessage(
            if (sender.allowFlight) {
                "Flight enabled."
            } else {
                "Flight disabled."
            }
        )

        return true
    }
}

val command = Bukkit.getPluginCommand("fly")
command?.setExecutor(FlyCommand())

logger.info("Fly command registered")
```

## Java

NanoScripter also supports Java scripts.

Create:

```text
plugins/NanoScripter/javaplugin/main.java
```

Example:

```java
class MyListener implements Listener {
    @EventHandler
    public void onBreak(BlockBreakEvent event) {
        Player player = event.getPlayer();
        player.sendMessage("You broke a block.");
    }
}

Bukkit.getPluginManager().registerEvents(
    new MyListener(),
    plugin
);

logger.info("Java plugin enabled");
```

## Commands

| Command      | Description                     | Permission            |
| ------------ | ------------------------------- | --------------------- |
| `/ns`        | Open the NanoScripter help menu | None                  |
| `/ns reload` | Reload all scripts              | `nanoscripter.reload` |
| `/ns list`   | List loaded scripts             | `nanoscripter.list`   |
| `/ns help`   | Open the help menu              | None                  |

Aliases:

```text
/nanoscripter
/ns
```

## Available APIs

NanoScripter provides access to the APIs available through the server environment.

### Bukkit / Spigot / Purpur

* Events
* Commands
* Tab completion
* Scheduler and tasks
* Inventories
* Items and ItemStacks
* Blocks and BlockData
* Entities
* Scoreboards
* BossBars
* Permissions
* Configuration
* Enchantments
* Potions
* World APIs

### Adventure

* Components
* MiniMessage
* Titles
* Action bars
* BossBars
* Sounds

### Java Standard Library

Standard Java functionality can also be used, including:

* Collections
* Lists, Maps and Sets
* UUID
* File I/O
* Date and time APIs
* Streams
* Lambdas
* Utility classes

## Hot Reload

One of NanoScripter's core features is runtime reloading.

After modifying a script, run:

```text
/ns reload
```

NanoScripter will reload the available scripts without requiring a full server restart.

This makes NanoScripter particularly useful for rapid development, testing and prototyping.

## Development

Clone the repository:

```bash
git clone https://github.com/ItzCubiq/NanoScripter.git
cd NanoScripter
```

Build the project using Maven:

```bash
mvn clean package
```

The compiled JAR will be available in:

```text
target/NanoScripter-1.0.0.jar
```

## Project Structure

```text
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

## Technology

| Component  | Version         |
| ---------- | --------------- |
| Minecraft  | Purpur 1.21.10+ |
| Java       | 21              |
| Kotlin     | 1.9.22          |
| Build Tool | Maven           |

### Dependencies

* Kotlin Compiler Embeddable
* Purpur API
* Adventure API

## Use Cases

NanoScripter is useful for quickly building:

* Custom commands
* Home and warp systems
* Combat mechanics
* Anti-griefing tools
* Economy systems
* Mini-games
* Statistics systems
* Notification systems
* Quest systems
* Server utilities
* Gameplay prototypes

## Contributing

Contributions are welcome.

To contribute:

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/my-feature
```

3. Commit your changes

```bash
git commit -m "Add my feature"
```

4. Push your branch

```bash
git push origin feature/my-feature
```

5. Open a pull request

Please keep contributions focused and include relevant documentation when introducing new functionality.

## Support

If you encounter a bug or have a feature request, open an issue in the repository.

## License

NanoScripter is licensed under the **MIT License**.

See [`LICENSE`](LICENSE) for the complete license text.

## Author

**Cuubiq**

Website: [cuubiq.cc](https://cuubiq.cc/?utm_source=chatgpt.com)

GitHub: [@cuubiq](https://github.com/cuubiq?utm_source=chatgpt.com)

---

**NanoScripter — write, reload, and run Minecraft plugins without the traditional development workflow.**
