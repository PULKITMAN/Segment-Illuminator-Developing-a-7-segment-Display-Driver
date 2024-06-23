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
