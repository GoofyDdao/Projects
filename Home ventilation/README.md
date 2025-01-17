# Home ventilation (automation). 
## How I use this project in my city apartment:
- I have a main exhaust ventilation and it is automatically controlled by smart home sensors (Sonoff D1).
- every 6 ... 9 months I need to clean (maintain) the main exhaust ventilation.
- and there is a backup exhaust ventilation which is operated manually.
- the main and backup exhaust ventilation must not interfere with each other (must not be able to work simultaneously).
- main and backup exhaust ventilation are located in different rooms (this is important).
- I had to do this automation.

## 1. RobotDyn AC Light Dimmer.  
 - this only works if your AC motor is dimmable.
 - it hums a lot when running (low frequency hum).
 - this is unacceptable (work stopped) - see note below.

![RobotDyn Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/PZEM-852.jpg)
![RobotDyn Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/20210331_202713.jpg)


## 2. Sonoff D1 Dimmer.  
 - this only works if your AC motor is dimmable.
 - it works very well (almost).
 
 ### Video of the driver's work:
 - https://youtu.be/S4nMcrPoYII
 
![Sonoff D1 Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/PZEM-862.jpg)
![Sonoff D1 Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/20210331_202908.jpg)

## More about using PZEM-004:
 - [Tasmota PZEM-004](https://tasmota.github.io/docs/PZEM-0XX/)
 - [about using PZEM-004](https://github.com/arendst/Tasmota/discussions/10567)

## How to use it:
1. Run commands in the console for ESP-01S (remove comments first):  
  `Rule1`  
  `ON Tele-ENERGY#Current>0.5 DO publish cmnd/Motor-1/Power1 0 ENDON`   // if motor#2 is ON, then turn OFF motor#1  
  `ON Tele-ENERGY#Current<0.5 DO Backlog publish cmnd/Motor-1/Power1 1; publish cmnd/Motor-1/Dimmer 25 ENDON`   // if motor # 2 is OFF, then turn on motor#1 and set motor#1 dimming to 25%  
  `Rule1 1`   // Enable Rule1  
    
    `Rule 5`   // Now the MQTT message will be sent once and only once as long as the condition (!!!) is met. It is ideal for turning on / off the on / off of the exhaust fan depending on external conditions.       
    https://tasmota.github.io/docs/Rules/#usage-of-one-shot-once
 

1. Run commands in the console for Sonoff D1 (remove comments first):  
  `Rule1`  
  `ON system#boot DO Backlog Power1 0; delay 10; Power1 1; Dimmer 25 ENDON`  //turn on motor#2 and set motor#2 dimming to 25%  
  `Rule1 1`   // Enable Rule1  
  
    `Rule2`  
    `ON Dimmer#State>80 DO Dimmer 25 ENDON`  //turn on motor#2 and set motor#2 dimming to 25% (note(!) - see below.)  
    `Rule2 1`   // Enable Rule2  

 ## Note:
- Sonoff D1 has problems on a regular basis and sets the dimming to 100% (it's very loud).  
- to treat problems with Sonoff D1 and you need Rule2.
 
 
 ## UPD#1:

If you’re having “ghost switching” events:

 1. Pairing a RF remote with D1 could stop them.
 2. Or remove from the board R6 R7 R8 R9 + R11 R12 R13 R14.
![Sonoff D1 Dimmer](https://user-images.githubusercontent.com/4712485/98549844-ba77e300-2271-11eb-8a0c-0db1fcc8c9cd.jpeg)
 3. Or remove U1 + U2 from the board.
![Sonoff D1 Dimmer](https://user-images.githubusercontent.com/14799318/111128907-bd634700-8575-11eb-8fa9-497a3380addb.jpeg)

**Best regards,   
TrDA**
