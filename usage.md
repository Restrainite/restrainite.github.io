---
layout: default
title: Installation and Usage
nav_order: 2
---

# Installation and Usage

## Download

You can download the latest Restrainite.dll from [Releases](https://github.com/Restrainite/Restrainite/releases).

## Installation

1. Install either [MonkeyLoader](https://github.com/ResoniteModdingGroup/MonkeyLoader.GamePacks.ResoniteModLoader) or
   [ResoniteModLoader](https://github.com/resonite-modding-group/ResoniteModLoader).
2. Place [Restrainite.dll](https://github.com/Restrainite/Restrainite/releases/latest/download/Restrainite.dll) into your 
   `rml_mods` folder. This folder should be at `C:\Program Files (x86)\Steam\steamapps\common\Resonite\rml_mods` for a 
   default install. You can create it, if it's missing.
3. If you use ResoniteModLoader, install [ResoniteModSettings](https://github.com/badhaloninja/ResoniteModSettings)
4. Start Resonite.
5. If you use ResoniteModSettings, enable `showNames - Whether to show the internal key names next to descriptions` in the ResoniteModSettings Mod settings.
6. Check the settings menu to customize your options.

{: .important }
With the current use of dynamic variables, it's not possible to restrict the access by others. Anyone in
your game world can toggle it. Please keep that in mind and use the options in the extensive settings menu.
There is currently no known way to restrict this based on user ids or similar, because of how the FrooxEngine and 
the network protocol works. (PRs welcome!) We might add an option to use cloud variables in the future.

## Settings

Restrainite offers you, the restrainee, detailed controls over which restrictions can be applied to you. These can be
changed in real-time if you have a way to edit mod configurations from in-game.

- If you are using ResoniteModLoader, install the [ResoniteModSettings](https://github.com/badhaloninja/ResoniteModSettings/releases) mod.
- If you are using MonkeyLoader, mod setting should be available in the stock settings menu.

If you use ResoniteModSettings, enable `showNames - Whether to show the internal key names next to descriptions` in the ResoniteModSettings Mod settings.

The mod uses presets to easily switch between different sets of restrictions. When the `None` preset is active, the mod
is inactive and will not create status components. This means that the mod is practically undetectable when inactive.

The mod settings are broken up into a couple of groups as follows.

### Presets

Restrainite has a preset system to quickly switch between different sets of active restrictions. There are a total of 8
preset options:
- 2 Default (All & None)
- 5 Stored (Alpha, Beta, Gamma, Delta, Omega)
- A "Customized" fallback, when not using a stored preset.

When the `Preset` option is changed to *All* or *None*, every restriction type is enabled or disabled respectively. The
*Customized* preset is automatically switched to if you have a mixture of enabled/disabled restrictions, and you aren't
using one of the stored presets. The *Stored* presets are persistent, meaning any restrictions changed while one is
active will be saved to that preset. The *Customized* preset is not saved.

The `Preset on Startup` option will determine what preset is used by default, but this gets overridden by the options
under listed in the "World visibility/access presets" section below.

### Prevention types

See the [Features / Restrictions](features.html) page for a description of each restriction type. All the toggles in
this section determine whether the respective restriction can or can not be applied to you. Enabling an option here does
not apply the restriction, it only allows it to be applied by compatible items.

Again, if your currently selected `Preset` is a stored preset, any changes you make will be saved to that preset.

### Password

It's possible to set a password for each preset. Please note, that the password is not secret, once it's being used and then
anyone can read it in the inspector or via Protoflux. If someone is copying the password manually or automatically with the 
intent of misusing it, this is a breach of consent and a moderation issue.

- If a password is set, then the restrictions will only activate, if the password is also set in a 
`DynamicValueVariable<string>` component named `Password` in the slot or a child slot of the
`DynamicVariableSpace` `Restrainite`.
- If no password is set, the value of the `DynamicValueVariable<string>` component named `Password` is ignored.

The `DynamicVariableSpace` `Restrainite Status` has a `DynamicValueVariable<bool>` component named `Requires Password` 
to show, if a password is required or not.

### World visibility/access presets

All the options in this section, `Change to Preset, if world permissions are ___` are a safety mechanism to disable (or
automatically enable) parts of the mod if your current world's visibility and/or access level is changed. Setting one of
these values to "DoNotChange" will, as it says, not change the preset if the condition is met.

The default options will disable all prevention types if the world goes from private to public.

### Miscellaneous

- `Allow Restrictions from Focused World only`: When enabled, only your currently focused world is checked, when
determining which restrictions should be applied. Otherwise, any world you have open can apply restrictions that will
affect you in your currently focused world.
- `Set online status to busy`: When you are unable to reply to messages due to restrictions, automatically set online 
status to busy, if you are not invisible.
- `Send dynamic impulses`: Sends dynamic impulses to any Flux within your user root every time a restriction is enabled
or disabled.

Two or more impulses will be send:
 - One of type string to `Restrainite Change`, that contains a string representation of the change.
 - One of type bool to `Restrainite ` and the name of the restriction, e.g. `Restrainite Prevent Equipping Avatar`.
 - If the restriction is of type float, it will send one of type float to `Restrainite ` and the name of the restriction, 
e.g. `Restrainite Hearing Volume`.
 - If the restriction is of type string, it will send one of type string to `Restrainite ` and the name of the restriction,
   e.g. `Restrainite Show User Avatars`.

## Features / Restrictions

See [Features / Restrictions](features.html) page.

## How to interact with the mod

### Status output
This mod creates a `DynamicVariableSpace` `Restrainite Status` under the root slot of the User and 
a `Restrainite Status` slot with all active restriction options. If the preset in the settings menu is set to `None`, 
the `DynamicVariableSpace` and the `Restrainite Status` slot will not be created, or it will be deleted, if it already exists. 
Restriction settings, that are not enabled by the user, will also not have a slot under the `Restrainite Status` slot. 
These `DynamicValueVariable<bool>`s are for output of the current state only and should not be modified. 
The status is also available under the UserRoot slot in Userspace.

### To interact with this and activate restrictions
- Create an empty slot or use an existing one.
- Add a `DynamicVariableSpace` component with the name `Restrainite` to it.
- Add a `DynamicReferenceVariable<User>` component with the name `Target User`, that points to the user who should be 
affected by the restriction.
- If a password is set, add a `DynamicValueVariable<string>` component with the name `Password` and the value of the password.
- Add a `DynamicValueVariable<bool>` component with the name listed in the tag of the restriction under the `Restrainite Status`
slot or on the [features page](features.html).
- Toggle the value to enable/disable the restriction.

[Screenshot of the steps above](basic_setup.jpg)

For certain features (marked with **[+ string]** on the [features page](features.html)), it's also possible to add 
a `DynamicValueVariable<string>` component with the same name, to select for example which Context Menu Items should 
be shown or hidden. The string is a comma separated list. If items are from the base game, use the locale keys to 
refer to them, e.g. Interaction.Undo. See [Resonite Locale](https://github.com/Yellow-Dog-Man/Locale/blob/main/en.json)

For certain features (marked with **[+ float]** on the [features page](features.html)), it's also possible to add 
a `DynamicValueVariable<float>` component with the same name, to set a value. 
Unless otherwise noted, the smallest value is used, if more than one exists.

If you create a grabbable control object, we recommend to use the tag `RestrainiteRemote` on the object root. This helps with the restrictions 
`Deny Grabbing By Slot Tags` and similar.

The `DynamicVariableSpace` `Restrainite Status` in Userspace contains a `DynamicValueVariable<string>` named `Preset` to easily read and change 
the current preset selected on the configuration screen.

Restrictions are disabled, if a local world is focused.

### How to use By Slot Tags restrictions

There are currently the following restrictions that can be restricted to slot tags:
- `Allow Grabbing By Slot Tags` and `Deny Grabbing By Slot Tags`
- `Allow Touching By Slot Tags` and `Deny Touching By Slot Tags`
- `Allow Hearing By Slot Tags` and `Deny Hearing By Slot Tags`

This checks the tag of slot that triggered the event, for example the one containing the audio output component, and it
checks the tag of the object root slot, that is the current or any parent slot that contains the object root component.

If the slot tag is empty, it will be evaluated as the string `null`.

If `Allow * By Slot Tags` is active, the component slot tag and/or the object root slot tag must be in the allow list,
to be allowed by the restriction. If neither of the tags is in the allow list, it is disallowed.

If `Deny * By Slot Tags` is active and the component slot tag and/or the object root slot tag is in the deny list, then
it is disallowed by the restriction. Deny takes precedence over Allow.

This behaviour has slightly changed in version v1.2.0.

## How to get yourself unstuck

With the default settings, restarting the game will remove all restrictions. If you still manage to get yourself 
completely stuck, you can always delete or modify the Restrainite settings file in the Resonite game folder. 
- For MonkeyLoader that is under `MonkeyLoader/Configs/Restrainite.json`.
- For ResoniteModLoader that is under `rml_config/Restrainite.json`. 
