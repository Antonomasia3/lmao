Oftentimes, you may hear this talk about "symbols" around these places. Here, you can learn what those are, how are they helpful to ExplorerPatcher and what to do in case of errors.

## What are "symbols"?
Symbol files represent files which tell various things about an executable in a human-readable form. These are very useful especially when debugging programs. They do not contain the source code, but rather pointers about what certain places in the executable file are and do. For example, a program's usually made up of a bunch of functions put together in an executable. A function is a block of organized, reusable instructions that is used to perform a single, related action. When debugging, it's often useful to have a general idea of what the functions in a program do, in order to know what to expect. Symbol files aid in this, containing the names the programmer used for those blocks of instructions when programming.

## What does ExplorerPatcher do with symbol files?
As I said before, symbol files can offer valuable information about certain places in a program. It's easier to talk when referencing an example, so let's take the `Win`+`X` menu as an example.

Windows still contains code that builds and manages the menu in a DLL called `twinui.pcshell.dll`. As it stands, the DLL does not contain any information to help identify where that code exactly is. Thus, its symbol file can be used to gather this information from. It contains information about where functions with names like `CLauncherTipContextMenu::GetMenuItemsAsync` and `CLauncherTipContextMenu::_ExecuteCommand` are located in the actual binary. Without symbols, identifying these places is much much harder, relying on techniques such as matching an expected pattern of how the instructions should look against the actual binary. This is more prone to breaking, but can sometimes be used to circumvent the need for symbols. In ExplorerPatcher, this is used in the code that enables the Windows 10 network flyout, for example.

So, ExplorerPatcher uses functions already present in Windows' libraries to enable certain functionality. The way it identifies where those functions are is by using symbol files.

## Which ExplorerPatcher functionality requires the use of symbol files?
Currently, symbol data is required for the following functionality:

* `twinui.pcshell.dll`: `Win`+`X` menu
* `twinui.pcshell.dll`: skinning and unskinning some context menus
* `twinui.pcshell.dll`: press `Win`+`C` to open the clock flyout instead of Microsoft Teams
* `StartDocked.dll`: open Start directly to "All apps"
* `StartDocked.dll`: maximum numbers of apps to shown in the "Most used" section

## How does ExplorerPatcher obtain the necessary symbol files?
For binaries (EXEs, DLLs, CPLs etc) shipped with certain builds of the Windows operating systems, Microsoft makes symbols available for public download on their public service for debugging purposes. The information about where to download the symbol file associated with a certain binary is contained in the binary itself. Currently, Microsoft publishes symbols for these types of OS builds:

* stable builds of the operating system (builds serviced during Patch Tuesday of each month, "B" releases)
* builds shipped via the Dev channel of the Windows Insider Program

Patch Tuesday refers to the first Tuesday of the month, when updates are usually delivered to Windows stable builds. Although usually they are published at the time the build is pushed via Windows Update, sometimes delays happen. There is nothing I can do on my side about this. It's just how Microsoft processes these things. It's usually a matter of maximum a couple of hours before they are finally published.

Symbols are usually NOT made available for the following types of builds:
* builds shipped via the Beta and Release Preview channel  of the Windows Insider Program
* "C" and "D" stable OS builds - these are builds labeled as "Preview" and offered via Windows Update in the second part of a month, representative of what will generally arrive on the next Patch Tuesday; these are optional, the user has to explicitly click "Download and install" to have them applied on their computer, they are never automatically installed by Windows Update

When File Explorer starts up, ExplorerPatcher tries to load symbol data cached from a previous run of this check from the registry or from an internal table of symbol data for some known versions of the operating system. If ExplorerPatcher is unable determine this information, the program attempts to download the symbol files from Microsoft's servers, gather the necessary data from the files, and cache it in the registry for future use, so that this process is not repeated again at each File Explorer start-up for this OS build. If this fails, the program will run, but the functionality described above as dependent on symbol data from certain system files will not be available (i.e. will not work, the UI elements regarding it are still available in the "Properties" window).

## How can I determine if ExplorerPatcher needs symbol data for my OS build?

First of all, you can tell this from the version of the release: it usually indicates the highest build on which it was tested and confirmed to work. It also usually contains hardcoded (built-in) data for the files in that build, so no download is necessary. For example, the current ExplorerPatcher version is `22000.348.39.0`. That means it was tested and confirmed to work up to Windows 11 build 22000.348. It also contains built-in symbol data information up to that build, so no symbol data download is necessary when using that build, it will automatically use what it has built-in. Mainly, ExplorerPatcher is tested to work on the current stable build of Windows 11, as that is what I daily drive and also because testing against Insider builds is pretty difficult since things change a lot in there, so developing a patch this month might be rendered useless the next one when things are changed again or reverted altogether. So yeah, officially, ExplorerPatcher is supported only up to the builds that are listed in the release notes.

So, if you run `22000.348.39.0` on OS build `22000.348`, everything will just work. 

If you run `22000.348.39.0` on a newer build, ExplorerPatcher will try to download, parse and cache into the registry symbol data from Microsoft. Until that's done, the functionality described above as needing symbol data will be unavailable. If it succeeds, a one-time notification will show, informing you about the success of the operation and asking you to manually restart File Explorer to have the symbol data be used by ExplorerPatcher to enable the additional functionality. From this point on, the information for this build is cached in the registry and will be used the next times you run File Explorer on this build, bypassing the start-up symbol availability check and download. 

