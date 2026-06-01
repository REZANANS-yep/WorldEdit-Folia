# WorldEdit - Folia / Canvas adaptation

Unofficial fork of [WorldEdit by EngineHub](https://github.com/EngineHub/WorldEdit), adapted to run cleanly under
**[Folia](https://github.com/PaperMC/Folia)** region threading (and its
[Canvas](https://github.com/CraftCanvasMC/Canvas) fork) on modern Paper builds, including **Minecraft 26.1.2**.

**This is not a full Folia rewrite.** WorldEdit itself already runs fine on Folia/Canvas for normal selection and
editing work. The only thing broken was player teleportation: the navigation commands `/up`, `/jumpto`, `/thru`,
`/ascend`, `/descend` and `/unstuck` threw `UnsupportedOperationException: Must use teleportAsync while in region
threading` and failed.

**What this fork changes (and only this):** in `worldedit-bukkit` the `BukkitPlayer` teleport paths
(`trySetPosition` and `setLocation`) took a Folia branch that called the bundled `PaperLib.teleportAsync`. That
bundled PaperLib cannot parse a two-digit Minecraft major version (`26.x`) and silently falls back to a synchronous
`entity.teleport`, which Folia/Canvas reject from a region thread. Both branches now call Paper's native
`player.teleportAsync(...)` directly - region-thread-safe, and it also works on plain Paper. Two lines of behavior,
nothing else in WorldEdit is touched.

**Actively developed and supported** by the [suzeren.org](https://suzeren.org) network, where it runs in production
on a Canvas (Folia) backend. Branch: `folia`, built against the same Java 21 toolchain as upstream (GraalVM 25 runtime).

<p align="center">
  <a href="https://pterohost.com">
    <img src="https://pterohost.com/images/branding/logo-sm.webp" alt="Pterohost - game server hosting with Folia and Paper support" height="64">
  </a>
</p>
<p align="center">
  <b>Этот форк развивается и тестируется на <a href="https://pterohost.com">Pterohost</a></b><br>
  Игровой хостинг с нативной поддержкой Folia и Paper, мгновенный деплой и удобная панель управления.<br>
  <i>Developed and battle tested on <a href="https://pterohost.com">Pterohost</a> - game server hosting with first class Folia and Paper support.</i>
</p>
<p align="center">
  <a href="https://discord.gg/BayzJzArBa">Pterohost Discord</a>
  &nbsp;|&nbsp;
  <a href="https://suzeren.org">suzeren.org</a>
</p>

---

<h1>
    <img src="worldedit-logo.svg" alt="WorldEdit" width="400" /> 
</h1>

**A Minecraft Map Editor... that runs in-game!**

* With selections, schematics, copy and paste, brushes, and scripting!
* Use it in creative, survival in single player or on your server.
* Use it on your Minecraft server to fix griefing and mistakes.

Java Edition required. WorldEdit is compatible with NeoForge, Fabric, Bukkit, Spigot, Paper, and Sponge.

## Download WorldEdit

This place contains the Java code for WorldEdit, but if you want to just use WorldEdit, get the mod or plugin from Modrinth:

https://modrinth.com/plugin/worldedit/versions

Edit the Code
---------

Want to add new features to WorldEdit or fix bugs yourself? You can get the game running, with WorldEdit, from the code here, without any additional outside steps, by doing the following *four* things:

1. Download WorldEdit's source code and put it somewhere. We recommend you use something called Git if you already know how to use it, but [you can also just download a .zip file](https://github.com/EngineHub/WorldEdit/archive/master.zip). (If you plan on contributing the changes, you will need to figure out Git.)
2. Install any version of Java greater than or equal to 21.
   * Note that if you do _not_ install JDK 21 exactly, Gradle will download it for you on first run. However, it is still required to have some form of Java installed for Gradle to start at all.
3. Open terminal / command prompt / bash and navigate to the directory where you put the source code.
4. Run **one** of these following commands:
   * Mac OS X / Linux: `./gradlew :worldedit-fabric:runClient`
   * Windows - Command Prompt: `gradlew :worldedit-fabric:runClient`
   * Windows - PowerShell: `.\gradlew :worldedit-fabric:runClient`

🎉 That's it. 🎉 It takes a long time to actually transform WorldEdit into a mod. If it succeeds, **the Minecraft game will open and you can create a single player world with WorldEdit**.

When you make changes to the code, you have to restart the game by re-running the command for your changes to take effect. If there are errors in your Java syntax, the command will fail.

For additional information about compiling WorldEdit, see [COMPILING.md](COMPILING.md).

### Using a Java IDE

To edit WorldEdit in a Java IDE, follow these steps:

1. Download and install [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/).
2. In the IDE, open the folder that you saved WorldEdit's code in. This creates a new project in IDEA.

That's pretty much it.

If you want to be able to run the game also, follow these instructions:

1. Go to Run -> Edit Configurations.
2. Add a Gradle task:
   1. Choose `worldedit-fabric` for the project.
   2. For the tasks, type in `runClient`
3. Click OK
4. Under the Run menu again, go to "Debug [your new task]".

### Speeding up the Edit-Test-Edit-Test Cycle

It's a little annoying have to restart the game to test your changes. The best way to reduce the time is to run the server instead (using `runServer` instead of `runClient`) and then reconnect to the server after restarting it.

Submitting Your Changes
------------

WorldEdit is open source (specifically licensed under GPL v3), so note that your contributions will also be open source. The best way to submit a change is to create a fork on GitHub, put your changes there, and then create a "pull request" on our WorldEdit repository.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for important guidelines to follow.

Links
-----

* [Visit our website](https://enginehub.org/)
* [Discord](https://discord.gg/enginehub)
* [Issue tracker](https://github.com/EngineHub/WorldEdit/issues)
* [Continuous integration](https://builds.enginehub.org) [![Build Status](https://ci.enginehub.org/app/rest/builds/buildType:bt10,branch:master/statusIcon.svg)](https://ci.enginehub.org/viewType.html?buildTypeId=bt10&guest=1)
* [End-user documentation](https://worldedit.enginehub.org/en/latest/)

Supporters
----------

[![YourKit Logo](https://www.yourkit.com/images/yklogo.png)](https://www.yourkit.com/)

YourKit supports open source projects with innovative and intelligent tools for monitoring and profiling Java and .NET applications.
YourKit is the creator of [YourKit Java Profiler](https://www.yourkit.com/java/profiler/),
[YourKit .NET Profiler](https://www.yourkit.com/.net/profiler/),
and [YourKit YouMonitor](https://www.yourkit.com/youmonitor/).
