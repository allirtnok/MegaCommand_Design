# MegaCommand

## Description:

The MegaCommand is an Arduino Mega MIDI shield that is backwards compatible with the R&W MiniCommand hardware and MIDICtrl framework. The PCB is a through-hole design (no SMD soldering skills required). 

* 4 x MIDI ports (2 in, 2 out)
* 4 x Rotary Encoders + Push button
* 4 x Buttons
* 1 x LCD display (Choose between OLED or LCD)
* 128KBytes of SRAM (0-63KB accessible natively, 64-128KB accessible with bank selection)
  RAM Distribution: 

Stack is 8KB in size. 

56KB of RAM reserved for global objects, variables. (bank switchable)

* 1 x Dual Channel 12bit DAC (1.0.1a only)
* 2 x 10pin Expansion ports (1.0.2 only)

The MIDICtrl20 framework respository contains the software component of this project.
https://github.com/jmamma/MIDICtrl20_MegaCommand

## Project Status:

Updete: New board has been designed and tested. 

1_0_2a12

Changes include:

- 2 x 10pin expansion ports.
- Removal of HD44780 support.
- Removal of 12bit DAC.
- Throuh hole Yamaichi SD_Card slot now supported. SD-Card breakout no longer required.
- All mounting holes for MIDI DIN ports now available
- DC power jack polarity was reversed.

__ALL INFORMATION BELOW IS PROVIDED AS A CONVENIENCE AND COULD BE SUBJECT TO ERROR OR CHANGE.

## Parts:

[Bill of Materials]

1.0.2a:
https://github.com/jmamma/MegaCommand_Design/blob/master/1_0_2/BOM_1_0_2a11

1.0.1a:
https://docs.google.com/spreadsheets/d/1SPOctEUJUs_R-fi7xMjIrdiOk7FmjT5jRd9NrTtHMDI/edit?usp=sharing 

## Display

The 1.0.1a MegaCommand board has support for 2 display types (HD44780 + OLED).
The 1.0.2a MegaCommand board only support the OLED display

