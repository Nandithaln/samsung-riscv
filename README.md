# samsung-riscv
RISC-V Talent Development Program 2025 ,powered by Samsung Semiconductor Research India(SSIR) along with VLSI System Design(VSD)
## DETAILS
**Name:** Nanditha LN 

**College:** S J B Institute Of Technology 

**Email-ID:** nandithaln03@gmail.com 

-----------------------------------------------------------------------------------------------------------------------------------------------------------

<details>
<summary
>
  <b>Task 1</b> :
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

<details>
<summary>
<b>Task 2:</b> This task is to compile a new simple C program and collect the RISC-V object dump using both -O1 and -Ofast </summary>

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

<details>
<summary>
<b>Task 3 : </b> the third task is To identify **15 unique RISC-V instructions and determine the 32-bit instruction** code</summary>

RISC-V (Reduced Instruction Set Computer - Version 5) is an open, free instruction set architecture (ISA) that follows the RISC principles. It was designed to be simple, clean, and extensible, making it suitable for a wide range of computing applications.

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
     
**Example:** ```add``` instruction adds two registers and stores the result in a third register.

### 2. I-Type/Immediate type 
* Used for operations that involve an immediate value (constant).

      [imm[11:0] | rs1 | funct3 | rd | opcode]
        12bit     5bit   3bit    5bit  7bit

    * **imm[11:0]:** 12 bits immediate value (constant).
    * **rs1:** 5 bits specifying the source register.
    * **funct3:** 3 bits specifying the operation.
    * **rd:** 5 bits specifying the destination register.
    * **opcode:** 7 bits specifying the operation.
      
  **Example:** ```addi``` adds an immediate value to a register.

### 3. S-Type/Store type
  * Used for store instructions that write data from a register to memory.

        [imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | opcode]
           7bit      5bit   5bit   3bit    5bit       7bit   

     * **imm[11:5]:** 7 bits of the immediate value.
     * **rs2:** 5 bits specifying the source register (data to be stored).
     * **rs1:** 5 bits specifying the base register (address for storing).
     * **funct3:** 3 bits specifying the store operation.
     * **imm[4:0]:** 5 bits of the immediate value.
     * **opcode:** 7 bits specifying the store instruction.

Example: ```sw``` stores a word (32 bits) from a register to memory.

 ### 4. B-Type/Branch type 
  * Used for conditional branch instructions.
 
        [imm[12] | imm[10:5] | rs2 | rs1 | funct3 | imm[4:1] | imm[11] | opcode]

      * **imm:** 12 bits immediate value that represents the offset for the branch.
      * **rs2:** 5 bits specifying the second register (used for comparison).
      * **rs1:** 5 bits specifying the first register (used for comparison).
      * **funct3:** 3 bits specifying the branch condition (e.g., equal, not equal).
      * **opcode:** 7 bits specifying the branch instruction.
        
**Example:** ```beq``` branches if two registers are equal.

### 5. U-Type/Upper-immediate type
* Used for instructions that need a large immediate value (used for loading constants).

       [imm[31:12] | rd | opcode]

  * **imm[31:12]:** 20 bits of the immediate value (upper part of the immediate).
  * **rd:** 5 bits specifying the destination register.
  * **opcode:** 7 bits specifying the operation.
    
**Example:** ```lui``` loads an immediate value into the upper 20 bits of a register.

### 6. J-Type/Jump type
* Used for jump instructions that use a large offset.

       [imm[20] | imm[10:1] | imm[11] | imm[19:12] | rd | opcode]

    * **imm:** 21 bits immediate value that specifies the jump target.
    * **rd:** 5 bits (usually unused in jump instructions).
    * **opcode:** 7 bits specifying the jump operation.

***Example:** ```jal``` performs a jump and link.


### **1. `addi` - Add Immediate** (for initializing `temp = 0`)
- **Format Type**: **I-type**
  - **Explanation**: The `addi` instruction adds an immediate value to a register.
- **32-bit Binary**:  
  `000000000000 | 00000 | 000 | 01000 | 0010011`
  - This corresponds to `addi x8, x0, 0`.

### **2. `lw` - Load Word** (loading `num` from memory)
- **Format Type**: **I-type**
  - **Explanation**: Loads a word from memory into a register.
- **32-bit Binary**:  
  `000000000000 | 00000 | 010 | 00001 | 0000011`
  - This corresponds to `lw x1, 0(x0)` (assuming `num` is stored at address 0).

### **3. `addi` - Add Immediate** (setting loop index `i = 2`)
- **Format Type**: **I-type**
  - **Explanation**: Adds immediate value to the register for the loop variable `i = 2`.
- **32-bit Binary**:  
  `000000000010 | 00000 | 000 | 00010 | 0010011`
  - This corresponds to `addi x2, x0, 2`.

### **4. `div` - Division** (for `num / 2` in the for loop)
- **Format Type**: **R-type**
  - **Explanation**: Divides the contents of two registers (`num` and `2`).
- **32-bit Binary**:  
  `0000001 | 00001 | 00010 | 000 | 0110011`
  - This corresponds to `div x3, x1, x2`.

