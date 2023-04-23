This document describes all the options currently provided by ExplorerPatcher. This is valid for and was compiled at the time of version 22000.343.41.12. Although I strive to keep this up to date, some things might change slightly in the future. If you notice any inconsistencies, feel free to mention them for fixing in the [Discussions](https://github.com/valinet/ExplorerPatcher/discussions) section.

# Taskbar

## Taskbar style

### Windows 10 (default)
Enables the familiar Windows 10 taskbar. It supports all the familiar features, like enabling button labels (never combine), separate network/volume/battery indicators, docking to the top/bottom/right/left side of the screen, plus customizable options via ExplorerPatcher.

> ![image](https://user-images.githubusercontent.com/6503598/150659166-9b980623-66dc-4716-8c7a-72521cc23c98.png)
>
> Windows 10 taskbar

### Windows 11
Enables the new Windows 11 taskbar. It currently lacks support for showing labels, but supports centered icons; the network/volume/battery indicators are grouped in a single button that opens the "control center".

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

Note: This setting is not available when using the Windows 11 taskbar on Windows 11 build 22621 or higher (22H2).

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

This allows you to enable/disable the custom skinning of pop-up menus displayed by the taskbar: its context menu, and also the context menus for the network, volume, battery, Bluetooth and "Safe to Remove Hardware" icons.

> ![image](https://user-images.githubusercontent.com/6503598/150659850-aa3b5f97-21fe-46b2-b333-43dd3467411f.png)
>
> Context menu with skin

> ![image](https://user-images.githubusercontent.com/6503598/150659856-1675b4ae-4636-4e9a-8882-142fde7d009e.png)
>
> Context menu without skin

## Center tray icon pop-up menus

This will have the context menus for the network, volume, battery, Bluetooth and "Safe to Remove Hardware" icons display centrally with respect to the icon position, if possible.

## Flyout behavior for tray icon pop-up menus

This makes the context menus for the network, volume, battery, Bluetooth and "Safe to Remove Hardware" icons toggle when the icon is right clicked (or clicked, depending on the icon): the first click shows the menu, the second click dismisses it, the third click shows the menu, the fourth click dismisses it and so on.

## Show touch keyboard button

> ![image](https://user-images.githubusercontent.com/6503598/150659929-e00d5ec4-ef40-4be4-9ea9-e99c0573c959.png)
>
> Touch keyboard button on the Windows 10 taskbar

## Show seconds in the clock

This works only with the Windows 10 taskbar. It allows displays seconds in the clock, besides the hours and minutes.

> ![image](https://user-images.githubusercontent.com/6503598/150659943-465ec876-d591-4ace-8847-4ae69e4034d1.png)

## Hide Control Center button

This allows hiding the control center icon when using the Windows 10 taskbar.

> ![image](https://user-images.githubusercontent.com/6503598/150659959-ee21ac88-8e65-40f7-87b7-6660ee8344e7.png)

The control center icon opens the following flyout (`Win`+`A`):

![image](https://user-images.githubusercontent.com/6503598/150659991-bfd5226e-87cc-4bbb-9c4d-9008e5ee02b8.png)

## Choosing "Open Network & Internet settings" when right clicking the network icon should open:

* Network section in the Settings app (default)
* Network and Sharing Center in Control Panel
* Network Connections in Control Panel

This allows you what clicking on this item in the context menu of the network icon should do.

> ![image](https://user-images.githubusercontent.com/6503598/150660045-3785c3ea-6283-469d-92d4-a6e46b0a0feb.png)

## When clicking a system icon in the Windows 10 taskbar system tray, open:

### Network

* Control Center
* Windows 11 WiFi flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660069-75805500-95e7-45c5-b48f-5178898a02b9.png)
* Windows 10 flyout (default)
> ![image](https://user-images.githubusercontent.com/6503598/150660078-0e1495c6-d558-4bdd-a31c-4b69ad1d5015.png)
* Windows 8 flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660088-5a604761-8e26-47c7-8183-3e7d8492beab.png)
* Network section in the Settings app (default)
* Network and Sharing Center in Control Panel
* Network Connections in Control Panel

### Sound

* Windows 10 flyout (default)
> ![image](https://user-images.githubusercontent.com/6503598/150660107-cadf7f2a-512a-4395-967e-c92bcf27bab8.png)
* Windows 7 flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660118-b3fd2fcc-9e5a-4229-98aa-0442323a9058.png)

### Clock
* Windows 11 flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660132-a361d24d-7e5e-489c-b92a-12449db79670.png)
* Windows 10 flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660142-5d99ffeb-88ff-4542-9f91-c0ecc917cc78.png)
* Windows 7
> ![image](https://user-images.githubusercontent.com/6503598/150660148-79e3f7ad-44a2-42d5-8b17-9412eaa5ef47.png)

### Battery
* Windows 10 flyout
> ![image](https://user-images.githubusercontent.com/6503598/150660175-4d7a074e-ac1a-4475-9bf5-bfdff7427287.png)
* Windows 7 flyout (not recommended); instead, use [Battery Mode](https://github.com/tarcode-apps/BatteryMode)
> ![image](https://user-images.githubusercontent.com/6503598/150660184-c6c80b65-433e-4866-846d-9dd71d4306fb.png)

### Language switcher
* Windows 11 (default)
> ![image](https://user-images.githubusercontent.com/6503598/150660214-1f886a3b-14a0-4aae-b75a-5328e406b26b.png)
* Windows 10 (with link to "Language Preferences")
> ![image](https://user-images.githubusercontent.com/6503598/150660222-dad34faf-4472-4e9d-8b36-27b57d41dcc4.png)
* Windows 10
> ![image](https://user-images.githubusercontent.com/6503598/150660230-e7fa351e-13c5-4644-b060-d44e0f8001f6.png)

# File Explorer

## Disable the Windows 11 command bar

This allows hiding this part of the interface in a File Explorer window:

> ![image](https://user-images.githubusercontent.com/6503598/150660261-5e265b4a-6f2e-4771-a322-3fa7b4ceb0a0.png)

Instead, the Windows 10 ribbon will be shown:

> ![image](https://user-images.githubusercontent.com/6503598/150660322-8fdd1488-b3b0-4c46-9dbf-7f1477fe21bb.png)

## Disable the Windows 11 context menu

This allows disabling the new context menu when right clicking on stuff in File Explorer:

> ![image](https://user-images.githubusercontent.com/6503598/150660281-0a45843e-8a0c-4762-8dc2-82b895be4cba.png)

Instead, the proper, legacy menu that is displayed by clicking "Show more options" in that menu is displayed directly:

> ![image](https://user-images.githubusercontent.com/6503598/150660291-8ca29833-7c2b-4bb7-a4ae-a6571cf1066e.png)

## Disable the navigation bar

Completely removes the navigation bar from File Explorer windows.

> ![image](https://user-images.githubusercontent.com/6503598/150660341-ec05dcfb-86d5-405f-8b92-e7ab52c194cf.png)

## Disable modern search bar

This can disable the new search bar that shows results in a pop-up window as you type and instead use the legacy one (from Windows 10 builds prior to 1903) that displayed the results in the File Explorer window directly.

## Hide search bar completely

Allows you to hide the search bar in File Explorer windows completely.

> ![image](https://user-images.githubusercontent.com/6503598/150660389-aa8ce908-49d7-452b-969c-7c8598b03a45.png)

## Register as shell extension

This option is extensively documented [here](https://github.com/valinet/ExplorerPatcher/wiki/Using-ExplorerPatcher-as-shell-extension).

# Start menu

## Open Start on monitor containing the cursor

When enabled, when opening the Start menu using the `Win` key, it opens on the monitor that contains the mouse cursor at that time. The default behavior is for Start to open on the primary monitor.

## Open Start at logon

Opens the Start menu when you sign into the computer, as in Windows 8.

## Open Start in All apps by default

Directly opens the "All apps" list when you open the Start menu.

## Maximum number of frequent apps to show

This allows you to adjust how many applications to show in the "Most used" list that's displayed at the beginning of the "All apps" list in the Start menu. To have it display an entire screen, use value "11".

If you do not see this list, go to Settings > Personalization > Start and enable "Show most used apps".

## Position on screen

Determines where the Start menu will display on the screen, when invoked:

* Left
* Center (default)

# Window switcher

## Window switcher (Alt-Tab) style

### Windows 11 switcher
Full screeen, slow, tiny selection outline, slow opening times
> ![image](https://user-images.githubusercontent.com/6503598/150660605-6637a142-5af4-475b-a966-20f509b5e8fb.png)
### Windows 10 switcher
Pretty good but lacks customization options
> ![image](https://user-images.githubusercontent.com/6503598/150660619-450d0120-e9b8-400f-a3b0-6af122b68b56.png)
### Windows NT switcher
The classic simple icon-based interface hosted by `csrss`
> ![image](https://user-images.githubusercontent.com/6503598/150660671-b095c7ee-b2cc-4ca9-888f-6ec03577b9f0.png)
### Simple Window Switcher
My own take on implementing this kind of functionality
> ![image](https://user-images.githubusercontent.com/6503598/150661107-52a2aa31-4c8d-45fd-abca-ca5b9ef0614b.png)

Options for the Simple Window Switcher are described [here](https://github.com/valinet/ExplorerPatcher/wiki/Simple-Window-Switcher).

# Other

## Remember last used section in this window

When opening "Properties", it will open in the last section that you were on when you last used it. Without this turned on, it always opens at the first section, currently "Taskbar".

## Open clock flyout when pressing Win+C instead of Microsoft Teams

## Show separators between taskbar toolbars

> ![image](https://user-images.githubusercontent.com/6503598/150660759-c187bc67-ed82-449b-a8c4-493fa5621bc5.png)

## Show Command Prompt instead of PowerShell in Win+X menu

## Add shortcut to program settings in Win+X menu

This basically adds a link to the "Properties" window in the `Win`+`X` menu as well. The `Win`+`X` menu displays when you press that key combination or when you right click the Start button and displays a list of links to common places in the operating system.

> ![image](https://user-images.githubusercontent.com/6503598/150660814-db934724-c9ca-4f59-a759-d19a4e38e439.png)

## Remove shortcut key from program settings in Win+X menu

This removes the possibility to open the "Properties" menu that you can choose to insert in the `Win`+`X` menu by pressing the `P` key when the menu opened.

## Disable Office hotkeys (Ctrl+Alt+Shift+Windows key combinations)

This is described in-depth [here](https://github.com/valinet/ExplorerPatcher/discussions/661).

## Disable rounded corners for application windows

Allows you to restore sharp window corners as in Windows 10.

> ![image](https://user-images.githubusercontent.com/6503598/150660875-fe0429c2-0910-4bf8-900e-aa21d44ec33c.png)
>
> Default, rounded corners in Windows 11

> ![image](https://user-images.githubusercontent.com/6503598/150660883-632d7721-6ac1-40a2-b473-e1d98701a1db.png)
>
> Sharp, 90-degree angle corners, as in Windows 10

## Default action in the Alt+F4 dialog on the desktop

When pressing `Alt`+`F4` on the desktop, the "Shut Down Windows" dialog is displayed. Use this option to configure what the default in that list is:

* Switch user
* Sign out
* Sleep
* Hibernate
* Shut down (default)
* Restart

## Snap Assist style

Configure the appearance of the Snap Assist functionality:

> ![image](https://user-images.githubusercontent.com/6503598/150660930-a74d31ec-c5a8-42f5-97c2-2d96d1efa5a0.png)
>
> Windows 11 appearance (default)

> ![image](https://user-images.githubusercontent.com/6503598/150660936-aef575cb-3e03-45e3-a6a1-80473d2289c4.png)
>
> Windows 10 appearance

## Prevent the following Control Panel links from being redirected to the Settings app

* System / About page - this makes it so that when you right click a This PC window and choose "Properties" or you choose "Properties" from the toolbar or ribbon, it will open the legacy "System" page in the Control Panel, instead of the Settings > System > About.
* Programs and Features - this makes it so that when you click "Uninstall a program" in the ribbon or toolbar of a This PC window, it will open "Programs and Features in the Control Panel, instead of Settings > Apps > Apps and features.
* Adjust date/time - this makes it so that when you right click the clock and choose "Adjust date/time", it will open the legacy Control Panel interface for configuring the clock, instead of Settings > Time & language > Date & time.
* Customize notification icons - this makes it so that when you right click the clock and choose "Customize notification icons", it will open the legacy Control Panel interface for configuring the notification icons, instead of Settings > System > Notifications.

# Updates

This section is described [here](https://github.com/valinet/ExplorerPatcher/wiki/Configure-updates).

# Advanced

This section is described [here](https://github.com/valinet/ExplorerPatcher/wiki/About-advanced-settings).

# About

This displays general information about the program. It also allows you to manage the settings of the application, like exporting your current configuration to a file, importing a config from an existing file, or restoring the defaults of ExplorerPatcher. You can read more about this [here](https://github.com/valinet/ExplorerPatcher/wiki/Settings-management).

# Restart File Explorer

This restarts the File Explorer process, that is responsible with hosting the shell, including the desktop, taskbar, and folder windows. It is mainly useful for applying certain tweaks right away, without needing to sign out and back in or to reboot the computer.