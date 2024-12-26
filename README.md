# gtav-ps4-sourcecode-build-guide
This tutorial will accompany you in compiling and setting up GTA 5 PS4 source code. Only official tutorial is this one for now


# GTAV Base PKG and Update PKG Installation Guide

## What You Need:
- A decent computer
- A brain
- A Jailbroken PS4 (Required for running the build)
- PS4 Firmware version 5.05 or higher

## GTAV Downloads

### Base PKG:
You can download the base PKG for GTAV from the following link:

[Download Base PKG for GTAV](https://1fichier.com/?owilwri8303p58o3x72u&af=3662447)

### Update PKG (v1.46):
You can download the Update PKG for version 1.46 from the following link:

[Download Update PKG v1.46](https://1fichier.com/?xdiqoe5n3c6mqgixa0ns&af=3662447)

---

**BEFORE WE PROCEED, ALL CREDIT GOES TO `JORBY`. WITHOUT HIM, THIS WOULD NEVER BE POSSIBLE, AND THANKS TO `Mojso` FOR THE HELP TOO!**

---

## Create X:\ Drive:
  - Create a new folder called “GTA” to the Desktop or anywhere that you want.
  - Inside the “GTA” folder create a folder called “gta5”.
  - Copy all content from the “GTAV Source” Folder to “gta5”.
  - Now right click on the “gta5” folder and turn off the “Read-Only” option then press “Apply”.
### 5. **Map the X: Drive to the Folder Using the `net use` Command**
   - Open **Command Prompt** with Administrator privileges:
     - Search for **cmd** in the Start menu.
     - Right-click **Command Prompt** and select **Run as administrator**.
   - Run the following command, replacing `<username>` with your actual username and `<path_to_gta_folder>` with the location where the **GTA** folder is saved:
     ```bash
     net use X: \\localhost\c$\Users\<username>\Desktop\<path_to_gta_folder> /persistent:yes
     ```
     For example:
     ```bash
     net use X: \\localhost\c$\Users\Seb\Desktop\GTA /persistent:yes
     ```

     - **Note**: Replace `<username>` with your actual Windows username, and `<path_to_gta_folder>` with the correct path to your **GTA** folder if it's not on the Desktop.

### 6. **Verify the X: Drive**
   - Open **File Explorer**.
   - You should now see the **X:** drive mapped to your **GTA** folder.

---

## Notes:
- The `net use` command maps the folder as the **X:** drive. You can access the folder as if it were a separate drive on your computer.
- The **/persistent:yes** flag ensures that the drive will be mapped automatically every time you log in to Windows.

## Build Preparations

1. **Download 7Zip-ZSTD**  
   Most of the zipped files are ZSTD compressed, and regular 7z does not work. You need to download and install **7Zip-ZSTD**.

2. **Download Main-User-Tools.zip**  
   Extract the contents of the downloaded `Main-User-Tools.zip` to a location you can easily remember. For example, we'll use:  
   `X:\1. Main-User-Tools`.
   Download link : https://drive.google.com/drive/folders/1jxQApVu7knH2emiUG8U2LvTmCRR_fvpm?usp=sharing

   If you don’t have the Source Code, in `Main-User-Tools.zip\1. Main-User-Tools\1. SRC`, there is a `ReadME.txt` file to assist you in downloading the Source Code.

3. **Disabling Antivirus**  
   It’s recommended to disable Windows Antivirus or your Anti-Virus program of choice as it usually results in fewer problems when compiling and faster build times.

4. **Source Code Directory**  
   The directory where the Source Code needs to be placed is:  
   `X:\gta5`.  
   Make sure to unset the **Read-Only** attribute on the folder containing the Source Code.

5. **Required Software**  
   You will need the following software for the build:
   - Visual Studio 2012 + Update 4
   - Visual Studio 2017 Community Edition with specific workload
   - IncrediBuild 4.0 or newer
   - Redistributables
   - DirectX SDK (June 2010)

   These files can be found in `X:\1. Main-User-Tools\3. Redistributables`.

### Installation of Required Tools

1. **Visual Studio 2012 Installation**  
   Open `X:\1. Main-User-Tools\3. Redistributables\1. VS12\VS Ultimate` and launch `vs_ultimate.exe`. Make sure to check the box for **Microsoft Foundation Classes for C++** during installation.

1b. **Visual Studio 2012 Update 4 Installation**  
   After Visual Studio 2012 is installed, go to `X:\1. Main-User-Tools\3. Redistributables\1. VS12\VS Update 4` and launch `VS2012.4.exe` to install the update.

2. **Visual Studio 2017 (Community Edition) - Important Note**  
   Open `X:\1. Main-User-Tools\3. Redistributables\2. VS17\` and launch `vs_Community.exe`.  
   If you are using **Visual Studio 2017 Community Edition**, you **must** install the **Desktop Development with C++** workload.  
   - Open the Visual Studio Installer and select **Desktop Development with C++** under workloads.
   - This is required for compiling C++ code correctly during the build process.

3. **IncrediBuild Installation**  
   Open `X:\1. Main-User-Tools\3. Redistributables\3. Incredibuild` and run `Install.bat`. Note that this will require **Administrator Privileges**.
 - At „Welcome“ select „Install IncrediBuild“
 - At Component Selection select IncrediBuild Agent and IncrediBuild Coordinator
 - Do not change any other settings

4. **DirectX SDK (June 2010) Installation**  
   Open `X:\1. Main-User-Tools\4. Redistributables\3. DirectX SDK (June 2010)` and launch `DXSDK_Jun10.exe`.  
   If you encounter error **S1023**, uninstall **Visual C++ 2010 Redistributable** and reinstall **DirectX SDK (June 2010)**.

5. **Git Installation**  
   To install Git, open your browser and go to the [Git Website Download Page](https://git-scm.com/downloads).  
   Choose your operating system, download the correct version for your PC, and install it.  
   Alternatively, use the one in `X:\1. Main-User-Tools\3. Redistributables\5. GIT` and launch `Git-2.47.0.2-64-bit.exe`.

6. **ORBIS SDK SETUP**  
   Open `X:\1. Main-User-Tools\0a. ORBIS SDK SETUP` and launch `VsiInstallerPS4.exe`.  
   Choose Visual Studio 2017, and install it.

7. **ORBIS VS INTEGRATION**  
   Open `X:\1. Main-User-Tools\4. Redistributables\6. VS SCE` and launch `VsiInstallerPS4.exe`.  


8. **ENV VARIABLE**  
   Open `X:\1. Main-User-Tools\0b. ENV SETUP` and launch the 2 .bat files `(SORYNX) SDK ENV PS4 ORBIS (ADMIN).bat` and `setup_env.bat`.  


---

## Patches

In order to get the game to run, you’ll be required to apply some patches. You can find the mirrors to the diffs/patches [here](https://drive.usercontent.google.com/uc?id=16H-J03XOw6r4Pdv7AQdS-s6Pl8ImzRBh&authuser=0&export=download).  
Follow the instructions for each patch. Usually, it’s just running:  
**12/24/2024:**  
`git apply --reject --whitespace=fix patchname.patch`  
This patch is the base patch file. All subsequent patch files are derived from this and are expected to be applied incrementally. They are required.  

All the `.patch` files need to be in `X:\gta5\src\dev_ng\` along with `Patch_Source.bat`. Run `Patch_Source.bat` to apply the patches.

now go to `X:\gta5\src\dev_ng\rage\base\src\system\main.cpp` open the file and search for `bool g_EnableRfs = true;` and change true to false.

---

## Prebuilding

Now that the base preparations are out of the way, we can finally get to building some requirements.

---

## Building Shaders

Shaders are required for the game to load (obviously), so in order to get them working, we must build them. To do so:

1. Open `X:\gta5\src\dev_ng\game\VS_Project\load_sln_unity_2012.bat` and open it with Visual Studio 2012.

2. After you’ve opened the project in Visual Studio 2017, at the top change from **Win32** to **ORBIS**.  
   Right-click on one of the projects and go to **BankRelease**, then change from **Durango** to **ORBIS**.

3. Select all the projects, except the project **Properties** → **C/C++** → **General**, find:  
   **Treat Warnings As Errors**, and set it to **No**.  
   Then find **Processor Compilation** and set that to **Multi Yes** (Should work?).  
   This will speed up the time it takes to build the solution since it’ll be using the processor and ignoring all warnings, which is what we expect to occur.

4. Next, find **shaders_rc**, select it in Visual Studio, right-click it, and press **Rebuild**.  
   This will begin rebuilding your Shaders in IncrediBuild.

5. To see the progress and watch its status, in the taskbar, open the Overflow Menu (the small `^` in the taskbar on the right).  
   Find **IncrediBuild Agent** (the one with a green arrow), right-click it, and press **Build Monitor**.  
   In **Build Monitor**, on the left press the icon at the top that should say **Progress**.  
   You should now see what you're building, and at the bottom left of the window, you'll see a percentage of how complete it is out of 100%.

Once the shaders are built, close Visual Studio 2017 and proceed to the next steps.

---

## Building Scripts:

   - To build scripts, run this in command prompt  
----------------------------------------------------------------------------------
```batch
X:
cd X:\gta5\src\dev_ng
setenv
cd ..\..\tools_ng\bin\RageScriptEditor
ragScriptEditor
```
----------------------------------------------------------------------------------
   - After the editor launches, select “File > Open Project”
   - Then open “X:\gta5\script\dev_ng\singlesplayer\GTA5_SP.scproj”
   - On the top switch ‘Windows x86’ to ‘PlayStation 4’.
   - After that select “Compiling > Intelibuild > Build Project” and wait until the compiling finishes.

---

## Building the Game / Requirements

In `X:\1. Main-User-Tools\2. Meta Files`, you will have the files `studios.meta` & `local-ip.bat`. If you run it, there are instructions for you to edit the `studios.meta` file.  
You want to edit the `local-ip.bat`. A text file will be generated called `SubnetMask`. Then you can copy/cut and paste the `X:\gta5\tools_ng\etc\globals` (or use the shortcut provided to you named **Globals Folder**).

Should the `local-ip.bat` file not work for you:

- **In Windows 11**:  
  Navigate to `local-ip.txt` in the `studios.meta` file to  
  Settings → Network & Internet → Advanced Network Settings. Select the Network Adapter you're using and press **View Additional Properties**.  
  Note down your IPv4 Address and put that within your `studios.meta` file, then you can copy/cut and paste the `studios.meta` file to `X:\gta5\tools_ng\etc\globals` (or use the shortcut provided to you named **Globals Folder**).

- **In Windows 10**:  
  Navigate to Settings → Network & Internet → Change Adapter Options. Select the Network Adapter you're using, right-click it, and press **Details**.  
  Note down your IPv4 Address, close all the windows you've opened, and put the IPv4 Address within your `studios.meta` file. Then you can copy/cut and paste the `studios.meta` file to the `Globals Folder`.

---

In `X:\1. Main-User-Tools\5. Error Fix` you will have the file `any_types.h`. You will need to copy/cut and paste the `any_types.h` file into `X:\gta5\src\dev_ng\rage\base\src\forceinclude\templates` or use the shortcut that is already in the file. Then run `makeheaders.bat`.

---

## Building the Game

Run `load_sln_unity_2012.bat` in `X:\gta5\src\dev_ng\game\VS_Project`.  
At the top, change from **Win32 to Orbis** and use **BankRelease**, and after everything is done, press **Build**, then **Build Solution**. The game should begin compiling.  
If everything was done correctly, you will get `game_orbis_bankrelease.elf`. Rename it to `eboot.bin`. Now I will tell you how to make the `update.pkg`.

---

## EXTRACT CONTENT OF PKG UPDATE

1. Download the PS4 Patch builder
2. Extract the folder from the zip file.
3. Run `Patch Builder v.1.3.3.exe`. (don't worry if it's detected as a virus, it is a false positive)
4. On the right side under Package Extraction, select the 3 dots and choose your Package file.
5. Press “Extract Package”, select all, and press Extract. You need to do this with `Update RPF v1.46`.

---

## Transferring Build Files + BUILD PACKAGE:

1. Install the unmodified PKG of the base game on your PS4. https://1fichier.com/?owilwri8303p58o3x72u&af=3662447
2. Open the update 1.46 PKG with PS4 Patchbuilder and extract it using the guide above.
3. Paste the compiled shaders into ‘common\shaders’. You need both `orbis` and `orbis final`.
4. Paste the compiled `scripts.rpf` into `\ps4\levels\gta5\script`.
5. Place the `gameconfig2699.xml` file in the main directory.  
   - The correct `gameconfig2699.xml` file can be obtained from `Required Files/gameconfig2699.xml`.
6. Place the compiled “eboot.bin” file in the main directory as well.
7. Then rebuild the package with PS4 Patch Builder.
8. Install the modified update PKG on the PS4 using Remote PKG INSTALLER, FTP, or USB.

---
