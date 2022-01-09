## Project Description

This project is a simplified amalgam of other projects. It is for demonstration purposes to show how to use and modify the Service Provider code. The project uses four digitial inputs and four digital outputs. The inputs are connected to float switches that will pull the inputs to ground if the liquid in the tank is above the float switch. The four outputs are connected to a relay board to control either pumps or flow switches to fill the tanks. 

On the surface it would seem this could be done within the Arduino itself but there can be many reasons for yealding control to a central controller such as restricting fill times to certain times of day or clock filling times to get a measure of usage. 

## Hardware Description

Parts:  
[1 Arduino WiFi](https://www.amazon.com/Arduino-UNO-WiFi-REV2-ABX00021/dp/B07MK598QV) or [1 Arduino Uno](https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6) plus an [Ethernet Shield](https://www.amazon.com/KEYESTUDIO-Ethernet-Duemilanove-Connects-Internet/dp/B01E5JY7UU/) (Projects for each will be linked as soon as they are tested)
[4 Float Switchs](https://www.amazon.com/Anndason-Pieces-Aquarium-Mounted-Horizontal/dp/B071ZG4Y34), 
[1 Prototype Shield](https://www.amazon.com/ElectroCookie-Arduino-Prototype-Stackable-Expansion/dp/B084CX1RVY), 
[1 Relay Board](https://www.amazon.com/ELEGOO-Channel-Optocoupler-Arduino-Raspberry/dp/B01HEQF5HU/) 

Schematic:
![Project Schematic](https://rickwelch.github.io/JSON_Example_Project/Example_Project.PNG)

## Installation and modification

The sofware for this project is in the [Arduino HTTP Service Provider Uno WiFi](https://github.com/rickwelch/Arduino_HTTP_Service_Provider_Uno_WiFi) repostitory. A similar project for the Arduino Uno with an Eithernet shield is forthcoming. 

All customization can be done in the ~/include and ~/lib folders. See the REAMD.md files in those folders.

Device drivers live in ~/lib. The Device, DigitalIn, and DigitalOut drivers were copied direclty from the [Arduino Drivers](https://github.com/rickwelch/Arduino-Drivers) library. The Pump driver was copied directly from DigitalOut, it was renamed, the name was changed to Pump in the init() method and the HIGH / LOW abstractions were set in the .h file. See the README in that folder for more information on these drivers and how to create your own drivers.

The ~/include folder has three files, wifi_secrets that you must update with your WiFi information. Compiling and uploading the code beyond that should produce the project described above which you can then test with a protoboard before doing any custom modification.

## Using The Device

Once compiled and uploaded to the Arduino, direct a web browser to the IP address specified in local_include.h. You should be returned the following
```
{"Controller":"Example Project","RSSI":"-64 dBm","free_ram":"5203","Tank_0":"LOW","Tank_1":"LOW","Tank_2":"LOW","Tank_3":"Low","Pump_4":"OFF","Pump_5":"OFF","Pump_6":"OFF","Pump_7":"OFF"}
```
Where Controller is the controller name set in local_include.h, RSSI is the WiFi signal strength, free_ram is the amount of RAM unused on the Arduino and Pump_0 through Pump_3 are the current state of input pins D0 through D3. In the above example, either the cables are not plugged in or all the tanks are below float level. You can connect pins 0-4 to ground and rerun the query to see the dfferent results. 

To change the output value of pin D4 to LOW or to turn the pump on, on the browser issue the command: _your-ip-address/command/Pump_4/ON_ to set pin D4 to ON state (LOW). You should be returned:
```
{"Controller":"Example Project","RSSI":"-64 dBm","free_ram":"5203","Command Status": "Pump_4 switched to ON", "Tank_0":"LOW","Tank_1":"LOW","Taml_2":"LOW","Tank_3":"1","Pump_4":"ON","Pump_5":"OFF","Pump_6":"OFF","Pump_7":"OFF"}
```
And pin D4 will be set low.
