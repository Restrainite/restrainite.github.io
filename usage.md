---
layout: default
title: Installation and Usage
nav_order: 2
---

# Installation and Usage

## Download

You can download the latest dll from [Releases](https://github.com/Restrainite/RestrainiteMod/releases).

## Installation

1. Install either [MonkeyLoader](https://github.com/ResoniteModdingGroup/MonkeyLoader.GamePacks.ResoniteModLoader) or
   [ResoniteModLoader](https://github.com/resonite-modding-group/ResoniteModLoader).
2. Place [Restrainite.dll](https://github.com/Restrainite/RestrainiteMod/releases/latest/download/Restrainite.dll) into your 
   `rml_mods` folder. This folder should be at `C:\Program Files (x86)\Steam\steamapps\common\Resonite\rml_mods` for a 
   default install. You can create it, if it's missing.
3. If you use ResoniteModLoader, install [ResoniteModSettings](https://github.com/badhaloninja/ResoniteModSettings)
4. Start Resonite.
5. Check the settings menu to customize your options.

## Settings

The mod uses presets to easily switch between different sets of restrictions. When the `None` preset is active, the mod
is inactive and will not create status components.

## Features / Restrictions

See [Features / Restrictions](features.html) page.

## How to interact with the mod

This mod creates a DynamicVariableSpace `Restrainite Status` under the root slot of the User and 
a `Restrainite Status` slot with all active restriction options. If the preset in the config is set to None, 
the DynamicVariableSpace and the Restrainite slot will not be created, or it will be deleted, if it already exists. 
Restriction settings, that are not enabled by the user, will also not have a slot under the Restrainite slot. 
The tag of each restriction slot contains the name of the DynamicValueVariable required to set the value.

To interact with this, create an empty slot. Add a DynamicVariableSpace with the name `Restrainite` to it. Add a 
`DynamicReferenceVariable<User>` component with the name `Target User`, that points to the user who should be 
affected by the restriction. Add a `DynamicValueVariable<bool>` component with the name listed in the tag of the 
restriction. Toggle the value to enable/disable the restriction.

For certain features, it's also possible to add a `DynamicValueVariable<string>` component with the same name, to select
 for example which Context Menu Items should be shown or hidden. The string is a comma seperated list. If items are 
from the base game, use the locale keys to refer to them, e.g. Interaction.Undo. 
See [Resonite Locale](https://github.com/Yellow-Dog-Man/Locale/blob/main/en.json)

If you create a remote, use the tag `RestrainiteRemote` on the object root. This helps with the restrictions 
`Deny Grabbing By Slot Tags` and similar.

## How to get yourself unstuck

With the default settings, restarting the game will remove all restrictions. If you still manage to get yourself 
completely stuck, you can always delete or modify the Restrainite settings file. 
For MonkeyLoader that is under `MonkeyLoader/Configs/Restrainite.json`.
