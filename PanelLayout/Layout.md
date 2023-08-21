## Panel Layout for PCB

The panel dimensions provided in the section "Original Design" below are based on my own module build, since I am not following the standard HP (1HP eq. 5.08mm) size. An alternative by building an HP-standard size panel can be found in the section "HP Standard Design" further below.

### Original Design
Coordinates given in the table fit to the layout of components given in the PCBc in folder GerberFiles.
The layout is the same for both versions.

Panel size: 52mm x 128.5mm

The numbers in the table are refering to the numbers in the picture below.
Coordinates origin is the lower left corner of the panel.


| No. | X-coord. [mm] | Y-coord. [mm] | Comment |
| --- | --- | --- | --- |
| 1A | 4 | 108.7 | Corner coordinates |
| 1B | 28 | 108.7 | Corner coordinates |
| 1C | 4 | 93.5 | Corner coordinates |
| 1D | 28 | 93.5 | Corner coordinates |
| 2 | 12 | 101 | Encoder |
| 3 | 10 | 80 | Tactile Switch |
| 4 | 26 | 80 | Tactile Switch |
| 5 | 42 | 80 | Tactile Switch |
| 6 | 9 | 67 | LED |
| 7 | 20.5 | 67 | LED |
| 8 | 31.5 | 67 | LED |
| 9 | 43 | 67 | LED |
| 10 | 9 | 57 | Jack |
| 11 | 20.5 | 57 | Jack |
| 12 | 31.5 | 57 | Jack |
| 13 | 43 | 57 | Jack |
| 14 | 9 | 42 | Jack |
| 15 | 20.5 | 42 | Jack |
| 16 | 31.5 | 42 | Jack |
| 17 | 43 | 42 | Jack |
| 18 | 6 | 30 | Mounting hole for Din Socket |
| 19 | 14 | 22 | Din 5 Socket 57GB5FX |
| 20 | 22 | 14 | Mounting hole for Din Socket |
| 21 | 30 | 14 | Mounting hole for Din Socket |
| 22 | 38 | 22 | Din 5 Socket 57GB5FX |
| 23 | 46 | 30 | Mounting hole for Din Socket |

![Panel](https://user-images.githubusercontent.com/97026614/223692954-4e899adf-e36d-4aba-8087-6218ee39ac6d.png)

### HP Standard Design
For building the panel with a size following the HP standard, you can use the panel Gerber file provided in the folder "GerberFiles".
I ordered my own panel via such gerber file built out of PCB material.

On my own panel, the module name is "ITO". When using the panel Gerber file, the name will be "YARNS".

Here are a few parameters of the panel.
| Parameter | Value |
| --- | --- |
| Width | 10HP |
| Encoder hole diameter | 9mm |
| Jack hole diameter | 6.1mm |
| Tact switch hole diameter | 5.1 mm |
| LED hole diameter | 3.1mm|
| MIDI connector hole diameter | 15.5mm |
| MIDI connector mounting hole diameter | 3mm |
| Module mounting hole diameter | 3.2mm|
