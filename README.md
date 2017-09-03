# README!

#### Build and Deploy, Wuthering Bytes, 2017

This repository contains example Arduino code for the [Microchip ExLoRer board by SODAQ](http://support.sodaq.com/sodaq-one/explorer/).

## Directories

### Arduino 

In the `Arduino` directory are a number of examples for reading data from on-board sensors, sending it to Cayenne through TTN, and getting LoRaWAN radio information using [The Things Network library](https://github.com/TheThingsNetwork/arduino-device-lib).

### SODAQ Arduino

In the `SODAQ Arduino` directory are two Arduino reference examples from SODAQ, `microchip-lorabee` providing a basic LoRaWAN implementation, and `microchip-serial-passthrough` proving a useful debugging tool to interactively talk to the onboard RN2483 radio chip using the serial console of the Arduino IDE.

### Reference

In the `Reference` directory are documents detailing the implementation of the SODAQ design as well as notes about the Cayenne LPP protocol and library, including its usage and capabilities.

### ExpLoRer→TTN→Cayenne

In the `ExpLoRer→TTN→Cayenne` directory are two Arduino sketches, the first for reading on-board temperature and sending it to TTN, and the second encoding this data as a Cayenne LPP payload. Both these examples use the SODAQ reference code as a base.

### assets

The `assets` directory contains screen captures for the documentation only.

## Documents

There are two supporting documents for the workshop.

[SODAQ ExLoRer Board Notes for deployment.md] runs through how to install the nescessary libraries and board definitions to make the ExpLoRer work correctly with the Arduino IDE, and how to install Node-Red (optionally).

[Setting up integrations with TheThingsNetwork and Cayenne.md] explains the steps needed to set up an account on TheThingsNetwork, create an applicaiton, and associate devices with it.
Additionally, it explains how to integrate this application with Cayenne and configure a device on the Cayenne platform.
