# THC-Up-and-Down-Only
CNC plasma cutting automatic torch height controller built for arduino uno

It uses code from swolebro, the legend who wrote a super quick THC see here (https://github.com/swolebro/swolebro-youtube/blob/master/arduino/thc/thc.ino) 

Although I have not done much cutting yet, I have setup a unimig cut45 plasma cutter on my cnc and I can confirm that this THC is working well. 

You can test this on the wokwi online simulator - see here https://wokwi.com/projects/339317146336100947 the labelling system leaves a bit to be desired but each components ID should enlighten you as to what is what. The project will show you how to connect all the basic components up, ie without optos etc.

I am no programmer or electronic giru so take precautions if you are considering testing it out. Swolebro has some great and entertaining info on his CNC build on youtube regarding some electronics that should be considered ie optos and volt regulator etc and also how his portion of the code works. (electronics  -- https://www.youtube.com/watch?v=lkKd5P8oH5Q&list=PL9xPdBFt5g3Q6TkuhhfQmQNm6TdvNkPuX&index=20) & (code -- https://www.youtube.com/watch?v=nmXoZt423WI&list=PL9xPdBFt5g3Q6TkuhhfQmQNm6TdvNkPuX&index=21)

If anyone can make use of this and has any good feedback that'd be muchly appreciated.


-----I/O that must be connected--------

1 External Aref voltage supply ~5Volt

2 analogs 
-Torch voltage from a plasma cutter CNC port
-potentiometer input for setting voltage required

2 digital outputs
-Up signal to tell the controller to raise the cutting torch
-Down signal the opposite of up


-----controls on the THC-------------

-THC on switch

-1 x 10k pot (for setting volts)

-LCD

-THC on green LED

-THC raise red LED

-THC lower yellow LED

-Reset button to reset the arduino would be a great addition currently I power it down to change the volt setting 


-----connections to THC--------

- +torch voltage from plasma cutter (51:1 voltage divider)
- -torch voltage from plasma cutter
- ~5 volt DC regulated supply (the built in arduino regulator just isn't accurate enough)

-----connections from THC--------

- Up/raise torch to controller input
- Down/lower torch to controller input

-----how it functions (or should)-----

- when booted (without thcOnSwitch being in the on position) an LCD will show the current voltage setting
- you can now adjust this setting using the potentiometer
- Once set, use the thcOnSwitch to turn on the THC (this locks the setting, currently ONLY a reset with the switch off will allow resetting these)
- The green LED indicates THC is on
- if the torch voltage is above ~3 volts the THC is enabled
- when the voltage coming from the plasma is below the setting an Up signal will be output and the red LED will light up
- when the voltage is above the setting a Down signal will be output and the yellow LED will light up

To use this on linuxcnc/Plasmac choose mode 2 which will accept the up and down signals and respond accordingly when the THC has been enabled via the GUI and G-code that you are running.
