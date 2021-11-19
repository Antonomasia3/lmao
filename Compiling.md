ExplorerPatcher builds are automated using GitHub Actions. When a new commit is pushed, a new pre-release containing the binaries is created as well, so people always have access to the latest version, compiled independently. Also, artifacts are uploaded, containing the unpacked resources, symbol files, and anything else generated during the compilation process.

You can also use the existing infrastructure to build a custom commit. For that, go to [the build GitHub Actions page](https://github.com/valinet/ExplorerPatcher/actions/workflows/build.yml), click run workflow. On newer builds, specify only a commit number. On older builds, you can specify "x64"  for Configuration, and "x64" for build directory.

Also, if you want to build this yourself on your local machine, then follow the instructions below. Also, you can consult the [build.yml](https://github.com/valinet/ExplorerPatcher/blob/master/.github/workflows/build.yml) file to see how the automated process does it. If you encounter some issues when following the steps below, or should you want to find out more information and the latest tips from other users/me regarding how to pull this off, also consult the relevant thread in Discussions located [here](https://github.com/valinet/ExplorerPatcher/discussions/190).

The following prerequisites are necessary in order to compile this project:

* Microsoft C/C++ Optimizing Compiler - this can be obtained by installing either of these packages:

  * Visual Studio - this is a fully featured IDE; you'll need to check "C/C++ application development role" when installing. If you do not require the full suite, use the package bellow.
  * Build Tools for Visual Studio - this just installs the compiler, which you'll be able to use from the command line, or from other applications like CMake

  Download either of those [here](http://go.microsoft.com/fwlink/p/?LinkId=840931). The guide assumes you have installed either Visual Studio 2019 or 2022, either Build Tools for Visual Studio 2019 or 2022.

* A recent version of the [Windows SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/) - for development, version 10.0.19041.0 was used, available [here](https://go.microsoft.com/fwlink/p/?linkid=2120843) (this may also be offered as an option when installing Visual Studio)

* [CMake](https://cmake.org/) - for easier usage, make sure to have it added to PATH during installation

* Git - you can use [Git for Windows](https://git-scm.com/download/win), or git command via the Windows Subsystem for Linux.

Steps:

1. Clone git repo along with all submodules

   ```
   git clone --recursive https://github.com/valinet/ExplorerPatcher
   ```

   If "git" is not found as a command, type its full path, or have its folder added to PATH, or open Git command window in the respective folder if using Git for Windows.

2. Compile funchook (type this in a PowerShell window):

   ```
   cd libs
   cd funchook
   md build
   cd build
   cmake -G "Visual Studio 16 2019" -A x64 ..
   (gc .\funchook-static.vcxproj) -replace '<RuntimeLibrary>MultiThreadedDLL</RuntimeLibrary>', '<RuntimeLibrary>MultiThreaded</RuntimeLibrary>' | Out-File .\funchook-static.vcxproj
   cmake --build . --config Release
   ```

3. Compile ExplorerPatcher

   * Double click the `ExplorerPatcher.sln` file to open the solution in Visual Studio. Choose Release and your processor architecture in the toolbar. Press `[Ctrl]`+`[Shift]`+`[B]` or choose "Build" - "Build solution" to compile.

   * Open an "x86 Native Tools Command Prompt for VS 2019" (for x86), or "x64 Native Tools Command Prompt for VS 2019" (for x64) (search that in Start), go to folder containing solution file and type:

     * For x86:

       ```
       msbuild ExplorerPatcher.sln /property:Configuration=Release /property:Platform=IA-32
       ```

     * For x64:

       ```
       msbuild ExplorerPatcher.sln /property:Configuration=Release /property:Platform=amd64
       ```

   Debug builds mostly work as well, although they may have some quirks or issues. I mostly test the software as release builds.

   The resulting libraries will be in the "build\Release" or "build\Debug" folder in the directory containing the solution file.

4. To generate an `ep_setup.exe` file suitable for an uploading on an ExplorerPatcher update server (which means inserting the MD5 hash of `ExplorerPatcher.amd64.dll` in the setup program), after the build is completed, run this in the `build` folder:

   ```
   ep_setup_patch.exe
   ```

That's it. Later, if you want to recompile, make sure to update the repository and the submodules first:

```
git pull
git submodule update --init --recursive
```

