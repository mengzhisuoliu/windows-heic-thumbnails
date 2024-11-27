# Windows HEIC Thumbnail Provider

Windows 10 does not support HEIC files by default, which are the native photo image format of recent iPhones.

HEIC files are similar to JPEG files, but with better quality in half the file size.

This small shell extension adds the ability for Windows Explorer to display thumbnails of **.heic** or **.heif** files.

![20220606-201945-explorer](https://user-images.githubusercontent.com/323682/172850354-902dbd7d-686f-4749-acc5-23990e65128e.png)

To open or edit HEIC files you'll still need another application such as [Paint.NET](https://www.getpaint.net/) or [Krita](https://krita.org/).

# Installing

- Requires Windows 10 (64-bit)
- Install the latest [Microsoft Visual C++ Redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe), if required. You may already have this installed, but if you get an error when you run the `regsvr32` command, install this and then try again.

1. Create a folder, such as `C:\HEICThumbnailHandler\` to place the DLL files.
2. Download the [latest release of HEICThumbnailHandler](https://github.com/brookmiles/windows-heic-thumbnails/releases/latest).
3. Extract the files `HEICThumbnailHandler.dll`, `heif.dll`, and `libde265.dll` into the folder you created (`C:\HEICThumbnailHandler\`).
4. Register the DLL:
	- Press `Win+R`
	- Type `cmd`
	- Click `OK`
	- Type `cd C:\HEICThumbnailHandler\`
	- Type `regsvr32 HEICThumbnailHandler.dll`

Windows Explorer should begin displaying thumbnails for `.heic` and `.heif` files.

# Uninstalling

1. Un-Register the DLL:
	- Press `Win+R`
	- Type `cmd`
	- Click `OK`
	- Type `cd C:\HEICThumbnailHandler\`
	- Type `regsvr32 /u HEICThumbnailHandler.dll`
2. Delete the `HEICThumbnailHandler` folder.

Existing thumbnails may continue to display, but new thumbnails will not be created.

# Building

This project was built with Visual Studio 2022.

Requires [libheif](https://github.com/strukturag/libheif) which can be installed with [vcpkg](https://github.com/microsoft/vcpkg).

`vcpkg install libheif:x64-windows`

Optionally use the included vcpkg overlay which removes the dependancy on the x265 encoder, a 5MB dll which is not used.

`vcpkg install libheif:x64-windows --overlay-ports=..\windows-heic-thumbnails\vcpkg-overlay`
