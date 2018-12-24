---
title: Source Code
category: Start Line
order: 3
---

> The Github Repository for the start line can be found [here](https://github.com/ThwackTimingSystems/ThwackTimingGateStartLine)

As the start line is based around an Arduino Uno, its code is written in the Arduino programming language (an extension of C). A walk-through of the code can be found below 

##Initialization
```c
#include <Key.h>
#include <Keypad.h>

// constants won't change. They're used here to set pin numbers:
const int wandPin = 2;     // the number of the wand pin
const int ledPin =  13;      // the number of the LED pin
const int rttPin = 3;

// variables will change:
int wandState = 0;         // variable for reading the wand status
int currentRacerId = 1;
int delayTimerStart = 0;
String nextRacerId = "";
```
Before anything else, we include some libraries we'll use to accept input from the keypad later
Also, we initialize some constants, to keep track of which pins we have input devices plugged into, and some variables, to keep track of various things throughout the program

## Keypad Setup
```c
//-----------------
//set up keypad
//-----------------
const byte ROWS = 4; // Four rows
const byte COLS = 3; // Three columns
// Define the Keymap
char keys[ROWS][COLS] = {
  {'1','2','3'},
  {'4','5','6'},
  {'7','8','9'},
  {'#','0','*'}
};
// Connect keypad ROW0, ROW1, ROW2 and ROW3 to these Arduino pins.
byte rowPins[ROWS] = { 9, 8, 7, 6 };
// Connect keypad COL0, COL1 and COL2 to these Arduino pins.
byte colPins[COLS] = { 12, 11, 10 }; 
// Create the Keypad
Keypad kpd = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS );
```
This section initializes the keypad to accept input using the library imported above. For more explanation on this section, check out [this](https://playground.arduino.cc/code/keypad)

##Setup
```c
void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize the wand pin as an input:
  pinMode(wandPin, INPUT);
  pinMode(rttPin, INPUT);
  // initialize serial communication:
  Serial.begin(9600);
}
```
The setup Arduino function is run before the primary loop of the program begins. In our case, it sets each pin we are using to be an input or an output, and opens a serial communication channel over the Xbee with a baud rate of 9600.

##Accept Input From Keypad
```c
void loop() {
  //---------
  //accept ID input from keypad
  //press '*' or '#' to clear ID if you accidentally mistype
  //----------
  char key = kpd.getKey();
  if(key && key!='*' && key!='#'){  // Check for a valid key.
    nextRacerId = nextRacerId + key;
    if (nextRacerId.length()>3){
      nextRacerId = nextRacerId.substring(1, 4);
    }
  }
  if(key && key =='*' || key =='#'){
    nextRacerId = "";
  }
```
Here is the first section of the `loop()` function, which loops continuously while the Arduino is powered on. This first section is in charge of accepting input on the keypad. Before racers start, they input their unique racer id (from 0-256) so their time can be tracked back to them later. This code block keeps track of digits as a user enters them, throwing out the oldest if more than three digits are entered. If a mistake is made, '#' or '*' can be entered to clear the input buffer.

##Check If Wand Has Been Tripped
```c
  //If the limit switch is not tripped (LOW signal)
  //then the wand has been triggered and start signal should be sent
  if (digitalRead(wandPin); == LOW) {
    sendStartSignal(nextRacerId.toInt%256);
    nextRacerId = "";
  }
  else{
    digitalWrite(ledPin, LOW);
  }
```
This code snippet checks to see if a racer has tripped the wand, and sends the start signal to the finish line if so. Its important to remember that when the wand is closed the limit switch is tripped. So, rather than check for a `HIGH` signal, as you would with a button, we check for a `LOW` signal.

##Round Trip Time Test System
```c
  //send first rtt test packet
  if(digitalRead(rttPin) == HIGH){
    int header = 1; //00000001
    int checkSum = calculateCheckSum(header);
    Serial.write(header);
    Serial.write(checkSum);
    int delayTimerStart = millis();
  }

  //send rtt test result back to finish line
  if (Serial.available()>0){
    serialFlush();
    int header = 19; //00010011
    int delayTime = millis()-delayTimerStart;
    int checkSum = calculateCheckSum(header)+calculateCheckSum(delayTime);
    Serial.write(header);
    Serial.write(delayTime);
    Serial.write(checkSum);
    while(Serial.available()>0){
      Serial.read();
    }
  }
}
```
This code block implements the latency correction feature of the timing gate by conducting a test of the round-trip-time (rtt) of a packet. First, the start line sends a packet to the finish line and starts a timer. The finish line responds as quick as possible. When the start line receives this response, it stops the timer. Half this calculated time is the time it takes a packet to travel from the start line to the finish line. This time is reported back to the finish line, so it can add this time onto racer's times to account for packet transmission latency.

##Check Sum Calculation Function
```c
int calculateCheckSum(byte input){
  int tot = 0;
  for (int i = 0; i<8; i++){
    tot += input>>i & 1;
  }
  return tot;
}
```
Part of the custom communication protocol used by the Thwack Timing Gate is a check sum: a mathematical function that takes a variable length input and returns a fixed length output. This check sum is computed over a packet before its sent and then transmitted along with the packet. The receiver performs the same computation over the received packet. If this computation mirrors the checksum originally transmitted, the packet is valid and can be used. If the checksums aren't the same, the packet has been corrupted in transit and must be thrown out.

##Serial Flush Function
```c
void serialFlush(){
  while(Serial.available() > 0) {
    char t = Serial.read();
  }
}
```
A simple function to empty all data out of the Xbee's incoming buffer

##Send Start Signal Function
```c
void sendStartSignal(int Id){
  int header = 16; //00010000
    int checkSum = calculateCheckSum(header)+calculateCheckSum(Id);
    Serial.write(header);
    Serial.write(Id);
    Serial.write(checkSum);

    //Illuminate LED to show packet has been sent
    digitalWrite(ledPin, HIGH);
    //delay(1000);
}
```
This function is called when the wand is tripped, and sends the start signal to the finish line. This involves creating a header that specifies the packet is a start packet, calculating a checksum over this header and the racer ID, and then packaging up the header, the racer ID, and the checksum and transmitting it over the Xbee.

