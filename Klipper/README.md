# Installation

## KIAUH

**Note:** KIAUH takes a little bit more work to set up, but is ideal for running
multiple instances of klipper, and also makes it possible to install any and
all frontends including Mainsail, Fluidd, and Octoprint! A huge thanks to
th33xitus for making [KIAUH](https://github.com/th33xitus/kiauh)!

**Step 1:**

Follow the instruction on [KIAUH's github page](https://github.com/th33xitus/kiauh#--%EF%B8%8F-instructions-) to install both the recommended operating
system for KIAUH and the script itself.

**Step 2:**

KIAUH is set by default to install klipper from the klipper3d repo, however, we
need to install it from the dockterj branch. This can be accomplished by editing
the file `klipper_repos.txt.example`.

SSH into your raspberry pi, and run the following commands:
```
cd kiauh
sudo nano klipper_repos.txt.example
```
Now, you should be presented with a screen that looks like this:

![](https://i.imgur.com/kWNYJNQ.png)

Delete the four uncommented lines, and add the line `https://github.com/dockterj/klipper` in their place.
Your screen should now look like this:

![](https://i.imgur.com/UTat7JL.png)

Now, hit Control+x to exit, then hit `y` to save the modified buffer.

**You must save the file as `klipper_repos.txt`, otherwise KIAUH will not recognize the file as valid.**

Hit `y` to save the file under a different name.

If you want to check to be sure the edit was successful, you can type `ls` into the command line. If the
file `klipper_repos.txt` is there, then the edit was successful.

**Step 3:**

Now you're ready to start KIAUH! Enter `./kiauh/kiauh.sh` to start the script.

Once in KIAUH, you should see a screen like this:

![](https://i.imgur.com/mJKOZqq.png)

KIAUH, by default, uses the official master branch of klipper. To tell KIAUH to
use this branch instead, we need to add the custom repo you created to KIAUH.

Input the number `6` to enter KIAUH's settings, then hit enter. 
You should now see a screen like this:

![](https://i.imgur.com/AMtFrQm.png)

Input `1` to set the custom repository. You'll see a screen like this:

![](https://i.imgur.com/w1uRnS1.png)

Input `0` to set the custom repository, you'll be presented with a screen like this:

![](https://i.imgur.com/0CWf11R.png)

Then input `b` and `b` again to get back to the main menu.

**Step 4:**

Now you can install Klipper! Input `1` to get to the installation menu. Once there,
input `1` again to enter the klipper installation procedure.

Input `1` to install python 3.x, then set the number of Klipper instances your would
like to install.

![](https://i.imgur.com/lEuWk4T.png)

You may be presented with a prompt like this:

![](https://i.imgur.com/mHdaWpC.png)

Input `y` for this prompt to avoid potential problems down the road.

Let the process complete, and now Klipper is fully installed! From here you can
install Moonraker, your interface of choice, and whatever other programs you may want 
that KIAUH offers.

**Step 5:**

Depending on the printer that you are running, you will either want to use the
`/config/printer-makerbot-replicator2-2012.cfg` config file or the
`/config/printer-makerbot-replicator2x-2012.cfg` config file.

Mainsail and Fluidd both allow you to copy over example configs from
within the web interface, however, Octoprint does not. These following steps
will detail the process of doing this through the ssh terminal. If this does
not apply to you, you can skip to the next step.
    
If you are still in KIAUH, input `Q` to close it, then type `cd` to navigate
back to the pi directory, which is represented by a `~`. The text preceding
your cursor will look similar to `pi@replicator2x:~ $`
    
Type `cd klipper/config` into the command line. You are now in Klipper's example
config folder. Type either `cp printer-makerbot-replicator2-2012.cfg ~/printer_data/config/`
or `cp printer-makerbot-replicator2x-2012.cfg ~/printer_data/config/` to copy the example
config for your printer into your printer's configuration directory.
    
Now type `cd ~/printer_data/config` to move over to your printer's configuration directory.
Type `rm printer.cfg` to remove the placeholder printer config that comes with klipper. Now
type `mv printer-makerbot-replicator2-2012.cfg printer.cfg` or 
`mv printer-makerbot-replicator2x-2012.cfg printer.cfg`, depening on your printer, to rename
the example config to the config name recognized by Klipper.

**Step 6:**

Now we're going to flash Klipper to the printer's mainboard.
    
Plug the printer into one of the Pi's usb ports. Verify that the device
appears in /dev/serial/by-id by executing the command `ls /dev/serial/by-id`.
If the printer is connected, this command will return a dialogue that looks like
this:

![](https://i.imgur.com/zxS6FMs.png)

Copy this by highlighting it, then right clicking it. Open up a temporary notepad document
and paste it into that, you'll need this to update your printer.cfg.

Find the section of your config that looks like this:
```
[mcu]
serial: dev/serial/by-id/[your-serial-id-here]
restart_method: mightyboard
baud: 250000
```

Update the `serial: [your-serial-id-here]` line with the line you saved earlier.
When completed the line should look similar to:
```
serial: /dev/serial/by-id/usb-MakerBot_Industries_The_Replicator_5533034353435160A141-if00
```
    
Now, go back to the command line and run:
```
cd ~/klipper/
make menuconfig
```
   
In this menu, choose the atmega1280, 16mhz, and uart0.

**Note:** See below for the note about atmega2560.
    
Once you enter those settings, hit `Q` to exit, then `Y` to save.
    
Now run the command `make`. This will build the firmware for your
particular machine.
    
Now, run the commands:
```
sudo service klipper stop
make flash FLASH_DEVICE=/dev/serial/by-id/dev/serial/by-id/[your-serial-id-here]
sudo service klipper start
```
Where an example of FLASH_DEVICE will look like:
```
FLASH_DEVICE=/dev/serial/by-id/dev/serial/by-id/usb-MakerBot_Industries_The_Replicator_5533034353435160A141-if00
```
This will flash your printer. If it fails, you may need to power off and then power on your printer,
or attempt to connect and disconnect with Klipper. It should flash after you try one or both of these things.

Congratulations! You now have Klipper installed on your Replicator 2 or 2X!
Head over to https://www.klipper3d.org/ for documentation on futher tuning
of your printer and to learn the specifics of what Klipper is capable of.

# Configs

Configuration Files for the Replicator 1, 2, and 2X can all be found in the [Configs Folder](https://github.com/Sgail7/Replicator-Revival-Project/tree/main/Klipper/Configs)

These configs are based on the example configs provided in Dockterj's Klipper Fork and the official config example repository. I have tuned my configs over many more hours than I care to admit. Mostly, these tunings include macros to add functionality and ease of use to your Replicator and provide all of the sections that I have found necessary to get the most out of these printers. Please choose the correct configuration for your printer, and also choose the correct Slicer Profile to accompany it.

# Nozzle Alignment

**This section is only relevant for the Replicator 1 Dual and Replicator 2X!**

**Note: To run this gcode, you will need to be using the Center Origin Configuration file for your printer! Once you have obtained your nozzle offset, you may switch back to the Front Left Corner Origin Configuration file and transfer the values that you found to that configuration file.**

This fine piece of gcode was adapted from the [nozzle alignment script](https://github.com/makerbot/ReplicatorG/blob/master/machines/replicator2/onboard/nozzleCalibration.gcode) found in the ReplicatorG source code. It preforms the exact same alignment process as the original Makerbot firmware did and is by far the easiest way to calibrate the x and y nozzle offset of these printers.

In an ideal world, this tuning would be unnecessary. Unfortunately, no machining process is perfect, and as a result the x and y positions of the left nozzle relative to the right nozzle on the Replicator 1 Dual and the Replicator 2X are usually slightly misaligned. To correct for this, this gcode instructs your printer to make a series of lines in the x and y directions on your printer, offsetting each by 0.10 mm. Once these lines have been printed, visual inspection is employed to determine which lines match up best to each other.

13 Lines are printed in the X and Y directions respectively. The offset of line #1 in the X direction is -0.60mm, relative to the right nozzle; The offset of line 13# is 0.60mm, again relative to the right nozzle. Likewise, the offset of line #1 in the Y direction is -0.60mm, and the offset of line #13 is 0.60mm. Line #7 for both directions has an offset of 0.00mm. To find the offset nozzle offset for your printer, you will inspect each of these lines, starting at line #1, until you find the set of lines that look to be in parallel. Note the line number that you stopped on, and then do this again for the other axis. Use these line numbers to find your offset.

As an example, assume that I found that Line #5 in the X direction, and Line #7 in the Y direction were my two best line pairs.

For the X-axis: Since the offset of line #1 is -0.60mm, I can find that line #5 is -0.20mm.

For the Y-axis: Since the offset of line #7 is 0.00mm, I can find that there is no appreciable offset in the Y direction between my two hotends.


# Printer Profile Information

**Please be sure to use the correct origin profile for your printer configuration. The Center Origin profiles will not work with a Left Front Origin configured printer and vice versa.**

Both PrusaSlicer and SuperSlicer profiles have been provided for these printers. I highly recommend using SuperSlicer, as it gives more control over the part cooling fan, which I have found to be very helpful for ensuring the quality of the top and bottom solid infill on parts printed at higher speeds. If you are using a PrusaSlicer version older than 2.6, I suggest commenting the M204 macro out of your printer profile. Since PrusaSlicer did not have a Klipper gcode flavor until version 2.6, certain acceleration commands would cause errors in the M204 macro that I have used, causing prints to fail. Luckily, this usually happens at the very beginning of a print, not wasting much filament or time, however, it is still annoying, so please be weary of this quirk.

# Nevermore Filter


# Macros


# Bltouch

