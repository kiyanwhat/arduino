<b>Analog Input</b>

A potentiometer is a simple knob that provides a variable resistance, which you can read into the Arduino board as an analog value. In this example, you'll connect a poterntiometer to one of the Arduino's analog inputs to control the rate at which the built-in LED on pin 13 blinks.

<b>Hardware Required</b>

Arduino Board
Potentiometer (or another variable resistor like a photosensitive resistor and 10K resistor)
built-in LED on pin 13

<b>Circuit</b>
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/graph-circuit3.png"></img>
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/PhotoCellA0.png"></img>
<br>
Connect three wires to the Arduino board. The first goes to ground from one of the outer pins of the potentiometer. The second goes from 5 volts to the other outer pin of the potentiometer. The third goes from analog input 0 to the middle pin of the potentiometer.
For this example, it is possible to use the Arduino board's built in LED attached to pin 13. To use an additional LED, attach its longer leg (the positive leg, or anode), to digital pin 13, and it's shorter leg (the negative leg, or cathode) to the ground (gnd) pin next to pin 13. Because of the low amount of current coming from digital pin 13, it is not necessary to use a current limiting resistor in this particular case.
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/AnalogReadSerial_sch.png"></img>
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/PhotoResistorA0_schem.png"></img>
<br>
<b>Code</b>

In the beginning of this program, the variable sensorPin is set to to analog pin 0, where your potentiometer is attached, and ledPin is set to digital pin 13. You'll also create another variable, sensorValue i to store the values read from your sensor.
The analogRead() command converts the input voltage range, 0 to 5 volts, to a digital value between 0 and 1023. This is done by a circuit inside the Arduino called an analog-to-digital converter or ADC.
By turning the shaft of the potentiometer, you change the amount of resistance on either side of the center pin (or wiper) of the potentiometer. This changes the relative resistances between the center pin and the two outside pins, giving you a different voltage at the analog input. When the shaft is turned all the way in one direction, there is no resistance between the center pin and the pin connected to ground. The voltage at the center pin then is 0 volts, and analogRead() returns 0. When the shaft is turned all the way in the other direction, there is no resistance between the center pin and the pin connected to +5 volts. The voltage at the center pin then is 5 volts, and analogRead() returns 1023. In between, analogRead() returns a number between 0 and 1023 that is proportional to the amount of voltage being applied to the pin.
That value, stored in sensorValue, is used to set a delay() for your blink cycle. The higher the value, the longer the cycle, the smaller the value, the shorter the cycle.
```c
/*
  Analog Input
 Demonstrates analog input by reading an analog sensor on analog pin 0 and
 turning on and off a light emitting diode(LED)  connected to digital pin 13. 
 The amount of time the LED will be on and off depends on
 the value obtained by analogRead(). 
 
 The circuit:
 * Potentiometer attached to analog input 0
 * center pin of the potentiometer to the analog pin
 * one side pin (either one) to ground
 * the other side pin to +5V
 * LED anode (long leg) attached to digital output 13
 * LED cathode (short leg) attached to ground
 
 * Note: because most Arduinos have a built-in LED attached 
 to pin 13 on the board, the LED is optional.
 
 
 Created by David Cuartielles
 modified 30 Aug 2011
 By Tom Igoe
 
 This example code is in the public domain.
 
 http://arduino.cc/en/Tutorial/AnalogInput
 
 */

int sensorPin = A0;    // select the input pin for the potentiometer
int ledPin = 13;      // select the pin for the LED
int sensorValue = 0;  // variable to store the value coming from the sensor

void setup() {
  // declare the ledPin as an OUTPUT:
  pinMode(ledPin, OUTPUT);  
}

void loop() {
  // read the value from the sensor:
  sensorValue = analogRead(sensorPin);    
  // turn the ledPin on
  digitalWrite(ledPin, HIGH);  
  // stop the program for <sensorValue> milliseconds:
  delay(sensorValue);          
  // turn the ledPin off:        
  digitalWrite(ledPin, LOW);   
  // stop the program for for <sensorValue> milliseconds:
  delay(sensorValue);                  
}
```
