# Using Cayenne LPP

Cayenne LPP is a simple, standards-based data structure designed to place multiple *sensor readings* into a binary-format sequence of identifiable *frames* (or *channels*) as a single payload. 

The Cayenne LPP protocol (based on the [IPSO] specification) follows a fairly simple approach: first, a variable is created to store and construct the  the payload object in, then sensor readings are attached to it. Finally, the payload can be read from it before re-initialising or re-using it.

## Declare the Cayenne LPP object in Arduino sketch

First, we must declare the object in our sketch:

```
	CayenneLPP lpp(51); 
```
 

51? What's the 51?
* Maximum payload size of the `lpp` object
* Transmitted data likely to be smaller than this
* Only need to reduce this size if your sketch is tight!

## Initialise and reset the Cayenne LPP object for data

```
	lpp.reset()
```
 
This resets the internal cursor and data tracking of the LPP object, allowing new data to be attached.

## Add data to the Cayenne LPP object

There are a number of methods defined allowing different data types to be attached to the `lpp` object.

In the following definitions, `channel` refers to which indexed position in the payload the sensor reading is placed at; different types of sensor data use different amounts of storage, so it's best to allow the Cayenne LPP class manage the tracking and positioning of data.

Starting at `channel` position `1`, sensor readings (including arbitrary analogue and digital readings) can be attached to the `lpp` object. 

For example, to add a digital (boolean) value to channel 1, an analogue value to channel 2, and a set of GPS coordinates to channel 3, the following could be used (obviously, changing the hardcoded values to either function return values or pre-calculated variables):

``` 
	lpp.addDigitalInput(1, 0);
	lpp.addAnalogInput(2, 0.5);
	lpp.addGPS(53.784, -2.051, 108.0);
```
 
 
### Available datatypes for Cayenne LPP

The following is a list of methods for storing specific data types built in to the Cayenne LPP class. If your sensor isn't listed, you may wish to use one or more addAnalogInput channels to store the values for parsing later.

```
	uint8_t addDigitalInput(uint8_t channel, uint8_t value);
	uint8_t addDigitalOutput(uint8_t channel, uint8_t value);
	
	uint8_t addAnalogInput(uint8_t channel, float value);
	uint8_t addAnalogOutput(uint8_t channel, float value);
	
	uint8_t addLuminosity(uint8_t channel, uint16_t lux);
	uint8_t addPresence(uint8_t channel, uint8_t value);
	uint8_t addTemperature(uint8_t channel, float celsius);
	uint8_t addRelativeHumidity(uint8_t channel, float rh);
	uint8_t addAccelerometer(uint8_t channel, float x, float y, float z);
	uint8_t addBarometricPressure(uint8_t channel, float hpa);
	uint8_t addGyrometer(uint8_t channel, float x, float y, float z);
	uint8_t addGPS(uint8_t channel, float latitude, float longitude, float meters);
```
 
### Limitations of the Cayenne LPP storage objects

This isn't a perfect solution, though - there are some compromises baked-in to make the storage requirements low.

* Sensor readings are rounded to specific degrees of precision (*resolution*)
* Not every type of sensor is supported
* There are defined ranges of tolerance set in the specification, regardless of the capabilities of the hardware in use


| Sensor Type        | ID | Data Size (bytes) | Resolution | Signed? | Notes                   |
|--------------------|----|-------------------|------------|---------|-------------------------|
| Digital Input      | 0  | 1                 | boolean    |         |                         |
| Digital Output     | 1  | 1                 | boolean    |         |                         |
| Analogue Input     | 2  | 2                 | 0.01       | ✓       |                         |
| Analogue Output    | 3  | 2                 | 0.01       | ✓       |                         |
| Illuminance Sensor | 65 | 2                 |            |         | Lux, MSB                |
| Presence Sensor    | 66 | 1                 |            |         |                         |
| Temperature Sensor | 67 | 2                 | 0.01 °C    | ✓       | MSB                     |
| Humidity Sensor    | 68 | 1                 | 0.5%       | ✕       |                         |
| Accelerometer      | 71 | 6                 | 0.001 G    | ✓       | per axis; MSB order     |
| Barometer          | 73 | 2                 | 0.01 hPa   | ✕       | MSB order               |
| Gyrometer          | 86 | 6                 | 0.01 °/s   | ✓       | per axis; MSB order     |
| GPS                | 88 | 9                 |            | ✓       | MSB order; lat/long/alt |

## Retrieve the Cayenne LPP payload from the lpp object for transmission

Finally, the payload can be extracted for sending through TheThingsNetwork or over a similar LoRaWAN (or other) standard.

```
	lpp.getBuffer()
	lpp.getSize()
``` 

Both these methods can be used with the [SODAQ LoRaBEE] class directly:

```
	LoRaBee.send(1, (uint8_t*)lpp.getBuffer(), lpp.getSize())
```

