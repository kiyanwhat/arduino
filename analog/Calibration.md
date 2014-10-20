<b>Calibration</b>

This example demonstrates one techinque for calibrating sensor input. The Arduino takes sensor readings for five seconds during the startup, and tracks the highest and lowest values it gets. These sensor readings during the first five seconds of the sketch execution define the minimum and maximum of expected values for the readings taken during the loop.

<b>Hardware Required</b>

Arduino board
(1) LED
(1) analog sensor (a photocell will do)
(1) 10K ohm resistor
(1) 220 ohm resistor
breadboard
hook-up wire

<b>Circuit</b>

Analog sensor (e.g. potentiometer, light sensor) on analog input 2. LED on digital pin 9.
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/calibration.png"></img>
<br>
Connect an LED to digital pin 9 with a 220 ohm current limiting resistor. Connect a photocell to 5V and then to analog pin 0 with a 10K ohm resistor as a reference to ground.
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/calibration_sch.png"></img>
<br>
<b>Code</b>

Before the setup, you set initial values for the minimum and maximum like so:
```c
int sensorMin = 1023;        // minimum sensor value
int sensorMax = 0;           // maximum sensor value
```
These may seem backwards. Initially, you set the minimum high and read for anything lower than that, saving it as the new minimum. Likewise, you set the maximum low and read for anything higher as the new maximum, like so:
```c
// calibrate during the first five seconds 
 while (millis() < 5000) {
   sensorValue = analogRead(sensorPin);

   // record the maximum sensor value
   if (sensorValue > sensorMax) {
     sensorMax = sensorValue;
   }

   // record the minimum sensor value
   if (sensorValue < sensorMin) {
     sensorMin = sensorValue;
   }
 }
```
This way, any further readings you take can be mapped to the range between this minimum and maximum like so:
```c
// apply the calibration to the sensor reading
sensorValue = map(sensorValue, sensorMin, sensorMax, 0, 255);
```
Here's the whole program:
```c
/*
  Calibration
 
 Demonstrates one technique for calibrating sensor input.  The
 sensor readings during the first five seconds of the sketch
 execution define the minimum and maximum of expected values
 attached to the sensor pin.
 
 The sensor minimum and maximum initial values may seem backwards.
 Initially, you set the minimum high and listen for anything 
 lower, saving it as the new minimum. Likewise, you set the
 maximum low and listen for anything higher as the new maximum.
 
 The circuit:
 * Analog sensor (potentiometer will do) attached to analog input 0
 * LED attached from digital pin 9 to ground
 
 created 29 Oct 2008
 By David A Mellis
 modified 30 Aug 2011
 By Tom Igoe
 
 http://arduino.cc/en/Tutorial/Calibration
 
 This example code is in the public domain.
 
 */

// These constants won't change:
const int sensorPin = A0;    // pin that the sensor is attached to
const int ledPin = 9;        // pin that the LED is attached to

// variables:
int sensorValue = 0;         // the sensor value
int sensorMin = 1023;        // minimum sensor value
int sensorMax = 0;           // maximum sensor value


void setup() {
  // turn on LED to signal the start of the calibration period:
  pinMode(13, OUTPUT);
  digitalWrite(13, HIGH);

  // calibrate during the first five seconds 
  while (millis() < 5000) {
    sensorValue = analogRead(sensorPin);

    // record the maximum sensor value
    if (sensorValue > sensorMax) {
      sensorMax = sensorValue;
    }

    // record the minimum sensor value
    if (sensorValue < sensorMin) {
      sensorMin = sensorValue;
    }
  }

  // signal the end of the calibration period
  digitalWrite(13, LOW);
}

void loop() {
  // read the sensor:
  sensorValue = analogRead(sensorPin);

  // apply the calibration to the sensor reading
  sensorValue = map(sensorValue, sensorMin, sensorMax, 0, 255);

  // in case the sensor value is outside the range seen during calibration
  sensorValue = constrain(sensorValue, 0, 255);

  // fade the LED using the calibrated value:
  analogWrite(ledPin, sensorValue);
}
```
