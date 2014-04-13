

Some code that uses a 2D array to selectively turn on specific pixels.
'''
boolean view[7][7];

void setup() {
  for (int i = 0 ; i < 14 ; i++) {
     pinMode(i, OUTPUT); 
     digitalWrite(i, LOW);
  }
  for (int x = 0 ; x < 7 ; x++) {
     for (int y = 0 ; y < 7 ; y++) {
       view[x][y] = false;
     } 
  }
}

void on(int x, int y) {
  view[x][y] = true; 
}
void off(int x, int y) {
  view[x][y] = false; 
}

void allOn() {
  for (int x = 0 ; x < 7 ; x++) {
     for (int y = 0 ; y < 7 ; y++) {
       view[x][y] = true;
     } 
  }
}

void allOff() {
  for (int x = 0 ; x < 7 ; x++) {
     for (int y = 0 ; y < 7 ; y++) {
       view[x][y] = false;
     } 
  }
}

void output(int times) {
   output(20, times); 
}

void output(int ledDelay, int times) {
  for (int i = 0 ; i < times ; i++) {
    for (int x = 0 ; x < 7 ; x++) {
       for (int y = 0 ; y < 7 ; y++) {
         if(view[x][y]) {
           digitalWrite(y, LOW);
           digitalWrite(x + 7, HIGH);
           delayMicroseconds(ledDelay);
           digitalWrite(x + 7, LOW);
         } else {
           digitalWrite(y, HIGH);
           delayMicroseconds(ledDelay);
         }
      } 
    }
  }
}

void loop() {
  allOff();
  on(random(0, 7), random(0, 7));
  output(1000);
}
'''
