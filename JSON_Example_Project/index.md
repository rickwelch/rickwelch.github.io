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

Links to both projects when available

All customization can be done in the ~/include and ~/lib folders. 

Device drivers live in ~/lib. There are currently four drivers there but the intent is to keep adding to this library. Briefly, all drivers use the Device base class. The DigitialOut and DigitalIn are for Arduino pin outs and pin ins. Moisture is the capacitive moisture sensor driver and TimedRelay allows for enableing a digital pin out for a certain number of milliseconds.  See the README in that folder for more information on these drivers and how to create your own drivers.

The ~/include folder has three files, wifi_secrets that you must update with your WiFi information. Compiling and uploading the code beyond that should produce the project described above which you can then test with a protoboard before doing any custom modification.

## Using The Device

Once compiled and uploaded to the Arduino, direct a web browser to the IP address specified in local_include.h. You should be returned the following
```
{"Controller":"Example Project","RSSI":"-64 dBm","free_ram":"5203","DigitalIn_0":"1","DigitalIn_1":"1","DigitalIn_2":"1","DigitalIn_3":"1","DigitalOut_4":"1","DigitalOut_5":"1","DigitalOut_6":"1","DigitalOut_7":"1"}
```
Where Controller is the controller name set in local_include.h, RSSI is the WiFi signal strength, free_ram is the amount of RAM unused on the Arduino and DigitalIn_0 through DigitalIn_3 are the current state of input pins 0 through 3. In the above example, either the cables are not plugged in or all the tanks are below float level. You can connect pins 0-4 to ground and rerun the query to see the dfferent results. 

To change the output value of pin 4, on the browser issue the command: _your-ip-address/command/DigitalOut_4/0_ to set pin 4 low. You should be returned:
```
{"Controller":"Example Project","RSSI":"-64 dBm","free_ram":"5203","DigitalIn_0":"1","DigitalIn_1":"1","DigitalIn_2":"1","DigitalIn_3":"1","DigitalOut_4":"0","DigitalOut_5":"1","DigitalOut_6":"1","DigitalOut_7":"1"}
```
And pin 4 will be set low.
