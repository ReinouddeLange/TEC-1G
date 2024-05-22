
I tried to figure out how to set the jumpers / switches for my EEPROM.

My EEPROM (28C256) has almost the same pinout as the 27C512 EPROM on which the schematics are based on:
<img height="350" src="https://github.com/ReinouddeLange/TEC-1G/assets/6297024/484bbbe8-2381-4a4f-b84c-6ed7f92b9db9">
<img height="350" src="https://github.com/ReinouddeLange/TEC-1G/assets/6297024/e5ae1d11-2cc0-403d-9c1f-9338a53a701a">

As you can see they are almost identical but some pins differ. A14 is on pin 1 where the 27C512 has A15.
Pin 27 which is /WE on the 28C256 is A14 on the 27C512.

In the schematics we find some switches or jumpers regarding these pins:

<img width="500" alt="Schematics TEC-1G - SW3 - SW4 - JP3 - JP4 - JP5" src="https://github.com/ReinouddeLange/TEC-1G/assets/6297024/298ed533-237d-4d96-a7c7-449f4a7dc58e">

For my EEPROM the following settings work:

<img width="150" alt="JP3-JP5" src="https://github.com/ReinouddeLange/TEC-1G/assets/6297024/a947ca78-0e8b-4e81-819f-b8d5242b5112">

The EEPROM has 28 pins, so all jumpers are at the bottom.


SW3 is set to 2-3, so A14 which is in fact /WE on my EEPROM is HIGH. That is correct, we don't want Write enabled.


SW4 is set to 1-2, so A15 which is in fact A14 on my EEPROM is LOW. This will determine which monitor is used.

<img width="200" alt="SW3 - SW4" src="https://github.com/ReinouddeLange/TEC-1G/assets/6297024/ea182651-9c71-425b-bf39-fc8236015eff">


Todo: test what happens with monitor if I change SW4.



