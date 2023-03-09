# Yarns - MIDI Interface for Eurorack
A clone of the Mutable Instruments Yarns module with the use of the STM32 Blue Pill.

<img height="500" src="https://user-images.githubusercontent.com/97026614/223657089-82efd055-cdff-4eb9-b70a-7c2a5eb571f1.jpeg"> <img height="500" src="https://user-images.githubusercontent.com/97026614/223657125-6b767e3e-1bdc-40aa-a2dd-f709823024fb.jpeg">

<img height="500" src="https://user-images.githubusercontent.com/97026614/223657164-ab034583-c9b3-4876-a634-69e908206191.jpeg"> <img height="500" src="https://user-images.githubusercontent.com/97026614/223657198-960ad1d0-c098-48db-9bb1-e8eee3b7d0b6.jpeg">

## Module Build and PCBs
If you want to build the module yourself, I uploaded firmware, schematic, BOM and Gerber files for the PCBs.

NOTE:
Firmware and schematic differ from the original design due to restrictions on the Blue Pill board.
More details are given below in section Firmware.

There are two different versions for the control board, an "original" and a "Thonk" version.
Reason is that for my own module I am using specific 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="CtrlBoard_Orig_Front" src="https://user-images.githubusercontent.com/97026614/223882409-a0e01bbb-1429-45ac-9db1-6acc8be54e8c.png">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created a control PBC version with footprints for those components.
Choose the one you need.

<img width="300" alt="CtrlBoard_Thonk_Front" src="https://user-images.githubusercontent.com/97026614/223657314-b8215264-4f26-43f3-bc7c-962a51cc4c66.png">

The layout of the main PCB is the same for both versions.

<img width="300" alt="MainBoard_Back" src="https://user-images.githubusercontent.com/97026614/223657241-768dcd3b-16e5-4eb8-83ff-713927b73ea8.png">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.
I cannot guarantee, if this set of zipped Gerber files works also for other providers, like e.g. PCBWay. I have not tried that. But I saw online, that others did it.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files.

## Additional Information about specific Components
Most of the components are through-hole, including the microchip part, thanks to the available Blue Pill board. However, there are a few components, which I did not find as THT version, or which I got used to due to frequent usage in other projects (like bypass caps for ICs and NPN transistors).
The SMD components are:
- DAC8564 (DAC, 16-TSSOP package, the most challenging component due to its size)
- LM1117-3.3 (voltage regulator, SOT223 package)
- MCP1703 (voltage regulator, SOT223 package)
- SN74AHCT1G125 (buffer, SOT235 package)
- MMBT3904 (SMD version of the 2N3904 transistor, SOT23 Package)
- 0.1uF bypass caps for ICs (1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider tht fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

The original version from Mutable Instruments is using the OPA4171 quad op amp for the 4 CV output channels. The component was not available at the time, when I built the module, I tried it with the TL074 quad op amp. The pinout is the same, so it can easily be replaced. However, it turned out that the module also works with the TL074.

The connection between the two DIN sockets (MIDI in and MIDI out) need to be done via cables or wire. I used some cut-off wires from the resistor legs, as shown in the photos.

<img src="https://user-images.githubusercontent.com/97026614/223745359-48be0a93-28bd-4e39-a4ab-bc4f0b771a85.jpeg" width="300px">  <img src="https://user-images.githubusercontent.com/97026614/223745402-1c278206-f033-4aa8-bd8c-6516cb1f8507.jpeg" width="300px">

The numbers of the pin labels on the control PCB refer to the pin numbers of the sockets. E.g. MIDI OUT5 needs to be connected to pin 5 of the MIDI output socket. The numbering of socket pins are given in the graph below.

<img src="https://user-images.githubusercontent.com/97026614/223753028-2cfd518f-4616-40f8-bb37-e06b050f2a99.png" width="300px">

## Firmware
I shared the .hex files for the STM32F103 chip (bootloader and main) in the folder Firmware.
Those files and the schematic differ from the originals from Mutable Instruments.
Reason is the use of the Blue Pill board, as the chip's pins C13, C14, and C15 are already occupied on the Blue Pill board.
But the original design from Mutable Instruments is using them for the encoder.

Therefore, I changed the coding in two source code files, so that instead pins A0, A1, and A2 are used, which are not in use in the original design.
In my version, the following original source code files have been adjusted:
- encoder.cc (in subfolder /drivers)
- encoder.h (in subfolder /drivers)

If you want to compile your own .hex files, you need to search the texts in the below table and replace them in the entire file, as stated.
| File name | Original | Replace with |
| --- | --- | --- |
| encoder.cc | Pin_13 | Pin_1 |
| encoder.cc | Pin_14 | Pin_2 |
| encoder.cc | Pin_15 | Pin_0 |
| encoder.cc | GPIOC | GPIOA |
| encoder.h | Pin_15 | Pin_0 |
| encoder.h | GPIOC | GPIOA |

If you want to see more about the chip programming process, you can check out my [YouTube video](https://youtu.be/TBMySGm7jKk) about my other MI clone build of the Braids module. The process described in there is also valid for the Yarns module.

## STM32F103 Version
CAUTION! There are three different versions of the Blue Pill board available.
The difference is the version of the ST32F103 microchip on the board.
The versions differ in the flash memory size:
- STM32F103C6: 32kB flash memory
- STM32F103C8: 64kB flash memory
- STM32F103CB: 128kB flash memory

The code size requires the 128kB version.
However, that version is currently (Feb2023) difficult to find, if available at all.

I gave it a try and bought the 64kB version.
Surprisingly, the programmer showed 128kB available flash memory, and the code could be loaded.
I tried it with several boards.
So it seems STM3F103C8 is ok for this module.
