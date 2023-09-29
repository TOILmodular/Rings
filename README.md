# Rings - Resonator Eurorack Module
A clone of the Mutable Instruments Rings module.

Check out [this YouTube video](https://youtu.be/Ztzl9nVm6xI) for a jam session demo of the module.

<img height="500" src="https://github.com/TOILmodular/Rings/assets/97026614/36dbae5c-1500-4edd-9f83-524d7e4a963c">
<img height="500" src="https://github.com/TOILmodular/Rings/assets/97026614/d5b82f52-5ba1-4d7b-b68c-416dfbceac1b">

<img height="500" src="https://github.com/TOILmodular/Rings/assets/97026614/ee58af83-ef26-4978-acad-feafa655d0a1"> <img height="500" src="https://github.com/TOILmodular/Rings/assets/97026614/af841008-7d60-4d70-b48e-1994269e847c">

## Module Build and PCBs
In the folder GerberFiles, I added two different versions for the control board, an "original" and a "Thonk" version.
Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Rings_CtrlPCB_Orig" src="https://github.com/TOILmodular/Rings/assets/97026614/a5c27f82-242c-4156-849e-1837e471bf96">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB version, called "Thonk", with footprints for those components.

<img width="300" alt="Rings_CtrlPCB_Thonk" src="https://github.com/TOILmodular/Rings/assets/97026614/f5a423b3-6077-45cc-ac7e-93030f5c5a2a">

There are also two different versions of the main PCB due to the fact that a different version of the audio codec chip WM8731 is used. One of them is using a QFN version of the IC, while the other ones package is SSOP. You will find more details about the reason for that in the section "Additional Information about specific Components" below.

NOTE: I did not test the correctness of the "WM8731SSOP28" version of the main PCB.

<img width="300" src="https://github.com/TOILmodular/Rings/assets/97026614/ece902e3-4a55-40cc-8f9c-20ea700ef991">

<img width="300" src="https://github.com/TOILmodular/Rings/assets/97026614/509bf489-021d-4d74-a3df-214cbb4248a1">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. The layout is the same for all PCB versions.

In addition, there is a Gerber file for the panel, following the HP standard. My own modules do not follow that width standard, as I am only using sliding nuts in my racks.

You can use the panel Gerber file to have the panel built out of PCB material.

## Additional Information about specific Components
There are several SMD components, which I listed below. Besides the STM32F405 microcontroller, the other main SMD part is the WM8731 audio codec chip from Cirrus Logic. The production of that chip is now discontinued. The the only ones I found offered by certified dealers have the package type QFN (quad flat no lead).

<img width="600" alt="WM8731 Close-Up" src="https://github.com/TOILmodular/Clouds/assets/97026614/1727ba69-bf46-4bc6-9adb-7a7ef0d35d4d">

Soldering such a part by hand might seem to be difficult. But I made the experience, that it is actually very easy to solder. You can check out [this YouTube video](https://youtu.be/pF8kdi-zm-c) about how I soldered that chip for my other DIY clone of Mutable Instruments Clouds.

As mentioned above, I created two PCB version for the main board, "WM8731QFN" and "WM8731SSOP28". The latter one contains the footprint of the WM8731 chip with the package 28-SSOP, which was also used in the original Mutable Instruments module, as far as I know. I did not find any official online dealer, who still has such chips in stock. However, they mught still be offered by non-certified dealers on platforms, like Ebay.

Here is a list of SMD parts in my design.
- STM32F405RGT6 (microcontroller, version 7 is also working fine)
- WM8731 (audio codec, 28-VQFN or 28-SSOP package)
- NJM4580 (dual op amp, 8-SOIC, TL072 also works fine)
- LM1117-3.3 (voltage regulator, SOT-223 package)
- LM4040B10 (voltage regulator, SOT-23-3 package)
- MMBT3904 (transistor, SOT-23-3 package)
- 0.1uF capacitors (1608 package)
- BLM18R (ferrite bead, 1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

## Schematics
Due to the fact that the pin layout of the two package versions for the WM8731 chip are different, I uploaded two versions of the module schmatic in the folder "Schematic". The file "Schematic_Rings.pdf" contains the layout for the QFN package version, while the file "Schematic_Rings_WM8731SSOP28.pdf" is the one with the SSOP package.

## Firmware
I shared the .hex files for the STM32F405 chip (bootloader and main) in the folder Firmware.

## Programming
The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="245" alt="ProgrammingConnectors1" src="https://github.com/TOILmodular/Rings/assets/97026614/c66c2573-c085-4518-a28f-8aa0f665fca7">
<img width="312" alt="ProgrammingConnectors2" src="https://github.com/TOILmodular/Rings/assets/97026614/0d6f9800-10da-4272-8e9e-248578f61d43">

## Calibration
The calibration procedure is the same, as the one for the original module from Mutable Instruments.

1. Disconnect all CV inputs.
2. Connect the note CV output of a well-calibrated keyboard interface or MIDI-CV converter to the V/OCT input.
3. Connect a patch cable to the Frequency CV input. Leave the other end of the cable unplugged (this prevents the internal connection to +/- 1 semitone to be activated).
4. Hold both the polyphony and resonator type buttons for two seconds to enter the calibration procedure. The first LED will blink.
5. Play a C2 note, or send a 1V voltage from your CV source.
6. Press the polyphony button. The second LED will blink.
7. Play a C4 note, or send a 3V voltage from your CV source.
8. Press the polyphony button.
