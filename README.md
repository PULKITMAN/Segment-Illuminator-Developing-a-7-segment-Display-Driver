# VSDsquadron-mini-internship
RISC-V Research Internship.

## Task - 1 -> Using a RISC-V simulator, write a C program to count the sum of all numbers from 1 to n.

## Writing a C code to count sum of numbers from 1 to n
1. I started by opening Terminal and creating and opening a new C file in Leafpad and named it as sum1ton.c . I wrote the code in it as shown in below image.
![code ](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/0d647449-334d-415f-9237-8736b00b070e)
2. After that, it was compiled, run in the terminal to verify, and the desired output was obtained.
![result 1](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/0c544287-ae29-426f-8ce9-61aa62fd8699)
3. Tried with many values of n and obtained results, such as n=100.
![code and result](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/b88546ed-16f9-426b-9e4c-1c549559a9c0)
## Running above program in RISC-V Simulator
After running the code in the terminal, I needed to run it in the RISC-V simulator. To do that, I was required to run a specific set of code, which I completed in the steps below:
1. In order to produce a file with the ".o" extension(Assembled File), I first wrote the code to build it using the RISC-V gcc compiler with  'O1' as compiler option.
![risc v gcc file](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/7291f1b8-71ca-4b39-90e8-1269fe36f168)
2. Next To obtain the assembly code for the aforementioned C program, I wrote the code ***riscv-unknown-elf-objdump -d sum1ton.o***. I received many assembly codes in return. Merely by appending "| less" to the command, the number of assembly codes shown were lowered. I searched the "main" section to get the instructions for our main code. The byte address for main was found to be 10184 and got 35 instrusctions when using option 1. I saw that the address of every instruction that followed was increased by 4.
![main assembly](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/2ef3878a-4e56-48cd-a773-2f953ef3c94c)
3. After this I run the identical instructions with a different parameter, instead of ***O1***, I used ***Ofast***. I didn't observed any changes in the instructions.
   
![main assembly fast](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/1d3d065d-cc21-4200-93d1-4564f364b854)

### Task 1 finished


## Task - 2 -> Write a simple C program for your project selected and compile with RISC-V GCC
### My project is to develop a 7 segment display driver.
Before writing the code first we should understand what is a "***7 segment display***" and how does it work. Once we understand how does it works we can develop the driver to run it very easily.

### An Overview of 7 Segment Display
One of the most basic kinds of display devices is a 7-segment display, which can show characters from "A" to "F" in addition to numbers from 0 to 9. The term "7 Segment Display" refers to the configuration of seven LEDs, which are placed in the shape of a "8" using hexagonal bars.

Each LED is known as a ‘Segment’ with names a, b, c, d, e, f and g. Most 7 Segment Display have an additional segment in the form of a dot(known as dp). It is technically an 8 Segment Display with 7 Segments responsible for displaying the main numerical data and one dot segment.

Pinout and labelling of the 7 segment display is as shown below:

![7-Segment-Common-Anode-Common-Cathode-Pinout](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/b07d4c34-53b3-4f76-8384-b815d33de140)

It requires you to turn on or off a collection of Segments in order to display a specific number. For instance, all segments must be ON except for segment "g" in order to display the number "0".

The following image shows how the numbers '0' through '9' and the letters 'A' to 'F' will look like on a standard 7 Segment Display.

![7-Segment-Display-Number-Formation-Segment-Contol](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/3a419c06-db5a-4dcd-beed-354f13a0fea6)

### Types of 7 Segment Displays
There are two main kinds of 7-segment displays, depending on how the LEDs are connected inside. The two are known as the "common cathode" and "common anode".

#### Common Cathode
The cathodes of all eight LEDs in a Common Cathode type 7 Segment Display are linked and made common for the display unit as a whole. Consequently, the full 7-segment display device may be controlled with just 8 pins or connections.

The following image shows the internal connection of a Common Anode type 7 Segment Display:

