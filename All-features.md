This document describes all the options currently provided by ExplorerPatcher. This is valid for and was compiled at the time of version 22000.343.41.12. Although I strive to keep this up to date, some things might change slightly in the future. If you notice any inconsistencies, feel free to mention them for fixing in the [Discussions](https://github.com/valinet/ExplorerPatcher/discussions) section.

# Taskbar

## Taskbar style

### Windows 10 (default)
Enables the familiar Windows 10 taskbar. It supports all the familiar features, like enabling button labels (never combine), separate network/volume/battery indicators, docking to the top/bottom/right/left side of the screen, plus customizable options via ExplorerPatcher.

> ![image](https://user-images.githubusercontent.com/6503598/150659166-9b980623-66dc-4716-8c7a-72521cc23c98.png)
>
> Windows 10 taskbar

### Windows 11
Enables the new Windows 11 taskbar. It currently lacks support for showing labels, but supports centered icons; the network/volume/battery indicators are grouped in a single button that opens the "action center".

> ![image](https://user-images.githubusercontent.com/6503598/150659189-c3381a2b-2836-4296-933f-002e67277aa2.png)
>
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
>
> Appearance of the Cortana button on the Windows 10 taskbar

## Show Search button

This displays an icon that opens Windows Search (`Win`+`Q`) when clicked.

> ![image](https://user-images.githubusercontent.com/6503598/150659541-6088837a-5fb3-481f-bdda-c57d6ff62ee5.png)
>
> Appearance of the Search button on the Windows 10 taskbar

## Show Task View button

This displays an icon that opens Task View (`Win`+`Tab`) when clicked.

> ![image](https://user-images.githubusercontent.com/6503598/150659564-ebe71257-35b5-468d-8f10-00371c7f08e0.png)
>
> Appearance of the Task View button on the Windows 10 taskbar

## Show Desktop button

This can be used to hide the "Show Desktop" icon located at the far right of the taskbar.

> ![image](https://user-images.githubusercontent.com/6503598/150659604-ba2f5ace-03ab-469c-885d-78eed39bd298.png)
>
> Appearance of the Show Desktop button on the Windows 10 taskbar

## Automatically hide the taskbar

This can be used to have the taskbar automatically hide away when the mouse is not hovering over it or when it doesn't have the focus anymore.

## Start button style

Allows easy customization of the icon that is displayed when using the Windows 10 taskbar. Current options are:

### Windows 10 (default)
> ![image](https://user-images.githubusercontent.com/6503598/150659653-a4433d82-6695-479f-bbe6-0cb4e2ab49bb.png)

### Windows 11
> ![image](https://user-images.githubusercontent.com/6503598/150659661-6b697b9d-713e-457c-9fe8-3ee0c028f2cc.png)

## Combine taskbar icons on primary/secondary taskbar(s)

This allows you to choose the behavior of the Windows taskbar in regards to how the icons of the running programs act:

### Never combine (default)

Each window has its own button on the taskbar, and the title of the window is displayed near the icon, in its taskbar button.

> ![image](https://user-images.githubusercontent.com/6503598/150659738-432cf00f-8279-48da-a87b-976a1bde3fb5.png)

### Always combine, hide labels

Windows belonging to the same application instance receive a single taskbar button; the program name is not displayed, only its icon. This behavior is similar to what the Windows 11 taskbar offers.

> ![image](https://user-images.githubusercontent.com/6503598/150659758-dbbd572a-57a8-4549-948f-b4578f828307.png)

### Combine when taskbar is full

This is basically "never combine" until the taskbar becomes too cluttered with applications, at which point it switches to "always combine, hide labels".

## Taskbar icon size

### Large (default)

In this mode, the clock displays two lines of text (the time and the date).

> ![image](https://user-images.githubusercontent.com/6503598/150659783-eff641a5-b7db-4018-9b96-06ebf8c10100.png)

### Small

In this mode, the clock only displays a single line of text (the time).

> ![image](https://user-images.githubusercontent.com/6503598/150659790-58d74ed8-0999-4f73-9b81-ad76140a0f7a.png)

# System tray

## Skin taskbar and tray pop-up menus

This allows you to enable/disable the custom skinning of pop-up menus displayed by the taskbar: its context menu, and also the context menus for the network, volume, battery, Bluetooth and "Safe to Remove Hardware".

> ![image](https://user-images.githubusercontent.com/6503598/150659850-aa3b5f97-21fe-46b2-b333-43dd3467411f.png)
>
> Context menu with skin

> ![image](https://user-images.githubusercontent.com/6503598/150659856-1675b4ae-4636-4e9a-8882-142fde7d009e.png)
>
> Context menu without skin





