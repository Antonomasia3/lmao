The default installation of ExplorerPatcher works great, enabling lots of customization possibilities. There is one area it cannot touch though: Open/Save file dialogs. Technically, that's because those run in the process that invoked them (say, you click File - Open in Notepad, the Open dialog runs in `notepad.exe`). Currently, ExplorerPatcher only injects the following processes (by exploiting the DLL search order):

* `explorer.exe` - that's where the taskbar and most of the stuff live in at runtime
* `StartMenuExperienceHost.exe` - that's the process that hosts the Start menu
* `ShellExperienceHost.exe` - that's the process that hosts the taskbar flyouts (like network, battery, sound etc)

So, for certain tweaks enabled by ExplorerPatcher to have effect in all applications, you can have it get injected in all applications. There are multiple ways to do this, and what ExplorerPatcher employs is registering itself as a shell extension which will have it get loaded in every process that invokes an Open/Save file dialog.

**!!! IMPORTANT !!! Injecting in all process is no mean feat: that means most processes running on you system have this piece of code running into it. While I strive to provide clean and bug free releases, mistakes or problems may appear from time to time, and this has the potential of making more troublesome than usual to recover the system if something goes wrong, so beware before deciding towards using this.**

Currently, only a small subset of functionality is enabled by using ExplorerPatcher as a shall extension:
* Disable immersive context menus in Open/Save file dialogs
* Disable the navigation bar in all Open/Save file dialogs
* Hide the search bar

That's it. If you don't need those, I don't recommend using this. Also, here's what ClassicShell's developer had to say about this matter, basically in line with what I caution against here. From [here](http://www.classicshell.net/faq/#explorer_saveas):

> **Can Classic Shell add Up button to the system SaveAs or Open dialogs?**
>
> No. The SaveAs and Open dialogs are controlled by the application - Notepad, Word, Photoshop, etc. It is theoretically possible to do something about it, but there are many problems to do it correctly. Here's just a few:
>
>    Every application is unique. There is no way to ensure stable work for arbitrary applications. Often applications take steps to customize their dialogs and there is a great potential for conflict.
>    Doing anything like this is a guaranteed way to get an endless list of compatibility bugs. Unlike Microsoft I don't have a compatibility lab with access to thousands of applications to play with. If a problem appears with some application that I don't have there is no way for me to debug it.
>    The first step in any such feature will be to inject code in every running application. This act will most likely be flagged as malware by anti-virus software. It will also negatively affect system performance.
>
> Maybe a future version of Classic Shell will have this feature if I find solutions to all the problems.

With those things considered, here's what you should know: shell components register themselves as COM objects in the system. ExplorerPatcher's CLSID (a CLSID is a GUID, which is an ID that does not need a central authority to guarantee its uniqueness property) is `{D17F1E1A-5919-4427-8F89-A1A8503CA3EB}`. This feature creates and deletes the following registry entries:

* `HKLM\SOFTWARE\Classes\CLSID\{D17F1E1A-5919-4427-8F89-A1A8503CA3EB}` - COM component in-process server registration for 64-bit processes
* `HKLM\SOFTWARE\WOW6432Node\Classes\CLSID\{D17F1E1A-5919-4427-8F89-A1A8503CA3EB}` - COM component in-process server registration for 32-bit processes
* `HKLM\SOFTWARE\Classes\Drive\shellex\FolderExtensions\{D17F1E1A-5919-4427-8F89-A1A8503CA3EB}` - contains information about the type of shell extension ExplorerPatcher is

The checkbox in the interface automatically registers or removes the registration for the component on your system. After removing the registration, it is recommended to reboot the system so that the library gets unloaded from all applications. The way this works in the back is that either of these commands get executed:
* `regsvr32 "%PROGRAMFILES%\ExplorerPatcher\ExplorerPatcher.amd64.dll"` - to register
* `regsvr32 /u "%PROGRAMFILES%\ExplorerPatcher\ExplorerPatcher.amd64.dll"` - to remove the registration

The way `regsvr32` works is it simply calls either the `DllRegisterServer`, either the `DllUnregisterServer` exports from ExplorerPatcher, and that takes care of servicing this task on the system.

When uninstalling, ExplorerPatcher has its registration automatically removed from the system, if you previously registered it, using any of the above methods.