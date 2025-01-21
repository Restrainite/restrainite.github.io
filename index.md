---
layout: default
title: Home
---

## Welcome

Restrainite is a [ResoniteModLoader](https://github.com/resonite-modding-group/ResoniteModLoader) mod for 
[Resonite](https://resonite.com/) that allows others to control restrictions of the local user. 

With the current use of dynamic variables, it's not possible to restrict the access. Anyone in
your game world can toggle it. Please keep that in mind and use the options in the extensive settings menu.
There is currently no known way to restrict this based on user ids or similar, because of how the FrooxEngine works. 
(PRs welcome!) We might add an option to use cloud variables in the future.

## Beta Release

We are currently polishing up the mod and expect a release on **Friday, 24th January 2025**.

## Settings

The mod uses presets to easily switch between different sets of restrictions. When the `None` preset is active, the mod
is inactive and will not create status components.

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

## How to interact with the mod

This mod creates a DynamicVariableSpace `Restrainite Status` under the root slot of the User and 
a `Restrainite Status` slot with all restriction options. If the preset in the config is set to None, 
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

If you create a remote, use the tag "RestrainiteRemote" on the object root. This helps with the restrictions 
`Deny Grabbing By Slot Tags` and similar.

## Why does this exist?

There are people who have various reasons for wanting certain features of the game disabled. A lot of these features 
can also be disabled through other means like Protoflux and could be seen as malicious, because then they could be 
applied to anyone. Those in-game items already exists. In NeosVR there also existed the NeosNoEscape mod, with similar 
objectives.

Some features can't be disabled with in-game code, so people could try to find in-game exploits to achieve their goal.
This presents a strong incentive to not report any security exploits they find. The primary motivation behind this mod 
is not to remove safety features, but give people a consenting choice to disable them.

If someone is using this mod maliciously, this a moderation issue. 

## How to get yourself unstuck

With the default settings, restarting the game will remove all restrictions. If you still manage to get yourself 
completely stuck, you can always delete or modify the Restrainite settings file. 
For MonkeyLoader that is under `MonkeyLoader/Configs/Restrainite.json`.
