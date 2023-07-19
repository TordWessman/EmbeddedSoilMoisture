
Simple library for a polarity shifting soil moisture sensor utilizing a CD405X (or equivalent) multiplexer and using 2 measuring rods per measuring area (i.e. a pot).

### Electrolysis

The sensor determines the soil moisture level by measuring the resistance between the measuring rods. This is prone to electrolysis, which potentially degrades the rods. By combining the use of graphite rods and by shifting polarity, this issue seems to be reduced.

### Example

The code below 


```

R2Moist* sensor;

uint8_t controlPorts[SENSOR_ROD_COUNT] = {0, 12}; // IO ports used for the polarity shift.
uint8_t multiplexerPorts[3] = {16, 5, 4}; // IO ports used for the 8-bit multiplexer.
uint8_t sensorPairs[4] = {6, 3, 2, 1}; // Multiplexer ports used by the multiplexer. These comes in pairs, so port {6, 3} corresponds to the first sensor rod pair and {2, 1} is used for the second rod pair. 

void setup() {

  Serial.begin(9600);
  sensor = new R2Moist(
    new R2Multiplexer(multiplexerPorts, 3),
    17,
    controlPorts, 
    sensorPairs,
    2);
  
}

void loop() {

  int read0 = sensor->read(0); // Read the first sensor rod pair.
  int read1 = sensor->read(1); // Read the second sensor rod pair.

  Serial.print("Measurement for sensor 0: "); Serial.print(read0);
  Serial.print("| Measurement for sensor 1: "); Serial.println(read1);

  delay(1000);

}
```
### TODO

Provide a diagram for the actual circuit and some description that actually makes sense.