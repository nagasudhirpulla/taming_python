# 
## What is an Installer

-   Installer should contain required files and setup a software in a client machine
-   Running an installer file should
    -   Pastes the required files in appropriate folder locations
    -   Runs required automation scripts to setup the required software components
    -   Creates shortcuts to access the software

## Inno Setup

-   InnoSetup is a software that can create an installer for software files
-   It can be downloaded from [https://jrsoftware.org/isdl.php](https://jrsoftware.org/isdl.php)

## Simple python based UI for demo

-   Running the following python script creates a simple application with a UI
-   Create an exe file from the python script using the pyinstaller command `pyinstaller --onefile --noconsole .\\index.py`

```python
# Install tkinter with "pip install tk"
# Install pyinstaller with pip install pyinstaller. 
# Create exe with "pyinstaller --onefile --noconsole .\\index.py"
# Import Module
from tkinter import Tk, Menu, Label, Entry, Button

# create root window
root = Tk()

# root window title and dimension
root.title("Awesome UI App")
# Set geometry(widthxheight)
root.geometry('350x200')

# adding menu bar in root window
# new item in menu bar labelled as 'New'
# adding more items in the menu bar
menu = Menu(root)
item = Menu(menu)
item.add_command(label='New')
menu.add_cascade(label='File', menu=item)
root.config(menu=menu)

# adding a label to the root window
lbl = Label(root, text="Write Something...")
lbl.grid()

# adding Entry Field
txt = Entry(root, width=10)
txt.grid(column=1, row=0)

# function to display user text when
# button is clicked
def clicked():
    res = "You wrote " + txt.get()
    lbl.configure(text=res)

# button widget with red color text inside
btn = Button(root, text="Click me",
             fg="red", command=clicked)
# Set Button Grid
btn.grid(column=2, row=0)

# Execute Tkinter
root.mainloop()

```

## Create installer with InnoSetup

-   The following is a sample InnoSetup script (script.iss) that creates an installer named `Awesome Demo App Setup.exe` for the software files. Compiling the below script with InnoSetup creates the `Awesome Demo App Setup.exe` file.
-   After running the installer, a desktop shortcut and start menu shortcut are created to open the installed application

```bash
#define MyAppName "Awesome Demo App"
#define MyAppVersion "1.0"
#define MyAppPublisher "Learning Software"
#define MyAppURL "<https://youtube.com/%40learningsoftwareskills>"

[Setup]
; NOTE: The value of AppId uniquely identifies this application. Do not use the same AppId value in installers for other applications.
; (To generate a new GUID, click Tools | Generate GUID inside the IDE.)
AppId={{da3f91c1-3c42-4260-b5e9-2e1ca5f8e217}}
AppName={#MyAppName}
AppVersion={#MyAppVersion}
;AppVerName={#MyAppName} {#MyAppVersion}
AppPublisher={#MyAppPublisher}
AppPublisherURL={#MyAppURL}
AppSupportURL={#MyAppURL}
AppUpdatesURL={#MyAppURL}
DefaultDirName={autopf}\\{#MyAppName}
DefaultGroupName={#MyAppName}
; Comment the following line to run in administrative install mode (install for all users).
PrivilegesRequired=lowest
OutputDir=Installer
OutputBaseFilename={#MyAppName} Setup
SolidCompression=yes
WizardStyle=modern
SetupIconFile=favicon.ico

[Files]
Source: "dist\\index.exe"; DestDir: "{app}"
Source: "readme.md"; DestDir: "{app}"; Flags: isreadme
Source: "favicon.ico"; DestDir: "{app}"

[Icons]
Name: "{autoprograms}\\{#MyAppName}"; Filename: "{app}\\index.exe"; WorkingDir: "{app}"; IconFilename: "{app}\\favicon.ico"
Name: "{autodesktop}\\{#MyAppName}"; Filename: "{app}\\index.exe"; WorkingDir: "{app}"; IconFilename: "{app}\\favicon.ico"

```

-   `#define` is used to define the variables used in the iss script
-   The following sections are defined in the iss script file
    -   `[Setup]` section configures the main settings of the installer
    -   `[Files]` section defines the files to be copied into the installation folders
    -   `[Icons]` section configures the shortcuts to launch the program
-   The documentation page at [https://jrsoftware.org/ishelp/index.php?topic=consts](https://jrsoftware.org/ishelp/index.php?topic=consts) contains the explanation about the constants {app}, {autoprograms}, {autodesktop}, {autopf} used in the iss script
    -   `{app}` - directory where the software files would be present after installation
    -   `{autopf}` - program files folder
    -   `{autoprograms}` - Programs folder on the Start Menu
    -   `{autodesktop}` - desktop folder

## References

-   Inno Setup docs - [Inno Setup Help](https://jrsoftware.org/ishelp/)
-   [https://youtu.be/l1p2GQxcP54?si=tSVenL46C1bKaQzj](https://youtu.be/l1p2GQxcP54?si=tSVenL46C1bKaQzj)
-   run script after installation - [windows - How to run a PowerShell Script after Inno Setup installer - Stack Overflow](https://stackoverflow.com/questions/56419077/how-to-run-a-powershell-script-after-inno-setup-installer)
-   Sign the installer [https://revolution.screenstepslive.com/s/revolution/m/10695/l/563371-signing-installers-you-create-with-inno-setup](https://revolution.screenstepslive.com/s/revolution/m/10695/l/563371-signing-installers-you-create-with-inno-setup)
-   Sign an exe with sign tool - [https://stackoverflow.com/questions/252226/signing-a-windows-exe-file](https://stackoverflow.com/questions/252226/signing-a-windows-exe-file)
-   [https://learn.microsoft.com/en-us/windows/win32/seccrypto/using-signtool-to-sign-a-file](https://learn.microsoft.com/en-us/windows/win32/seccrypto/using-signtool-to-sign-a-file)
-   [https://www.youtube.com/watch?v=vAfYP9hiC0M](https://www.youtube.com/watch?v=vAfYP9hiC0M)
-   Sample Innosetup script - [https://github.com/nagasudhirpulla/FolderProtectionService/blob/master/src/FolderProtectionService/InstallerAssets/AppInstallerGenScript.iss](https://github.com/nagasudhirpulla/FolderProtectionService/blob/master/src/FolderProtectionService/InstallerAssets/AppInstallerGenScript.iss)
-   InnoSetup script syntax - [https://jrsoftware.org/ishelp/topic_scriptformatoverview.htm](https://jrsoftware.org/ishelp/topic_scriptformatoverview.htm)
-   InnoSetup script constants - [https://jrsoftware.org/ishelp/index.php?topic=consts](https://jrsoftware.org/ishelp/index.php?topic=consts)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2ODA4NzExMF19
-->