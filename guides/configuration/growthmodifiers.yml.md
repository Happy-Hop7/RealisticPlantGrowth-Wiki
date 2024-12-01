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

{% hint style="success" %}
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

{% hint style="success" %}
To use non-vanilla biomes, reference them by their correct namespace. \
For example, for a biome from the Terralith Datapack, use `terralith:moonlight_valley`
{% endhint %}

{% hint style="warning" %}
The `Default` section also serves as the fallback configuration for any `BiomeGroups` not covered by a dedicated section.
{% endhint %}

***



## Example Configurations

Here are some example configurations with explanations to help guide you through the configuration process.

### Example 1

In this example, the Bamboo plant's growth parameters are being configured. \
The configuration assigns the `BiomeGroup` called `Tropical` to the Bamboo plant , and further specifies its growth characteristics within this group.

\
The `GrowthRate` is set to `100%`, meaning the Bamboo grows at a rate equivalent to vanilla Minecraft, maintaining the default growth speed. Additionally, if you configure the [`min_natural_light`](config.yml.md#min_natural_light) setting, Bamboo can still grow in underground farms illuminated by UV-Light Blocks (defined under [`uv_blocks`](config.yml.md#uv_blocks)), but at a reduced growth rate of `35%` compared to the normal rate.

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



Within the `Default` section, various growth parameters for Cocoa are specified, but these settings apply only to jungle biomes. The `GrowthRate` is set to `100%`, meaning Cocoa grows at the standard rate as per vanilla Minecraft. If underground farms use UV-Light Blocks, defined under [`uv_blocks`](config.yml.md#uv_blocks), Cocoa can still grow, but at a reduced rate of `55%`.

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

In this configuration example, the growth parameters for melons are defined based on the biomes in which they are grown. The configuration specifies two biome groups, `DesertBiomes` and `ForestBiomes`, and also includes specific rules for the `PLAINS` and `SWAMP` biomes. \
Together, these define where melons can grow and what growth behavior to expect.



The `DesertBiomes` group has its own dedicated section, which adjusts melon growth to reflect the harsher conditions of desert environments. The `GrowthRate` is reduced to `50%`, meaning melons grow more slowly in these biomes. However, if UV-Light Blocks are used, the `UVLightGrowthRate` increases to `75%`, providing a slight improvement in growth speed under artificial light. The `NaturalDeathChance` is set at `10%`, indicating a higher risk of melons dying naturally in deserts, but this risk is mitigated when UV light is present, reducing the `UVLightDeathChance` to `5%`.

In contrast, the `ForestBiomes` group does not have its own modifier section. Instead, these biomes fall under the settings defined in the `Default` section. The same applies to `PLAINS` and `SWAMP` biomes, which are explicitly listed under the Default section. Here, melons grow at the standard `GrowthRate` of `100%`, mirroring vanilla Minecraft behavior. The `UVLightGrowthRate` is also set to `100%`, allowing for typical growth under UV light. The `NaturalDeathChance` is relatively low at `5%`, with an even smaller `UVLightDeathChance` of `3%`, making these biomes more favorable for melon cultivation.

The `Default` section also serves as the fallback configuration for any `BiomeGroup` not covered by a dedicated section. By including `PLAINS` and `SWAMP` directly and applying it to `ForestBiomes`, the `Default` section ensures that melons grow consistently in these environments without additional customization.

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

### Order of valid Biome Checking

When determining which `BiomeGroup` a specific biome belongs to during a growth event, the system checks the order of appearance in the `BiomeGroups.yml` configuration file.&#x20;

If a biome is assigned to multiple `BiomeGroups`, only its <mark style="color:red;">**first appearance**</mark> in the file is considered valid. Subsequent appearances of the same biome in other `BiomeGroups` are ignored during this decision-making process.

This means the order in which biomes are listed within `BiomeGroups.yml` is critical.&#x20;

For example, if the `DESERT` biome is listed first under the `DesertBiomes` group and later under `AridBiomes`, the system will recognize it only as part of `DesertBiomes` for that plant. The `AridBiomes` assignment would be ignored during growth calculations.

To avoid conflicts or unintended behavior, you should ensure that:

1. Each biome is assigned to only one `BiomeGroup`.
2. If assigning a biome to multiple groups is unavoidable, carefully order the groups in `BiomeGroups.yml` based on priority, keeping the **first appearance rule** in mind.

### Growth Modifier Selection

This table illustrates the conditions under which different growth events for plants occur.&#x20;

Each condition is determined by four factors: \
whether the biome is valid, whether the environment is dark, whether UV light is enabled, and whether fertilizer is active. \
Depending on the combination of these factors, one of four outcomes (or a special case) is triggered.

#### Key Factors:

1. **Valid Biome**: Indicates if the plant is in a biome where growth is allowed. A valid biome is essential for normal growth.
2. **Is Dark**: Specifies whether the environment is dark. Darkness can inhibit growth or trigger plant death in some cases.
3. **UV Enabled**: Determines if UV light is present. UV light can promote growth or act as a special modifier.
4. **Fertilizer Enabled**: Indicates whether fertilizer is active. Fertilizer often enhances growth under valid conditions.

<table data-full-width="false"><thead><tr><th width="134">Valid Biome</th><th width="105">Is Dark</th><th width="120">UV Enabled</th><th width="165">Fertilizer Enabled</th><th>Event</th></tr></thead><tbody><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><strong>Special Case</strong> - <br><mark style="color:yellow;">UV-Light</mark> * <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:blue;">Normal</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:blue;">Normal</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:blue;">Normal</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:blue;">Normal</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:purple;">Kill Plant</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:red;">false</mark></td><td><mark style="color:yellow;">UV-Light</mark></td></tr><tr><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:green;">true</mark></td><td><mark style="color:yellow;">UV-Light</mark> + <mark style="color:orange;">Fertilizer</mark></td></tr></tbody></table>

#### Growth Event Outcomes:

1. <mark style="color:purple;">**Kill Plant**</mark>:\
   The plant gets killed, regardless of other factors.
   * **Example**: If a plant is in an invalid biome without fertilizer, it will die immediately.
2. <mark style="color:orange;">**Fertilizer Effect**</mark>:\
   Fertilizer can enable growth even in an invalid biome at a reduced growth rate.
   * **Example**: In an invalid biome with fertilizer applied, the plant can grow at the `fertilizer_invalid_biome_growth_rate`
3. <mark style="color:blue;">**Normal Growth**</mark>:\
   When the plant is in a valid biome, it grows under default conditions defined by `GrowthRate` and `NaturalDeathChance`.
   * **Example**: A plant in a valid biome, without UV light or fertilizer, grows at the standard rate.
4. <mark style="color:blue;">**Normal Growth**</mark>**&#x20;with&#x20;**<mark style="color:orange;">**Fertilizer**</mark>:\
   If fertilizer is applied in a valid biome, the plant benefits from enhanced growth while maintaining the default biome conditions. This results in faster growth.
   * **Example**: A plant in a valid biome with fertilizer applied grows more quickly than normal due to the fertilizer effect.
5. <mark style="color:yellow;">**UV Light Growth**</mark>:\
   In a valid biome, UV light allows plants to grow even in dark environments, such as underground farms. The UV light modifier overrides the need for natural sunlight.
   * **Example**: A plant in a valid biome can grow underground with UV light, even if there is no direct sunlight access.
6. **Special Case –&#x20;**<mark style="color:yellow;">**UV Light**</mark>**&#x20;+&#x20;**<mark style="color:orange;">**Fertilizer**</mark>:\
   When both UV light and fertilizer are active in an invalid biome with no direct sunlight access, the plant enters a special growth rate, which is determined by a combination of the `fertilizer_invalid_biome_growth_rate` and the `UVLightGrowthRate`.
   * **Example**: A plant in an invalid biome, surrounded by darkness, grows at a combined special rate when exposed to both UV light and fertilizer.

***
