# Miscellaneous Component notes

## Keyes Infrared Temperature Sensor Module KY-140 MLX90614 Arduino Flux Workshop x 2

[example](http://forum.arduino.cc/index.php?topic=89926.0)

```
#include <i2cmaster.h>

void setup()
{
 Serial.begin(115200);
 Serial.println("Setup...");
 
 setupI2CBus();
}

void loop()
{
 float celcius1 = readDevice(A1);
 float celcius2 = readDevice(A2);
 float celsius3 = readDevice(A3);

 // Print Data To Screen...
 Serial.print("Temp sensor: A1: ");
 Serial.print(celcius1);
 Serial.print(" A2: ");
 Serial.println(celcius2);
 Serial.print(" A3:");
 Serial.println(celcius3);

 delay(3000); 
}

/////////////////////////////////////////////////////////
//
// helper functions
//
void setupI2CBus()
{
 i2c_init(); //Initialise the i2c bus
 PORTC = (1 << PORTC4) | (1 << PORTC5); //enable pullups
}

float readDevice(int address)
{
 int dev = address << 1;
 int data = 0;
 int pec = 0;

 // RAW READ
 i2c_start_wait(dev + I2C_WRITE);

 i2c_write(0x07);

 i2c_rep_start(dev + I2C_READ);

 data = i2c_readAck() * 256;
 data = data + i2c_readAck(); 

 pec = i2c_readNak();

 i2c_stop();
 
 // PROCESS DATA
 data = data & 0x7FFF;
 float temp = (data * 0.02) - 273.16;
  return temp;
}
```

## Keyes Vibration Sensor Module KY-075 801S 20cm Infrared Arduino Pi Flux Workshop x 3



## 	 RFID Set IC inductive module card key fob headers SPI Flux Workshop x 5 - there are no fobs with this item

[library download](https://github.com/miguelbalboa/rfid/)
[example via](https://github.com/miguelbalboa/rfid/blob/master/examples/DumpInfo/DumpInfo.ino)

```

#include <SPI.h>
#include <MFRC522.h>

constexpr uint8_t RST_PIN = 9;          // Configurable, see typical pin layout above
constexpr uint8_t SS_PIN = 10;         // Configurable, see typical pin layout above

MFRC522 mfrc522(SS_PIN, RST_PIN);  // Create MFRC522 instance

void setup() {
	Serial.begin(9600);		// Initialize serial communications with the PC
	while (!Serial);		// Do nothing if no serial port is opened (added for Arduinos based on ATMEGA32U4)
	SPI.begin();			// Init SPI bus
	mfrc522.PCD_Init();		// Init MFRC522
	mfrc522.PCD_DumpVersionToSerial();	// Show details of PCD - MFRC522 Card Reader details
	Serial.println(F("Scan PICC to see UID, SAK, type, and data blocks..."));
}

void loop() {
	// Look for new cards
	if ( ! mfrc522.PICC_IsNewCardPresent()) {
		return;
	}

	// Select one of the cards
	if ( ! mfrc522.PICC_ReadCardSerial()) {
		return;
	}

	// Dump debug info about the card; PICC_HaltA() is automatically called
	mfrc522.PICC_DumpToSerial(&(mfrc522.uid));
}
```

## Keyes Hall/Holzer Effect Sensor Module KY-024 49E 5118G Arduino Pi Flux Workshop x 5



## MQ-135 Pollution Sensor Genuine Keyes Module Arduino Raspberry Flux Workshop x 5

[arduino.cc hardware MQ sensor reference](http://playground.arduino.cc/Main/MQGasSensors)

[MQ-135 project documentation](https://hackaday.io/project/3475-sniffing-trinket/log/12363-mq135-arduino-library) (arduino library)[https://github.com/GeorgK/MQ135]

## Moisture Detection Sensor Module Soil Water Arduino Raspberry Pi Flux Workshop x 5

## Rain Water Detection Sensor Module Weather Arduino Raspberry TTL Flux Workshop x 3

This set is ideally suited to adding water detection to your project. This is a sensor module which can detect water droplets and relay a signal to a micro-controller or project. This allows you to build in water detection, for your weather, watering or aquatic based project.
The control board can output both digital and analog signals. The digital output will produce a HIGH signal until a water droplet is detected upon which it is driven LOW. This will also light the DO-LED on the control board. The analog output will change with the level of water detected upon the plate when read by an analogue pin.
Please do not hesitate to contact us if you require further information regarding the module's operation.

|Pin|	Description|
|---|--------------|
|-	|Detection plate|
|+	|Detection plate|
|A0	|Analog output|
|D0	|Digital output|
|GND|	Ground |
|VCC|	3 - 5V |


## Keyes Tilt Switch KY-040 Easy Ball 5V Arduino Raspberry Pi Flux Workshop x 2

## LC Technology LDR Sensor Module Light Dependant Resistor Photo Flux Workshop x 8

## BMP-280 BMP280 Precision Temperature/Barometric Pressure Sensor for Arduino-Pi x 10

[library download](https://github.com/mahfuz195/BMP280-Arduino-Library)
[example](https://github.com/mahfuz195/BMP280-Arduino-Library/blob/master/Examples/measurment/measurment.ino)

## DS18B20 Waterproof Temperature Sensor for Arduino, Pi - New & Tested, UK Seller x 5

Install Library in Arduino IDE - Use menu *Sketch*→*Include Library*→*Manage Libraries...* then search for *DS18B20 dallas*.
[library download](https://github.com/milesburton/Arduino-Temperature-Control-Library)
[example](https://github.com/milesburton/Arduino-Temperature-Control-Library/blob/master/examples/Single/Single.pde)

## 5A AC 125-250V Roller Lever Arm Terminal Microswitch Limit Open/Close KW12-3 x 10

