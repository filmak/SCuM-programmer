# SCuM Programmer

Load this firmware onto an nRF52840-DK to turn it into a programmer for SCuM!

The Single Chip micro-Mote (SCuM) is a 2x3mm2 single-chip standard-compatible Smart Dust chip, see https://www.crystalfree.org/

## Use

### program the nRF52840-DK

_Note_: you only need to do this once.

- download `scum-programmer.hex` from the https://github.com/openwsn-berkeley/SCuM-programmer/releases/latest/
- plug in your nRF52840-DK into your computer, drive "JLINK" appears
- drag-and-drop `scum-programmer.hex` onto this drive
- when the LEDs of the board go round-and-round, you're set!

![](static/round_and_round.gif)

### interact with SCuM's serial port

* Connect SCuM's UART to the following pins on the nRF52840-DK


| DK      | SCuM                     | description                         |
| ------- | ------------------------ | ----------------------------------- |
| `VBAT`  | `VDDIO`                  | provides power to SCuM (1.8V)       |
| `VBAT`  | bootload src select      | configure SCuM to bootload over 3wb |
| `P0.28` | `3WB_CLK`                | 3-wire bus, clock signal            |
| `P0.29` | `3WB_DATA`               | 3-wire bus, data signal             |
| `P0.30` | `3WB_EN`                 | 3-wire bus, enable signal           |
| `P0.31` | `HRESET`                 | hardware reset                      |
| `P0.03` | `VDDD`                   | to perform a "tap" operation        |
| `P0.02` | UART TX (SCuM transmits) | SCuM UART TX passthrough
| `GND`   | `GND`                    | ground                              |


* open the serial port corresponding to your nRF52840-DK using a serial terminal (e.g. TeraTerm), using **19200 baud**.

### load code onto SCuM

scum_nrf_programmer.py
-Build project in Keil.
-Copy the path to .../objects/<Project Name>.bin
-Edit "scum_nrf_programmer.py"    # Path to SCuM binary
                                    binary_image="<path to>/objects/<Project Name>.bin"

                                  # Com port of nRF board 
                                    nRF_port="COM<X>"
- Example output of succsessful SCuM Flash
![](image.png)

### calibrate SCuM

_Coming soon!_

# Build

- install SEGGER Embedded Studio for ARM (Nordic Edition)
- open `scum-programmer/scum-programmer.emProject`
