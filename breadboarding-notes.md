# File Description
This file will contain my notes and things I would like to remind myself during debugging so that I'm not stuck in integration hell

# Registers
## Registers 1 and 2:
### 74HC173 Quad D-flip flop (i.e. 4 bit register)
- OE and OE2 are inverted inputs that control whether the chip will output values or not, regardless of if you're storing values or not
- E1 and E2 are inverted inputs that when enabled, will allow the chip to store bits on the next rising edge of clock pulse
- I toggle the line connected to E1 and E2 (one single line since they're connected to each other) to enable reading from bus
- CP pin is the clock pulse pin
- MR is the manual reset pin, probably will set it only at the beginning of execution
## 74HC243 quad bus transceiver
- I set OEB to constant high
- I toggle OEA for enabling writing. (remember OEA is low for Hi-Z state, and high for writing).
- Although the bus is bidirectional, I will only be going from B to A

# Computer Clock
## Manual mode clock (LM555 monostable mode)
- Time constant ~ 0.517s
- trigger is inverted (took me wayyyy too long to figure that out)

## Automatic clock (LM555 astable mode)
- duty cycle: ~50%
- time period: ~ 1s

# What I've learnt, both about circuits and life
- Voltage dividers are literally everywhere
- Loading resistance is VERY important
- Maybe stuff isn't broken. Maybe I just don't know how to use it just yet
