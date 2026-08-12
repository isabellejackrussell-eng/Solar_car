# ENEL373 LTspice Setup Guide

This guide was made by Bailey Allen, based on the original guide by Dr. Chris Hann.

- [Windows](#windows)
- [macOS](#macos)
- [Linux](#linux)



## Windows

### Installation

Choose one of the following methods to install LTspice on Windows:

#### Method 1: Download using `winget`

1. Open the start menu and search for 'Terminal'.

2. Within the terminal, run:

    ``` powershell
    winget install AnalogDevices.LTspice
    ```

    <p align="center">
        <img src="images/windows_terminal_install.png" alt="winget install" width=600"/>
    </p>

3. Accept any licenses and wait for the installation to complete.

#### Method 2: Download from the LTspice website

1. Go to the [LTspice download page](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html) and download the Windows version (24+).

    <p align="center">
        <img src="images/download_page.png" alt="LTspice Download Page" width="400"/>
    </p>

2. Launch the LTspice installer, and follow the install instructions.

3. Ensure that you set LTspice to install for *All users*.

    <p align="center">
        <img src="images/windows_installation_type.png" alt="LTspice Installer" width="400"/>
    </p>

### Project Setup

1. There is a bug in the LTspice software which is sometimes present where an `e` may appear in the first line of the `standard.bjt` file. You need to delete this before proceeding.

    - Open File Explorer, and in the path bar, type `%localappdata%` and press enter.

        <p align="center">
        <img src="images/windows_fileexplorer_localappdata.png" alt="%localappdata% in file explorer path"/>
        </p>

    - Navigate to `LTspice\lib\cmp\` and open the `standard.bjt` file in a text editor.

    - Delete the `e` character from the first line of the file. If there is no `e`, then you can skip this step!

    ``` spice
    ⌄
    e* Copyright � 2000 Linear Technology Corporation.   All rights reserved.
    *
    *
    .model 2N2222 NPN(IS=1E-14 VAF=100
    +   BF=200 IKF=0.3 XTB=1.5 BR=3
    +   CJC=8E-12 CJE=25E-12 TR=100E-9 TF=400E-12
    +   ITF=1 VTF=2 XTF=3 RB=10 RC=.3 RE=.2 Vceo=30 Icrating=800m  mfg=NXP)

    ...
    ```

2. Back to your project directory, open the `run_TL494_test_CEH.asc` file in LTspice. It should show an empty spot for the TL494 to be placed.

    <p align="center">
    <img src="images/windows_ltspice_project_new.png" alt="LTspice basic project" width="600"/>
    </p>

3. Drag the `TL494_CEH.sub` file into the LTspice window, which should open a window showing the code for the TL494 chip.

4. Ensure that *both* `.lib` lines between the `***`'s correspond to the pathname for the `standard.dio` and `standard.bjt` files within your LTspice directory.

    The default path should work without alteration, however if LTspice has issues finding the files, you may need to change to the full path of these files, for example:

    ``` spice
    .lib C:\Users\USERNAME\AppData\Local\LTspice\lib\cmp\standard.dio
    ```

5. On the blue `.subckt` line, highlight `TL494_CEH`, right-click, then select *Create Symbol*.

    <p align="center">
    <img src="images/windows_ltspice_tl494_code.png" alt="LTspice basic project" width="600"/>
    </p>

6. Save the `TL494_CEH.asy` file to the same directory as your project.

    You can now close the <img src="images/ui/file_asy.png" height="15px">`TL494_CEH.asy` and <img src="images/ui/file_sub.png" height="15px">`TL494_CEH.sub` files by right clicking on their tabs and selecting **× Close**.

    <p align="center">
    <img src="images/windows_ltspice_close_tabs.png" alt="LTspice basic project" width="600"/>
    </p>

7. You should now be back to the `run_TL494_test_CEH.asc` schematic. To insert the TL494, click on *Component* <img src="images/ui/component.png" height="15px">.

8. Change the *Top Directory* to your project directory. Select `TL494_CEH`, and click *Place*.

    <p align="center">
    <img src="images/windows_ltspice_component_select.png" alt="LTspice basic project" width="500"/>
    </p>

9. Drag and drop the TL494 into the empty spot in the schematic. To stop placing components, right-click.

10. To simulate the circuit, we first need to change the simulation settings. Click *Simulate* > <img src="images/ui/settings.png" height="15px"> *Settings*.
    
    <p align="center">
    <img src="images/windows_ltspice_edit_settings.png" alt="LTspice edit simulation settings" width="500"/>
    </p>

11. Within Settings, go to the *SPICE* tab. Change `Gmin`, `Abstol`, `Chgtol`, and `Volttol` to *1e-006*. Change the *Default Integration method* to `Gear`, otherwise there are errors in the ode45 solver and it runs very slowly. Click *OK* to confirm settings.

    <p align="center">
    <img src="images/windows_ltspice_simulation_settings.png" alt="LTspice simulation settings" width="400"/>
    </p>
    
12. To run the simulation, click <img src="images/ui/run.png" height="15px">*Run*.

13. To check if the simulation ran correctly, select click the `E1` wire <img src="images/ui/probe_red.png" height="15px">. A square wave should show in the waveform viewer.

    <p align="center">
    <img src="images/windows_ltspice_simulation_probe.png" alt="LTspice waveform viewer" width="600"/>
    </p>

## macOS

### Installation

Choose one of the following methods to install LTspice on Windows:

#### Method 1: Download using `homebrew`

Note, this method requires the [Homebrew Package Manager](https://brew.sh/) to be installed.

1. Open a console window.

2. Within the terminal, run:

    ``` bash
    brew install ltspice
    ```

    and enter your user password if prompted.

    <p align="center">
        <img src="images/macos_console_install.png" alt="winget install" width=600"/>
    </p>


#### Method 2: Download from the LTspice website

1. Go to the [LTspice download page](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html) and download the macOS version (17+).

    <p align="center">
        <img src="images/download_page.png" alt="LTspice Download Page" width="400"/>
    </p>

2. Launch the LTspice.pkg installer, and follow the install instructions.


### Project Setup

1. Back to your project directory, open the `run_TL494_test_CEH.asc` file in LTspice. It should show an empty spot for the TL494 to be placed.
    
    You may need to set LTspice as the default application for `.asc` files. Right-click on the file, select *Get Info*, change the *Open with* option to LTspice, and click *Change All...*.

    <p align="center">
    <img src="images/macos_ltspice_project_new.png" alt="LTspice basic project" width="600"/>
    </p>

3. Right click the `TL494_CEH_macOS.sub` in finder, and select *Get Info* as before. Change the *Open with* option to LTspice.

    If LTspice does not show in the drop-down list, select *Other...*, and search for LTspice.app in your applications folder. If LTspice is greyed out, change the *Enable* dropdown to *All Applications*.

    <p align="center">
    <img src="images/macos_ltspice_set_default_app.png" alt="LTspice basic project" width="600"/>
    </p>

    Once LTspice is selected, click *Change All...*, and then you should be able to open the file by clicking on it in finder.

4. Ensure that *both* `.lib` lines between the `***`'s correspond to the pathname for the `standard.dio` and `standard.bjt` files within your LTspice directory.

    The default path should work without alteration, however if LTspice has issues finding the files, you may need to change to the full path of these files, for example:

    ``` spice
    .lib /Users/$USER/Library/Application Support/LTspice/lib/cmp/standard.bjt
    ```

5. On the blue `.subckt` line, highlight `TL494_CEH`, right-click, then select <img src="images/ui/new_symbol.png" height="15px">*Create Symbol*.

    <p align="center">
    <img src="images/macos_ltspice_tl494_code.png" alt="LTspice basic project" width="600"/>
    </p>

6. Save the `TL494_CEH.asy` file to the same directory as your project.

    <p align="center">
    <img src="images/macos_ltspice_tl494_save.png" alt="LTspice basic project" width="600"/>
    </p>

    <p align="center">
    <img src="images/macos_ltspice_tl494_save_directory.png" alt="LTspice basic project" width="600"/>
    </p>

    You can now close both the `TL393_CEH_macOS.sub` and `TL494_CEH.asy` files.

7. You should now be back to the `run_TL494_test_CEH.asc` schematic. To insert the TL494, Secondary click anywhere on the schematic, and select<img src="images/ui/t_square.png" height="15px">*Draft* > <img src="images/ui/file_asy.png" height="15px">*Component*, or simply press the `F2` key.

8. Change the *Top Directory* to your project directory. Select `TL494_CEH`, and click *Ok*.

    <p align="center">
    <img src="images/macos_ltspice_component_select.png" alt="LTspice basic project" width="500"/>
    </p>

9. Drag and drop the TL494 into the empty spot in the schematic. To stop placing components, secondary-click.

10. To simulate the circuit, we first need to change the simulation settings. Click <img src="images/ui/tools.png" height="15px"> *Tools*.

11. Within Settings, go to the *SPICE* tab. Change `gmin`, `abstol`, `chgtol`, and `volttol` to *1E-006*. Change the *Default Integration method* to `Gear`, otherwise there are errors in the ode45 solver and it runs very slowly. Click *OK* to confirm settings.

    <p align="center">
    <img src="images/macos_ltspice_simulation_settings.png" alt="LTspice simulation settings" width="400"/>
    </p>
    
12. To run the simulation, click <img src="images/ui/run_macos.png" height="15px">*Run*.

13. To check if the simulation ran correctly, select click the `E1` wire <img src="images/ui/probe_red.png" height="15px">. A square wave should show in the waveform viewer.

    <p align="center">
    <img src="images/macos_ltspice_simulation_probe.png" alt="LTspice waveform viewer" width="600"/>
    </p>




## Linux

🚧 Under Construction 🚧
