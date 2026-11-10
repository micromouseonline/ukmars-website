---
title: Arduino Sketch Sample code
date: '2024-07-26T18:11:59Z'
lastmod: '2024-07-26T19:05:26Z'
weight: 2
wp_id: 3203
---

## For an Arduino Sketch

Your Arduino program needs to have the following structure and sequence of parts:  
• A set of constant definitions that define the pins being used by the Nano as specified in the first part of the Pin Assignments page  
• A set of definitions to define each of the global variables used in the program  
• A void setup (){ ………..} section that specifies which pins are inputs and which are outputs using the pinMode statements, and a Serial.begin(9600); statement to define the speed of communication to the PC as specified in the second section of the Pin Assignments page  
• A void loop () section that will call the procedures that make the robot do what we want it to do or to test various functions of the robot. This can ideally be controlled by the result of reading the 4 way switch or the function button being pressed.  
• A number of procedures each of which is defined by void procedurename (){……} that do a specific function

// After the void setup() section we can then have a void loop() section such as this which calls the linefollow() function:

void loop()  
{linefollow() }

// Then, here is a simple line following function – Note again that all the variables used will need to have been defined up front

void linefollow()  
{  
basespeed = 70; // 70 and 20 work  
adjustment = 20;  
rightspeed = basespeed;  
leftspeed = basespeed;  
digitalWrite(rmotorDIR, HIGH); // set right motor forward  
digitalWrite(lmotorDIR, HIGH); // set left motor forward  
analogWrite(rmotorPWM, rightspeed); // set right motor speed  
analogWrite(lmotorPWM, leftspeed); // set left motor speed  
while(true)  
{  
photoread();  
sensdiff = lfrontsens – rfrontsens;  
adjustment = sensdiff /5 ;  
if (rfrontsens \> lfrontsens) //  
{posn = 1;  
rightspeed = basespeed – adjustment; //  
leftspeed = basespeed + adjustment; //  
analogWrite(rmotorPWM, rightspeed); // set right motor speed  
analogWrite(lmotorPWM, leftspeed); // set left motor speed  
digitalWrite(sensorLED1, HIGH);  
digitalWrite(sensorLED2, LOW);  
}  
if (rfrontsens \< lfrontsens) //  
{posn = 2;  
rightspeed = basespeed – adjustment; //  
leftspeed = basespeed + adjustment; //  
analogWrite(rmotorPWM, rightspeed); // set right motor speed  
analogWrite(lmotorPWM, leftspeed); // set left motor speed  
digitalWrite(sensorLED1, LOW);  
digitalWrite(sensorLED2, HIGH);  
}  
if (rfrontsens == lfrontsens) //  
{posn = 3;  
rightspeed = basespeed ; //  
leftspeed = basespeed ; //  
analogWrite(rmotorPWM, rightspeed); // set right motor speed  
analogWrite(lmotorPWM, leftspeed); // set left motor speed  
digitalWrite(sensorLED1, HIGH);  
digitalWrite(sensorLED2, HIGH);  
}  
}  
}

// Photoread is a function used by linefollow that will read the 4 line following sensors. Note, you will have to also define the variables lfrontsens, rfrontsend, rsidesens and lsidesens as global variables at the start of the program using lines such as

int rfrontsens = 0; //Right front sensor value  
int lfrontsens = 0; //Left front sensor value  
int rsidesens = 0; //Right side sensor value  
int lsidesens = 0; //Left side sensor value

void photoread(){  
// read both line sensors then the two side sensors  
digitalWrite(trigger, HIGH);  
delayMicroseconds(150); // wait for LED to light up fully  
lfrontsens = analogRead(lfront);  
rfrontsens = analogRead(rfront);  
rsidesens = analogRead (rside); // read right side photo sensor input  
lsidesens = analogRead (lside); // read left side photo sensor input  
digitalWrite(trigger, LOW); }
