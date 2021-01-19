# Logitech-G29-Load-Cell

I will not repeat text what you can find in the References, and keep the story short:

My ideas to develop this program was due to the inspiration and using the ideas of References:

# References
1) https://github.com/GeekyDeaks/g29-load-cell (orignal idea did come from here)
2) https://github.com/Skidude88/Skidude88-G29-PS4-LoadCell-Arduino/wiki (orignal idea did come from here)
3) https://github.com/olkal/HX711_ADC (libary for the HX711 I did use)
4) https://github.com/iforce2d/thrustTester (to get the defalt setup of the HX711 from 10 to 80 Hz, strage my HX711 did end up with 89 Hz)
5) https://circuitjournal.com/50kg-load-cells-with-HX711 (wiring with 2 cells)
6) https://www.youtube.com/watch?v=iywsJB-T-mU (at 7:15, due to ESP32 speed)
7) https://www.youtube.com/watch?v=99u9cy7Mnl4 (for mod the rubber to simulate more like a load cell)
8) Google Store: Serial Bluetooth Terminal from Kai Morich

and I will not refere it more in the text, since it is a mix overall and all of them above did contribut to my result.

The reson for this is that the G29 use pot.meter from 0-100% break over distance => give the output voltage to regulate coresponding break %
The force feedback is more or less linear, at the end we touch a rubber what will simulate a higher pressure but anyway the muscle memory is difficult
and constant good breaking espesally in trail breaking is difficult. With an load cell we are simulating more close to real hydralic breaks in real life
where we have overporosional force to push to reach higher break.

Then the g29 and PS4 do not give any possibilites to trim the break to your driving style and this was alos one of my reason to have an micro controller so that I could setup the break after my condisitons.

# Shopping list:
1) Load Cells with HX711 
2) Micro controller 
3) Enclosering for the Micro Controller/HX711 and for the Load Cells
4) Resistors and cables

# How-to and why

To use PWM signal to generate the needed voltage range was not good if not using a low filter or a DAC. Since I am using ESP32 anyway to other Arduino projects and for IoT and they are cheep and can even over Amazone go under 6 Euro (included delivery) is an very unexpensive MC.
The advantage:
1) rel. fast 2xCPU with 32 bit
2) 2 x8 bit DAC (range 0-255)
3) Bluetooth for seiral com. for changing parameters in the setup/trimming the break
4) Voltage range 0-3.3V fits anyway to the G29 what also is in this range

That was the reason to use ESP32 and as I was work with the project I wanted to "simulate" a "PWM" with my DAC between 2 values and here the multitask function of the ESP32 was perfect, letting the main program calulate the values for breaking and if a needed value was between, lets say 231 and 232 I would let the DAC jump between 231 and 232 in an constant loop (of course calculated how many times of 231 and 232 to get the right simulated value let say 231.12) so in this case the task would not have any "delay" but just looping and looping with the lastest known values until the task did get new values to loop. Fantatic the ESP32 :)













