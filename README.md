# VSDsquadron-mini-internship
RISC-V Research Internship.
<details>
   <summary>Task - 1 -> Using a RISC-V simulator, write a C program to count the sum of all numbers from 1 to n.</summary>
   
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
</details>

---

<details>
   <summary>Task - 2 -> Write a simple C program for your project selected and compile with RISC-V GCC</summary>
   
## My project is to develop a 7 segment display driver.
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

The following image shows the internal connection of a Common Cathode type 7 Segment Display:

![7-Segment-Display-Pinout-Image-2](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/7002c2e7-2e7a-4ada-ba51-89cb9435de03)


#### Common Anode
In a Common Anode type 7 Segment Display, the anodes of all the 8 LEDs are connected together and made common for the entire display unit. As a result, we have just 9 pins/connections to control the entire 7 Segment Display unit (8 Cathode pins of 8 LEDs and one common Anode pin).

The following image shows the internal connection of a Common Anode type 7 Segment Display:

![7-Segment-Display-Pinout-Image-3](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/8eab72bd-7ed7-4d91-8e40-3f33d88e7837)

There is one important thing about common anode and common cathode type 7 Segment Displays that we need to remember. In case of Common Anode 7 Segment Display, we connect the common anode pin to VCC (i.e., positive of the power supply, usually +5V) all the time. To turn ON a particular segment, we make the corresponding cathode pin LOW.

In case of Common Cathode 7 Segment Display, we connect the common cathode pin to GND (i.e., negative of the power supply) all the time and make a particular anode pin HIGH to turn ON the corresponding segment.

Since we now have basic knowledge of the 7 segment display we can start making the driver for the display.

I am first making the driver for the common cathode display. There will be '4' inputs which will have value either as '0' or '1'. These 4 inputs will represent a 4 bit number thus giving us 16 different values so that we can dispaly the numbers from '0' to '9' and alphabets from 'A' to 'F'.

There will be 7 different outputs each representing a segment of the display and all the outputs will have values either as '0' or '1'.

The truth-table shown in the below image shows the state of the outputs for various inputs. Since, we are making driver for common cathode display, '1' represents that the corresponding LED is on and vice-versa.

![IMG_20240625_023954](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/b2867ec1-fa90-4088-8681-7d80b559fee0)

---

To code we can think of making an array of numbers containg decimal counterpart of (abcdefg)<sub>2</sub>. Then according to the input we will take out the number from the array and assign 'a' to 'f' their respective '1s' and '0s'.

The image shown below shows my code. To check the output I have displayed the value of (abcdefg)<sub>2</sub> for the corresponding input number. We can clearly see that the output value is matching the values from the truth-table.

![code for driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/53a12bc7-a0b6-4651-919b-a594249b2393)

The image attached below shows the output.

![compiled code result driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/b11e2f95-54c3-49bc-a842-8e7c8027912a)


Now we should update our code and compile it using "***risc-v gcc***" which is the main task.

#### Updated Code:

![code for driver riscv](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/98dc65bd-d821-4590-a61c-ec3b2c1f69f1)

#### Compiled Risc v file(.o file) generated:

![risc v compiled driver basic](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/51845bcb-e377-406d-9eda-910819553672)

#### "main" method in assembly language:

![ins set driver basic main](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/ad1d6b57-a898-4a6c-bbfb-e064d8c3c9d1)

#### "assign" method in assembly language:

![ins set driver basic assign](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/7e08a0bb-2a08-400b-9190-075722a105a0)

## Task 2 completed

</details>

---

<details>
   <summary>Task - 3 -> SPIKE Simulation and observation with -O1 and -Ofast. Upload snapshot of compiled C Code, RISC-V Objdmp with above options on your GitHub repo</summary>

The snap of code which I used:

![code for driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/53a12bc7-a0b6-4651-919b-a594249b2393)

Outputs from C language GCC and RISC-V GCC:

![same output basic driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/561d2121-c63a-49cb-9d99-a1511079b244)

We can clearly see that both the outputs are same.
### ***objdmp*** of "O1" mode: 

![objdump o1 main basic driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/47a3139c-f16a-4d75-bc17-81f51cd5d556)

![objdump o1 assign basic driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/1f4e9670-756c-48b4-bd77-4f516b533163)

---
### ***objdmp*** of "Ofast" mode:

![objdump fast main basic driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/643c22b1-d462-4a6a-a12a-8adb3fb64f17)

![objdump fast assign basic driver](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/42143712-439a-457e-8573-af480d81014e)

---

## Task 3 completed

</details>

---

<details>
   <summary>Task - 4 -> RISC-V INSTRUCTIONS</summary>
   
## INSTRUCTION SET ARCHITECTURE(ISA)

You have to know the language of computer hardware in order to control it. A computer's vocabulary is referred to as an instruction set, and the words that make up its language are called instructions.

The abstract model of a computer includes an Instruction Set Architecture (ISA), which specifies how the software controls the central processing unit (CPU). The Instruction Set Specification Architecture (ISA) serves as an interface between the hardware and software, defining the capabilities and methods of the processor.

