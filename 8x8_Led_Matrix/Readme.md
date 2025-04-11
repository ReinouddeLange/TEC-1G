# 8x8 Led Matrix
## The beginning...
Years ago I got myself an 8x8 Led Matrix Dual Color display. I intended to use it on an Arduino, but never got so far and the matrix was lying around without being used.
<p align="center" ><img width="300" alt="TEC-1 8x8 led matrix schematics" src="https://github.com/user-attachments/assets/28e21825-a8d7-44a5-8af1-ad22df587d2c"/></p>

So, one day I got the idea to hook it up on the TEC. First I started to wire it up on a breadboard:
<p align="center" ><img width="400" alt="Breadboard setup" src="https://github.com/user-attachments/assets/b7cf068f-bfbe-4cb3-be01-10cfa33e0849" /></p>

I had a quick look at the schematics from the TE magazine and soon it started to do something. Since we have two colors and twice the amount of columns I added a third 74LS273

<p align="center" ><img width="400" alt="TEC-1 8x8 led matrix schematics" src="https://github.com/user-attachments/assets/72958514-1d5b-45d7-a3e1-5271da147f7e"/></p>
<br>

## Version 1
Originally I had the plan to use a experiment PCB, but the thought of soldering all those wires discouraged me a bit and I thought I'd have a go using KiCad and design a PCB:

<p align="center" ><img width="300" alt="PCB" src="https://github.com/user-attachments/assets/64123196-de9e-45f9-ae1e-5d4f6d1789a9" /></p>

I ordered the PCB and to my surprise it worked very well! Here is my first version next to the version Ben Grimmet made:
<p align="center" ><img width="400" alt="TEC-1 8x8 led matrix RdL and Ben Grimmet version" src="https://github.com/user-attachments/assets/b1630003-4a62-47b0-bc6f-30cfc586f8d4" /></p>

## Version 2
Maybe I should have taken a closer look on how the TEC programs are written for the original 8x8 matrix. I only looked at the datasheet for the 8x8 matrix, which uses rows and columns. The first row is at the top and the first column is at the left: <br>

<p align="center" ><img width="500" alt="8x8 led matrix connections" src="https://github.com/user-attachments/assets/88813d37-8e6f-4f80-ad62-7cba5bfefbcd" /></p>

When you would run an original program the effect would be like the matrix is rotated 90 degrees compared to the original 8x8 matrix.

<p align="center" ><img width="287" alt="TEC-1G 8x8 led matrix v1 RdL" src="https://github.com/user-attachments/assets/c52e493c-442e-4a80-8b37-d57d3546a201" /></p>

The original 8x8 matrix seems to be designed from a mathematical point of view, like a first quadrant of an x-y system: <br>
<p align="center" ><img width="300" alt="TEC-1 8x8 led matrix original" src="https://github.com/user-attachments/assets/2ac487e5-b892-430b-b21b-ea84573e481e" /></p>

So I designed a version 2 with rotated display, bigger footprint for the transistors and all latches connected to reset line (credits to Brian Chiha):
<p align="center" ><img width="300" alt="PCB v2" src="https://github.com/user-attachments/assets/ffbf3bef-a75c-4fd2-b7e6-438e467699d5" /></p>

Final schematics:
<p align="center" ><img width="1200" alt="8x8 led matrix schematics v2" src="https://github.com/user-attachments/assets/c57f3681-07ac-4136-a0de-69326830769e" /></p>

## Assembly information


|Id|Designator|Package|Quantity|Designation|
|:---|:---|:---|:---|:---|
|2|U4|YSM-1288CR3G2C|1|YSM-1288CR3G2C|
|3|U3,U2,U1|DIP-20_W7.62mm_Socket|3|74LS273|
|4|R16,R15,R14,R13,R12,R11,R10,R9|R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal|8|1K|
|5|R8,R7,R6,R5,R4,R3,R2,R1|R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal|8|220R|
|6|Q8,Q7,Q6,Q5,Q4,Q3,Q2,Q1|TO-92_Inline|8|BC547|
|7|J1|PinHeader_2x10_P2.54mm_Horizontal|1|Conn_02x10_Odd_Even|

### Credits
Thanks to Brian Chiha for the advice, review and testing of boards v1 and v2.
