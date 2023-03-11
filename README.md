# Replicator-Revival-Project
Giving life back to the Makerbot Replicator 1, 1 Dual, 2, and 2X 3D Printers.

This repository is the be all end all of information regarding the Makerbot 2 and 2X.
It will include instructions on installation of modern firmware, support for legacy
firmware and techniques, motion system conversions, common problems and fixes, BOMs,
CAD models, and more.

If there is anything that you feel that I have missed, or that you have extra information
regarding, please please please open an issue or make a pull request! Useful information
about these printers is hard to come by, and finding people who have a lot of experience 
with them is even harder!

There are three parent sections to this repository, Klipper, Sailfish, and Hardware. These are the names
of the two firmwares that are currently supported by the Makerbot 2 and 2X. Klipper and Sailfish will be 
dedicated to installation instructions for each firmware, and the benefits of each. The Hardware section
will include everything physically related to the printers, including, but not limited to, full CAD assemblies,
Bills of Materials, common problems and fixes, common mods and printable pieces, and instructions for all
things.

I plan to add a research section as well, including papers detailing specific information regarding these
printers. For instance, how adjustable acceleration on Klipper affects print quality found in a quantitaive
way.

### How to Choose an Operating System

## Sailfish
If you are still running the original Makerbot firmware, and don't want to spend any money on a raspberry pi,
fear not! This is the perfect option for you. Sailfish was made as a competitor to Marlin some years ago, and
was specifically compatable with the Makerbot proprietary software and their file types, known as `.x3g`.

This software is the best choice if you want your printer up and running fast. It will work with your existing 
makerbot slicing software, and will be the most familiar in terms of interface on the printer when compared
to the original makerbot software.

## Klipper
If you are seeking modern print quality and speed, along with features not supported by Sailfish, then
Klipper is for you! Klipper will require an external computing source to run, such as a raspberry pi or
similar device. Using klipper will allow these printers to run the normal `.gcode` files, give them input
shaper, linear advance, an actively supported firmware, and access to automatic bed leveling.

I highly recommend Klipper if you are restoring one of these printers. It boosts their capabilities ten-fold,
and allows you an upgrade path via current hardware support that is locked off to you in Sailfish.

### Instructions
