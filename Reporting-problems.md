I try my best to assist in solving most problems encountered regarding this application. To be able to better manage the time and resources available, I kindly ask to follow this set of guidelines when it comes to interacting with this repository.

## MUST READ rules regarding problem reporting

### Make sure the "problem" is an actual problem

Make sure the "problem" you are facing is actually a problem with ExplorerPatcher. The easiest way to do this is to check whether you can reproduce the issue on a clean Windows 11 install, for example, in a virtual machine. If that's not possible to evaluate, at least disable all other programs, shell extensions, themes etc that might interfere, or at the very least make sure to specify their presence when filling the report. The information is VERY useful in order to quickly and reliably asses the problem.

### Familiarize with ExplorerPatcher's features 

Make sure the "problem" you are facing is indeed a "problem", not some feature/quirk you may simply have missed (sometimes because of skipping the advice of consulting the documentation, or at the very least the README). The documentation is provided to help you and also to avoid opening tickets for the most basic things in the world. PLEASE take a bit of time to get familiar with the program and read the provided docs.

### Search past threads

PLEASE refrain from opening duplicate issues. Consult the [Frequently Asked Questions](https://github.com/valinet/ExplorerPatcher/wiki/Frequently-asked-questions) and **use the search function in both Issues and Discussions**, and even Google before opening a thread, in order to make sure that the answer you are looking for hasn't been offered already. This, of course, saves you tons of time in the end, as a lot of the times the answer is already on these forums, so you can save the time you'd otherwise wait for a repost of the information, and also it saves other users’ time and my time, as we do not have to answer again to a previously asked question. 

### Be verbose

PLEASE describe things in detail. Refrain from generic titles (i.e. "does not work", "broken" [#486](https://github.com/valinet/ExplorerPatcher/issues/486), "thing <insert name> is buggy" [#605](https://github.com/valinet/ExplorerPatcher/issues/605)) or useless 1-line descriptions (that sometimes just repeat the title, e.g. [#621](https://github.com/valinet/ExplorerPatcher/issues/621)). The better documented the initial report, the easier it is to develop a fix for it. Badly formatted tickets just take time and attention from the real problems and add no value.

Useful things to include:

* Windows build number
* ExplorerPatcher version
* Relevant third party programs/tweaks used (for example, OpenShell, Start11, StartAllBack, 7+ Taskbar Tweaker etc)

VERY useful things to include:

* The exact commit of the ExplorerPatcher release you are using
* If you report a crash, a crash dump is VERY useful. Use [these instructions](https://docs.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps) to enable **full** crash dumps on your Windows install, and then submit `explorer`'s crash dump correlated with the problem you are reporting.

Useless things to include:

* Personal feelings, especially if not even remotely based on some fact
* Windows Event Log output, besides the information about the crashing module. The information there is 99% of the times useless, being too generic. Instead, use [these](https://docs.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps) to enable and collect full crash dumps and submit that.

### Self fix
ExplorerPatcher is a collaborative, open development project that relies on user contributions as well. For simple issues, like typos in the docs, small and relevant changes in the code etc, you can fork the repository, make the change there and submit a pull request for review directly. This is often preferable, if documented well, than asking for the change from me in a new thread.

## How to report a problem?

Open a new thread in [Discussions](https://github.com/valinet/ExplorerPatcher/discussions). There, the community or myself (knowledgeable people) can help assist you and hopefully a solution is determined.

DO NOT OPEN A THREAD IN **ISSUES**. PLEASE DON'T DO THAT. THE *ISSUES* SECTION IS INTENDED FOR DEVELOPERS TO TRACK ACTUAL ISSUES, PROBLEMS, BUGS, WORK IN PROGRESS FEATURES OF THE APPLICATION. THE ONLY REASON THIS SECTION IS OPEN TO THE GENERAL PUBLIC IS BECAUSE SOME DESIGN GENIUS AT GITHUB/MICROSOFT DECIDED NOT TO OFFER AN OPTION TO RESTRICT THIS AND [CONSTANTLY IGNORED THE COMMUNITY ASKING THIS FOR YEARS](https://github.com/dear-github/dear-github/issues/293).

Even if you think something belongs to the Issues section, or you are 100% sure you found a bug, don't open a ticket there. Instead, raise a new thread in Discussions. I will come, evaluate it, and when I confirm it, I will manually promote it as an issue. This way, I can keep that section focused, containing items of interest for the development of this application. Otherwise, things become a mess, as is the case with tons of projects on GitHub which simply have gotten their issues tracker out of control, filled with duplicate support requests, reports etc. Some developers end up in a point of having nothing else to do to get some use out of it then to close all issues, no matter their state, and start fresh, as was the case recently with [the issues section of the TaskbarX project](https://github.com/ChrisAnd1998/TaskbarX/issues/809#issuecomment-1001003632). Of course, that's a huge stress for the developer and introduces the risk of getting real issues lost in a sea of invalid reports.

Unfortunately, this happens to a degree in ExplorerPatcher still: at the beginning of 2022, there are approximately 250 issues all time. Out of those, 50 or so are marked "fixed" with no open issues. That suggests that 20-30% of the raised tickets are actually valid. The rest are simply duplicates or invalid tickets (support tickets, feature requests etc). That's not good.

TL;DR DO NOT OPEN TICKETS IN ISSUES. Open them in Discussions.

## What about general questions, questions about the functionality of ExplorerPatcher or feature requests?

Those are welcome as well, use [Discussions](https://github.com/valinet/ExplorerPatcher/discussions) to address them.

## Other aspects

Please note that issues/discussions not adhering to these guidelines will most probably be ignored and may simply be closed/deleted without any explanation as a reply.

Despite having the possibility to do so, I vouch not to edit or alter any third party reply or post on these forums.

ExplorerPatcher is provided AS-IS. I do my best to make it work under most circumstances, although I can mention in advance some configurations for which I won't provide active support and the reasons why:

* **ExplorerPatcher running on Windows Insider Preview builds** is not supported. The reason is because code there changes so often that developing and maintaining patches against that is not feasible long term. Some features and the program may generally work, but active or long term support is not provided for these builds.
* **ExplorerPatcher running on preview stable builds (C and D releases)** is not supported. This mostly has to do with symbol unavailability, otherwise the program generally works as well as it does on public releases, so there shouldn't be much difference. Read more about how symbols affect ExplorerPatcher [here](https://github.com/valinet/ExplorerPatcher/wiki/Symbols).
* **ExplorerPatcher on ARM64** is not supported. This is because I do not own (or need) an ARM64 machine, so I cannot test it there. Some patches may be architecture specific; EP is not the average Electron-based web wrapper. It cannot run as-is, care has to be taken to natively compile and test it against that architecture. Emulation doesn’t cut it, in this case. If someone’s willing to pick up the port for the architecture, they have my support and maybe something comes out of it. But personally, at the moment, I have no plans of working on that.
* **ExplorerPatcher on Windows 10** is not supported. This should be pretty obvious from the headline of the project: "restore a productive working environment on Windows 11". I moved on from Windows 10 to Windows 11. I do not have time to fully test against both versions. I daily drive stable Windows 11 (builds based on 22000), so I test on that. If someone wants to help maintain a Windows 10 port, sure, they have all my support. As it stands now, PLEASE do not try running this on Windows 10. There are no checks for preventing you from doing so an you will probably brick your system; not really, but you should be prepared with knowledge to restore `explorer` to a non-crashing state (i.e. delete `dxgi.dll` from `C:\Windows` BY RENAMING IT TO `dxgio.dll` FIRST, starting `explorer`, confirming it no longer crashing, and then deleting `dxgio.dll`)