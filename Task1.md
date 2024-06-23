# Using a RISC-V simulator, write a C program to count the sum of all numbers from 1 to n.

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
