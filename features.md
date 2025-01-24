---
layout: default
title: Features / Restrictions
nav_order: 3
---

# Features/Restrictions

_(As of version Beta 1.0.0)_

## Interaction
- `Prevent Equipping Avatar`: Prevents equipping in-world avatars or switching from inventory.
- `Prevent Using Tools`: Prevents equipping tools, and drops them if already equipped.
- `Prevent Grabbing`: Prevents grabbing objects physically/via laser, and drops any that are already grabbed.
- `Prevent Laser Touch`: Prevents any laser-based interaction.
- `Prevent Physical Touch`: Prevents any physically-based interaction.
    - _PreventLaserTouch_ & _PreventPhysicalTouch_ also prevent grabbing respectively.
- `Prevent Spawn Objects`: Prevents spawning objects into the current world.
- `Prevent Save Items`: Prevents saving items to the inventory.
- `Allow Grabbing By Slot Tags`: **[+ string]** When enabled, only allows grabbing items with tags in this list.
- `Deny Grabbing By Slot Tags`: **[+ string]** When enabled, prevents grabbing any items with tags in this list.
  - _AllowGrabbingTags_ is evaluated before _DenyGrabbingTags_ if both are enabled.
  - Slots without tag will be evaluated with the string `null`. 
  - _PreventGrabbing_ takes precedence over both of these options.
- `Allow Touching By Slot Tags`: **[+ string]** When enabled, only allows interacting with items with tags in this list.
- `Deny Touching By Slot Tags`: **[+ string]** When enabled, prevents interacting with any items with tags in this list.
  - _AllowTouchingTags_ is evaluated before _DenyTouchingTags_ if both are enabled.
  - Slots without tag will be evaluated with the string `null`.
  - _PreventPhysicalTouch_ and _PreventLaserTouch_ take precedence over these options.
- `Prevent Non Dash Userspace Interaction`: Prevents interacting with anything in userspace besides the dashboard (facet anchors, userspace inspectors, etc.).

## Respawning and changing worlds
- `Prevent Respawning`: Prevents respawning, including emergency respawn gesture.
- `Prevent Emergency Respawning`: Prevents using the emergency respawn gesture (can still respawn via session users tab).
- `Prevent Switching World`: Prevents starting a new world, joining another session, leaving the current world, or changing focus.

## Visual
- `Show User Avatars`: **[+ string]** When enabled, only user avatars are shown, whose user ID (not usernames) is in the list.
- `Hide User Avatars`: **[+ string]** When enabled, user avatars are hidden, whose user ID (not usernames) is in the list.
- `Disable Nameplates`: Hides all avatar nameplates.

## Audio
- `Prevent Hearing`: Forces all other users voices to be muted.
- `Enforce Selective Hearing`: **[+ string]** When enabled, All users will be muted except those whose user IDs (not usernames) are in this list.
  - _PreventHearing_ takes precedence over _EnforceSelectiveHearing_.
- `Prevent Speaking`: Forces the user to be muted.
- `Enforce Whispering`: Forces the user to only be able to talk in whisper mode (they can still mute themselves).
  - _PreventSpeaking_ takes precedence over _EnforceWhispering_.

## UI
- `Prevent Opening Context Menu`: Prevents opening the context menu, and closes it if already opened.
- `Show Context Menu Items`: **[+ string]** When enabled, any context menu items not in this list will be hidden.
- `Hide Context Menu Items`: **[+ string]** When enabled, any context menu items in this list will be hidden.
  - _ShowContextMenuItems_ is evaluated before _HideContextMenuItems_ if both are enabled.
  - For default context menu items, you need to list their locale string names. See the [How to interact with the mod](usage.html#how-to-interact-with-the-mod) section.
- `Prevent Opening Dash`: Prevents opening the dashboard, and closes it if already opened.
- `Show Dash Screens`: **[+ string]** When enabled, any dashboard screens not in this list will be hidden.
- `Hide Dash Screens`: **[+ string]** When enabled, any dashboard screens in this list will be hidden.
  - The exit screen can not be hidden.
  - _ShowDashScreens_ is evaluated before _HideDashScreens_ if both are enabled.
  - For non-custom screens, you need to list their locale string names. See the [How to interact with the mod](usage.html#how-to-interact-with-the-mod) section.
- `Disable Notifications`: The user can't see notifications anymore.
- `Prevent Sending Messages`: The user can't send messages to contacts.
- `Prevent Invite Contact`: The user can't invite contacts to the current world.
- `Prevent Third Person View`: Desktop users can't switch to third person view anymore.

## Locomotion
- `Prevent User Scaling`: Prevents the user from rescaling themselves.
- `Prevent Crouching`: Prevents crouching in desktop mode.
- `Prevent Jumping`: Prevents jumping, but does not prevent exiting anchors.
- `Prevent Running`: Prevents running, when using keyboard (double tap or shift) or gamepad controls (joystick press).
- `Prevent Climbing`: Prevents climbing by grabbing the world or characters.
- `Prevent Change Locomotion`: Prevents the user from changing their locomotion mode.
- `Reset User Scale`: Utility variable that resets a user to their default scale.
  - You should use this by enabling then disabling in the next frame. Think of it like an impulse.
  - Keeping it enabled does not prevent the user from rescaling themselves, and will only prevent other items from using this.
- `Prevent Leaving Anchors`: Prevents the user from leaving any anchor themselves.
- `Prevent Movement`: Prevent the user being able to move around via VR controller or keyboard.
- `Prevent Turning`: Prevent the user from turning his body via VR controller or look around via mouse or keyboard. The user is still able to look around in VR by turning his head. Turning can't be restricted for Gamepad users.
