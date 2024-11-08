---
description: Configuration Guide for Growth Modifiers.
---

# 📊 GrowthModifiers.yml

{% embed url="https://github.com/Happy-Hop7/RealisticPlantGrowth/blob/master/src/main/resources/GrowthModifiers.yml" %}

***

## Introduction

The **Realistic Plant Growth** GrowthModifiers configuration file allows you to adjust the growth rate behavior of specified plants in relation to the vanilla game. By default, a growth rate of `100%` mirrors vanilla behavior. Higher rates can speed up plant growth, while lower rates can slow it down. \


This guide will walk you through the process of customizing these settings to fit your gameplay preferences. The best way to do this is, by providing example configurations and explaning them in detail.

{% hint style="info" %}
Plants not listed in the `GrowthModifiers.yml` file will use the vanilla Minecraft plant growth behavior.
{% endhint %}

{% hint style="warning" %}
Growth rates above 100% (compared to vanilla Minecraft) are not supported during the BETA phase of this plugin.
{% endhint %}

***



## GrowthModifiers File Structure

The following sections outline possible components of a plant configuration. \
Some of these sections are mandatory, while others are optional. \
Please note that there is a specific order in which the plugin checks these sections, and this order should be considered during configuration.

{% code title="GrowthModifiers.yml" %}
```yaml
PLANT_NAME:
  BiomeGroup:
    Groups:
      - BiomeGroupName1
      - BiomeGroupName2
    BiomeGroupName1:
      GrowthRate: X
      UVLightGrowthRate: Y
      NaturalDeathChance: Z
      UVLightDeathChance: W
  Default:
    GrowthRate: X
    UVLightGrowthRate: Y
    NaturalDeathChance: Z
    UVLightDeathChance: W
    Biome:
      - BIOME1
      - BIOME2
```
{% endcode %}

***



## Key Sections

The GrowthModifiers configuration file includes several parameters to adjust plant growth rates and death chances. \
Below are the key sections and parameters you need to understand.



### PLANT\_NAME:

The material name of the plant you are configuring. \
The specified growth modifiers will be applied to this plant. \
Ensure the material name matches a Minecraft [Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html) name (e.g., BAMBOO, CACTUS).

```yaml
PLANT_NAME:
  # The Material name of the plant you are configuring.
  # The configured GrowthModifiers are then applied to this plant.
  # This must be a Minecraft Material name (e.g., BAMBOO, CACTUS).
```

{% hint style="info" %}
For now, only official Minecraft material names listed [>here<](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html) are supported. \
In future updates, this will be expanded to include an API that supports custom plant materials.
{% endhint %}

{% hint style="warning" %}
Some material names are mapped to simplify the configuration process. \
For example, instead of using `MELON_STEM`, you can use `MELON` to configure the growth of melons.
{% endhint %}



### BiomeGroup

This section is specifically for handling biome groups. \
These groups can be created in the `BiomeGroups.yml` file.



### Groups

A list of BiomeGroup names you configured in `BiomeGroups.yml`.

```yaml
Groups:
  - BiomeGroupName1
  - BiomeGroupName2
```

