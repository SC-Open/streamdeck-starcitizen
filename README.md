# streamdeck-starcitizen

**Elgato Stream Deck button plugin for Star Citizen**

![Elgato Stream Deck button plugin for Star Citizen](https://i.imgur.com/FSHsXRG.png)

**At least streamdeck software version 6 is required.**

This plugin gets the key bindings from the Star Citizen game files.

The bindings in the streamdeck plugin are automatically updated when changing bindings in Star Citizen options screen.

The bound key is shown in the dropdown, localised for the current keyboard language (So: US keyboard shows WSAD, French keyboard shows ZSQD)

**The plugin does not contain any button images or ready made streamdeck profiles.**

Credit goes to https://github.com/SCToolsfactory/SCJMapper-V2 and https://github.com/dolkensp/unp4k for all the code to get the `defaultProfile.xml` from the p4k file etc.

The static button works in a similar way, to the streamdeck 'Hotkey' button type.
So, there is only one image and there is no game state feedback for these buttons.
The differences with the 'Hotkey' buttons are, that it gets the keyboard binding from the game.
When the stream deck button is pushed, the 'key down' event is sent to the keyboard
and only after the stream deck button is released, the 'key up' event is sent to the keyboard.

The plugin's multi-action button behaviour is different : when the stream deck button is pushed, the 'key down' event is sent to the keyboard.
After a user-definable delay (default = 40 ms) the 'key up' event is sent to the keyboard. 
Nothing happens when the streamdeck button is released.

Both the static- and multi-action buttons can be used inside the streamdeck built-in multi-action button's action list.

The multi-action button can also be used as a regular streamdeck button, in case a fixed user-definable delay is required between the key down and key up events.

A sound can be played when pressing a button.

**You can clear the sound path, by clicking on the label in front of the file picker edit box.**

You can, for example, use the 'multi-action switch' function, that is built into the streamdeck software, to set up a toggle function.
You can add the relevant function of this plugin to both the ON-and OFF-action of the 'multi-action switch' function.
You can then set up different images for each toggle state.
The disadvantage is: that if you would press e.g. the gear up/down toggle button while the ship is still on the ground/powered off, 
then the button image would be out of sync.

The plugin also has a Dial button for use with the 4 dials on the Streamdeck+ model.

There are 5 bindings (They must be keyboard bindings, you can't bind the mouse wheel!) :

- Dial Clockwise
- Dial Counter-Clockwise
- Dial Press
- Touch screen press
- Touch screen long press

![Dial Image](https://i.imgur.com/MjcGque.png)

When a dial is rotated, the 'key down' event is sent to the keyboard once. 
When you let go of the dial for at least 100ms : the 'key up' event is sent to the keyboard. 

When a dial button is pushed, the 'key down' event is sent to the keyboard. 
When a dial button is released, the 'key up' event is sent to the keyboard. 

When the touch screen is pressed or long-pressed, the behaviour is like the multi-action button :
The 'key down' event is sent to the keyboard. After a user-definable delay (default = 40 ms) the 'key up' event is sent to the keyboard. 

After you install the plugin in the streamdeck software, then there will be new button types in the streamdeck software.

Choose a button in the streamdeck software (drag and drop), then choose a Star Citizen function for that button 
(that must have a keyboard binding in Star Citizen. **A mouse, gamepad or joystick binding won't work!**) 
and then choose any picture for that button.

Add an image to a button in this way:

![Button Image](https://i.imgur.com/xkgy7uZ.png)

Animated gif files are supported. Dial images are 200x50

When the plugin is first started, it finds and opens the game file :

`C:\Program Files\Roberts Space Industries\StarCitizen\LIVE\Data.p4k`

and extracts `defaultProfile.xml` and also english text resources. This could take more than 10 seconds.

**The plugin should automatically find the actual path where Star Citizen was installed.**

The path, that is found by the plugin, is logged in the `%appdata%\Elgato\StreamDeck\Plugins\com.mhwlng.starcitizen.sdPlugin\pluginlog.log` file.

If the path is incorrect, then the `%appdata%\Elgato\StreamDeck\Plugins\com.mhwlng.starcitizen.sdPlugin\appsettings.config` file can be adjusted with the correct paths to the p4k file and the actionmaps.xml directory :

```
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="SCData_p4k" value ="C:\Program Files\Roberts Space Industries\StarCitizen\LIVE\Data.p4k" />
  <add key="SCClientProfilePath" value ="C:\Program Files\Roberts Space Industries\StarCitizen\LIVE\USER\Client\0\Profiles\default" />
</appSettings>
```

Compressed versions (files ending in .scj) are cached in the plugin directory and should be automatically refreshed, the next time Star Citizen is updated to a new version AND the plugin is also restarted.

You can also delete the .scj files and restart the plugin, to extract the files from the p4k file again.

For easier debugging, installation and testing, `defaultProfile.xml`, `keybindings.csv`, `joystickbindings.csv`, `mousebindings.csv`, `unboundactions.csv` and `PropertyInspector\StarCitizen\Static.html` files are created in the plugin directory.

The plugin uses all the active keyboard bindings from `defaultProfile.xml` and then overrules some of the bindings, with any custom keyboard bindings from this file :

`C:\Program Files\Roberts Space Industries\StarCitizen\LIVE\USER\Client\0\Profiles\default\actionmaps.xml`

The `PropertyInspector\StarCitizen\Static.html` and `PropertyInspector\StarCitizen\Macro.html` file is dynamically updated, in case more custom keyboard bindings were added to `actionmaps.xml`, 
that didn't have any corresponding keyboard bindings in `defaultProfile.xml`.

If nothing happens, when pressing streamdeck buttons: you could try to start streamdeck.exe as administrator.

The plugin installer is here: https://github.com/mhwlng/streamdeck-starcitizen/releases

To install the plugin, double click the file `com.mhwlng.starcitizen.streamDeckPlugin` which should install the plugin.

(This only works, if the plugin not already installed. Otherwise you will need to uninstall or remove the plugin first.)

This .streamDeckPlugin file is a zip file and the contents are simply copied to :

`%appdata%\Elgato\StreamDeck\Plugins\com.mhwlng.starcitizen.sdPlugin`

To update to a new version :

Stop the Stream Deck application:

`c:\Program Files\Elgato\StreamDeck\StreamDeck.exe`

Then delete the `%appdata%\Elgato\StreamDeck\Plugins\com.mhwlng.starcitizen.sdPlugin` directory. (make a backup copy first)

Then start the streamdeck software again.

Then double click the file `com.mhwlng.starcitizen.streamDeckPlugin` as usual.

MAKE SURE that you save any images, profiles etc. that you put in these directories yourself, BEFORE deleting the directory.
And put them back after the installation.
The plugin installer doesn't come with button images.

Also, the plugin can be uninstalled and the directory completely deleted by right-clicking on any button and selecting uninstall (make a backup copy first) :

![Button Image](https://i.imgur.com/BAkEuEq.png)

The button configurations are not stored in the plugin directory.

After uninstalling and re-installing the plugin, all the button definition should still be there.

The com.mhwlng.starcitizen.sdPlugin directory contains a pluginlog.log file, which may be useful for troubleshooting.

Thanks to :

https://github.com/BarRaider/streamdeck-tools

https://github.com/SCToolsfactory/SCJMapper-V2

https://github.com/dolkensp/unp4k

https://github.com/ishaaniMittal/inputsimulator

https://nerdordie.com/product/stream-deck-key-icons/