1) HD44870 LCD is the original LCD used in the MiniCommand and compatible with the LCD libraries.
2) OLED 128x32 display is a new display of similar size but with the ability to display 4 lines of text and custom graphics, it uses the SPI bus. (OLED display requires resistor position changes to enable SPI mode as per adafruit documentation https://learn.adafruit.com/2-3-monochrome-128x32-oled-display-module/assembly-1):

## Build 

```
VERIFY CHIP ORIENTATION BEFORE SOLDERING.

OLED/HD44780 display must be installed last.

Take care in making sure the ICs are inserted the correct way around.

You do not want to have to try and desolder 32 pins.

## Build Order: 

  1. ICS: RAM, Octal Latch, Shift Registers
  2. Arduino male headers. 
  3. Capacitors. (Make sure the 220uF electrolytic cap fits when the arduino is connected)

TEST POINT: Run the SRAM firmware test.

  4. MEC switches (Make sure these sit completely flush with the board and are not leaning to one side)
  5. LCD Trimmer (1_0_1 board only only)
  6. Resistor arrays
  7. Encoders (Make sure these sit completely flush with the board and are not leaning to one side)  
  
TEST POINT: Run the button and encoder test firmware.
  8. ICS: MIDI Optocouplers, HEX buffer, DAC (1_0_1 board only) 
  9. Resistors + diodes
10. MIDI DIN ports. (1_0_1 board requires removal of the 2 front pins by pulling the entire piece of aluminum from the connector)
 
TEST POINT: Run the MIDIPort test firmware.

 11. Power Jack (+9V tip)
 12. SDCard headers (the female header is placed on the bottom side of the board, and the pins are soldered from the top side. Solder male headers to the sd-card breakout board)
     (1_0_2 board can use the Yamaichi SD card holder and the above header is not required.)
     
TEST POINT: Run the SDCARD test firmware
 
 HD44780:
 13. Display header HD44780 (soldered from the top side of the board, the bottom side is intentionally obstructed by MIDI ports). There are 2 display header locations, one for each display type, choose the correct one.
 14. Display HD44780 (Soldered to the display header once the header is installed, max height of display should be 1.5-2mm above mec switches (without switch cap).
 
 OLED:
 13. Oled display requires correct resistor poisiton in order to be configured for SPI mode. (See documentation above to confirm the resistor placement)
 14. Male header to be soldered to OLED board. Header is then soldered on to MegaCommand PCB. The height of the OLED display is important. The distance between the mainboard pcb, and the bottom on the OLED pcb should be 5mm when soldered.
 
 15. LEDs (+ anode pin nearest to the bottom of the board for both LEDs. ). When soldered, the tip of the LED should measure 11mm above mainboard pcb.
 
 16. Power switch. (optional, you can solder a short between the two right most pins on EG1212B  
 
 Expansion Headers (1_0_2 board only):
 
 17. These are short 5mm headers. It might not be possible to buy them at the right length so you'll need to cut them down to 10 pin.
 
TEST POINT: Run the LCD and LED test firmware.

## Important

Display must be installed last.

The MIDI DIN ports get soldered on before the display

For the 1_0_1 board: the DIN ports require that the 2 front legs are removed from each DIN connector (don't just cut the legs, pull the entire piece of aluminium out with a pair of pliers, this will prevent shorts with the display header). Once the MiDI DIN ports are in. The header for the HD44780 display is soldered from the display side of the board; the reverse side in which you would normally solder from is intentionally obstructed by the MIDI ports.
This is not ideal, but was necessary due to the space limitations of the board.

5) To install the male headers that connect to the MC to the ArduinoMega, insert the headers in to the ArduinoMega then solder with the arduino attached to the headers. This will ensure perfect alignment.
```

## Enclosure:


1.0.2a:

New stl files added (Thanks to Ozone)

1.0.1a:

The enclosure is based on a standard 1590BB guitar pedal enclousre.

STL files for both the enclosure body and lid are provided in this git repository. The files can be 3D printed or you can investigate having an aluminium enclosure CNC milled.

## PCB Fabrication:
[PCBWay.com fabrication options](https://github.com/jmamma/MegaCommand_Design/blob/master/pcb_fabrication_preferences.jpg)

Gerber files (pcb layout diagrams used for fabrication) are included in the ./gerber/ directory above.

Download gerbers and submit to PCB manufacturer.

Circuit Schematic and Board Layout is present in Eagle files.

## About:

The MegaCommand shield was designed to be backwards compatible with the original MiniCommand hardware. 

However, there are notable differences between the two systems, including new pin assignments which must be taken account for when using the original MidiCtrl libraries.

The original MiniCommand used the ATMega64 microprocessor whilst the MegaCommand Shield is built on top of ArduinoMega which uses the ATMega2560 processor. The ATMega2560 shares most of the IO functionality of the ATMega64 but has additional pins, and a differernt pin-to-port layout.

The MegaCommand Shield accesses the ATMega2560 processor on board the ArduinoMega through the exposed headers, not all pins on the ATMega2560 are exposed through this Arduino interface.

Incorporating the differences between both processors and subsequent pin availability the following pin assignment has been made as the best possible substitutes for the original hardware layout.

## Arduino IDE, Cores & MIDICtrl library

Once you've built a MegaCommand you can write sketches within the Arduino IDE to test the hardware and run custom firmwware.
Before you start coding you need to decide which core you are going to use.

## Arduino Cores
In ArduinoLand, a Core is a collection of initialisation functions and associated libraries, used for configuring the underlying hardware; it is analogous to an Operating System kernel.

There are two cores to keep in mind:

Arduino Core:

This is the standard core, that comes installed default with the Arduino IDE. If you use this core with the MegaCommand you can program the MegaCommand like an ordinary arduino shield. The built in arduino functions can be used to control the hardware using the pin assignement detailed below.

MegaCommand Core:

This is based on Wesen's core for the MiniCommand and allows the MIDICtrl framework to run on the ArduinoMega.
By using this core you can take advantage of the powerful MIDI libraries and GUI functionality.

For example, the MegaCommand core is necessary for running the MCL firmware and controlling the Elektron instrument range.


### Installing the MIDICtrl core.
(Instructions for OSX, should be similar for Windows)

1) Download the Arduino IDE https://www.arduino.cc/en/Main/Software (1.8.5 tested)

2) Get the MIDICtrl library and MegaCommand Core (same repo):
```
   cd /Applications/Arduino.app/Contents/Java/hardware/
   git clone https://github.com/jmamma/MIDICtrl20_MegaCommand
```
### Selecting the Core

1) Open the Arduino IDE, Under the Tools menu, select the core you wish to use from the "Board:" menu

The default Arduino core is named "Arduion/Genuino Mega or Mega 2560"

The MegaCommand core will be listed at the bottom. 

## MegaCommand vs MiniCommand
```
4 Midi Ports vs 3
256k ROM vs 64K
USB vs No USB

--

MegaCommand pin changes from original MiniCommand are as followed:

MicroSD board:

CS = PB0

SRAM

BankSel = PL6

Key Scanning (Shift Registor Circuit):

PL0 = OUT
PL1 = SHIFT
PL2 = CLK

HD44780 LCD Circuit:

E = PL4
R/S = PL3

LEDs:

PE5 = LED0
PE4 = LED1

MIDI:

TXD0 and RXD0 (USART0) are reserved for Arduino USB interface.

Therefore we shift midi ports by 1.

MIDI Port 1:

RXD1 = MIDI Port 1 IN.
TXD1 = MIDI Port 1 OUT

Midi Port 2:

RXD2 = MIDI Port 2 IN
TXD2 = MIDI Port 2 OUT ( New port, not available on original Minicommand)
```




