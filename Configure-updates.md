ExplorerPatcher has a built-in updates module. You can use it to have the program notify you when a new application update is available.

## How does it work?

The update module checks whether the latest release on GitHub is different than what you have installed. If it is, it notifies you, offering the possibility to directly download and install it from the application itself.

## Can it notify me when File Explorer starts?

Yes. Right click the taskbar, choose "Properties", then "Updates". There, you can choose one of the following three options for "When File Explorer starts":

* "Notify about available updates (default)". Every time the main File Explorer process starts (that is, mainly, at logon), provided there is an active Internet connection, ExplorerPatcher will check whether a new release is available on GitHub. If there is a no new version available, nothing happens; if there is a new version available, a notification like the following will be shown:

![image](https://user-images.githubusercontent.com/6503598/145718822-a28ddb1d-9307-4b44-bb0a-4e34746f6c7c.png)

* "Prompt to install available updates". Every time the main File Explorer process starts (that is, mainly, at logon), provided there is an active Internet connection, ExplorerPatcher will check whether a new release is available on GitHub. If there is a no new version available, nothing happens; if there is a new version available, the update will be automatically downloaded and installed. If you have User Account Control enabled (**highly recommended, default setting**), it will prompt you to elevate the updater. If not, the update will be automatically installed. After the product servicing is done, File Explorer will reload with the new version automatically.

* "Do not check for updates". The application never checks for updates automatically. You can still manually check for updates and install them using the configuration UI.

## I don't see any notifications

Make sure notifications are turned on in Windows:

![image](https://user-images.githubusercontent.com/6503598/145721275-87a118c8-7fbb-4956-98ae-8083de44789d.png)

It works when themes are disabled as well.

If you see the "Some settings are managed by your organization" message and you cannot turn those on, then you may have luck enabling them using the Group Policy editor:
* Open Start, type "gpedit.msc".
* In the window that opens, navigate to "User Configuration" > "Administrative Templates" > "Start Menu and Taskbar" > "Notifications". Double click "Turn off toast notifications", check "Not configured", then click "OK".

## Can I manually check for updates?

Yes. Right click taskbar, choose "Properties", then "Updates" and click "Check for updates". While the check is in progress, a notification like this will show:

![image](https://user-images.githubusercontent.com/6503598/145720302-11c2ae20-6d4c-4830-ae03-5687fda6d243.png)

If no update is found, that is followed by this:

![image](https://user-images.githubusercontent.com/6503598/145720328-c730bcec-8106-4cc5-90f4-d839a360dc49.png)

If an update is found, you will instead see this:

![image](https://user-images.githubusercontent.com/6503598/145718822-a28ddb1d-9307-4b44-bb0a-4e34746f6c7c.png)

To update to the new version, click "Update program and restart File Explorer" in the same section in Properties.

## Can I receive pre-release versions as well?

Yes, but this is opt-in and disabled by default. To enable, right click the taskbar, choose "Properties", then "Updates", and then tick "Receive pre-release versions, if available". As noted in the UI, this is not recommended for general users, so please take note of the following:

* Pre-releases contain the latest code in the repository. Although the general aim is to have stable releases, some commits may break stuff from time to time. This is usually addressed in subsequent commits, but sometimes it may take a while until a fix is available.
* Pre-releases are great when you want to have access to the latest stuff in the upstream without having to set up your own build infrastructure. You can use these to help test the next stable version of the application.
* Once a pre-release stabilizes and its quirks are mostly ironed out, and is a bit tested by interested users, it is manually promoted to a release, in which case it is then offered to the general public via the regular updates as well.
* Pre-releases and releases are both built using the same infrastructure, in the cloud, on GitHub Actions. These builds are automated, on clean Windows machines, so you can be sure the source code is touched solely by that. I stopped uploading manual builds a while ago, in order to ensure the distributed binaries are as clean as possible.

Please note that when you enable that option, you can still receive releases as well. You will simply receive the newest thing available, be it a pre-release or a release, whereas without that, the updater only offers to install things marked as releases.

Also, note that you can only make at most 60 requests per hour to the pre-release server on GitHub, this is due to limitations imposed by them on unauthenticated use of their API. For the use case here, this is more than enough, but it's mentioned just so that you know.

## I have enabled pre-releases, upgraded to the latest pre-release because I want feature x, and now I disabled them, waiting for the stable release. Yet, when checking for updates, I am offered the latest stable version, which is older than the pre-release I want.

This behavior has been addressed and is no longer happening. Since ExplorerPatcher version 22000.434.41.12, the updater only suggests a new version if it has a bigger version number, no matter what channel you perform the check for updates against.

This is expected. The updater offers either releases only, either releases and pre-releases. When you tell it not to check for pre-releases, of course it offers you the latest release, which indeed may be older. In this scenario, I recommend turning off the updater until the release containing the changes you want is made available, and manually checking until then.

See [this](https://github.com/valinet/ExplorerPatcher/discussions/540) as well.

## How does the internal mechanism of the updater work?

As I said, the updater is very simple. Each `ep_setup.exe` file contains in its first few bytes the hash of the ExplorerPatcher file contained inside it. The updater determines the location of the most recent `ep_setup.exe` according to your settings (i.e. from releases only, or including pre-releases as well), it downloads the first few bytes of that, extracts the hash from there and compares it against the hash of the current ExplorerPatcher. If the two differ, then the remote file is offered as an update ready for installation. File versions are not involved, because there may be multiple *commits* with the same file version. More details are given [here](https://github.com/valinet/ExplorerPatcher/discussions/540#discussioncomment-1782287).

## Can I configure my own update servers?

Sure. Configure the following two REG_SZ entries in `HKEY_CURRENT_USER\Software\ExplorerPatcher`:

* `UpdateURL`: configures the main update URL, for releases only. It has to serve the executable file directly, similar to the default of: https://github.com/valinet/ExplorerPatcher/releases/latest returns
* `UpdateURLStaging`: configures the update URL for pre-releases and releases. It has to return JSON, similar to what the default of: https://api.github.com/repos/valinet/ExplorerPatcher/releases?per_page=1 returns