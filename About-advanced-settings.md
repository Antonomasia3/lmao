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
```

This is VERY useful to determine whether the application leaks memory. Basically, all the entries shown should come from controlled and known sources. It is of high importance especially for the application developers.

## Show Windows build info on the desktop

Displays the current Windows build on the desktop, similar to how it appears by default in Insider Preview builds. Like so:

![image](https://user-images.githubusercontent.com/6503598/145723758-7e7eef77-a586-409d-b6c1-22f9248551dd.png)

## Enable advanced mitigations for correct rendering using classic theme

Enables supplementary hooks and code paths in ExplorerPatcher that mitigate issues with the Windows UI when themes are disabled. This is mainly used by people using this to enable the classic theme. More details about this [here](https://github.com/valinet/ExplorerPatcher/discussions/167) and [here](https://github.com/valinet/ExplorerPatcher/discussions/101).

## Enable SysListView32 for Explorer views

Enables the legacy control used to display folders in File Explorer. This control is deprecated, but some people prefer it, especially because it integrates better with the classic theme, providing less padding. On the other hand, it has known issues with the dark theme, for example, as described [here](https://github.com/valinet/ExplorerPatcher/issues/316).

## Enable symbols download

You can use this to prevent the application from automatically downloading symbol data from Microsoft when symbol data is not already present locally or built right into the application itself. This is usually the case with new Windows Insider builds, or immediately after a new Windows stable build is released. More information about symbols is available [here](https://github.com/valinet/ExplorerPatcher/wiki/Symbols).

## Do not hook Start menu from main Explorer process (permanently disabled)

This does not have any effect and should be left disabled.

## Supplementary delay at logon

Allows you to configure a custom delay at logon before the `ShellDesktopSwitchEvent` switch event is signaled. Signaling this event is what makes `winlogon` hide the login screen (the thing where it shows your user account's name and the text "Welcome") and display the desktop. By default, the application automatically determines the best delay to apply, but you can override that here.

P.S. The delay at logon when using the `UndockingDisabled` registry entry instead of `explorer` is caused because nothing signals that event in Windows 11 when using the classic taskbar, for some reason only Microsoft *may* know.