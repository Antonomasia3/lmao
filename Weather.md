Is it raining cats and dogs today, or is it going to be sunny? Don't take the umbrella with you unless it's absolutely necessary - ExplorerPatcher helps you with that.

One of the (few) useful features Microsoft made very late during the Windows 10 development lifecycle was to introduce a weather widget in the taskbar. Unfortunately, for some bizarre reason, it hasn't made the cut to Windows 11. [There are mentions about it here and there](https://github.com/valinet/ExplorerPatcher/issues/153) in the code base that shipped with OS build 22000, but the thing seems not to be compiled in altogether. Further evidence is the fact that `explorer` explicitly denies adding the menu entry for "News and interests" to the taskbar context menu no matter the circumstances.

It was a long kind-of-forgotten, kind-of-secret wish of mine to do something about this. So, I spent the last few days continuously working on re-implementing this functionality from scratch, to work with the Windows 10 taskbar that's still around, akin to what Microsoft actually ships in Windows 10. The result is available as a preview starting with pre-release 22000.469.42.0.

## What is it?

The weather widget, when enabled, sits at the far right end of the task list, near the system tray, exactly where the "People" button would sit. Currently it offers 5 modes for presenting itself:

**Icon and description**

Displays an icon indicating the current conditions, the temperature, plus a short description of the actual conditions.

![image](https://user-images.githubusercontent.com/6503598/151263341-fa8f895a-5975-4fa1-a14a-b3a53a6d98d8.png)

**Icon and temperature**

Displays an icon indicating the current conditions, plus the temperature.

![image](https://user-images.githubusercontent.com/6503598/151263475-e5734069-4119-4e4e-9c22-3d27a11b44fd.png)

**Icon only**

Displays only an icon indicating the current conditions.

![image](https://user-images.githubusercontent.com/6503598/151263519-b8e19125-29ee-4783-b06c-d9a95ede1079.png)

**Temperature only** and **Temperature and description**

These two are exactly like their counterparts above, only that the icon is not displayed.

When clicked, it expands into a panel near the corner of the screen, showing you a brief forecast for the coming days, plus more details about the current conditions, and a glance at what's coming up in the next hours. In fact, it's exactly the same weather widget that Google presents [in their search pages](https://www.google.com/search?q=weather), only this time it's integrated right into the taskbar, complete with Mica material support.

![image](https://user-images.githubusercontent.com/6503598/151263919-2fb3e6da-b48c-4955-b5e3-a77c2030e871.png)

## How to enable it?

Right click the taskbar, and choose "Properties". In theere, go to "Weather" on the left side, and check "Show Weather on the taskbar".

## What configuration options does it offer?

Well, besides the layouts explained above, it currently offers the following features:

* **Configurable update frequency** - alter how often the data refreshes in the background. The default is every 20 minutes.
* **Choice of Celsius or Fahrenheit**
* **User-defined location and language**
You can type in the name of any place on Earth. If Google is able to find and display a weather widget for it on the regular web, it will work here too.

For testing, start by typing "weather in bucharest" etc in your browser; if you're looking for a ZIP code, try "weather in zip 90210". Then, to have it work with this widget, when configuring it, just omit the "weather in" part and type the city name directly.

Or, if you leave it blank (as is the default), it will pick up your location based on your IP address. As well, you can also configure the language the messages are displayed in. Just type a two-letter code, like "en", "ro", "de", "fr" etc and you're good to go.

## Does it support the taskbar being placed on any of the 4 edges?

Yes, it's one of the design goals, unlike the stock widget from Windows 10. Although, of course, it works best when the taskbar is placed either at the top, either at the bottom.

## What are the system requirements?

To display the web content, the widget makes use of the Microsoft WebView2 component. This is a built-in system component in Windows 11 - if you have a fairly untouched system installation, you should be good to go. Otherwise, please install the [Evergreen WebView2 standalone component](https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download-section). Please note that Microsoft WebView2 is a separate product from Microsoft Edge.

## Where is the browser data stored?

It's located at `%APPDATA%\ExplorerPatcher\ep_weather_host`.

## What happens if I do not have those components? Will ExplorerPatcher still work?

Yes. Instead of the weather widget, you will see the regular "People" button.

## Does this run in-process in `explorer`?

No, the weather widget infrastructure is hosted by the COM Surrogate in a separate process, in order to isolate and containerize the different parts of the application, in a similar strategy to how the recently introduced Desktop Window Manager add-ons run out-of-process as well.

## Is there any special installation required?

No, just upgrade to the latest pre-release, for now. The installer takes care of registering the necessary components on the system.

## Does this support the Windows 11 taskbar?

No, just the good old Windows 10 one. There's no point in developing anything for the new one on this matter, as Microsoft will ship similar functionality in the upcoming feature update.

Please, let's keep the discussion organized. This is the first iteration of this. Feedback will surely be taken into consideration, and we can ship a good implementation to everyone. A crop of new features will be added and existing aspects will be polished. For example, dark mode support for the widget is on the roadmap, as well as many other great new features. Now, I just a need to rest a bit, it was a pretty wild sprint during the past couple of days.

## My desktop broke after enabling "Show Weather on the taskbar", how do I workaround this?

1. Press Ctrl + Alt + Delete at the same time, open Task Manager, click File -> Run new task, and "Open" `regedit.exe` with administrative permissions.
2. Go to `Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\People`
3. Double-click "PeopleBand", then change its value data to `0`.
4. Use Restart File Explorer (*); an alternative is to open Task Manager, click File -> Run new task, and "Open" `explorer.exe`.

## I am facing a layout or some other issue with the content displayed by the weather widget. Is there a way to debug it?

You can try enabling developer mode. Since the widget is just a WebView2 instance that displays a cropped Google search web page, you can use this setting to enable developer mode: go to `HKEY_CURRENT_USER\SOFTWARE\ExplorerPatcher` in the registry and create a DWORD value called `WeatherDevMode` and set its value to 1.

This will enable developer mode in the weather widgets, which enables the following features that aid in debugging eventual issues:

* Context menus work.
* Browser developer tools (right click - "Inspect" or F12).
* Other shortcut keys (like F5).
* Script pop-ups (for `alert`, `confirm`, and `prompt` JavaScript functions).
* The weather widget can be resized freely.
* The weather widget can be moved around on the screen freely.
* The WebView2 component fits and fills the entire widget area, instead of displaying a crop to the weather portion of the page.

This can be used to debug various issues. For example, it was used to fix [#934](https://github.com/valinet/ExplorerPatcher/issues/934).