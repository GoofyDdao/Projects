## 0. About using SPI multi display.   
 -  Step by step [instructions for E-Paper Display](https://github.com/arendst/Tasmota/discussions/11850).  

## 1. SPI multi display.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4151.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4152.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/20210917_191722.jpg)   

## 2. How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file:    

 - Enter the command in the console to initialize the displays after restarting the ESP8266:  
   `Rule1 ON system#boot DO Backlog Power2 1; Power3 1; Power4 1; DisplayText [z]; ENDON`  
 - Run commands in the console for test Display:    
   `Backlog DisplayText [z]; DisplayText [f0s2x2y2tS]`  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton2 E-PAPER#1; WebButton3 E-PAPER#2; WebButton4 E-PAPER#3`  

Wemos Pin|GPIO|Component|e-Paper|
:-:|:-:|:-:|:-:
D5|14|EPaper29 CS|CS
D6|12|SSPI MOSI|DIN
D7|13|SSPI SCLK|CKL