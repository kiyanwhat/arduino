<b>Pitch follower using the tone() function</b>

This example shows how to use the tone() command to generate a pitch that follows the values of an analog input

<b>Hardware Required</b>

8-ohm speaker
1 photocell
4.7K ohm resistor
100 ohm resistor
breadboard
hook up wire

<b>Circuit</b>
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/arduino_speaker_photocell_bb.png"></img>
<br>
Connect one terminal of your speaker to digital pin 9 through a 100 ohm resistor, and its other terminal to ground. Power your photoresistor with 5V, and connect it to analog 0 with the addition of a 4.7K resistor to ground
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/arduino_speaker_photocell_schem.png"></img>
<br>
<b>Code</b>

The code for this example is very simple. Just take an analog input and map its values to a range of audible pitches. Humans can hear from 20 - 20,000Hz, but 120 - 1500 usually works pretty well for this sketch.
You'll need to get the actual range of your analog input for the mapping. In the circuit shown, the analog input value ranged from about 400 to about 1000. Change the values in the map() command to match the range for your sensor.
The sketch is as follows:
```c
/*
  Pitch follower
 
 Plays a pitch that changes based on a changing analog input
 
 circuit:
 * 8-ohm speaker on digital pin 9
 * photoresistor on analog 0 to 5V
 * 4.7K resistor on analog 0 to ground
 
 created 21 Jan 2010
 modified 31 May 2012
 by Tom Igoe, with suggestion from Michael Flynn

This example code is in the public domain.
 
 http://arduino.cc/en/Tutorial/Tone2
 
 */


void setup() {
  // initialize serial communications (for debugging only):
  Serial.begin(9600);
}

void loop() {
  // read the sensor:
  int sensorReading = analogRead(A0);
  // print the sensor reading so you know its range
  Serial.println(sensorReading);
  // map the analog input range (in this case, 400 - 1000 from the photoresistor)
  // to the output pitch range (120 - 1500Hz)
  // change the minimum and maximum input numbers below
  // depending on the range your sensor's giving:
  int thisPitch = map(sensorReading, 400, 1000, 120, 1500);

  // play the pitch:
  tone(9, thisPitch, 10);
  delay(1);        // delay in between reads for stability
}
```
