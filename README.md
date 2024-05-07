1. Introduction
The first design of a Teensy-based TNC as a replacement for the SCS Tracker was conceived by Peter Mack and Hans-Peter Helfert, DL6MAA, of SCS. It was based on a stack of a Teensy 4.0 board on top of an audio shield, which was itself on top of a piece of generic PCB for holding some components like a PTT transistor and some LEDs. Soon however, the stack of three PCBs was found to be sub-optimal and the idea of designing a custom PCB came into existence. Peter designed a first version of such a custom PCB, but lacked the time to finish it.

2. The present design
The present design was made by Robert, DM4RW, starting from the initial design of Peter. It is made using KiCad, now in version 7 (note that earlier versions of KiCad cannot open files saved in KiCad 7 format). The idea of the design revolves around putting the SGTL5000 sound chip (the same as used on the audio shield) together will all other components required on a main PCB, no longer requiring the use of an audio shield. Also the Teensy 4.0 micro-controller board finds a place on the main PCB, slightly elevated so as to allow space for components directly under the Teensy.

3. The PCB
The PCB provides space for the SGTL5000 sound chip plus its supporting components, a GPS/GNSS module, connectors such as SMA for an antenna for GPS/GNSS and mini-DIN-6 for connecting a transceiver, signaling LEDs, a 3,5mm RST socket for auxiliary use and a push button to initiate firmware updates. In addition, the design provides for its own power supply allowing power to be provided via pin 5 of the mini-DIN-6 socket as well as PTT via separate PTT line and via the audio-out line (the latter can be activated with a jumper).

4. Specifics of the design
The GNSS module used so far is a Quectel LC76. This is not obligatory, any GPS/GNSS module having the same pin-out and having the same physical size can be used, as long as its (serial) interface to the Teensy runs with 9k6 bps. A simple power back-up arrangement was made, using an over-sized capacitor. This will not allow the GNSS module to continue to run for a long time, but it at least bridges shorter interruptions of the power supply. The LC76 automatically recognizes whether the antenna needs power or not, and deactivates power if there is something wrong the antenna line or the antenna. The Teensy uses an unshielded processor. The external antenna is therefore a requirement and should be put away from the PCB as far as possible, preferably with a free sight to the skies.

The SGTL5000 sound chip finds its place beneath the Teensy. It is the 20 (21) pin version, as opposed to the 32 pin version used on the audio shield. However, the 32 pin version has been discontinued, the 20 pin version not. Note that the chip is very small: it measures 4×4mm with 5 pins on each side, plus a 21st pin on the bottom. There is no means of soldering this by hand, a decent re-flow installation is the least you need to put it into place.

The 3,5mm RST socket is meant to support auxiliary services. As to the date of writing, no firmware supporting such services in a flawless manner has been issued. The RST socket may therefore be omitted, it does not change the behavior of the TNC in any way.

The on-board power supply accepts input voltages between 8 and 28 volts on pin 5 of the mini-DIN-6 socket, and reduces this to 5 volts for the Teensy. It is based on a step-down converter by TI, the TPS54202(H). It is important to note that this converter comes in two flavors, with the H at the end and without. The only difference is the “enable voltage”. The one needs a high voltage, the other a low. For the H version, resistor R13 must be omitted, otherwise the converter won’t start. For the flavor without the H, resistor R13 has to be on the board. Simple measures were taken to prevent current flowing in an uncontrolled manner from computer to external power supply or vice versa in case the Teensy is connected to USB AND external power. However, for that to work, the Teensy must be slightly modified in that the trace connecting the power coming from the USB to the main 5v rail on the Teensy is interrupted (see the Teensy documentation that comes with every Teensy). It is then bridged by a diode that is on the PCB. If you do not need an external power supply, all components related to the power supply can be safely omitted. In that case, powering the TNC can only be done via USB connected to the Teensy.

5. About the files
You’ll find the KiCad files which you can open with the freely available KiCad. At least version 7 should be used, or higher. But not lower, that won’t work. You’ll find Gerber files with which the PCBs can be produced. Furthermore there is a BOM (bill of materials) and P&P (pick-and-placement) files. These were generated to have the board produced by JLCPCB and in addition to that, have all SMD components soldered on the board by JLCPCB. Only the GNSS module and wired components must then be soldered in order to get a fully charged RPR TNC. However, you can choose any other service provider that does the same, although in that case you’d be surely advised to regenerate all files according to the instructions of that service provider. Also with JLCPCB it pays off to check whether their requirements have changed and if so, regenerate all files.

Robert, DM4RW (Meersburg, 07/05/2024)