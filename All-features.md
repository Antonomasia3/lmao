This document describes all the options currently provided by ExplorerPatcher. This is valid for and was compiled at the time of version 22000.343.41.12. Although I strive to keep this up to date, some things might change slightly in the future. If you notice any inconsistencies, feel free to mention them for fixing in the [Discussions](https://github.com/valinet/ExplorerPatcher/discussions) section.

# Taskbar

## Taskbar style

### Windows 10 (default)
Enables the familiar Windows 10 taskbar. It supports all the familiar features, like enabling button labels (never combine), separate network/volume/battery indicators, docking to the top/bottom/right/left side of the screen, plus customizable options via ExplorerPatcher.

> ![image](https://user-images.githubusercontent.com/6503598/150659166-9b980623-66dc-4716-8c7a-72521cc23c98.png)
> Windows 10 taskbar

### Windows 11
Enables the new Windows 11 taskbar. It currently lacks support for showing labels, but supports centered icons; the network/volume/battery indicators are grouped in a single button that opens the "action center".

> ![image](https://user-images.githubusercontent.com/6503598/150659189-c3381a2b-2836-4296-933f-002e67277aa2.png)
> Windows 11 taskbar

ExplorerPatcher enahnces it by providing an enhanced context menu that displays proper options, as the legacy taskbar did, including Task Manager:

> ![image](https://user-images.githubusercontent.com/6503598/150659209-de8d3943-785a-4f5b-95d8-792347658ce6.png)

There are also a number of fixes ExplorerPatcher applies to this new taskbar:
* As shipped by Microsoft, a taskbar displayed on a secondary monitor does not react when the mouse is over it and auto hide is on; fixed this (#589)
* As shipped by Microsoft, under certain circumstances, the main taskbar does not show its system tray when `explorer` starts up and auto hide is on; fixed this
* As shipped by Microsoft, a taskbar displayed on a secondary monitor might display a wrong contextual menu when auto hide is on; fixed this

## Primary/secondary taskbar location on screen

This allows you to set the location of the taskbar on the screen.

When using the Windows 10 taskbar, the following locations are supported:

* Bottom (default)
* Left
* Right
* Top

When using the Windows 11 taskbar, the following locations are supported:
* Bottom (default)
* Top

Although it may not be obvious, when using the Windows 10 taskbar, you don't have to actually use this. You can actually achieve much more by right clicking any taskbar and unticking "Lock the taskbar" or "Lock all taskbars". Then, simply drag any of the taskbars to dock it to whatever edge of the screen you'd like. You can also move it to other monitors - this allows you to move the main taskbar (the one that contains the system tray) to a secondary monitor. This was actually a bug in Windows 10 that was fixed in Windows 11, but ExplorerPatcher restored this functionality due to popular demand.

Don't see additional taskbars on a multi-monitor configuration? Maybe you need to enable that: right click the main taskbar, choose "Taskbar settings", expand "Taskbar behaviors" and check "Show my taskbar on all displays".

> ![image](https://user-images.githubusercontent.com/6503598/150659429-ef73a3ae-0845-4ec3-87b7-0c2a061dc429.png)

## Extra button should be

It allows you to choose how the button having the Cortana icon should act:

* Stay hidden (default)
* Be visible and open Cortana when clicked (only when using the Windows 10 taskbar)
* Be visible and open Widgets when clicked

>![image](https://user-images.githubusercontent.com/6503598/150659475-02cb95dc-f1ce-490b-9528-38e3d2140cc0.png)
> Appearance of the Cortana button on the Windows 10 taskbar

## Show Search button

This displays an icon that opens Windows Search (`Win`+`Q`) when clicked.

> ![image](https://user-images.githubusercontent.com/6503598/150659541-6088837a-5fb3-481f-bdda-c57d6ff62ee5.png)
> Appearance of the Search button on the Windows 10 taskbar

## Show Task View button

This displays an icon that opens Task View (`Win`+`Tab`) when clicked.

> ![image](https://user-images.githubusercontent.com/6503598/150659564-ebe71257-35b5-468d-8f10-00371c7f08e0.png)
> Appearance of the Task View button on the Windows 10 taskbar

## Show Desktop button

This can be used to hide the "Show Desktop" icon located at the far right of the taskbar.

> ![image](https://user-images.githubusercontent.com/6503598/150659604-ba2f5ace-03ab-469c-885d-78eed39bd298.png)
> Appearance of the Show Desktop button on the Windows 10 taskbar



