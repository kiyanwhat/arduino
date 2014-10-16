<b>Bare Minimum code needed to get started</b>

This example contains the bare minimum of code you need for an Arduino sketch to compile: the setup() method and the loop() method.

<b>Hardware Required</b>

Arduino Board

<b>Circuit</b>

Only your Arduino Board is needed for this example.
<br>
<img src="http://arduino.cc/en/uploads/Tutorial/Arduino_bb.png"></img>
<br>
<b>Code</b>

The setup() function is called when a sketch starts. Use it to initialize variables, pin modes, start using libraries, etc. The setup function will only run once, after each powerup or reset of the Arduino board.
After creating a setup() function, the loop() function does precisely what its name suggests, and loops consecutively, allowing your program to change and respond as it runs. Code in the loop() section of your sketch is used to actively control the Arduino board.
The code below won't actually do anything, but it's structure is useful for copying and pasting to get you started on any sketch of your own. It also shows you how to make comments in your code.
Any line that starts with two slashes (//) will not be read by the compiler, so you can write anything you want after it. Commenting your code like this can be particularly helpful in explaining, both to yourself and others, how your program functions step by step.
```c
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly: 
  
}
```