This can also be an empty list if there is no fitting BiomeGroup. \
In such cases, the Biome list from the [Default](growthmodifiers.yml.md#default) section is used.

<details>

<summary>Empty Groups List Example</summary>

```yaml
PLANT_NAME:
  BiomeGroup:
    Groups: [ ]
```

</details>



### BiomeGroupName

If you have listed the name of a BiomeGroup under the [`Groups`](growthmodifiers.yml.md#groups) section, you can create a new section within the [`BiomeGroup`](growthmodifiers.yml.md#biomegroup) section with growth modifiers specifically for the named BiomeGroup.

\
Each biome group can have specific settings for growth rates and death chances. \
Replace `BiomeGroupName1` and `BiomeGroupName2` with your actual biome group names.

This section is <mark style="color:orange;">**optional**</mark>. \
If there is no matching section for the listed BiomeGroupName, the modifiers from the [Default ](growthmodifiers.yml.md#default)section are applied to the BiomeGroupName.

```yaml
BiomeGroupName1:
  GrowthRate: X  # The growth rate percentage for this biome group.
  UVLightGrowthRate: Y  # The growth rate percentage under UV light for this biome group.
  NaturalDeathChance: Z  # The chance of natural death for plants in this biome group.
  UVLightDeathChance: W  # The chance of death under UV light for plants in this biome group.

```



### Default

The default configuration applies to all biomes listed under `Biome` and if no specific biome group configuration is set.

If your `Biome` list consists only of the keyword `ALL`, the `Default` section applies to all possible biomes.

```yaml
Default:
  GrowthRate: X  # The default growth rate percentage.
  UVLightGrowthRate: Y  # The default growth rate percentage under UV light.
  NaturalDeathChance: Z  # The default natural death chance.
  UVLightDeathChance: W  # The default death chance under UV light.
  Biome:
    - BIOME1  # List of biomes included in the default group.
    - BIOME2

```

{% hint style="info" %}
To use non-vanilla biomes, reference them by their correct namespace. \
For example, for a biome from the Terralith Datapack, use `terralith:moonlight_valley`
{% endhint %}

***



## Example Configurations

Here are some example configurations with explanations to help guide you through the configuration process.

### Example 1

In this example, the Bamboo plant's growth parameters are being configured. \
The configuration assigns the `BiomeGroup` called `Tropical` to the Bamboo plant , and further specifies its growth characteristics within this group.

\
The `GrowthRate` is set to `100%`, meaning the Bamboo grows at a rate equivalent to vanilla Minecraft, maintaining the default growth speed. Additionally, if you configure the [`min_natural_light`](config.yml.md#min\_natural\_light) setting, Bamboo can still grow in underground farms illuminated by UV-Light Blocks (defined under [`uv_blocks`](config.yml.md#uv\_blocks)), but at a reduced growth rate of `35%` compared to the normal rate.

The configuration also sets a `NaturalDeathChance` of `5%`, indicating a small chance of Bamboo dying naturally in tropical biomes. In contrast, the `UVLightDeathChance` is set to `15%`, reflecting a higher chance of Bamboo dying in underground farms lit by UV-Light Blocks compared to those exposed to natural skylight.

The `Default` section, with its empty parentheses, signifies that Bamboo cannot grow in any other biomes outside the specified `Tropical` group. Thus, only the biomes listed under the [`Tropical`](growthmodifiers.yml.md#biomegroup-tropical) BiomeGroup are considered valid for Bamboo growth.



{% code title="Example 1" %}
```yaml
BAMBOO:
  BiomeGroup:
    Groups:
      - Tropical
    Tropical:
      GrowthRate: 100
      UVLightGrowthRate: 35
      NaturalDeathChance: 5
      UVLightDeathChance: 15
  Default:
    Biome: [ ] # No growth in other biomes
```
{% endcode %}

<details>

<summary>BiomeGroup: Tropical</summary>

{% code title="BiomeGroups.yml" %}
```yaml
# Tropical biomes
Tropical:
  # Jungle
  - JUNGLE
  - BAMBOO_JUNGLE
  - SPARSE_JUNGLE
  # Swamp
  - MANGROVE_SWAMP
  - SWAMP
```
{% endcode %}

</details>



### Example 2

In this configuration example, the growth parameters for the Cocoa plant are defined. \
The `BiomeGroup` section, which typically defines specific biome groups with tailored growth settings, is assigned an empty list in this case. This indicates that no specific biome groups are configured for Cocoa, and the configuration relies entirely on the `Default` section for its settings.



Within the `Default` section, various growth parameters for Cocoa are specified, but these settings apply only to jungle biomes. The `GrowthRate` is set to `100%`, meaning Cocoa grows at the standard rate as per vanilla Minecraft. If underground farms use UV-Light Blocks, defined under [`uv_blocks`](config.yml.md#uv\_blocks), Cocoa can still grow, but at a reduced rate of `55%`.

The configuration also defines the chances of Cocoa plants dying under different conditions. The `NaturalDeathChance` is set at `5%`, indicating a slight chance of Cocoa dying naturally in jungle biomes. The `UVLightDeathChance` is set at `25%`, reflecting a higher chance of Cocoa dying when exposed to UV light in underground farms.

Lastly, the `Biome` key within the `Default` section lists specific biomes where Cocoa growth is allowed. These include `JUNGLE`, `BAMBOO_JUNGLE`, and `SPARSE_JUNGLE`, restricting Cocoa growth exclusively to these jungle biomes.

{% code title="Example 2" %}
```yaml
COCOA:
  BiomeGroup:
    Groups: [ ]
  # The default section applies only to jungle biomes
  Default:
    GrowthRate: 100
    UVLightGrowthRate: 55
    NaturalDeathChance: 5
    UVLightDeathChance: 25
    # Cocoa growth is limited to jungle biomes
    Biome:
      - JUNGLE
      - BAMBOO_JUNGLE
      - SPARSE_JUNGLE
```
{% endcode %}



### Example 3

🚧 Work in Progress 🚧

{% code title="Example 3" %}
```yaml
MELON:
  Groups:
    - DesertBiomes
    - ForestBiomes
    
  DesertBiomes: # Applies to all biomes in the DesertBiomes group.
    GrowthRate: 50  # Slower growth in desert biomes.
    UVLightGrowthRate: 75  # Slightly faster growth under UV light in deserts.
    NaturalDeathChance: 10  # Higher natural death chance in deserts.
    UVLightDeathChance: 5  # Lower death chance under UV light in deserts.
  
  Default: # Default section applies to the PLAINS, SWAMP and all ForestBiomes biomes.
    GrowthRate: 100  # Default growth rate matches vanilla behavior.
    UVLightGrowthRate: 100  # Default UV light growth rate matches vanilla behavior.
    NaturalDeathChance: 5  # Default natural death chance.
    UVLightDeathChance: 3  # Default UV light death chance.
    Biome:
      - PLAINS
      - SWAMP
```
{% endcode %}

<details>

<summary>BiomeGroup: DesertBiomes</summary>

{% code title="BiomeGroups.yml" %}
```yaml
DesertBiomes:
  - DESERT
  - BADLANDS
```
{% endcode %}

</details>

<details>

<summary>BiomeGroup: ForestBiomes</summary>

{% code title="BiomeGroups.yml" %}
```yaml
DesertBiomes:
  - FOREST
  - FLOWER_FOREST
  - DARK_FOREST
```
{% endcode %}

</details>

***



## Advanced Topics

🚧 Work in Progress 🚧

### Order of valid Biome Checking



### Growth Modifier Selection

The following table shows which growth modifier applies under which conditions. \
There are five cases, plus one special case, that can occur.

<table data-full-width="false"><thead><tr><th width="134">Valid Biome</th><th width="105">Is Dark</th><th width="120">UV Enabled</th><th width="165">Fertilizer Enabled</th><th>Event</th></tr></thead><tbody><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td>Special Case:<br><mark style="color:yellow;">UV-Light</mark> * <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:blue;">Normal</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:blue;">Normal</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:blue;">Normal</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:blue;">Normal</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:yellow;">UV-Light</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:yellow;">UV-Light</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr></tbody></table>



***