![image](https://user-images.githubusercontent.com/6503598/143228543-e3d7eeed-02e2-4ed3-8fba-4908c3ce5f41.png)

If it fails, ExplorerPatcher will usually work without the functionality described above as requiring symbol data and no notification will be shown in this case. Telling if you're in this mode is easy: press `Win`+`X` for example. If nothing shows, you're likely in this mode.

The second method you can tell what state ExplorerPatcher is in is by watching the information printed in the debug console ("Properties" - "Advanced" - "Enable console"):

* If ExplorerPatcher uses built-in symbol information, you will see some lines like the following printed at the very beginning of the console output:

```
[Symbols] Identified known "twinui.pcshell.dll" with hash 8b23b02962856e89b8d8a3956de1d76c.
[Symbols] Identified known "StartDocked.dll" with hash b57bb94a48d2422de9a78c5fcba28f98.
```

* If ExplorerPatcher does not have built-in symbol information for the build you are running and it failed to gather symbol data (due to various reasons, like symbols not being available from Microsoft, the computer not being connected to the Internet etc), you will see output similar to this:

```
[Symbols] Started "Download symbols" thread.
[Symbols] Attempting to download symbols for unknown OS version 10.0.22000.348.
[Symbols] Downloading to "C:\Users\root\AppData\Roaming\ExplorerPatcher\".
[Symbols] Downloading symbols for "C:\Windows\system32\twinui.pcshell.dll"...
[Symbols] Symbols for "C:\Windows\system32\twinui.pcshell.dll" are not available - unable to download.
[Symbols] Please refer to "https://github.com/valinet/ExplorerPatcher/wiki/Symbols" for more information.
```

* If ExplorerPatcher does not have built-in symbol information for the build you are running and it succeeds to gather symbol data, you will see output similar to this:

```
[Symbols] Started "Download symbols" thread.
[Symbols] Attempting to download symbols for unknown OS version 10.0.22000.348.
[Symbols] Downloading to "C:\Users\root\AppData\Roaming\ExplorerPatcher\".
[Symbols] Downloading symbols for "C:\Windows\system32\twinui.pcshell.dll"...
[Symbols] Reading symbols...
[Symbols] Downloading symbols for "C:\Windows\SystemApps\Microsoft.Windows.StartMenuExperienceHost_cw5n1h2txyewy\StartDocked.dll"...
[Symbols] Reading symbols...
[Symbols] Finished gathering symbol data.
[Symbols] Finished "Download symbols" thread.
```

## Can you set a proxy for symbol downloading?
Not directly in ExplorerPatcher, but you can set up a system proxy and that should be picked up.

## Can you disable symbols download altogether?
Although not recommended, you can use this option: "Properties" - "Advanced" - "Enable symbols download *".

## Can the need for symbol data be overcome?
Yes and no. We can discuss this more in a separate thread, but to keep it short here:

* For things in `twinui.pcshell.dll`, there would be 2 alternatives: reimplementing the functions used from there, like a `Win`+`X` menu builder, code that adds and removes owner drawing for contextual menus etc, or shipping a version of the DLL with known symbol data with the program. The former is doable, although it's not on the roadmap and would take a while, while the latter would be much more practical, but it's kind of impossible since I do not have a license to redistribute Microsoft's binaries.
* For things in `StartDocked.dll`, it's actually much more complicated, since I need the symbols to know where to hook and modify the behavior of certain of its function in order to achieve the functionality described above. Much much harder to do without symbols, almost impossible I'd say.

## Does the symbol file contain the actual source code?
No, as I said, it just contains some pointers, some very succinct information about various things in a program. Symbols are usually generated by the compiler when the binary is created, and are usually distributed in one form or another with it by the vendor, although that's not always the case. Debugging or exploring an executable without symbol information is harder because you have to deduct from the instructions alone what that block of code might do. Although, it's not impossible to figure out what happens then either.

## Are then symbols a perfect substitute for actual access to the source code?
No, but they definitely help ease the process of making sense of what happens in an executable. Symbols apply to final executable, those that contain machine code, or instructions that the CPU executes directly. The source code is a much more rich functional description of how the program is to operate, and is consumed by a compiler which turns it into an executable, a machine-specific representation of the description in the source code. This transformation is not a bijection, in other words, it's an irreversible process: theoretically different source code can produce the same executable and you cannot obtain back the source code from the executable. Why the latter? Well, the executable lacks some of the original information; an easy example of that are the function parameters: the information about how many parameters a function takes is not contained in the executable, as it is not needed for successful execution. This information may be deducted from the context (the instructions themselves), but what you deduct is not guaranteed to have been how the original description in the source code looked like. Not to mention, executable files lack valuable information which you can usually find in the source code in the form of comments.

## Where does the name "symbol" come from?
Things of interests in a program are generically called "symbols". What makes a thing something of interest, is, again, dependent on the context, but symbol files usually contain information about "symbols" such as functions, global variables etc.