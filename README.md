# *Asic-design-class*
## *Task 1*: To compile c code using gcc:
  A c program to calculate the sum of n number was written and was compiled with gcc with the following command:
  
    `gcc -o sum1ton sum1ton.c`

![Screenshot 2024-07-17 160519](https://github.com/user-attachments/assets/f78e0c67-dc60-4f7a-a147-65d616c36c90)

After that `./sum1ton.o ` command was used to print the output.



![Screenshot 2024-07-29 204414](https://github.com/user-attachments/assets/055ac52b-72ba-4a90-a241-1e2400c940c5)



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


![Screenshot 2024-07-29 204146](https://github.com/user-attachments/assets/45049e12-4531-412d-93e4-a0e10936e18b)


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
| SLL r15, r11, r2     | 0x000259B3                 |

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

The verilog code was edited to process the above commands as shown below:

![Screenshot 2024-07-29 203739](https://github.com/user-attachments/assets/3d5100cb-ef54-43dd-94a0-2cb31629d040)



In order to plot the wave we use the gtkwave software with the following command:
`iiitb_rv32.vcd`

The output of each instruction is shown in the images below:

# **Note : We can notice some discrepency the above two images as the verilog code availabe is not designed in agreement to the ISA used to by us in the first program.**

```ADD r5, r6, r7```

The waveform for the above command using the provided verilog code is given below:
![Screenshot 2024-07-28 184830](https://github.com/user-attachments/assets/a1281f18-4ded-402e-9558-632fb2b14d12)


The waveform for the hardcoded command present in the code is given below:


![Screenshot 2024-07-24 134229](https://github.com/user-attachments/assets/0b4f832c-e13e-4b8c-8531-a7def4689610)



```SUB r7, r5, r6	```

The waveform for the above command using the provided verilog code is given below:

![Screenshot 2024-07-28 184853](https://github.com/user-attachments/assets/f2e4b21b-2812-46ec-8de9-6c83816dd82a)




The waveform for the hardcoded command present in the code is given below:


![Screenshot 2024-07-24 134655](https://github.com/user-attachments/assets/cf028489-8cb2-463c-b206-3a5498551384)


```AND r6, r5, r7```

The waveformk for the above command using the provided verilog code is given below:

![Screenshot 2024-07-28 184922](https://github.com/user-attachments/assets/6e581217-412d-48fc-8894-4aa621d07733)


The waveform for the hardcoded command is given below:

![Screenshot 2024-07-24 134711](https://github.com/user-attachments/assets/b73d7c4b-994c-4bca-88af-d9641f4e3ff8)

```OR r8, r6, r5```
The waveform for the above command using the provided verilog code is given below:


![Screenshot 2024-07-27 210534](https://github.com/user-attachments/assets/b0e8e892-e2da-4087-8994-ae67e21256fa)

The waveform for the hardcoded command is given below:

![Screenshot 2024-07-24 134728](https://github.com/user-attachments/assets/437b2dd2-c29b-4fcb-b9e0-d501fc005695)


```XOR r8, r5, r4```

The wave form for the above command is shown below:

![Screenshot 2024-07-27 210612](https://github.com/user-attachments/assets/8c42e1a7-b6e1-44e9-a0ae-1e869a8ce1ba)

The waveform for the harcoded instruction is given below:


![Screenshot 2024-07-24 134742](https://github.com/user-attachments/assets/9844c7e7-48ac-4aa6-8fe4-3e0629e2befc)


```SLT r10, r2, r4```

The waveform for the above code is shown below:

![Screenshot 2024-07-27 210613](https://github.com/user-attachments/assets/3b7912b3-14af-48c1-81ca-83d70212b2e3)

The waveform for the hardcoded instruction is given below:


![Screenshot 2024-07-24 134756](https://github.com/user-attachments/assets/94bae452-5fea-4ee7-9f04-7d99e9b13ce0)




```ADDI r12, r3, 5```
The waveform for the above instruction is given below:

![Screenshot 2024-07-27 210833](https://github.com/user-attachments/assets/646d4b83-c4ef-4420-8f14-f2e352f6f2ff)

The waveform for the hardcoded instruction is shown below:

![Screenshot 2024-07-24 134835](https://github.com/user-attachments/assets/4f271e06-7fc9-45e5-9148-a7d45a050dcf)


```SW r3, r1, 4```

The waveform for the above code is given below:


![Screenshot 2024-07-27 210847](https://github.com/user-attachments/assets/df3689dd-55d3-4695-a8e1-7850bf42950d)

The waveform for the hardcoded instruction is shown below:

![Screenshot 2024-07-24 135001](https://github.com/user-attachments/assets/07bc87a7-400e-46c3-bb35-adc69dc8c95c)




```SRL r16, r11, r2```

The waveform for the above code is given below:

![Screenshot 2024-07-27 210916](https://github.com/user-attachments/assets/30353054-7224-4891-82be-1dd08e1a2be6)

The waveform for the hardcoded instruction is shown below:

![Screenshot 2024-07-24 134916](https://github.com/user-attachments/assets/03488efd-20e2-4923-aff9-54002b53f7ea)




```BNE r0, r1, 20```


The waveform for the above code is given below:

![Screenshot 2024-07-27 210942](https://github.com/user-attachments/assets/805253cd-aa5d-44f9-81b0-f9067f9af6db)


The waveform for the hardcoded instruction is given below:

![Screenshot 2024-07-24 134938](https://github.com/user-attachments/assets/761978e0-af5e-4984-840b-368d3a13d7f0)



```BEQ r0, r0, 15```

The waveform for the above code is given below:

![Screenshot 2024-07-27 211010](https://github.com/user-attachments/assets/015f16dc-6ae9-4f19-8c18-7f9b3f4fd522)






```LW r13, r11, 2```

The waveform for the above code is given below:

![Screenshot 2024-07-28 190449](https://github.com/user-attachments/assets/fd9a0283-ef1e-4bd6-93bd-acbcbeb88e50)

```SLL r15, r11, r2 ```
# Note: This command was not executed because the verilog code did not had enough memory spaces for this command and the compiler showed this output of ignoring the last memory register.

![image](https://github.com/user-attachments/assets/1a3b0aeb-f598-4231-ace4-40cf6bcb9fc1)






