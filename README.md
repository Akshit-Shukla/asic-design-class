# *Asic-design-class*

<details>
<summary> Assignment 1</summary>
<br>

## *Task 1*: To compile c code using gcc:


  A c program to calculate the sum of n number was written and was compiled with gcc with the following command:
  
    `gcc -o sum1ton sum1ton.c`

![Screenshot 2024-07-17 160519](https://github.com/user-attachments/assets/f78e0c67-dc60-4f7a-a147-65d616c36c90)

After that `./sum1ton.o ` command was used to print the output.



![Screenshot 2024-07-29 204414](https://github.com/user-attachments/assets/055ac52b-72ba-4a90-a241-1e2400c940c5)

</details>

<details>
<summary> Assignment 2</summary>
<br>
## *Task 2*: To compile the same c code using RiscV gcc:
  The same c program was then compiled using RiscV gcc with the following command:
  
    `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

  After that, the following command is used to dump the assembly code in terminal:
  
  `riscv64-unknown-elf-objdump -d sum1ton.o | less` 

  
  
![Asic_Design_Task2](https://github.com/user-attachments/assets/1ec2ac62-58e8-4abd-bfac-4732a1a72a64)

</details>


<details>
<summary> Assignment 3</summary>
<br>
## *Task 3*: To run the RISCV executable created above using the riscV compiler in O1 and Ofast modes.

The same c program that was created above and compiled usingt the RISCV complier was run using the following command :

`spike pk sum1ton.o`

The output is shown below:

![Screenshot 2024-07-29 205712](https://github.com/user-attachments/assets/33c4f8d1-a419-473d-b1d9-25a6e2dbb978)


The same c program was then compiled using Ofast argument and the executable was run using spike command, as shown below:

![Screenshot 2024-07-29 205427](https://github.com/user-attachments/assets/c193a29e-845d-4270-b8ca-80fbd9060bec)


</details>

<details>
<summary> Assignment 4</summary>
<br>
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

</details>

<details>
<summary> Assignment 5</summary>
<br>
## *Task 5:*
To sort and organise a set of given instructions into their respective format type:

The Risc V instrucition are classified into the following types depending upon their architectures:

![Screenshot 2024-07-29 210135](https://github.com/user-attachments/assets/140a75b9-640b-4507-bfd2-62718c59fd3f)



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

</details>

<details>
<summary> Assignment 6</summary>
<br>
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

</details>

<details>
<summary> Assignment 7</summary>
<br>
## *Task 7:* The task is to write an Application in C, compile it with gcc and Risc-v gcc

**Application** : To perform convolution operation on an Image matrix with a blurring Kernel ( Image processing Application).

**Step 1** : The program to perform the applicaiton is shown below :


![Screenshot 2024-08-13 193642](https://github.com/user-attachments/assets/5be84c74-2714-4217-9098-14f6b92a3381)

**Step 2** : The program then compiled with the gcc is shown below:


![Screenshot 2024-08-13 193930](https://github.com/user-attachments/assets/c7ac3ecd-7c53-424c-9674-97b868e0a7a6)


**Step 3** : The program compiled with Risc-V gcc and run using "Spike command " is shown below:


![Screenshot 2024-08-13 190811](https://github.com/user-attachments/assets/f8fdbf63-6f53-46bd-90fa-91122478e5cc)

**Step 4 :** The Program was then run into the debugger mode as done previously is shown below:


![Screenshot 2024-08-13 191158](https://github.com/user-attachments/assets/c656cc2b-a490-47e6-8c54-244d5c31cdd7)


![Screenshot 2024-08-13 191653](https://github.com/user-attachments/assets/7b3f91d2-a7b0-428c-89d4-5b88c8011218)

</details>

<details>
<summary> Assignment 8</summary>
<br>

**Task:** To design a Baisc Risc-V processor core using TL-Verilog on Makerchip, MYTH Day 3_5 activities :

The variour parts of the code are shown below :

The generated Diagram is as shown below:


![Screenshot 2024-08-20 230431](https://github.com/user-attachments/assets/4d1b5e45-f439-4426-a76e-256526de441d)

The generated visual is as shown below:

![Screenshot 2024-08-21 100633](https://github.com/user-attachments/assets/7b75e567-6f16-4a13-bcf6-e36cb39af215)


Final Logs are shown below:

![Screenshot 2024-08-20 230551](https://github.com/user-attachments/assets/61b36c6f-2b49-45af-a2a3-51836c878f9a)

The test bench used for the verification of the result for the sample program is shown below:

![Screenshot 2024-08-20 230822](https://github.com/user-attachments/assets/711810a7-817b-4bf0-8ac3-e40d9d4022cf)

The signals including the "named clock : $clk_aks " is shown below :

![Screenshot 2024-08-20 230511](https://github.com/user-attachments/assets/ac948303-54d5-4eae-a0d9-a331feec960d)


The code segments are shown below:



![Screenshot 2024-08-20 231444](https://github.com/user-attachments/assets/5f4faef8-d76e-4d62-8a18-e30fea3b23ee)

![Screenshot 2024-08-20 231505](https://github.com/user-attachments/assets/036822db-8251-466b-9067-47247087e20d)

![Screenshot 2024-08-20 231523](https://github.com/user-attachments/assets/c2e2f40a-0ce0-4e66-8ac9-9303c4c55d28)

![Screenshot 2024-08-20 231539](https://github.com/user-attachments/assets/2796af0d-489c-42c1-aa7a-02bdb252b2c7)

![Screenshot 2024-08-20 231611](https://github.com/user-attachments/assets/d7bec662-2d1f-414f-bd5c-e84698637c98)

![Screenshot 2024-08-20 231631](https://github.com/user-attachments/assets/ff8f58cb-3aae-4397-abf5-81e9bb5732f3)

![Screenshot 2024-08-20 231657](https://github.com/user-attachments/assets/a176fa3d-efd3-403e-99c6-097a5f260227)

![Screenshot 2024-08-20 231711](https://github.com/user-attachments/assets/c68d7a68-213a-4af8-b548-4f09008c677d)

![Screenshot 2024-08-20 231722](https://github.com/user-attachments/assets/1130d1ea-a9fe-4b91-9a5a-3c0d3673b9fa)

![Screenshot 2024-08-20 231735](https://github.com/user-attachments/assets/06abaaf5-5a93-474a-ad25-d93d0f253362)

![Screenshot 2024-08-20 231747](https://github.com/user-attachments/assets/244522f0-049a-41f9-81aa-b2b4569e1776)


The waveforms for the `/xreg[14]` where the sum is being stored with each iteration is shown below:

![Screenshot 2024-08-21 101737](https://github.com/user-attachments/assets/2d7c5e9c-79a1-439c-b9c4-4bfb732c634b)

![Screenshot 2024-08-21 101757](https://github.com/user-attachments/assets/2592d947-6fc0-4d37-a1ba-f186981e47f7)

![Screenshot 2024-08-21 101818](https://github.com/user-attachments/assets/96384342-2812-4721-9592-9fd45e8817e5)

The final output after the loop ends and the testbecnch holds the data for 5 cycles is in the next image :

![Screenshot 2024-08-21 101837](https://github.com/user-attachments/assets/2c7673e2-661b-4352-a45c-e9e3ae0c8545)
















</details>

<details>
<summary> Assignment 9</summary>
<br>

**Task:** To convert the TL verilog code to Verilog code using Sandpiper, compile using Iverilog and plot the waveforms using GTKwave:

The command used to convert the code is given below:

![Screenshot 2024-08-26 222151](https://github.com/user-attachments/assets/869d5e45-730e-41f3-98fa-d484cb867316)

The generated verilog code is as shown below:

![Screenshot 2024-08-26 221716](https://github.com/user-attachments/assets/20e08120-25d7-4ecd-8b56-efbac5c6f0a2)

The command to compile the verilog code is as shown below:

![Screenshot 2024-08-26 222301](https://github.com/user-attachments/assets/05009fba-1825-47dd-a897-1ff33180a2ae)

The output waveform is as shown below including clk named CPU_clk_aks_a0 , reset and data :


![Screenshot_(134) 1](https://github.com/user-attachments/assets/4c3379c8-2273-42b6-a6e4-9170c2395e4c)

![Screenshot_(135) 1](https://github.com/user-attachments/assets/ba4bbf35-43e7-446e-8e2b-f1133c225ee4)


</details>

<details>
  <summary> Assignment 10 </summary>
  <br>
  **Task :** To generate waveform for DAC and PLL peripheral for Risc-V processor.

  The following commands were used to run out Risc-V core inside the VSDbabySoc and observe the ports of peripherals:
  ![Screenshot from 2024-08-31 17-37-52](https://github.com/user-attachments/assets/366b641e-4f09-43a0-a6ab-562a09fb16ba)




  Below is the output for the waveforms:

  Here, Vco_in is the input clk for the PLL and CLK is the clk output from the PLL. CLk_aks is the clock used inside the Risc-V core. RV_TO_DAC is the output wire connected to the Xreg[14] register of the register file, and OUT is the analog signal coming out of the DAC unit. 

  ![Screenshot from 2024-08-31 17-59-49](https://github.com/user-attachments/assets/179be68e-fd21-4c2c-9d21-b9372b79fbfe)

</details>

<details>
  <summary> Assignment 11 </summary>
  <br> 
   Day 1
    Below are the snapshots of the activities donw in the Day 1 of the task:
  
   ![Screenshot from 2024-10-19 11-05-14](https://github.com/user-attachments/assets/d037d9cf-40d6-4e5e-86fa-285a340a9687)

   ![Screenshot from 2024-10-19 11-10-10](https://github.com/user-attachments/assets/319886e9-57be-4225-822b-078fd15695d8)

   ![Screenshot from 2024-10-19 11-15-09](https://github.com/user-attachments/assets/bda176d1-5f0a-421a-8345-887f0e84b03d)

   ![Screenshot from 2024-10-19 11-44-59](https://github.com/user-attachments/assets/b465fe4e-57e7-4801-a33f-08b1063800f3)

   ![Screenshot from 2024-10-19 11-45-15](https://github.com/user-attachments/assets/c4a94d99-d855-4a2c-b3b1-59e5e88fb340)

   ![Screenshot from 2024-10-19 11-45-35](https://github.com/user-attachments/assets/d8ea82aa-788f-4755-81a5-5290559aaa4b)


   ![Screenshot from 2024-10-19 23-25-58](https://github.com/user-attachments/assets/9c6dc800-2a7b-480a-aed1-a829d9641053)

   ![Screenshot from 2024-10-19 23-27-28](https://github.com/user-attachments/assets/198ae750-3e82-43ac-a052-1f8905f820ed)

   ![Screenshot from 2024-10-19 23-27-58](https://github.com/user-attachments/assets/442cc227-6229-415d-a180-a89aa41ad7ca)


   ![Screenshot from 2024-10-19 23-28-35](https://github.com/user-attachments/assets/a8f3c82c-c5c8-4add-88e8-5bcf51f8834c)

   ![Screenshot from 2024-10-19 23-35-20](https://github.com/user-attachments/assets/4070634f-bf4b-4061-9afe-b70885a1af6d)

   ![Screenshot from 2024-10-19 23-35-32](https://github.com/user-attachments/assets/834fbecd-ea4b-4c3c-bf34-64f3e9f9cb14)

  ![Screenshot from 2024-10-19 23-36-25](https://github.com/user-attachments/assets/41e536f7-9307-4883-a77a-0b7849995e17)

![Screenshot from 2024-10-19 23-36-58](https://github.com/user-attachments/assets/e19cc036-7b8b-4efc-a69e-94737ab62cdd)

  Day 2:
    Below are the snapshots for day 2 activities :

    ![Screenshot from 2024-10-20 10-53-34](https://github.com/user-attachments/assets/3128cb2c-41e3-40f6-8957-f29384fb6c47)
![Screenshot from 2024-10-20 10-53-34](https://github.com/user-attachments/assets/26847e7f-a3cc-428b-92ff-000c9999614f)

    
![Screenshot from 2024-10-20 10-53-47](https://github.com/user-attachments/assets/33e72dd5-d963-4b3d-9e48-adfb91137fd0)












</details>




