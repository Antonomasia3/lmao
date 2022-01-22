ExplorerPatcher comes with a very basic installer that is designed to get you going as fast as possible.

## How to install?

Simply run the `ep_setup.exe` file. After granting it permission to elevate, File Explorer will restart and ExplorerPatcher will be fully installed. You can tell this because the taskbar will now be switched to the familiar Windows 10 one. If you still want to use the newer Windows 11 one, just head up to "Properties" and change the setting there, along with any other option you might fancy, by right clicking the taskbar and choosing "Properties".

## How to uninstall?

There are currently 4 ways of doing this:

* Identify "ExplorerPatcher" in Settings > Apps > Apps & features. Click the "three dots" button, and then click "Uninstall" and confirm the prompts.
* Identify "ExplorerPatcher" in Control Panel > Programs and Features. With it highlighted, click "Uninstall" and confirm the prompts.
* Run `ep_setup.exe /uninstall`.
* Rename `ep_setup.exe` to `ep_uninstall.exe` and execute that.

## Can I manually update to a newer version?

Yes. Just download the newer `ep_setup.exe` from GitHub Releases and run that. File Explorer will restart and the new version will load.

## Can I reinstall ExplorerPatcher?

Although not required and may hardly make any difference, you can execute `ep_setup.exe` again.

## How to obtain ExplorerPatcher's files without installing it on the machine?

You can run the installation program like this:

* `ep_setup.exe /extract` will extract the files in the current directory.
* `ep_setup.exe /extract C:\test` will extract the files in `C:\test`; you can use any fully qualified path there, this was just an example