# 8-bit-computer
This is my attempt at building an 8 bit computer from scratch using CMOS logic gates. This repository will contain documentation, notes, schematics, and instruction sets.
It will almost entirely be made out of the 74HC series of CMOS Logic Gate chips, except RAM.

# Progress:
- [x] Computer Clock
- [x] 8 bit data bus
- [x] General Purpose Register 1
- [x] General Purpose Register 2
- [ ] Output Register
- [x] Instruction Register
- [ ] memory module
- [ ] program counter
- [ ] ALU
- [ ] Computer logic

# What do I want it to do?
I want it to be able to
- perform simple arithmetic operations of addition, subtraction, multiplication, and possibly division.
- Read from and write to general purpose registers (I am thinking 4 registers.
- Read from and write to static memory (either matrix of latches or EEPROM) using a memory address register.
- run programs and access each instruction from memory into an instruction register.
- fetch next instruction location using a program counter.
- Have a SSD (seven segment display) that displays output that reads from the output register (possibly migrate to pixel based display in the future but not sure how current architecture would suit it)
- be programmed by a custom instruction set (possibly write my own assembly language and compiler since it will be specific to my architecure)

# Main modules
## Computer Clock
- Synchronizes all operations.
- I am thinking of a frequency of about 1kHz but honestly it can be a lot more, I will estimate based on total gate delays how faster I can make it, but honestly it doesn't matter because it's not like I'm doing anything complicated. Yet.
- I can use a 555 timer's astable mode to get a stable wave and then use a Schmitt-Trigger to convert it into a digital signal.
- I also want a manual clock functionality for debugging purposes. (I can use an SR latch to toggle modes)

## Registers
- I am thinking 2 general purposes registers.
- An instruction register will store the current 8 bit instruction.
- A memory address register will act as the interface between the processor and memory.
- Each register bit will have 3 states: 0 (low), 1 (high), and Hi-Z (disconnected) when it is writing to the bus. This will be achieved using a bus transceiver.
- Each register, when reading from the bus, will interact directly with the data bus.
- Output register that stores a value that determines what the SSD displays. i.e the SSD reads from the output register to display a number. I will probably use a 555 timer to cycle through each digit to enable it, thus being able to display 4 digits instead of only 1.
- Potential result register that temporarily stores the result of ALU-run operation.

## Memory Module
- Since this is an 8 bit computer, the first 4 bits will outline the instruction to be performed. Therefore I only have 4 bit memory addresses to work with. This means my RAM will only be a maximum of 16 bytes.
- There will be memory address register to access memory location in RAM.
- Problem is, this limits the number of instructions in one program to be a maximum of 16. If that issue arises later, I think I will use an Arduino that manually loads each instruction into the first memory location on each clock cycle and disable the program counter. Don't know if that would even work but it's an option.

## Program Counter
- This will be either a register or a 4-bit binary counter (I haven't decided so this isn't included in the registers submodule) that stores memory adddress of next instruction to execute.
- After completion of current instruction, the CPU will load the instruction from the program counter into the instruction register, and increment the memory location of the PC to point to the address of the next instruction.

## Output Register
- This will hold the value for the seven segment display.
- I am still figuring out the specifics of how I will display 4 digits instead of only 1 (more memory maybe??).

## Arithmetic Logical Unit (ALU)
- It will perform bitwise operations on one or two 8-bit numbers.
- It will handle addition, subtraction, and multiplication. If possible I'll try to also implement division.
- I might have a result register that stores the output of an operation temporarily before storing it into the first register in the argument.
- Goes without saying, when I mention that it can handle subtraction, that the ALU can handle negative numbers.
- Optionally I will implement flags such as zero flag, carry out flag, and comparision flag.

# Programming the CPU
- I want my computer to be able to run programs. For that it needs to recognize instructions, op codes, registers, and addresses.
- I plan on writing my own assembly language (and compiler that converts it to binary to load into the computer's memory)

# Acknowledgements
- Purdue University's ECE270 (Digital System Design) that taught me the fundamentals of logic gates and transistors
- [Ben Eater's](https://eater.net/) videos on the workings of each component of a basic CPU
