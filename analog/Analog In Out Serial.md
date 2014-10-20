<b>Analog In, Out Serial</b>

This example shows how to read an analog input pin, map the result to a range from 0 to 255, and then use that result to set the pulsewidth modulation (PWM) of an output pin to dim or brighten an LED.

<b>Hardware Required</b>

Arduino Board
Potentiometer
LED
220 ohm resistor

<b>Circuit</b>
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/analoginoutserial1_bb.png"></img>
<br>
Connect one pin from your pot to 5V, the center pin to analog pin 0, and the remaining pin to ground. Next, connect a 220 ohm current limiting resistor to digital pin 9, with an LED in series. The long, positive leg (the anode) of the LED should be connected to the output from the resistor, with the shorter, negative leg (the cathode) connected to ground.
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/analoginoutserial_sch.png"></img>
<br>

<b>Code</b>

In the program below, after declaring two pin assignments (analog 0 for your potentiometer and digital 9 for your LED) and two variables, sensorValue and outputValue, the only thing that you do will in the setup function is to begin serial communication.
Next, in the main loop of the code, sensorValue is assigned to store the raw analog value coming in from the potentiometer. Because the Arduino has an analogRead resolution of 0-1023, and an analogWrite resolution of only 0-255, this raw data from the potentiometer needs to be scaled before using it to dim the LED.
In order to scale this value, use a function called map()
outputValue = map(sensorValue, 0, 1023, 0, 255);
[Get Code]
outputValue is assigned to equal the scaled value from the potentiometer. map() accepts five arguments: The value to be mapped, the low range and high range of the raw data, and the low and high values for that data to be scaled too. In this case, the sensor data is mapped down from its original range of 0 to 1023 to 0 to 255.
The newly mapped sensor data is then output to the analogOutPin dimming or brightening the LED as the potentiometer is turned. Finally, both the raw and scaled sensor values are sent to the Arduino serial window in a steady stream of data.
```c
/*
  Analog input, analog output, serial output
 
 Reads an analog input pin, maps the result to a range from 0 to 255
 and uses the result to set the pulsewidth modulation (PWM) of an output pin.
 Also prints the results to the serial monitor.
 
 The circuit:
 * potentiometer connected to analog pin 0.
   Center pin of the potentiometer goes to the analog pin.
   side pins of the potentiometer go to +5V and ground
 * LED connected from digital pin 9 to ground
 
 created 29 Dec. 2008
 modified 9 Apr 2012
 by Tom Igoe
 
 This example code is in the public domain.
 
 */

// These constants won't change.  They're used to give names
// to the pins used:
const int analogInPin = A0;  // Analog input pin that the potentiometer is attached to
const int analogOutPin = 9; // Analog output pin that the LED is attached to

int sensorValue = 0;        // value read from the pot
int outputValue = 0;        // value output to the PWM (analog out)

void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600); 
}

void loop() {
  // read the analog in value:
  sensorValue = analogRead(analogInPin);            
  // map it to the range of the analog out:
  outputValue = map(sensorValue, 0, 1023, 0, 255);  
  // change the analog out value:
  analogWrite(analogOutPin, outputValue);           

  // print the results to the serial monitor:
  Serial.print("sensor = " );                       
  Serial.print(sensorValue);      
  Serial.print("\t output = ");      
  Serial.println(outputValue);   

  // wait 2 milliseconds before the next loop
  // for the analog-to-digital converter to settle
  // after the last reading:
  delay(2);                     
}
```