## RISC-V ISA

A RISC-V ISA is composed of optional extensions to the base integer ISA and a base integer ISA that is required in every implementation. With the exception of lacking branch delay slots and supporting optional variable-length instruction encodings, the base integer ISAs are remarkably comparable to the early RISC(Reduced Instruction Set Computer) processors.

By convention, RISCV instructions are each  **1 word = 4 bytes = 32 bits**. Divide the 32 bits of an instruction into **“fields”**.

RV32I has x0 register hardwired to constant 0, plus x1-x31 general purpose registers. All registers are 32 bits wide but in RV64I they become 64 bits wide. RV32I is a load-store architecture. This means that only load and store instructions access memory; arithmetic operations use only the registers. User space is 32-bit byte addressable and little endian. We can access the registers by specifying their index numbers.

We define 6 *instruction formats* in RISC-V -
1. R-format
2. I-format
3. S-format
4. B-format
5. U-format
6. J-format

![isa type risc v](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/afa984a7-9c10-4627-8bc1-73f59b681e6e)

## R-type Instruction

* R-type is an operation without immediate. The immediate is the number that exists as an integer in the instructions.
* The 7 bits from 0 to 6 are opcode (operation code), used to identify the type of instruction.
* Bits 7 to 11 are the index of the rd register. The Rd register is also called the destination register, and the destination register is the register used to store the result. 
* func3(3-bit), combined with opcode, this field describes what operation to perform.
* rs1 and rs2 arefunc7(7-bit), combined with opcode and fun3, this field describes what operation to perform. called source registers. In most cases, instructions need to read the values of the two source registers for operations. The index of rs1 is in bits 15-19, and the index of rs2 is in bits 20-24.
* This instruction requires opcode plus funct3, and sometimes funct7 together to determine the type of operation that this instruction allows the CPU to perform.

Below image shows the format of all the R-Type instructions:

![all r type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/f0654d42-2c5d-4dfb-8614-ca5c2e7692ef)

## I-type Instruction

* I stands for immediate in I-type instructions, indicating that operations are executed using registers and immediate values and are not dependent on memory locations.
* The upper 12 bits of I-type is an immediate number.
* The opcode is different from other instruction formats because the corresponding specific operations are different, and other parts are very similar to R-type.

Below images shows the format of all the I-Type instructions:

![all i type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/c18db051-a68b-4754-9ce7-9e9e69a59682)
![all L type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/b36f2032-e269-42ec-855d-0d951e14e076)


## S-type Instruction

* S stands for "store" in S-type instructions, indicating that they are store-type instructions that aid in storing register values in memory. This type of command is mostly used for storing.
* The characteristic of S-type instruction is that there is no rd register.
* The immediate is divided into two parts, the first part is in bit 11-5, and the second part is in bit 4-0.

Below image shows the format of all the S-Type instructions:

![all s type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/315a3dde-c506-4992-bb63-8eb6ac99faff)

## B-type Instruction

* B stands for branching in an instruction of the B-type, indicating that it is mostly used for branching under specific conditions.
* B-type instructions are mainly used as branch instructions, but they are conditional Branch. It means to decide whether to jump or not need to depend on whether the condition is valid.
* The instruction does not include rd register and funct7, but contains rs1, rs2, funct3 and immediate.
* The immediate is divided into two areas.

Below image shows the format of all the B-Type instructions:

![all b type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/00c85763-03bb-44aa-9d1d-371d06bdb4f7)

## U-type Instruction

* U-type instructions are used to send immediate data into the target register. The letter U stands for Upper Immediate instructions.
* A 20-bit immediate is provided in the U-type instruction.
* The final operation result is related to the 20-bit immediate, and the result is written back to the rd register.
* There are no funct3, rs1, rs2, and funct7 in U-type.
* This type of instruction structure is very simple.

Below image shows the format of all the U-Type instructions:

![all u type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/84cc49b1-ccf4-4187-950d-3688d266a351)

## J-type Instruction

* J stands for jump in J-type instruction, indicating that jump type instruction is implemented using this instruction format.
* The format of this instruction is very similar to U-type, it only have Rd register and immediate and opcode.

