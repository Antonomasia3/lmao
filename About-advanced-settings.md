The settings in this page are intended for specific use cases. Their functionality is described in this article. Please refrain from using them unless you are certain you need them.

## Enable console

This allocates a console window for Explorer. In there, debug information about what ExplorerPatcher is doing is printed. It may look something like this:

![image](https://user-images.githubusercontent.com/6503598/145723502-a969a371-c24c-434a-84b3-addc37d3934d.png)

This is very useful when debugging ExplorerPatcher. It may be useful to enable it when trying to trace an issue. In day to day use, it is not required and should be kept disabled.

Also, please note that closing that window will restart File Explorer. To be able to close it, disable "Enable console", then close the window.

## Dump memory leaks

Prints information about block of memory currently allocated by ExplorerPatcher in the console. Does something observable only if you have "Enable console" active.

Also, please note that memory allocations are instrumented only in debug builds. You will see nothing when using this with a release build of ExplorerPatcher, like the ones distributed from GitHub. As well, this option resets to disabled as soon as it is used, so you will always see a cross near it, never a tick.

The output looks something like this:

```
[Memcheck] Dumping memory leaks...
Detected memory leaks!
Dumping objects ->
C:\Users\root\Documents\Visual Studio 2019\Projects\ExplorerPatcher\ExplorerPatcher\SettingsMonitor.c(9) : {354} normal block at 0x000000001234AF50, 96 bytes long.
 Data: <        0       > 80 00 00 00 00 00 00 00 30 03 00 00 00 00 00 00
C:\Users\root\Documents\Visual Studio 2019\Projects\ExplorerPatcher\ExplorerPatcher\dllmain.c(5512) : {64} normal block at 0x0000000000679F50, 24 bytes long.
 Data: < `h             > 10 60 68 00 00 00 00 00 0C 00 00 00 00 00 00 00
C:\Users\root\Documents\Visual Studio 2019\Projects\ExplorerPatcher\ExplorerPatcher\dllmain.c(5375) : {63} normal block at 0x0000000000686010, 6720 bytes long.
 Data: <                > 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
Object dump complete.
[Memcheck] Memory leak dump complete.
[Memcheck] Objects in use:
GDI     GDIp    USER    USERp
281     295     157     180
```

This is VERY useful to determine whether the application leaks memory. Basically, all the entries shown should come from controlled and known sources. It is of high importance especially for the application developers.

## Double click the taskbar to toggle auto-hide

This option is not working as intended and it is subject to being removed in the future. What it should to is toggle the taskbar's auto-hide status when the user double clicks it. At the moment (v41.0), it works like this:

* Windows 10 taskbar: Works only on the primary taskbar, and only when the "Lock taskbar" option is set. Does not work when the taskbar is unlocked or on secondary taskbars.
* Windows 11 taskbar: Works on both primary and secondary taskbars

The reason it fails to work properly with the Windows 10 taskbar is because the old taskbar actually can do stuff in regard to user clicks on it (for example, its internal state machine transitions to a new state when the user presses the button, expecting an eventual drag). If I hook and inhibit this behaviors, you lose built-in features. If I do not inhibit it, the taskbar redirects the subsequent click (which would make a double click) to some other surface, and the hook is unable to capture it and figure out whether the user double clicked. The only way to reliably catch the double click is to install a global mouse hook, but I do not really fancy doing this just for this functionality. A working alternative that uses global mouse hooks is to use an AutoHotkey script. More details in [this thread](https://github.com/valinet/ExplorerPatcher/discussions/389), where the implementation of this feature is discussed.

## Show Windows build info on the desktop

Displays the current Windows build on the desktop, similar to how it appears by default in Insider Preview builds. Like so:

![image](https://user-images.githubusercontent.com/6503598/145723758-7e7eef77-a586-409d-b6c1-22f9248551dd.png)

## Enable advanced mitigations for correct rendering using classic theme

Enables supplementary hooks and code paths in ExplorerPatcher that mitigate issues with the Windows UI when themes are disabled. This is mainly used by people using this to enable the classic theme. More details about this [here](https://github.com/valinet/ExplorerPatcher/discussions/167) and [here](https://github.com/valinet/ExplorerPatcher/discussions/101).

## Enable SysListView32 for Explorer views

Enables the legacy control used to display folders in File Explorer. This control is deprecated, but some people prefer it, especially because it integrates better with the classic theme, providing less padding. On the other hand, it has known issues with the dark theme, for example, as described [here](https://github.com/valinet/ExplorerPatcher/issues/316).

## Hide the program settings item ("Properties") from the taskbar context menu

By default, to access the program's configuration interface, you can right click the taskbar and choose "Properties" from the context menu. However, that can interfere with some people's muscle memory of the menu, and thus this advanced option is provided to hide the item. Beware that if you enable this, you may be left with no graphical way of accessing the configuration interface (you still have the option to enable a similar item to be shown in the Win+X menu - check out the "Other" section). If you are facing such a situation, click the Start button, type "run" (or press [Win]+[R]) and enter the following command: `rundll32 C:\Windows\dxgi.dll,ZZGUI` to open the configuration window manually.

## Enable symbols download

You can use this to prevent the application from automatically downloading symbol data from Microsoft when symbol data is not already present locally or built right into the application itself. This is usually the case with new Windows Insider builds, or immediately after a new Windows stable build is released. More information about symbols is available [here](https://github.com/valinet/ExplorerPatcher/wiki/Symbols).

## Do not hook Start menu from main Explorer process (permanently disabled)

This does not have any effect and should be left disabled.

## Supplementary delay at logon

Allows you to configure a custom delay at logon before the `ShellDesktopSwitchEvent` switch event is signaled. Signaling this event is what makes `winlogon` hide the login screen (the thing where it shows your user account's name and the text "Welcome") and display the desktop. By default, the application automatically determines the best delay to apply, but you can override that here.

P.S. The delay at logon when using the `UndockingDisabled` registry entry instead of `explorer` is caused because nothing signals that event in Windows 11 when using the classic taskbar, for some reason only Microsoft *may* know.