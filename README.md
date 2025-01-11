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
$ riscv-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
$ riscv-unknown-elf-objdump -d sum1ton.o
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



