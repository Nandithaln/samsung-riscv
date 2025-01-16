# samsung-riscv
RISC-V Talent Development Program 2025 ,powered by Samsung Semiconductor Research India(SSIR) along with VLSI System Design(VSD)
## DETAILS
**Name:** Nanditha LN 

**College:** S J B Institute Of Technology 

**Email-ID:** nandithaln03@gmail.com 

-----------------------------------------------------------------------------------------------------------------------------------------------------------

<detail>
<summary>
  <b>Task 1 :</b>
  The given task is to install RISC-V toolchain using VDI link by following the steps mentioned in the shared pdf and compile a simple c program referring the lab vedio 
</summary> 

### What is RISC-V Toolchain?
> The RISC-V toolchain comprises the assembler, compiler, linker, and debugger, each playing a critical role in developing and debugging software for RISC-V microcontrollers. Understanding how these components work together empowers developers to write efficient code, leverage existing libraries, and debug their applications effectively. By harnessing the power of the RISC-V toolchain, developers can unlock the full potential of this open-source instruction set architecture.
> 
**1. Compiling a simple C program to find the sum from 1 to n**

![Sum1ton(C lab)](https://github.com/user-attachments/assets/ba20856e-fd95-45c2-9412-59f3a7791c21)

**2. O1 command and object dump**

### What is Object Dump?
>Objdump provides the address, the encoding, and the mnemonics. RISC-V objdump will work on any binary that contains RISC-V code. That includes executables, object files, and shared libraries.
>

Code for O1:

```
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
$ riscv64-unknown-elf-objdump -d sum1ton.o
```

![Cat command](https://github.com/user-attachments/assets/5118a693-c2ef-4bcb-9e99-ee57b94360ea)

![objdump](https://github.com/user-attachments/assets/8fdb3eba-d04a-49f6-a742-799e6d5f8d6d)

The main section is found in the object dump 

![objdump main section](https://github.com/user-attachments/assets/98b32a57-bf34-4a5d-808e-20ae755f2a8c)

**3. To find object dump using Ofast command**

Code:

```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
$ riscv-unknown-elf-objdump -d sum1ton.o
```
Here d stands for dis assemble 
![objectdump using Ofast](https://github.com/user-attachments/assets/e3e26e37-ff7e-4d3c-847d-c1d508b9d468)

--------------------------------------------------------------------------------------------------------------------------------------------------

<summary><b>Task 2:</b> This task is to compile a new simple C program and collect the RISC-V object dump using both -O1 and -Ofast </summary>

Program to find whether the entered number is prime number or not:
```
#include<stdio.h>
int main()
{
  int i,num,temp=0;
  printf("Enter a number");
  scanf("%d",&num);
  for(i=2;i<=num/2;i++)
  {
    if(num%i==0)
    {
     temp++;
     break;
     }
  }
  if(temp==0&&num!=1)
  {
   printf("%d is a prime number\n",num)
  }
  else
  {
   printf("%d is not a prime number\n",num)
  }
  return 0;
}
```
**The related files are attached below**
![prime c and output](https://github.com/user-attachments/assets/3a8c6706-fa53-41d4-ba40-9fc8c0e65a59)

### What is spike command?
>spike command is similar to the ```./a.out``` command where it is used to see the output but spike is used to see output in riscv simulator. The output produced is same as the a.out command.

``` spike pk prime.c```


**To find the ```objdump``` the procedure is similar to the previous task given where we run the program for sum1ton.c**

![output using spike](https://github.com/user-attachments/assets/df091ccd-e227-4504-b2c5-af8cf6beae2c)

![O1](https://github.com/user-attachments/assets/fc5ead42-208e-42ae-b286-993d5cf060ae)

![O1 obj](https://github.com/user-attachments/assets/fb002211-fcb3-452d-8421-80c7249218d4)

![Ofast](https://github.com/user-attachments/assets/cb3cc93b-3282-4a67-9ace-def8613d0277)

![Ofast obj](https://github.com/user-attachments/assets/ec740678-18c0-416f-b4e9-d10a38fc2bdc)

**To find the contents present in the main section or any other section the following code is used where lui stands for ***load upper immediate*****

```
spike -d pk prime.o

```

![load upper immediate](https://github.com/user-attachments/assets/96d1529f-d773-4685-88e6-8a22a20edfd3)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<summary><b>Task 3 : </b> the third task is To identify **15 unique RISC-V instructions and determine the 32-bit instruction** code</summary>

RISC-V (Reduced Instruction Set Computer - Version 5) is an open, free instruction set architecture (ISA) that follows the RISC principles. It was designed to be simple, clean, and extensible, making it suitable for a wide range of computing applications. Here's a breakdown of some key concepts about RISC-V instructions:

**1. Instruction Set**

**Base ISA:** RISC-V has a small, fixed set of base instructions. The simplest one is RV32I, which is a 32-bit integer base ISA. There's also RV64I for 64-bit systems.

**Extensions:** RISC-V is modular, with optional extensions like M (integer multiplication and division), A (atomic instructions), F (single-precision floating point), D (double-precision floating point), etc.

**Custom Extensions:** Users can define their custom extensions while keeping compatibility with the base ISA.


**2. Instruction Formats**

**Fixed-Length:** All instructions are 32 bits long (with some optional 16-bit compressed instructions for efficiency).
Formats: RISC-V has several instruction formats like R-type (Register), I-type (Immediate), S-type (Store), B-type (Branch), U-type (Upper Immediate), and J-type (Jump).

**3. Load/Store Architecture**
RISC-V follows the load/store architecture, meaning that it can only perform arithmetic operations on registers, not directly on memory. Data must first be loaded into registers, manipulated, and then stored back to memory if needed.

**4. Simplicity and Regularity**
Instructions have a consistent format, which simplifies decoding and execution.
There are fewer instructions compared to CISC (Complex Instruction Set Computer) architectures, making RISC-V simpler to implement in hardware.


**5. Advantages of RISC-V**

***Open Standard:*** It's not bound by proprietary rights, making it widely accessible for research, teaching, and industry.

***Scalability:*** Can be used in a wide range of devices from tiny embedded systems to powerful supercomputers.

***Efficiency:*** The simplicity and modularity often lead to better performance and energy efficiency.

**Step 1:** Create prime.o file 

### Why covert the c file to object file?
> The ```gcc``` compiler translates source code to machine code but in object file . The object file is a binary file that contains the machine code for the compiled source code, along with information about external symbols (functions or variables defined in other files).

Code:
```
$ cat prime.c
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o prime.o prime.c
$ ls -ltr
```

**Step 2:** Get the ```objdump``` for the object file and navigate to the ```main``` section 

Code:
```
$ risvc64-unknown-elf-objdump -d prime.o
```

**Step 3:** Identify the instruction format 

### RISC-V Instruction formats

In RISC-V, an instruction format refers to the layout or structure of an instruction in memory, defining how the binary representation of the instruction is split into various fields. Each field specifies different parts of the operation, like the opcode, registers, immediate values, etc.

RISC-V instructions are fixed-length (32 bits) and follow a few primary formats, each serving a different type of instruction (arithmetic, load/store, branching, etc.).

### Types of Instruction Format 

* **R-Type** - Register type
* **I-Type** - Immediate type
* **S-Type** - Store type
* **B-Type** - Branch type
* **U-Type** - Upper-intermmediate type
* **J-Type** - Jump type

### 1. R-Type/Register type
* Used for arithmetic and logical instructions that operate on registers.

      [funct7 | rs2 | rs1 | funct3 | rd | opcode]
        7bit   5bit  5bit    3bit    5bit  7bit 

   * **funct7:** 7 bits that specify the operation's variant.
   * **rs2:** 5 bits specifying the second source register.
   * **rs1:** 5 bits specifying the first source register.
   * **funct3:** 3 bits specifying the operation (e.g., add, sub, etc.).
   * **rd:** 5 bits specifying the destination register where the result will be stored.
   * **opcode:** 7 bits specifying the operation (e.g., arithmetic operation, logical operation).
     
**Example:** add instruction adds two registers and stores the result in a third register.
 
