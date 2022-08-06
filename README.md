# Design and programming of an electronic circuit for an analog sensors


## Table of contents
* [Introduction](#Introduction)
* [Technologies](#technologies)
* [Components required](#Components-required)
* [Connections](#Connections)
* [Block diagram & simulation ](#Block-diagram-&-simulation)



## Introduction
This projects is to learn about several types of analog sensors and understand their scientific principle, 
operation and programming with Arduino ,We will cover several types : 👍 

 1. Light Dependent Resistor (LDR) or Photoresistor 
 2. Analog Sound Sensor
 
   ### Light Dependent Resistor (LDR) or Photoresistor 
   
   is a device whose resistivity is a function of the incident electromagnetic radiation. Hence, 
   they are lightsensitive devices. They are also called as photoconductors, photoconductive cells or simply photocells.
   They are made up of semiconductor materials that have high resistance , we will use it in a progect to turn on and off a LED  .
   
   ### Analog Sound Sensor
   
   
     Sound detection sensor works similarly to our Ears, having diaphragm which converts vibration into signals.
     However, what’s different as that a sound sensor ,consists of an in-built capacitive microphone, peak detector and         an amplifier
     (LM386, LM393, etc.) that’s highly sensitive to sound.

     With these components, it allows for the sensor to work:

     Sound waves propagate through air molecules
     Such sound waves cause the diaphragm in the microphone to vibrate, resulting in capacitance change
     Capacitance change is then amplified and digitalized for processing of sound intensity



## Technologies
Projects is created with:
* Arduino IDE 1.8.19 [To Downloud](https://www.arduino.cc/en/software)
* Proteus [To Downloud](https://www.labcenter.com/simulation/)
	
## Components required
### 1.LDR to turn on and off a LED

    1. Arduino UNO
    2. LED
    3. jumper wirs
    4. Resistor 220 , 10k ohm 
    5. USB-A to Micro-USB Cable
    6. breadboard
    
### 2. Bipolar Stepper with L293D Motor Driver IC
    1. Arduino UNO
    2. 1  NEMA 17 bipolar stepper
    3. jumper wirs
    4. L293D Motor Driver IC
    5. bettrey  5 and 12 volt 
    6. breadboard

    
## Connections

### 1. LDR to turn on and off a LED

       Connect the 3.3v output of the Arduino to the positive rail of the breadboard
   
       Connect the ground to the negative rail of the breadboard
   
       Connect the 220ohm resistor to the long leg (+ve) of the LED
   
       Then we will connect the other leg of the resistor to pin number 13 (digital pin) of the Arduino
   
       and the shorter leg of the LED to the negative rail of the breadboard
   
       Attach the 10K resistor to one of the legs of the LDR
   
       Connect the A0 pin of the Arduino to the same column where the LDR and resistor is connected 
   
       And the the second (free) leg of the LDR to the positive rail

     
 ### 2. Bipolar Stepper with L293D Motor Driver IC
 
    connecting 5V output on Arduino to the Vcc2 & Vcc1 pins
    
    Connect ground to ground.
    
    connect the input pins(IN1, IN2, IN3 and IN4) of the L293D IC to 
    
    four digital output pins(12, 11, 10 and 9) on Arduino
    0ne coil of stepper moter connecting to Out1 & Out2 and the anthor coil connecting to Out3 & Out4
    
 
     
## Block diagram & simulation
### 1. LDR to turn on and off a LED  . 

![Untitled Sketch 2_bb](https://user-images.githubusercontent.com/64277741/183266515-1bc7303f-be9b-4761-84a2-21ce0f3e08e8.png)

Figure (1): LDR to turn on and off a LED

 #### when we put a finger in LDR the LED will light up .
 

#### The Code 
const int ledPin = 13;

const int ldrPin = A0;

void setup() {

Serial.begin(9600);

pinMode(ledPin, OUTPUT);

pinMode(ldrPin, INPUT);

}

void loop() {

int ldrStatus = analogRead(ldrPin);

if (ldrStatus <= 200) {

digitalWrite(ledPin, HIGH);

Serial.print("Its DARK, Turn on the LED : ");

Serial.println(ldrStatus);

} else {

digitalWrite(ledPin, LOW);

Serial.print("Its BRIGHT, Turn off the LED : ");

Serial.println(ldrStatus);

}

}


### 2. Bipolar Stepper with L293D Motor Driver IC .[see here ](https://github.com/Wafaa-Almadhoun/Stepper-motor-using-Arduino-UNO-R3-/blob/main/Bipolar%20Stepper%20with%20L293D%20Motor%20Driver%20IC.pdsprj)
![1](https://user-images.githubusercontent.com/64277741/179328636-268173e6-09b8-46fb-9431-1dfe2eae640f.PNG)
Figure (7): step one revolution in the other direction ("counterclockwise")

 ![2](https://user-images.githubusercontent.com/64277741/179328701-3dee3532-ada8-4ae9-abdd-f15dcee8762f.PNG)
Figure (8): step one revolution in one direction ("clockwise")

#### The code 

// Include the Arduino Stepper Library
#include <Stepper.h>

// Number of steps per output rotation NEMA 17

const int stepsPerRevolution = 200; 

// Create Instance of Stepper library

Stepper myStepper(stepsPerRevolution, 12, 11, 10, 9);


void setup()
{
  // set the speed at 20 rpm:
  
  myStepper.setSpeed(20);
  
}

void loop() 
{
  // step one revolution in one direction:
  
  myStepper.step(stepsPerRevolution);
  
  delay(1000);

  // step one revolution in the other direction:
  
  myStepper.step(-stepsPerRevolution);
  
  delay(1000);
}


### 3. BIG Stepper Motors NEMA 23 Bipolar with DM860A Microstep Driver  
![3BIG Stepper Motors NEMA 23 Bipolar with DM860A Microstep Driver](https://user-images.githubusercontent.com/64277741/179338072-d89222ff-f4ea-4005-a69e-4427b546f48d.png)

#### The Code 
// Defin pins
 
int reverseSwitch = 2;  // Push button for reverse
int driverPUL = 7;    // PUL- pin
int driverDIR = 6;    // DIR- pin
int spd = A0;     // Potentiometer
 
// Variables
 
int pd = 500;       // Pulse Delay period
boolean setdir = LOW; // Set Direction
 
// Interrupt Handler
 
void revmotor (){
 
  setdir = !setdir;
  
}
 
 
void setup() {
 
  pinMode (driverPUL, OUTPUT);
  pinMode (driverDIR, OUTPUT);
  attachInterrupt(digitalPinToInterrupt(reverseSwitch), revmotor, FALLING);
  
}
 
void loop() {
  
    pd = map((analogRead(spd)),0,1023,2000,50);
    digitalWrite(driverDIR,setdir);
    digitalWrite(driverPUL,HIGH);
    delayMicroseconds(pd);
    digitalWrite(driverPUL,LOW);
    delayMicroseconds(pd);
 
}




