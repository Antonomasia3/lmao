Besides providing a vast array of customization options, ExplorerPatcher has recently received the ability to export its configuration data to a file on the hard disk. The file can then be roamed to other computers and imported directly right from the "Properties" interface.

Currently, all options supplied via the user interface can be roamed using exported settings file.

# Export the current settings

For this, open "Properties", go to "About" and click "Export current settings". Choose a location where you'd like to save the file and that's it.

Beware that the exported files end in `.reg` extension. They also follow the syntax the Registry Editor is able to understand. Thus, it is possible to partially restore your settings by merging the file directly in the registry, using the Registry Editor. However, depending on your setup, this might sometimes only partially restore your settings. If you look on the file, you may notice a bunch of `;"Virtualized_{D17F1E1A-5919-4427-8F89-A1A8503CA3EB}_` string; those indicate pseudo-configuration settings: they are understood by the parser in ExplorerPatcher, but the Registry Editor doesn't know about them. The reason these exist is mostly because some settings do not map directly to registry entries. As an example, the taskbar position is presented as an individual setting in the interface, but it is actually stored in a byte array in the registry, along with other information. Other settings require special preparations to take effect: for example, registering as shell extension requires elevation beforehand etc.

# Import existing settings

Once you have an exported settings file, you can apply it to any ExplorerPatcher instance. To do this, open "Properties", go to "About" and click "Import settings". Locate your file and open it. Before merging the data, the program will ask whether you're sure to do it. Remember, once you overwrite the settings, you can only get back the old ones manually or from a backup. If you accept, the settings will be restored.

Take notice that, depending on your stored configuration data and the current status of the settings in the ExplorerPatcher instance where you are doing the import, some elevation messages might pop-up:

* A request from "Microsoft(R) Register Server": this is the helper program that registers ExplorerPatcher as a shell extension on the computer, if you opted for the setting.
* A request from "Windows Command Processor": this is the helper program that configures the service which restores not rounded corners in the Desktop Window Manager, if you opted for this setting.

After performing this operation, I strongly recommend restarting File Explorer so that all the configuration data loads properly.

# Restore default settings

Similar to the others, go to "Properties", the "About" section and click "Restore default settings". The process is similar to importing settings, only that you don't have to locate a file - the data is backed into the program's memory.

After performing this operation, I strongly recommend restarting File Explorer so that all the configuration data loads properly.

# About file compatibility between versions

The format currently in use is in its initial stages of existence. Some minor tweaks might still be made, but generally, the way it ought to work is the one presented in this document. However, I cannot guarantee portability of exported settings files between versions, but I can say that the chance of it working is VERY likely. Compatibility breaking changes might happen only if absolutely necessary.