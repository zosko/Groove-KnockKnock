# Groove Knock-Knock Sensor for SeeedStudio

## Previews

KiCad View|Seeed PCB
------|------
![](images/3dview.png)|![](images/pcb.png)

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


