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
     However, what’s different as that a sound sensor ,consists of an in-built capacitive microphone, 
     peak detector and an amplifier (LM386, LM393, etc.) that’s highly sensitive to sound.

     With these components, it allows for the sensor to work:

     Sound waves propagate through air molecules
     Such sound waves cause the diaphragm in the microphone to vibrate, resulting in capacitance change
     Capacitance change is then amplified and digitalized for processing of sound intensity,
      we will use it in a progect to control LED using a Sound .



## Technologies
Projects is created with:
* Arduino IDE 1.8.19 [To Downloud](https://www.arduino.cc/en/software)
	
## Components required
### 1.LDR to turn on and off a LED

    1. Arduino UNO
    2. LED
    3. jumper wirs
    4. Resistor 220 , 10k ohm 
    5. USB-A to Micro-USB Cable
    6. breadboard
    
### 2. Controling LED using a Sound
    1. Arduino UNO
    2. analog sound sensor
    3. jumper wirs
    4. LED
    5. Resistor 220 ohm 
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

     
 ### 2.Controling LED using a Sound
 
     connecting sound Sensor pin VCC  to 5V in Ardunio
     connecting sound Sensor pin GND  to GND in Ardunio
     connecting sound Sensor pin OUT  to pin2 in Ardunio
     connecting LED cathode  to GND  in Ardunio
     connecting LED anode to 220 resistor  and 
     connecting the another leg  of resistor to pin in Ardunio


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


### 2.Controling LED using a Sound

![sound sensor_bb](https://user-images.githubusercontent.com/64277741/183268395-1a4ef86f-f8ae-477f-b71e-4951612f03c2.png)

Figure (7): Controling LED using a Sound

#### when we make a loud sound the LED will light up .

#### The code 
int soundSensor=2;
int LED=4;
boolean LEDStatus=false;

void setup() {
 pinMode(soundSensor,INPUT);
 pinMode(LED,OUTPUT);

}

void loop() {

  int SensorData=digitalRead(soundSensor); 
  if(SensorData==1){

    if(LEDStatus==false){
        LEDStatus=true;
        digitalWrite(LED,HIGH);
    }
    else{
        LEDStatus=false;
        digitalWrite(LED,LOW);
    }
  }
 } 