### **5. `blt` - Branch if Less Than** (for checking if `i <= num / 2`)
- **Format Type**: **B-type**
  - **Explanation**: Branches if `x3 < x2`, checking loop condition.
- **32-bit Binary**:  
  `0000000 | 00010 | 00001 | 100 | 0000000 | 0000 | 0 | 1100011`
  - This corresponds to `blt x3, x2, end_loop`.

### **6. `rem` - Remainder** (for `num % i`)
- **Format Type**: **R-type**
  - **Explanation**: Computes the remainder when dividing `num` by `i`.
- **32-bit Binary**:  
  `0000001 | 00001 | 00010 | 100 | 0110011`
  - This corresponds to `rem x4, x1, x2`.

### **7. `beq` - Branch if Equal** (for `num % i == 0`)
- **Format Type**: **B-type**
  - **Explanation**: Branches if `x4 == x0`, i.e., when `num % i == 0`.
- **32-bit Binary**:  
  `0000000 | 00000 | 00001 | 000 | 0000000 | 0000 | 0 | 1100011`
  - This corresponds to `beq x4, x0, next`.

### **8. `addi` - Add Immediate** (for `temp++`)
- **Format Type**: **I-type**
  - **Explanation**: Adds immediate value to `temp` (incrementing it).
- **32-bit Binary**:  
  `000000000001 | 01000 | 000 | 00101 | 0010011`
  - This corresponds to `addi x5, x8, 1`.

### **9. `bne` - Branch if Not Equal** (for checking if `temp != 0`)
- **Format Type**: **B-type**
  - **Explanation**: Branches if `temp != 0`.
- **32-bit Binary**:  
  `0000000 | 00001 | 00001 | 001 | 0000010 | 0000 | 0 | 1100011`
  - This corresponds to `bne x5, x0, prime_not_prime`.

### **10. `jal` - Jump and Link** (for prime check: jump to print "prime")
- **Format Type**: **J-type**
  - **Explanation**: Jumps to a specified address and saves the return address in a register.
- **32-bit Binary**:  
  `000000000000 | 00010 | 0110111`
  - This corresponds to `jal x2, print_prime`.

### **11. `addi` - Add Immediate** (return 0, `temp = 0`)
- **Format Type**: **I-type**
  - **Explanation**: Add immediate value to register for the return value.
- **32-bit Binary**:  
  `000000000000 | 00000 | 000 | 01010 | 0010011`
  - This corresponds to `addi x10, x0, 0`.

### **12. `sw` - Store Word** (store the value of `num` for printing)
- **Format Type**: **S-type**
  - **Explanation**: Stores a word from a register to memory.
- **32-bit Binary**:  
  `0000000 | 00011 | 00001 | 010 | 00000 | 0100011`
  - This corresponds to `sw x1, 0(x3)`.

### **13. `lui` - Load Upper Immediate** (set up `x2` register with high immediate value)
- **Format Type**: **U-type**
  - **Explanation**: Loads a 20-bit immediate into the upper 20 bits of a register.
- **32-bit Binary**:  
  `000000000000 | 00010 | 0110111`
  - This corresponds to `lui x2, 0`.

### **14. `xori` - Exclusive OR Immediate** (for bitwise manipulation, if applicable)
- **Format Type**: **I-type**
  - **Explanation**: Performs bitwise XOR between a register and an immediate value.
- **32-bit Binary**:  
  `000000000000 | 00001 | 100 | 00010 | 0010011`
  - This corresponds to `xori x2, x1, 0`.

### **15. `and` - Bitwise AND** (for masking or setting flags)
- **Format Type**: **R-type**
  - **Explanation**: Performs a bitwise AND operation between two registers.
- **32-bit Binary**:  
  `00001 | 00010 | 00000 | 00000 | 0110011`
  - This corresponds to `and x2, x3, x0`.

---

<details>
<summary>
<b>Task 4:</b> the Task 4 is to perform a functional simulation of the given RISC-V Core Verilog netlist and testbench </summary>


**Step 1:**
   * To download the Verilog netlist and test bench from the reference GitHub repository https://github.com/vinayrayapati/rv32i
   * We are downloading the file because the designing of RISC-V architecture and writing its testbench is not a part of this internship.

 **Step 2:**
  * Install the suitable simulation tool that is ```iverilog``` and ```gtkwave```
  * To install them use the foloowing command
    ```
    $ istall apt iverilog
    $ install apt gtkwave
    ```
    **Step 3:**
     * To run and simulate use the foloowing command
       ```
       $ iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
       ```
     * This will create the vcd file

**Step 4:**
 * To see the waveform in gtkwave use the following command use the vcd file created earlier
   ```
   $ gtkwave iiitb_rv32i.vcd
   ```

**Step 5:**
 * Analyze the output waveform.
 * The bit pattern will not match the instruction found in Task 3
 * **O1 ≠ O2**

**1. ```Add R6, R2, R1```**

 *  A=1
 *  B=2
 *  The out put is 3 as the command ```Add``` adds the given inputs
 *  32 bit --> 02208300
   