![all j type ins encoding](https://github.com/PULKITMAN/VSD_MINI_ResearchInternship/assets/118650271/71f6238d-0567-4ef2-9ce7-b0d9c5412798)

# Lets decode the instructions given to us

```
ADD r1, r2, r3
```
> * This is a R-Type instruction.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r3: 00011
>   - rs1 = r2: 00010
>   - funct3: 000
>   - rd = r1 = 00001
>   - Opcode: 0110011

32 bit instruction: `0000000_00011_00010_000_00001_0110011`

---

```
SUB r3, r1, r2
```
> * This is a R-Type instruction.
> * From the image in R-Type sub block, we can see:
>   - func7: 0100000
>   - rs2 = r2: 00010
>   - rs1 = r1: 00001
>   - funct3: 000
>   - rd = r3 = 00011
>   - Opcode: 0110011

32 bit instruction: `0100000_00010_00001_000_00011_0110011`

---

```
AND r2, r1, r3
```
> * This is a R-Type instruction.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r3: 00011
>   - rs1 = r1: 00001
>   - funct3: 111
>   - rd = r2 = 00010
>   - Opcode: 0110011

32 bit instruction: `0000000_00011_00001_111_00010_0110011`

---

```
OR r8, r2, r5
```
> * This is a R-Type instruction.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r5: 00101
>   - rs1 = r2: 00010
>   - funct3: 110
>   - rd = r8 = 01000
>   - Opcode: 0110011

32 bit instruction: `0000000_00101_00010_110_01000_0110011`

---

```
XOR r8, r1, r4
```
> * This is a R-Type instruction.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r4: 00100
>   - rs1 = r1: 00001
>   - funct3: 100
>   - rd = r8 = 01000
>   - Opcode: 0110011

32 bit instruction: `0000000_00100_00001_100_01000_0110011`

---

```
SLT r10, r2, r4
```
> * This is a R-Type instruction.
> * SLT means Set if Less Than.
> * r10 is the destination register that sets to 1, if r2 is less than r4, else 0 if r2 is greater than r4.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r4: 00100
>   - rs1 = r1: 00010
>   - funct3: 010
>   - rd = r10 = 01010
>   - Opcode: 0110011

32 bit instruction: `0000000_00100_00010_010_01010_0110011`

---

```
ADDI r12, r3, 5
```
> * This is an I-Type instruction.
> * From the image in I-Type sub block, we can see:
>   - imm[11:0] = 5: 000000001001 
>   - rs1 = r3: 00011
>   - funct3: 000
>   - rd = r12 = 01100
>   - Opcode: 0010011

32 bit instruction: `000000001001_00011_000_01100_0010011`

---

```
SW r3, r1, 4
```
> * This is a S-Type instruction.
> * r3 is the source register. This instruction will store the value located in register r1 at the address obtained by adding the immediate value 4 with the address located in register r1.
> * From the image in S-Type sub block, we can see:
>   - imm[11:5]: 0000000
>   - rs2 = r3: 00011
>   - rs1 = r1: 00001
>   - funct3: 010
>   - imm[4:0]: 00100
>   - Opcode: 0100011

32 bit instruction: `0000000_00011_00001_010_00100_0100011`

---

```
SRL r16, r11, r2
```
> * This is a R-Type instruction.
> * SRL means Logical Shift Right.
> * r16 is the destination register, in which the value stored in r11 will be written after performing logical right shift based on the number stored in r2.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r2: 00010 
>   - rs1 = r11: 01011
>   - funct3: 101
>   - rd = r16 = 10000
>   - Opcode: 0110011

32 bit instruction: `0000000_00010_01011_101_10000_0110011`

---

```
BNE r0, r1, 20
```
> * This is a B-Type instruction.
> * BNE means Branch if Not Equal.
> * Here BNE specifies the condition that the value stored in r0 != (is not equal to) the value stored in r1. If the condition becomes true, Program Counter will be updated by PC + 20, else PC + 4 for next instruction.
> * From the image in B-Type sub block, we can see:
>   - imm[12|10:5]:0000001
>   - rs2 = r1: 00001 
>   - rs1 = r0: 00000
>   - funct3: 001
>   - imm[4:1|11]: 01000
>   - Opcode: 1100011

32 bit instruction: `0000001_00001_00000_001_01000_1100011`

---

```
BEQ r0, r0, 15
```
> * This is a B-Type instruction.
> * BEQ means Branch if Equal.
> * Here BEQ specifies the condition that the value stored in r0 == (is equal to) the value stored in r0. If the condition becomes true, Program Counter will be updated by PC + 15, else PC + 4 for next instruction.
> * From the image in B-Type sub block, we can see:
>   - imm[12|10:5]:0000000
>   - rs2 = r0: 00000 
>   - rs1 = r0: 00000
>   - funct3: 000
>   - imm[4:1|11]: 11110
>   - Opcode: 1100011

32 bit instruction: `0000000_00000_00000_000_11110_1100011`

---

```
LW r13, r11, 2
```
> * This is a I-Type instruction.
> * LW means Load Word.
> * r13 is the destination register that will hold the value fetched from the memory location calculated by using (address value stored in r11 + immediate value)
> * From the image in I-Type sub block, we can see:
>   - imm[11:0] = 2: 000000000010 
>   - rs1 = r11: 01011
>   - funct3: 010
>   - rd = r13 = 01101
>   - Opcode: 0000011

32 bit instruction: `000000000010_01011_010_01101_0000011`

---

```
SLL r15, r11, r2
```
> * This is a R-Type instruction.
> * SLL means Logical Shift Left.
> * r15 is the destination register, in which the value stored in r11 will be written after performing logical left shift based on the number stored in r2.
> * From the image in R-Type sub block, we can see:
>   - func7: 0000000
>   - rs2 = r2: 00010 
>   - rs1 = r11: 01011
>   - funct3: 001
>   - rd = r15 = 01111
>   - Opcode: 0110011

32 bit instruction: `0000000_00010_01011_001_01111_0110011`

## Task 4 Complete.

</details>
 

