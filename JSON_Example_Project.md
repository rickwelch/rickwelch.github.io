# Arduino JSON service provider Example Project.

+ Description of project
    - simple project with 4 digitial inputs and 4 outputs
    - currently in use for hydroponic tomatoes
+ Hardware Description
+ Clone and setup
+ How the UI works

## Project Description

This project started as a simple example project but became an actual project in use. I finally started to have some success with hydroponic tomatoes and were going away for 2 weeks. I added float switches on the tomato buckets and set up a 5 gallon tank to supply nutrients when the root tanks are low. I'm currently only using three of the four switches and pumps.

This project has four digitial inputs and four digital outputs. The inputs are connected to float switches that will pull the inputs to ground if the liquid in the tank is above the float switch. The four outputs are connected to a relay board to control either pumps or flow switches to fill the tanks. 

On the surface it would seem this could be done within the Arduino itself but there can be many reasons for yealing control to a central controller like restricting fill times or measuring filling times to get a measure of usage. 

## Hardware Description

Parts:  
[Arduino WiFi](https://www.amazon.com/Arduino-UNO-WiFi-REV2-ABX00021/dp/B07MK598QV) or [Arduino Uno](https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6) plus an [Ethernet Shield](https://www.amazon.com/KEYESTUDIO-Ethernet-Duemilanove-Connects-Internet/dp/B01E5JY7UU/) (Projects for each will be linked as soon as they become public)
[Float Switch](https://www.amazon.com/Anndason-Pieces-Aquarium-Mounted-Horizontal/dp/B071ZG4Y34), 
[Prototype Shield](https://www.amazon.com/ElectroCookie-Arduino-Prototype-Stackable-Expansion/dp/B084CX1RVY), 
[Relay Board](https://www.amazon.com/ELEGOO-Channel-Optocoupler-Arduino-Raspberry/dp/B01HEQF5HU/), 
[Submersible Pump](https://www.amazon.com/dp/B015GOGPSU)

Schematic:
![Project Schematic](https://rickwelch.github.io/JSON_Example_Project/Example_Project.PNG)

## Installation and modification

Links to both projects when available

All customization can be done in the ~/include and ~/lib folders. 

Device drivers live in ~/lib. There are currently four drivers there but the intent is to keep adding to this library. Briefly, all drivers use the Device base class. The DigitialOut and DigitalIn are for Arduino pin outs and pin ins. Moisture is the capacitive moisture sensor driver and TimedRelay allows for enableing a digital pin out for a certain number of milliseconds.  See the README in that folder for more information on these drivers and how to create your own drivers.

The ~/include folder has three files, wifi_secrets that you must update with your WiFi information. Compiling and uploading the code beyond that should produce the project described above which you can then test with a protoboard before doing any custom modification.
