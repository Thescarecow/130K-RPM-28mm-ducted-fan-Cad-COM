# 130K-RPM-28mm-ducted-fan-Cad-COM
Basic geometry shape and COM for a 28mm 130k RPM ducted fan for use in toolhead designs, also includes keep out space for direct wiring, allow for more keep outspace if using plugs.
Based on fans sorced from the following Aliexpress store due to the fact that the driver board is decoupled from the motor and is of a larger size then intergrated options allowing for the driver to be kept outside of the chamber as they can get quite warm.

https://www.aliexpress.com/item/1005008501972890.html?  

Cooling performance?  

Yes, all of it, airflow, pressure, noise. A single fan has more power draw then a ws7040 CPAP, this fan will overwelm your hotend with poor duct design and is totally unsutable for printing materials like ABS unless you have 75C+ chamber temperatures as the cooling performance is just overkill even at the lowest possible PWM output it will make your parts warp from overcooling.

COM:
To ensure the correct COM values of the part when you import the model, make sure the material is set to alum 6061 and the mass should be basically ~52.5g.

Wire/Plug keep outzone:
Not facted into COM values, acts as a guide to ensure you still have space for the wiring to the PCB, if not hard wiring add more space as required for the type of plug you plan to use.

NOTES:
These fans are LOUD and pull a lot of power (24v 130W 5.5A) at full RPM for this motor driver combo
High RPM Metal fan = will eat fingers, tools, bolts alike with stunning results, never run them with loose items around that could be sucked/fall into the blades while they are running

Possible issues so far
- Biggest question still unanswered for these fans is the life(hours of use) at elivated chamber temperatures, the fan disk is alum and the hub is steel with just a pressfit holding them together. 2x difference in CTE (coefficent of Thermal Expansion) means that at 80°c+ temperatures there is a risk it stops being a pressfit and more of a light tight leading the disk and shaft to seperate.
- life hours and failure modes and the hours the failure occured will be updated here.

Klipper Control & wiring PWM
Control can ben with the supplied POT or by PWM input (1khz-10khz range)
Expect PWM speed range to be around 10-99% but you might be able to get slower depending on your PWM signal and the driver

-Remove the supplied Pot control and wire up the pot GRN to the fan port ground and the PWM signal to the fan positive, 5v is not used and the wire can be removed
-Consider flyback or other voltage feedback protect between the fan driver and your MCU as you feel is required.

Example Klipper code to control them via 5V PWM from a fan port  

[fan_generic ChFan]   <--- change this to be [fan] if you want it controlable via default slicer settings which look for the fan  
pin: put the fan port pin as per your MCU here, ensure it is set to 5v output  
max_power:1.0  
cycle_time: 0.020  
kick_start_time: 0.5  
max_power: 1.0  
  Depending on your fan, you may need to increase this value  
  if your fan will not start. Can change cycle_time (increase)  
  if your fan is not able to slow down effectively  
off_below: 0.010  
