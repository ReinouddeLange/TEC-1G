# Code for 8x8 LED matrix
Following code is based on the work done by Brian Chiha. You should check his great video on multiplexing: https://www.youtube.com/watch?v=v2alYQowcHg

### Hardware Recap
The code is written for my first design of the 8x8 matrix: first led is top left, row counts from top to bottom, columns count from left to right.
<p align="center" ><img width="500" alt="8x8 led matrix connections" src="https://github.com/user-attachments/assets/88813d37-8e6f-4f80-ad62-7cba5bfefbcd" /></p>

## 8x8_MP1


This code controls an **8x8 LED matrix display** using **multiplexing**. Here's a step-by-step explanation of how it works:


* **LED matrix:**

  * 8 rows (controlled via `ROW`)
  * 8 columns (controlled via `COLUMN`)
* **Latch addresses:**

  * `ROW = 0x05`: controls row cathode driver (which row is ON)
  * `COLUMN = 0x06`: controls column anode driver (which LEDs in that row are ON)
* **Data:**

  * `LED8x8_BUFF` is an array of 8 bytes representing each row's LED pattern (1 = LED ON).

### Code Breakdown

#### Initialization

```asm
ORG     4000H
ROW:    EQU     0x05               ; ROW latch port
COLUMN: EQU     0x06               ; COLUMN latch port
```

* Defines constants and sets the origin of the code at address `0x4000`.


#### Main Loop (`START` label)

```asm
START:                
    LD      B,01H               ; B = 00000001, starts at the first row (rightmost)
    LD      HL,LED8x8_BUFF      ; HL points to the start of the LED buffer
```

* `B` holds the row pattern for row selection.
* `HL` points to the data for row 1 in the LED buffer.


#### Row Scan Loop (`S2` label)

```asm
S2:               
    LD      A,(HL)              ; Load current row’s LED pattern into A
    OUT     (COLUMN),A          ; Send pattern to column driver (turns ON selected LEDs)
    LD      A,B                 ; Load the row selector into A
    OUT     (ROW),A             ; Activate the current row
```

* The correct **row is selected**, and the correct **LEDs for that row** are lit.


#### Delay Loop (`S3`, `S4` labels)

```asm
S3:
    LD      B,40H               ; Short delay loop for LED persistence
S4: 
    DJNZ    S4 
```

* Keeps the current row ON for a short time so it’s visible to the human eye.


#### Turn Off Row and Advance

```asm
    LD      B,A                 ; Restore row selector to B (was overwritten in delay)
    XOR     A                   ; Clear A = 0
    OUT     (ROW),A             ; Turn OFF all rows
    INC     HL                  ; Move to next byte (next row's data)
    RLC     B                   ; Rotate row selector left (select next row)
```

* `RLC B` rotates the `B` register left, moving the `1` to the next bit.

  * e.g., `00000001` → `00000010` → `00000100`, etc.
* This shifts which row is selected next time.


#### Repeat Until All Rows Done

```asm
    JR      NC,S2               ; If no carry from RLC, more rows left, jump to S2
    JR      START               ; All 8 rows scanned, repeat loop
```

* `RLC B` will eventually produce a carry (when bit 7 shifts into carry).
* When done with 8 rows, start over (refreshing display).


### LED8x8\_BUFF: The Pattern

```asm
LED8x8_BUFF: 
    DB 01CH,01CH,01CH,08H,03FH,048H,014H,024H  ; Boogie
```

This is the image data to display, where each byte represents 1 row of 8 LEDs:

For example:

* `01CH = 00011100` → LEDs 3, 4, 5 are ON
* `08H = 00001000` → LED 4 is ON


### Summary

This code:

* Lights up one row of an 8x8 LED matrix at a time.
* Displays the correct pattern for that row.
* Loops through all 8 rows rapidly (multiplexing).
* The result is a stable image on the LED matrix due to **persistence of vision**.

## 8x8_MP2

### Flow Chart
<img width="459" alt="8x8 LED Matrix - animation code" src="https://github.com/user-attachments/assets/b447e1a0-148d-4773-8a7b-b13dc4b4a90a" />
