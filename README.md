# About

Somewhat rough but functional VR mod to allow HS2 VR fun.

Credit to https://github.com/OrangeSpork/HS2VR.
Credit to killmar-the-3rd for the initial implementation, this builds on his work. https://github.com/killmar-the-3rd/HS2VR
Credit for the underlying library (VRGIN) goes to Eusth (https://github.com/Eusth/VRGIN) and Ooetksh for their AI-Shoujo version.
The present Honey Select 2 VR mod is based off (https://github.com/Ooetksh/KoikatuVR). 

# What Works?

Everything, albeit with some quirks. Main game, Maker and Studio are all playable. The full game experience, only in 3D.

# FAQ

## No Controllers/I don't want to use mouse/keyboard
Switch to Standing mode then (def: Ctrl+c, Ctrl+c [dbl tap it]). Alternatively change the DefaultMode in VRSettings.xml.

## I can see the title scene in VR but have no UI
Two possibilities, One: you are in Standing mode (check VRSettings.xml to see your startup default) and have no controllers. Try making sure the controller is tracking and visible before starting HS2, things don't always attach correctly if you start the controller after the program starts. Two: the Steam and GlobalGameManagers patched in correctly to start Unity in VR but the plugin itself isn't installed or failed to start. Double check that the HS2VR.dll is in BepInEx/Plugins/HS2VR and/or check the output_log.txt and see if something killed the VR plugin from starting (missing prereqs or the like).

## Display is Blurry
Turn off TAA. Disable BetterAA (or uninstall it). Switch to SMAA (in Graphics->Post Processing)

## Mouse input is registering at all or not registering on parts of the window
The VR input system actually moves the system mouse pointer. Remove HMD and make sure there isn't another window (curse you steam VR status overlay) over the game window (or run game full screen). Probably the pointer has escaped and you are actually clicking into something else.

## Framerate Issues
Turn off MSAA. Turn off Realtime Reflection Probes (in Graphics->Settings).\
Keep 1 Directional Light with Shadows enabled (you can turn down shadow strength all the way to 0 if you like, just leave shadows enabled). If you don't know what this means, just don't turn off shadows globally or turn off shadows on the Cam light in specific.\
Turn down/off SSS.\
Turn down RenderScale (in VRSettings.xml file). Something along a .6 to a .8 should give you a nice little bump in frame rate.

## I have the hardware, can I make it look better?
In addition to the usual graphics quality settings, turn up RenderScale (in VRSettings.xml file). Something along 1.2 to 1.4 will look nicely sharper. Note above 1.8 will be a slideshow on best possible current hardware.

## What VR sets are supported?
Anything that supports SteamVR (OpenVR) should work just fine.

## Various ingame fluids aren't showing
In the game settings, set the various fluid types to Simplified. That'll fix most, though the drip from her afterwards does not seem to work, no fix for that currently available.


# Specific Improvements from V 0.2.0

Plugin coexists with the official VR plugin now, you can have them this installed and still use official VR as you wish.

Seated mode works (and is the new default). This mode is VR + mouse/keyboard, controllers not needed. Controls are the same as the 2D game except the UI floats in front of your face. Use the mouse and keyboard to drive. Switch to Standing mode (where the UI is attached to the controllers) by pressing Ctrl+C, Ctrl+C (double tapping ctrl-c). You can change the default mode (and various other stuff) in the VRSettings.xml file in game root.

Maker now functions and has a visible UI.

Major camera improvements for both seated and standing. Basically everything should now work as expected, no more ending up in strange places and facing backwards. Title, lobby, H and dialog scenes will attempt to adjust for the FOV change by moving the camera closer to the girl so she occupies the expected amount of view space (otherwise you feel weirdly far away). Note that the fixed VR FOV causes some camera positions to be a bit amusing (like the 2D view of the ledger books that in 3D has you standing on the counter instead).

Camera buttons in studio now work, as do the in scene movable camera views, though selecting the in scene cameras can be fun since the dropdown is invisible.

Compatibility with POVX plugin: https://github.com/Animal42069/HS2_PovX version 1.2.2(+)

Lock mode, when POVX is engaged pressing lock button (default 'L') will freeze the head updates and lock the POV camera in place. Press L again to release. Handy to avoid some of the shaky-cam jerkiness.

New Standing Mode Tools:

POV Tool (eyeball icon). Available when POVX is. 
- Press grip or A to engage POV mode. 
- Pressing trigger when POV is not engaged will engage POV
- Pressing trigger when POV is engaged will switch characters
- Long press trigger (1.5 secs, until it rumbles) and release will engage lock mode (discussed above)
- Press the touchpad button to switch focus characters (look at target)

Gimbal Tool (err, rotatory icon thingy)
- Press grip or A button and rotate controller to rotate view. Allows full 3d rotation rather than just the y rotation of the warp tool

Camera Tool - Studio Only (cam icon) (combines grip/A move of Warp Tool but swaps the actual warping for HS2 camera selection controls)
- Press trigger to switch through the camera presets (the 1-10 camera buttons)
- Long press trigger (hold for 1/2 second or more and release) to reverse switch through camera presets
- Press touchpad/touchstick button to cycle through Scene (object) cameras (the dropdown camera box) - last selection will return normal camera control (clear selection)
- Long press touchpad/touchstick (hold for 1/2 second or more and release) to reverse cycle through Scene (object) cameras (the dropdown camera box)
- Use Grip/A to move camera (like warp tool)
- When Scene/Object camera is engaged - Use Grip/A to fly the camera around (note: actually moves the camera object - so it'll permanently reposition it)

Tool Selection:
- In VRSettings.xml (run once with latest code to update the file with new options) you can select which tools are assigned to which controllers and in which order they appear. Leave a tool out entirely if you don't want it.

# Known Issues

Switching modes (Seated to Standing or vice versa) results in an awkward camera height, simply switch scenes or camera views to correct it.\
It's possible to come out of an HScene or Maker with the view tilted. If that happens switch modes and then switch back (Ctrl+C, Ctrl+C - double tap control c to switch).\
3D space studio object manipulation is basically impossible as the raycast source and your eyeballs are now different. You can use the move controller and HS2PE to work around a lot of this, but there are limits.\
Certain GUI elements in studio have a raycast component that renders them invisible in VR. Specifically the scene settings, camera light and the in-scene camera selection drop down. They are present and actually clickable just not visible. Maniputlation of scene settings will probably need to be done outside of VR unless you have incredible spatial memory. Camera light can be adjusted in Graphics instead. The camera selector drop down isn't too hard to click blind...

# Notes on Graphics Mod and VR

Some notes on VR graphics settings:

Since the VR interface is in scene TAA applies to it and tends to make it a bit blurry, probably stick to SMAA in scenes (though I break this guideline all the time...)\
For best VR performance I recommend turning off MSAA and Realtime Reflection Probes (on Settings) and lowering the SSS settings Postprocess Iterations to 2 and Shader Iterations per pass to 4. Deactivating dither may help, although I didn't notice a big difference.

Note: Be careful with shadows, it might be a quirk of my setup but turning off shadows cuts my frame rate in half. Don't assume turning shadows off improves frame rate in VR, test first.

# Simple Installation

Requires HS2DX (will not work with vanilla HS2), BepInEx

Unzip the HS2VR.zip file into your base game directory. 

BACKUP YOUR GLOBALGAMEMANAGERS (in HoneySelect2_Data and StudioNEOV2_Data - make a copy of the file globalgamemanagers somewhere safe)

Either patch the globalgamemanagers in HoneySelect2_Data and StudioNEOV2_Data yourself or use the ones from the release section. MAKE SURE YOUR GAME VERSION MATCHES THE GLOBALGAMEMANAGERS VERSION. As of latest this is for HS2DX V1.2.3 ONLY. If the word 'patch' confuses you, just download and unzip the one from the release section of the GitHub (where you download the plugin from).


# Installation Detail
## Enabling VR - Only Needed if you don't use the attached globalgamemanagers file
## Experts only - Mostly here in case there's a future game update and I'm mysteriously unavailable and someone needs to repatch this. 
## No Really - Just use the included version, it's easy to make small mistakes with the below and cause problems...weird problems.


- Get UABE (https://github.com/DerPopo/UABE).
- Open `HoneySelect2_Data/globalgamemanagers`
- Find the asset of Type BuildSettings
- Export Dump
- Open the exported dump with a text editor and change the lines

```
0 vector enabledVRDevices
0 Array Array (0 items)
0 int size = 0
```
to
```
0 vector enabledVRDevices
0 Array Array (2 items)
0 int size = 2
[0]
1 string data = "None"
[1]
1 string data = "OpenVR"
```
- Import Dump and save. It won't allow you to overwrite the file in the game directory, so save it somewhere else and make a backup of your original `globalgamemanagers` before copying your patched version into `HoneySelect2_Data`.

You can also find a pre-patched `globalgamemanagers` on discord.

To check that VR is working, start Steam VR and run `HoneySelect2.exe` with the the option `-vrmode "OpenVR"`. This should show the game in VR, albeit without any UI.

## Install the mod

Copy `BebInEx` and `HoneySelect2_Data` folders into your game directory. That should deposit `HS2VR` in `BebInEx/plugins` and `openvr_api.dll` in `HoneySelect2_Data/Plugins`.

If SteamVR is running, the game should start in VR mode. If you need to force the game into non-VR mode while SteamVR is running and don't want to disable the VR mod for whatever reason, pass the `--novr` command line argument.

## Controls
The controls follow the `VRGIN` setup: 
- The B/Y buttons switch the current tool.
- The menu tool gives access to the UI. Use the grip button to grap the UI plane and reposition it.
- The warp tool allows movement. Grip button moves the camera, grip+trigger rotates it. Clicking the touchpad warps the camera to the indicated location.
- The play tool allows for interaction during H-Scenes. For now, moving the touchpad up/down acts as the mouse wheel for starting, speed up, and speed down. Pressing touchpad left/right cycles through the finish options, pressing in the center actives the current active option.

# Building from source

The mod currently uses a patched `VRGIN.dll` from the AI-Shoujo VR mod by Ooetksh, not the included git submodule. Once that version of VRGIN makes it onto github, the repo can be updated to include it.
