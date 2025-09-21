# Collection-of-Macro-and-CustomBuildAction
With new version of B4X, #Macro is a useful addition.
It is a shortcut to automate some tasks and provide a very convenient way of using the IDEs.
It is an alternative to Comment links where you only need a mouse click instead of pressing the Control key and mouse click.
However, for those who prefer to use keyboard shortcuts, e.g Ctrl + 1, Ctrl + 2 it is still supported.

Tutorial : https://www.b4x.com/android/forum/threads/b4x-comment-links-and-macros.119897/

Here are my collection.\
You can rename the Title to any name as you like.\
You can also convert them back to comment links.

### Sync files (B4XPages)
This macro is used to be a comment link to copy asset files from Shared Files folder to Files folder
```
#Macro: Title, Sync files, ide://run?file=%WINDIR%\System32\Robocopy.exe&args=..\..\Shared+Files&args=..\Files&FilesSync=True
```

### Export project (B4XPages)
This macro is used to be a comment link to export B4XPages project as zip file
```
#Macro: Title, Export as zip, ide://run?File=%B4X%\Zipper.jar&Args=%PROJECT_NAME%.zip
```

### Sync json and binary layouts (B4XPages)
Please check: Tool [B4X] JsonLayouts - synchronize json and binary layouts
```
#Macro: After Save, Sync Layouts, ide://run?File=%ADDITIONAL%\JsonLayouts.jar&Args=%PROJECT%&Args=%PROJECT_NAME%
#Macro: Title, JsonLayouts folder, ide://run?File=%WINDIR%\explorer.exe&Args=%PROJECT%\JsonLayouts
```

### Go to top (B4XPages)
Instead of scrolling the page to top of page, one click action to go to top of page.
```
#Macro: Title, Top, ide://goto?Module=B4XMainPage
```

### Go to a common sub routine
I find this useful for B4J projects to jump to AppStart sub
```
#Macro: Title, AppStart, ide://goto?Module=Main&Sub=AppStart
```

### Open Objects folder
I find this useful for B4J projects to open the Objects folder (File.DirApp) for editting sqlite db or config.ini file
```
#Macro: Title, Objects, ide://run?file=%WINDIR%\SysWOW64\explorer.exe&args=%PROJECT%\Objects
```

### Open GitHub Desktop
This macro is used to be a comment link to open GitHub Desktop app.
```
#Macro: Title, GitHub Desktop, ide://run?file=%WINDIR%\System32\cmd.exe&Args=/c&Args=github&Args=..\..\
```

### Download required Additional Libraries
This is a convenient way to download all required libraries instead of searching for them one by one on the forum.
https://www.b4x.com/android/forum/threads/tool-additional-libraries-downloader.166880/
```
#Macro: Title, GetLibs, ide://run?file=%JAVABIN%\java.exe&args=-jar&args=%ADDITIONAL%\..\B4X\libget-non-ui.jar&args=%PROJECT%&args=False
```

### Copy a single file from source to release folder
If the b4xlib has only a single class, this macro can copy or overwrite the destination file.
```
#Macro: Title, Copy, ide://run?file=%WINDIR%\System32\cmd.exe&Args=/c&Args=copy&Args=%PROJECT%\MinimaList.bas&Args=%PROJECT%\..\release\MinimaList.bas
```

### Copy specific files from source to release folder
I use this macro to copy certain files that need to be updated in release folder.
```
#Macro: Title, Update, ide://run?file=%WINDIR%\System32\Robocopy.exe&args=%PROJECT%&args=%PROJECT%\..\release\&args=*.bas&args=*.json&args=*.b4j&args=*.html&args=*.example&args=help.css&args=main.css&args=main.js&args=/S
```

### Open release folder
I use release folder for preparation to create b4xlib or project template, excluding some unnecessary files. It is put at the same level of source folder.
```
#Macro: Title, Release, ide://run?file=%WINDIR%\SysWOW64\explorer.exe&Args=%PROJECT%\..\release
```

### Update version in manifest.txt using Manifest Writer
I use this tool to update new version value in manifest.txt before distributing the new b4xlib or project template. Other values can also be updated. This is more convenient than opening the release folder from file system and edit the file manually.
https://www.b4x.com/android/forum/threads/tool-manifest-txt-writer-for-b4xlib.168723/
```
#Macro: Title, Version, ide://run?file=%JAVABIN%\java.exe&Args=-jar&Args=%ADDITIONAL%\..\B4X\manifest-writer-non-ui.jar&Args=%PROJECT%\..\release&Args=%PROJECT%\..\release&Args=Version&Args=2.10
```

### Packaging B4XLib or B4XTemplate
After using the above macro to update the version number in manifest.txt for the B4XLib, this is a quick way to package the file into a b4xlib and automatically put it inside the Additional Library folder.
Note: I organized my project source code into "source" folder and use "release" folder for the required files which are going into the b4xlib or template.

**B4XLib:** (B4X cross platform library)
```
#Macro: Title, Publish, ide://run?file=%JAVABIN%\jar.exe&WorkingDirectory=..\..\release&Args=-cMf&Args=%ADDITIONAL%\..\B4X\%PROJECT_NAME%.b4xlib&Args=*
```

**Project Template:** (or platform specific b4xlib)
```
#Macro: Title, Publish, ide://run?file=%JAVABIN%\jar.exe&WorkingDirectory=..\..\release&args=-cMf&args=%ADDITIONAL%\Pakai Server%20(5.40).b4xtemplate&args=*
```

### Backup B4J server project
To backup my B4J server projects, I use the following macro.
```
#Macro: Title, Backup, ide://run?file=%JAVABIN%\jar.exe&WorkingDirectory=..&Args=-cMf&Args=%PROJECT_NAME%_2025-09-17_1821.zip&args=Files&args=Objects\www&args=Objects\config.*&args=Objects\LICENSE&args=*.bas&args=*.b4j&args=*.b4j.meta&args=libs.json
```

### Publish server app
After compiling the server app in release mode, compress the required files as a single zip file for uploading to VPS server.
```
#Macro: Title, Deploy, ide://run?file=%JAVABIN%\jar.exe&WorkingDirectory=../Objects&args=-cMf&args=Publish.zip&args=www&args=*.jar&args=*.ini
```

### Copy jSerial library (jssc.dll) when building Standalone Package
This CustomBuildAction is provided by Erel to solve my question here:
https://www.b4x.com/android/forum/threads/solved-error-building-standalone-package-with-jserial-library-v1-40.165988/#post-1017771
```
#CustomBuildAction: After Packager, %WINDIR%\System32\robocopy.exe, ..\ temp\build\bin\ jssc.dll
```

### Send compiled app into Additional Library folder (tool)
This CustomBuildAction is useful for copying the compiled result.jar as a new name into Additional Library folder and called using macro tag.
```
#If Release
#CustomBuildAction: 2, C:\Windows\System32\cmd.exe, /c copy %PROJECT%\Objects\result.jar %ADDITIONAL%\..\B4X\manifest-writer-non-ui.jar
#End If
```
