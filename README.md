# Replicator-Revival-Project
Giving life back to the Makerbot Replicator 1, 1 Dual, 2, and 2X 3D Printers!

This repository is the be all end all of information regarding the Makerbot 2 and 2X.
It will include instructions on installation of modern firmware, support for legacy
firmware and techniques, motion system conversions, common problems and fixes, BOMs,
CAD models, and more.

If there is anything that you feel that I have missed, or that you have extra information
regarding, please please please open an issue or make a pull request! Useful information
about these printers is hard to come by, and finding people who have a lot of experience 
with them is even harder!

# Table of Contents
- **[How to Choose Your Firmware](https://github.com/Sgail7/Replicator-Revival-Project#how-to-choose-an-operating-system)**

- **[Klipper](https://github.com/Sgail7/Replicator-Revival-Project#klipper)**
    - [Installation]()
    - [Configs]()
    - [Macros]()
    - [Nevermore Filter]()
    - [Nozzle Alignment for 2X]()
    - [Common Setting Values]()
    - [PrusaSlicer and SuperSlicer Profiles]()

- **[Sailfish](https://github.com/Sgail7/Replicator-Revival-Project#sailfish)**
    - [Installation]()
    - [ReplicatorG]()
    - [Nozzle Alignment]()
    - [Common Setting Values]()
    - [GPX](https://github.com/markwal/GPX)
    - [PrusaSlicer Profiles]()

- **[Hardware](https://github.com/Sgail7/Replicator-Revival-Project#hardware)**
    - [Bed Warping Information and Potential Fix]()
    - [X-Axis Cable Strain Relief]()
    - [General Maintenance]()
    - [Bed Surface]()
    - [Replacement Hardware]()
    - [Power Supply Information]()

- **[Documentation](https://github.com/Sgail7/Replicator-Revival-Project#documentation)**
    - [BOMs](https://github.com/Sgail7/Replicator-Revival-Project/tree/main/Documentation/BOMs)
    - [Printer CADs]()
    - [Printer Parts](https://github.com/Sgail7/Replicator-Revival-Project/tree/main/Documentation/Printer%20Parts)
    - [Mightyboard]()
        - [Revision E]()
        - [Revision G]()
        - [Revision H]()

# Description of Main Directories

## Klipper
The Klipper folder comprises all gathered information on running the [Klipper](https://github.com/Klipper3d/klipper) firmware on the Replicator
1, 2, and 2X. This includes, but is not limited to, installation instructions, macros, configuration files,
specific tuning files, and information on common settings.

## Sailfish
The Sailfish folder comprises all gathered information on running the [Sailfish](https://github.com/SaschaKP/Sailfish-MightyBoardFirmware/releases/tag/7.10.12) firmware on the Replicator 1, 2, and 2X.
This includes, but is not limited to, installation instructions, copies of needed software, and information on common settings.

## Hardware
The Hardware folder comprises all gathered information on Hardware modifications to fix common issues on
the Replicator 1, 2, and 2X. These are gathered from experience and previous forum posts that may be hard to find or simply
not exist anymore.

## Documentation
The Documentation folder comprises all information concerning the construction and parts of these printers. This includes
but is not limited to, full Bills of Materials of the Replicator 1, 2, and 2X, full CAD models of the Replicator 1, 2, and 2X,
and short write-ups of the benefits of different modifications to the Replicator 1, 2, and 2X.

## Printed Parts
The Printed Parts folder comprises all information concerning the addition of printed parts to these printers. This is comprised of all of the most useful printed parts that I have found or made for these printers. The purpose of this section is to reduce confusion on what available models will work best or be the most useful.

# How to Choose an Operating System

**WARNING**- Sailfish is no longer actively supported! If you choose to install Sailfish as your firmware, do not expect any updates or support for bugs that you may find!

**NOTE**- Changing the firmware on your printer is in no way required. If you are happy with the results from the original Makerbot Industries firmware, then you can ignore the Klipper and Sailfish sections entirely! Significant information and improvement can still be gained from the [Hardware](https://github.com/Sgail7/Replicator-Revival-Project/tree/main/Hardware) and [Documentation](https://github.com/Sgail7/Replicator-Revival-Project/tree/main/Documentation) sections alone.

## Klipper
If you are seeking modern print quality and speed, along with features not supported by Sailfish, then
Klipper is for you! Klipper will require an external computing source to run, such as a raspberry pi or
similar device. Using Klipper will allow the Replicator 1, 2, and 2X to use the common `.gcode` file format.
It will also give them access to input shaper, linear advance, an actively supported firmware, and automatic bed leveling.

I highly recommend Klipper if you are restoring one of these printers. It boosts their capabilities ten-fold,
and allows you an upgrade path via modern hardware support that is locked off to you in Sailfish.

## Sailfish
If you are still running the original Makerbot firmware, and don't want any signficant changes to the way your printer operates, Sailfish is for you! Sailfish was made as a competitor to Marlin some years ago, and was made specifically to be fast on 8-bit based mainboards. It is compatable with the Makerbot proprietary software and their proprietary file format, known as `.x3g`.

This software is the best choice if you want your printer up and running fast. It will work with your existing 
Makerbot slicing software, and will be the most familiar in terms of interface on the printer when compared
to the original makerbot software.

# Notes
These are the names
of the two firmwares that are currently supported by the Makerbot 2 and 2X. Klipper and Sailfish will be 
dedicated to installation instructions for each firmware, and the benefits of each. The Hardware section
will include everything physically related to the printers, including, but not limited to, full CAD assemblies,
Bills of Materials, common problems and fixes, common mods and printable pieces, and instructions for all
things.

I plan to add a research section as well, including papers detailing specific information regarding these
printers. For instance, how adjustable acceleration on Klipper affects print quality found in a quantitaive
way.
