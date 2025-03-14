# WIP NOT FOR GENERAL USE

# <img src="media/klipper_toolchanger_logo.png?raw=true" height="100" align="top" /> klipper-toolchanger

<a href="https://discord.gg/jJs73c6vSc" target="_blank" alt="Join our Discord">![Discord](https://img.shields.io/discord/1226846451028725821?logo=discord&logoColor=%23ffffff&label=Join%20our%20Discord&labelColor=%237785cc&color=%23adf5ff)</a>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://github.com/sponsors/DraftShift" target="_blank" alt="Sponsor Us">![GitHub Sponsors](https://img.shields.io/github/sponsors/DraftShift?logo=githubsponsors&label=Sponsors&labelColor=rgb(246%2C%20248%2C%20250)&color=rgb(191%2C%2057%2C%20137))</a>


Based on Viesturz's work on [klipper-toolchanger](https://github.com/viesturz/klipper-toolchanger)

Tool changing extension for [Klipper](https://www.klipper3d.org).

# Klipper Compat Version
- Klipper > Jun 14, 2024 (1591a51)
- ~~Danger Klipper > Feb 15, 2024 (0cd16e9)~~ No longer compat till they update probe.py

# Installation

**NOTE:** `python 3.9+` is required for this mod, make sure your klipper install is using `python 3.9+`, otherwise you need to reinstall klipper with `python 3.9+` before you continue

To install this plugin, run the installation script using the following command over SSH. This script will download this GitHub repository to your RaspberryPi home directory, and symlink the files in the Klipper extra folder.

```
wget -O - https://raw.githubusercontent.com/Stealthchanger/klipper-toolchanger/main/scripts/install.sh | bash
```

**Add to `printer.cfg` in this order**
- [toolchanger-tool_detection.cfg](macros/toolchanger-tool_detection.cfg)
- [toolchanger.cfg](examples/toolchanger.cfg)
- [toolchanger-macros.cfg](macros/toolchanger-macros.cfg)
- [toolchanger-homing.cfg](macros/toolchanger-homing.cfg)

**tool configs** one per tool, 2 examples to follow, they do not need to be names AVR<n>
- [tool-AVR0.cfg](examples/tool-AVR0.cfg)
- [tool-AVR1.cfg](examples/tool-AVR1.cfg)

**usermacros and extra-macros** are a good start for user macros and can be modified.  Make sure to keep the `_TOOL` and `_TOOLCHANGER` macros in the right macros as they add special features.

- [toolchanger-usermacros.cfg](examples/toolchanger-usermacros.cfg)
- [toolchanger-extra-macros.cfg](examples/toolchanger-extra-macros.cfg)

**Optional** leds is based on the offical [StealthBurner leds](https://github.com/VoronDesign/Voron-Stealthburner/blob/main/Firmware/stealthburner_leds.cfg) and converted to multi tool aware
- [toolchanger-leds.cfg](examples/toolchanger-leds.cfg)
- [tool-AVR0-leds.cfg](examples/tool-AVR0-leds.cfg)
- [tool-AVR1-leds.cfg](examples/tool-AVR1-leds.cfg)

**Optional** for calibration ball probe or modified sexcbolt
- [calibrate-offsets.cfg](examples/calibrate-offsets.cfg)
- [calibrate-offsets-macros.cfg](macros/calibrate-offsets-macros.cfg)

**Optional** for hotend fan rpm detection (requires all hotends to be configured with tachometer)
- [toolchanger-fan-stall-detect.cfg](examples/toolchanger-fan-stall-detect.cfg)

[PRINT_START slicer info](PRINT_START.md)

**Make sure that `safe_z_home` is not defined as homing needs to be overridden in [toolchanger-homing.cfg](macros/toolchanger-homing.cfg)**

**If you choose to not use `toolchanger-extra-macros.cfg` please make sure to use the `_TOOLCHANGER_PRINT_START_START` and `_TOOLCHANGER_PRINT_START_END` in your `PRINT_START` macro, also `_TOOLCHANGER_PRINT_END_START` and `_TOOLCHANGER_PRINT_END_END` in your `PRINT_END` macro.  These are important to initialize the toolchanger as well as special protection calls.**

# Components

* [Toolchanger](toolchanger.md) - tool management support.
* [Tool probe](tool_probe.md) - per tool Z probe.
* [Rounded path](rounded_path.md) - rounds the travel path corners for fast non-print moves.
* [Tools calibrate](tools_calibrate.md) - support for contact based XYZ offset calibration probes.
