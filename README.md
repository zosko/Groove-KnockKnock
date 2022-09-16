# Groove Knock-Knock Sensor for SeeedStudio

## Introduction

A Groove KnockKnock Sensor is a simple device that detects vibrations or shocks from knocking or tapping it. It is basically an electronic switch which normally open. When it detects any shock or vibrations, it closes.

## Components

A typical knock sensor consists of the main sensing element, which is a conductive vibrating spring, a Resistor and three Pins.
The three pins of the Knock Sensor Module are GND, +5V and Sig. The following image shows the components of a Knock Sensor Module as well as the pins on it.

![Interfacing-Knock-Sensor-with-Arduino-Knock-Sensor-Internal-Circuit](https://user-images.githubusercontent.com/3172271/190580857-06c8d065-1ab2-42f1-95cf-2c239dddc35c.jpg)

## How does a Knock Sensor Work?

If you take a look at the schematic of the knock sensor, it basically consists of a switch and a resistor. The Vibrating Spring is represented as a switch here.
The output pins of the sensor is pulled HIGH with the help of a 10KΩ Pull-up resistor.
Under normal condition i.e. when there is no shock or vibrations, the output of the Knock Sensor is HIGH.
When the sensor detects any vibrations or shocks, the vibrating spring i.e. switch closes and hence the output of the sensor (at the output pin) will become LOW.

## Interfacing Knock Sensor

Now that we have seen the components of a knock sensor and how a typical knock sensor works, let us proceed with interfacing.
I have designed a simple circuit using Arduino, Knock Sensor and an LED where the LED is turned on by Arduino when the knock sensor detects any vibrations.

Also the information of the knock sensor (knock or no knock) is displayed on the Arduino IDE’s serial monitor.

## Code

````c
const int knockPin = 8;

int knockVal = HIGH;
boolean knockAlarm = false;
unsigned long prevKnockTime;
int knockAlarmTime = 100;

void setup () {
  Serial.begin(9600);  
  pinMode(knockPin, INPUT) ;
}
void loop () {
  knockVal = digitalRead(knockPin);
  
  if (knockVal == LOW) {
    prevKnockTime = millis(); 
    if (!knockAlarm) {
      Serial.println("KNOCK, KNOCK");
      knockAlarm = true;
      delay(1000);
    }
  } else {
    if( (millis() - prevKnockTime) > knockAlarmTime && knockAlarm) {
      Serial.println("No Knocks");
      knockAlarm = false;
    }
  }
}
````

## Applications

The main purpose of the Knock Sensor is to detect vibrations or shocks. Hence, the main application of such sensor can be in Door Knock System, where when a door is knocked, a notifications (like a light or a buzzer) can be activated.

## Previews

KiCad View|Seeed PCB
------|------
![](images/3dview.png)|![](images/pcb.png)

## PCB Design

For PCB design i will use services from SeeedFusion. 

Seeed Fusion PCB Assembly Service offers one-stop prototyping for PCB manufacture, PCB assembly and as a result they produce superior quality PCBs and Fast Turnkey PCBA from 7 working days. When you prototype with Seeed Fusion, they can definitely provide Free DFA and Free functional tests for you! 

Check out their website to know about their manufacturing capabilities and service.
https://www.seeedstudio.com/pcb-assembly.html

## Reasons to choose Seeed Studio
- They provide PCB services at extremely low pricing and with excellent quality.
- Their offer is structured in such a way that everyone may have these boards at a reasonable price.
- They have a highly knowledgeable crew that leads their clients to avail deals and guides them about the costs and rates of different services.
- A four-layer board with a comparable feature costs $5 for 10 pieces and is made in four days.
- SMT stencil with size (10cm x 13cm) is available for $8.00 per piece.