![Add](https://github.com/user-attachments/assets/0818f8d0-3744-4469-81f3-50d591093e30)

 **2. ```ADDI R12, R4, 5```**

  * A=4
  * B=5
  * Output is 9 it adds the number with the immediate value
  * 32 bit --> 00520600
 
 ![addi](https://github.com/user-attachments/assets/65a51888-7f63-4829-95cb-9bf7c4d98ca7)

 **3.```AND R8, R1, R3```**

 * A=3
 * B=1
 * Output is 1 [ 3&1 = 1]
 * 32 bit --> 0230A400

 ![and](https://github.com/user-attachments/assets/1e7dd2e2-f149-4a65-b929-364efcb4f6c0)

 **4.```BEQ R0, R0, 15```**

 * Value stored= 0
 * incremented by 15=25
 * 32 bit --> 00F0002
 
![beq](https://github.com/user-attachments/assets/0bc9f531-5edb-4e94-b3e8-a83bd44e3674)

**5.```BNE R0, R1, 20```**

 * Checks both the value stored
 * if not equal increments by 20 = 46
 * 32 bit --> 01409002

![bne](https://github.com/user-attachments/assets/0ea6f2f1-f145-43a7-9596-c2a37e82e720)

**6.```OR R9, R2, R5```**

 * A=2
 * B=5
 * Output is 7
 * 32 bit --> 02513480

![or](https://github.com/user-attachments/assets/8b569d45-f71b-496a-a91e-9f8293bf964f)

**7.```SLL R15, R1, R2```**

 * The output is 4
 * this operator shifts 1 as the value is 2 001 is shifted to 100
 * 32 bit --> 2131843

![sll](https://github.com/user-attachments/assets/34e2e0fc-2639-4aa8-9685-5b45a66f2823)

**8.```SLT R1, R2, R4```**

 * Compares the stored value if true 1 else 0
 * 2 and 4 -- 2 < 4 hence 1
 * 32 bit --> 02415580

![slt](https://github.com/user-attachments/assets/2c58ca8d-3f57-457b-8f59-fc5d2683d6d2)

**9.```SUB R7, R1, R2```**

 * This operator or intsruction substracts the 2 stored value
 * A=1
 * B=2
 * A-B = 1-2 = -1
 * 32 bit --> 02209380
 
![sub](https://github.com/user-attachments/assets/ea0531eb-3a77-4cc5-9764-65b4d31c7c32)

**10.```XOR R10, R1, R4```**

 * It performs bitwise XOR function
 * A=1
 * B=5
 * output is 5
 * 32 bit --> 0240C500

![xor](https://github.com/user-attachments/assets/235de2a8-3f3f-446e-a00c-a4550e36ded7)

---

<details>
<summary>
<b>Task 5:</b> This task is to add project name with brief overview and components required </summary>
    
### Overview

This project adds a 16x2 LCD display to the digital lock system to show user-friendly messages. The system accepts input via push buttons to form a "password," compares it with a predefined code, and provides feedback on the LCD. If the password is correct, an LED or buzzer activates to indicate success. If incorrect, an error message appears, and the lock remains closed.


### Components required 

 * VSDSquadron Board: The RISC-V-based development board for running the code.
 * 16x2 LCD Display: To display messages like "Enter Password" or "Access Denied."
 * Push Buttons (3 or more): Used for entering the password.
 * Resistors:
     * Pull-up resistors for the push buttons.
     * 220-ohm resistors for LEDs.
 * LEDs:
   * One LED to indicate "Unlock."
   * Optionally, another LED for "Lock."
 * Buzzer (optional): Provides an audible alert on success.
 * Potentiometer (10k ohm): Adjusts the LCD screen's contrast.
 * Wires and Breadboard: For connections.

### Circuit Connection For Digital Lock System

  * Connect one terminal of each button to a GPIO pin
  * The other terminal of each button connects to GND.
  * Add pull-up resistors (10k ohm) to each GPIO pin to ensure stable input readings.
  * Unlock LED:
      * Connect the positive leg (anode) to GPIO_5.
      * Connect the negative leg (cathode) to GND through a 220-ohm resistor.
  * Connect the I2C module's:
       * SCL → GPIO_8
       * SDA → GPIO_9
       * VCC → 5V
       * GND → GND

### Pinout diagram 

   | **Component**        | **GPIO Pin**     | **Description**                   |
|----------------------|------------------|-----------------------------------|
| **Button 1**         | GPIO_0           | Input for first digit (Button 1)  |
| **Button 2**         | GPIO_1           | Input for second digit (Button 2) |
| **Button 3**         | GPIO_2           | Input for third digit (Button 3)  |
| **Lock LED**         | GPIO_5           | LED lights up when password is incorrect |
| **Buzzer**           | GPIO_7           | Provides sound feedback for correct password |
| **LCD SDA (Data)**   | GPIO_8           | I2C data line for LCD             |
| **LCD SCL (Clock)**  | GPIO_9           | I2C clock line for LCD            |
| **VCC**              | VCC (3.3V or 5V) | Power supply for components       |
| **GND**              | GND              | Ground connection for components |







