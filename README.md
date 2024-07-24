# *Asic-design-class*
## *Task 1*: To compile c code using gcc:
  A c program to calculate the sum of n number was written and was compiled with gcc with the following command:
  
    `gcc -o sum1ton sum1ton.c`

![Screenshot 2024-07-17 160519](https://github.com/user-attachments/assets/f78e0c67-dc60-4f7a-a147-65d616c36c90)

After that `./sum1ton.o ` command was used to print the output.



![Screenshot 2024-07-16 171156](https://github.com/user-attachments/assets/69a193ba-bee9-4067-8827-334c3cd42431)



## *Task 2*: To compile the same c code using RiscV gcc:
  The same c program was then compiled using RiscV gcc with the following command:
  
    `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

  After that, the following command is used to dump the assembly code in terminal:
  
  `riscv64-unknown-elf-objdump -d sum1ton.o | less` 

  
  
![Asic_Design_Task2](https://github.com/user-attachments/assets/1ec2ac62-58e8-4abd-bfac-4732a1a72a64)


## *Task 3*: To run the RISCV executable created above using the riscV compiler.

The same c program that was created above and compiled usingt the RISCV complier was run using the following command :

`spike pk sum1ton.o`

The output is shown below:


![Screenshot 2024-07-21 153539](https://github.com/user-attachments/assets/5d17e020-073f-41a9-a9d4-acc5d0fbc9bf)


## *Task 4*: To debug each line of the main and check its validity by manually comparing the output of that instruction and the value stored in the register used to store the value of that particular instruction.

The debugging includes these steps:

### Step 1: To run the riscV executable file the following command was used:

`spike pk sum1ton.o`

### Step 2: To verify whether gcc output and riscV output are same.

### Step 3: To the debugging mode of that file using the following command:

`spike -d pk sum1ton.o`

### Step 4: Then we get the program counter to point to the first line of the main function using this command :

`until pc 0 "address of first instruction" `

The address of the first instruction of main can be looked in objdump file as shown below, which in this case is 10184.


![Screenshot 2024-07-21 152915](https://github.com/user-attachments/assets/590019f9-339e-4337-8a4b-6556b00b1cbc)



Step 5: After that we use the `reg 0 'name of the register' ` command to check the current value stored in that register and compare it to the theoritcally calculated value.

For example : In the below snapshot the value of register A0 after the modification in the program should be = 0x21100   which is same as the value calculated by the instruction.

![Screenshot 2024-07-21 152830](https://github.com/user-attachments/assets/7eb3897e-b43d-496c-80c1-05d10424456d)

## *Task 5:*
To sort and organise a set of given instructions into their respective format type:

| Assembly Instruction | Instruction format |
|----------------------|----------------------------|
| ADD r5, r6, r7       | R                          |
| SUB r7, r5, r6       | R                          |
| AND r6, r5, r7       | R                          |
| OR r8, r6, r5        | R                          |
| XOR r8, r5, r4       | R                          |
| SLT r10, r2, r4      | R                          |
| ADDI r12, r3, 5      | I                          |
| SW r3, r1, 4         | S                          |
| SRL r16, r11, r2     | R                          |
| BNE r0, r1, 20       | B                          |
| BEQ r0, r0, 15       | B                          |
| LW r13, r11, 2       | I                          |
| SLL r15, r11, r2     | R                          |

The corresponding RISCV ISA fo the above instructions is shown in the table below:


| Assembly Instruction | Hexadecimal Representation |
|----------------------|----------------------------|
| ADD r5, r6, r7       | 0x00D302B3                 |
| SUB r7, r5, r6       | 0x40B383B3                 |
| AND r6, r5, r7       | 0x00F2B333                 |
| OR r8, r6, r5        | 0x00D322B3                 |
| XOR r8, r5, r4       | 0x00C292B3                 |
| SLT r10, r2, r4      | 0x004122B3                 |
| ADDI r12, r3, 5      | 0x00518293                 |
| SW r3, r1, 4         | 0x00312023                 |
| SRL r16, r11, r2     | 0x002585B3                 |
| BNE r0, r1, 20       | 0x00112163                 |
| BEQ r0, r0, 15       | 0x000003E3                 |
| LW r13, r11, 2       | 0x002585B3                 |
| SLL r15, r11, r2     | 0x002585B3                 |

## *Task 6:* The task is to run some assembly instructions using a given verilog code for a riscV processor.

There is some variations in the ISA followed by RISCV and the hardcoded ISA for the below given instrucions. The differences are shown in the table below:

|Operation	     |Standard RISCV ISA	|Hardcoded ISA |
|----------------|--------------------|--------------|
|ADD R6, R2, R1	 |32'h00110333	      |32'h02208300  |
|SUB R7, R1, R2	 |32'h402083b3	      |32'h02209380  |
|AND R8, R1, R3	 |32'h0030f433	      |32'h0230a400  |
|OR R9, R2, R5	 |32'h005164b3	      |32'h02513480  |
|XOR R10, R1, R4 |32'h0040c533	      |32'h0240c500  |
|SLT R1, R2, R4	 |32'h0045a0b3	      |32'h02415580  |
|ADDI R12, R4, 5 |32'h004120b3	      |32'h00520600  |
|BEQ R0, R0, 15	 |32'h00000f63	      |32'h00f00002  |
|SW R3, R1, 2	   |32'h0030a123	      |32'h00209181  |
|LW R13, R1, 2	 |32'h0020a683	      |32'h00208681  |
|SRL R16, R14, R2|32'h0030a123	      |32'h00271803  |
|SLL R15, R1, R2 |32'h002097b3	      |32'h00208783  |

The following commands were used to run the verilog code:

`iverilog -o Test_code Test_code.v Test_code_tb.b`
`./Test_code`

The above commands run the verilog code in which the above mentioned instructions are hardcoded and the output vectors are dumped into a file with .vcd extension.

In order to plot the wave we use the gtkwave software with the following command:
`iiitb_rv32.vcd`

The output of each instruction is shown in the images below:
`ADD R6, R2, R1`
`SUB R7, R1, R2	`
`AND R8, R1, R3`
`OR R9, R2, R5`
`XOR R10, R1, R4`
`SLT R1, R2, R4`
`SLT R1, R2, R4`
`ADDI R12, R4, 5`
`BEQ R0, R0, 15`
`SW R3, R1, 2`
`LW R13, R1, 2`
`SRL R16, R14, R2`
`SLL R15, R1, R2`






