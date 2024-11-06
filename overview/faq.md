---
description: Frequently Asked Questions about the Realistic Plant Growth Plugin.
---

# ⁉️ FAQ

<details>

<summary>Are Custom Biomes Supported?</summary>

Yes, custom biomes are now fully supported! 🥳🎉\
Starting with version `RealisticPlantGrowth-0.9-BETA`, you can integrate custom biomes on Paper servers and their forks. \
\
Simply reference the namespace in your `GrowthModifiers.yml` or `BiomeGroups.yml` to identify custom biomes.\
\
For example, with the [Terralith Datapack](https://modrinth.com/datapack/terralith), you would use the following format: `terralith:moonlight_valley`.

</details>

<details>

<summary>Which Custom Biome Plugins/Generators/DataPacks Are Supported?</summary>

**Realistic Plant Growth** is designed to be compatible with a variety of custom biome plugins and world generators, including those that introduce custom biomes with unique namespaces or modify existing vanilla biomes.

For example:

* [**Iris**](https://github.com/VolmitSoftware/Iris): Fully supported, using the `overworld:` namespace for its custom biomes.
* [**Terralith**](https://github.com/Stardust-Labs-MC/Terralith): Fully supported, using the `terralith:` namespace for its custom biomes.
* [**TerraformGenerator**](https://github.com/Hex27/terraformgenerator): Fully supported, using the `terraformgenerator:` namespace for its custom biomes.
* **Other Plugins/Generators**: Generally, any plugin or generator that either modifies existing biomes or adds new ones with a unique namespace should be compatible.

To check the namespace of any custom biome in-game, use **Minecraft's F3 debug screen**. When you’re in a specific biome, the biome information (including the namespace) will appear in the debug overlay.\
If you have questions about compatibility with a specific generator, feel free to join our [Discord server](https://discord.gg/PgUhUNGu2A) for support!

</details>

<details>

<summary>Config Setting XY Does Not Work</summary>

1. Check and make sure you configure the setting as described in [config.yml.md](../guides/configuration/config.yml.md "mention").
2. Verify that this feature is implemented in the version you are using; sometimes there is a note indicating that the feature is not yet supported.
3. Ensure there are no syntax errors in the `config.yml` file. You can check the syntax with an [online YAML validation tool](https://www.yamllint.com/https://www.yamllint.com/).
4. Try to restart your server after making changes to the configuration.

</details>

<details>

<summary>What Versions of Minecraft Are Supported?</summary>

Realistic Plant Growth currently supports Minecraft versions from **1.20.1 and above**

However, please note our Beta Support Policy: \
Version `0.9.0-BETA` is the final beta release that will support older versions of Minecraft. From this point on, during the beta phase and beyond, the plugin will **only support the latest Minecraft version**. \
This will continue until the full release, when all planned features are implemented.

If you’re using an older Minecraft version, `0.9.0-BETA` will be the last compatible update. For ongoing compatibility, we recommend updating to the latest Minecraft version once the plugin is out of beta.

</details>

<details>

<summary>What Java version do I need?</summary>

You need at least **Java 21** for this plugin.

</details>

***
