![Screenshot 2024-11-13 162445](https://github.com/user-attachments/assets/f9cecccc-d413-4dfc-9ae7-376a9b3111eb)
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

    
![Screenshot from 2024-10-20 10-53-34](https://github.com/user-attachments/assets/26847e7f-a3cc-428b-92ff-000c9999614f)

    
![Screenshot from 2024-10-20 10-53-47](https://github.com/user-attachments/assets/33e72dd5-d963-4b3d-9e48-adfb91137fd0)

![Screenshot from 2024-10-20 10-53-47](https://github.com/user-attachments/assets/f844ba76-00af-4890-ad92-25d574e58df3)

![Screenshot from 2024-10-20 10-54-01](https://github.com/user-attachments/assets/075b0d6f-8d7f-4dac-8325-f24409cab2a4)
![Screenshot from 2024-10-20 10-54-37](https://github.com/user-attachments/assets/652c1c74-04b5-4266-818f-f3078967486e)
![Screenshot from 2024-10-20 10-57-09](https://github.com/user-attachments/assets/d3efd071-ef34-4a50-815a-20e51fdc9ae1)
![Screenshot from 2024-10-20 10-58-45](https://github.com/user-attachments/assets/da6475d1-b42b-4bff-8d6e-4f3d9ec7c914)

![Screenshot from 2024-10-20 11-04-23](https://github.com/user-attachments/assets/cc245bb0-f5f7-41a4-b3d6-d84b5acca290)

![Screenshot from 2024-10-20 11-18-26](https://github.com/user-attachments/assets/17146423-e0bc-4345-9b3c-19f00a5e62c5)

![Screenshot from 2024-10-20 11-18-33](https://github.com/user-attachments/assets/f58a136a-13ba-4c90-8ac7-71fcd9bff176)

![Screenshot from 2024-10-20 11-18-39](https://github.com/user-attachments/assets/746d151a-8106-4725-8d3f-aa993a18c69e)

![Screenshot from 2024-10-20 11-18-45](https://github.com/user-attachments/assets/c220a0ca-5d38-49c8-81a1-f3cb5550573c)

![Screenshot from 2024-10-20 11-18-50](https://github.com/user-attachments/assets/b42c39fd-bb4b-4636-ab31-5fb107493e28)

![Screenshot from 2024-10-20 11-18-55](https://github.com/user-attachments/assets/d65ed5c0-3934-48b0-ad58-355b50aff823)

![Screenshot from 2024-10-20 11-19-01](https://github.com/user-attachments/assets/e0b05db8-3578-43cd-99f7-eda77b6b8830)

![Screenshot from 2024-10-20 11-19-14](https://github.com/user-attachments/assets/4924d4ed-7187-42de-9710-d421dc1f46c6)

![Screenshot from 2024-10-20 11-19-21](https://github.com/user-attachments/assets/ed80d092-3842-4375-9e75-211474bcf7ab)

![Screenshot from 2024-10-20 11-19-28](https://github.com/user-attachments/assets/7f3ae140-1bcf-4ce1-b8e7-9981ab3794c9)

![Screenshot from 2024-10-20 11-19-43](https://github.com/user-attachments/assets/76bd706f-88e0-4eba-b20c-c6b6b1368ea1)
  

![Screenshot from 2024-10-20 11-22-49](https://github.com/user-attachments/assets/3eb458ff-99e8-4c06-a4eb-8c74e6ab6ec5)

![Screenshot from 2024-10-20 11-23-52](https://github.com/user-attachments/assets/44d6154d-e854-451a-a569-457ab1489fd2)

![Screenshot from 2024-10-20 11-23-58](https://github.com/user-attachments/assets/ebe84035-b390-4e27-95f0-05a8db6ebfd6)


![Screenshot from 2024-10-20 21-53-15](https://github.com/user-attachments/assets/e66533af-2f03-4c2c-97b8-4ffb57a4e909)


![Screenshot from 2024-10-20 21-54-11](https://github.com/user-attachments/assets/49c81ada-7931-4546-af34-6a833e745864)


![Screenshot from 2024-10-20 11-24-03](https://github.com/user-attachments/assets/a9843318-1be4-43e7-beea-8f5c3aa9439b)


Asynchronous Reset :


![Screenshot from 2024-10-20 22-05-03](https://github.com/user-attachments/assets/92045009-e446-4b70-8e64-3aab92024708)


![Screenshot from 2024-10-20 22-06-37](https://github.com/user-attachments/assets/5530059c-57ac-44d3-b596-5bd593d0369c)


![Screenshot from 2024-10-20 22-06-53](https://github.com/user-attachments/assets/d86a7351-81c9-48a6-9e0d-2bc7e516412c)


![Screenshot from 2024-10-20 22-05-54](https://github.com/user-attachments/assets/1311027e-2681-47eb-85d2-a851eeee587c)


Synchronous Reset :



![Screenshot from 2024-10-20 22-12-38](https://github.com/user-attachments/assets/62c32ba4-1f10-48f5-8fbe-d3c5b58465a8)


![image](https://github.com/user-attachments/assets/d4e7b245-e4ed-4e23-b7b5-d232e8bd80d5)


![Screenshot from 2024-10-20 22-10-29](https://github.com/user-attachments/assets/2056767e-0d8d-4a77-b5e5-a3d630650782)


![Screenshot from 2024-10-20 22-10-14](https://github.com/user-attachments/assets/a42dcaa0-90fa-410b-b9c2-80f6b50025d2)

Asynchronous Set :

![Screenshot from 2024-10-21 09-18-50](https://github.com/user-attachments/assets/720d70d7-9ef5-47d3-a341-263e68005ca0)

![Screenshot from 2024-10-21 09-19-06](https://github.com/user-attachments/assets/fb68d1d5-ef04-49a7-8491-b14a66bcd621)

![Screenshot from 2024-10-21 09-18-12](https://github.com/user-attachments/assets/13bc970e-15e1-41b8-a332-567440c6bb43)

Asynchronous Reset :

![Screenshot from 2024-10-21 18-59-52](https://github.com/user-attachments/assets/884e4c74-4a10-4205-9416-336ac17b0025)

![Screenshot from 2024-10-21 19-00-14](https://github.com/user-attachments/assets/638f9370-4e23-4557-895a-b01375243cd2)

![Screenshot from 2024-10-21 19-01-37](https://github.com/user-attachments/assets/bc2e4d2d-8215-4558-8dcb-f4df36c080bd)

Asynchronous Set :

![Screenshot from 2024-10-21 19-04-20](https://github.com/user-attachments/assets/71c051f0-e0bf-46c4-b854-8a340b7711d9)



  ![Screenshot from 2024-10-21 19-05-03](https://github.com/user-attachments/assets/3e4c218f-7e00-4493-b210-bfa30874e788)


![Screenshot from 2024-10-21 19-25-17](https://github.com/user-attachments/assets/eb2c51d4-4e05-49f0-b7f3-104ce0522333)

Synchronous Reset :


![Screenshot from 2024-10-21 19-27-31](https://github.com/user-attachments/assets/75ea9493-6ba8-436e-933c-453676fc4d83)


![Screenshot from 2024-10-21 19-30-26](https://github.com/user-attachments/assets/ed6cfb9c-c6ce-482e-9835-2d9529338556)


![Screenshot from 2024-10-21 19-30-44](https://github.com/user-attachments/assets/e0e10d16-2957-4a50-bd03-fa4caa021bfb)


![Screenshot from 2024-10-21 19-31-17](https://github.com/user-attachments/assets/4076642d-a27d-42f9-95e4-5dcfddd55315)


Multiplication By 2 :


![Screenshot from 2024-10-21 19-34-05](https://github.com/user-attachments/assets/41ebb8e8-c540-4f20-9384-abbdfc130b82)


![Screenshot from 2024-10-21 19-35-52](https://github.com/user-attachments/assets/de2bcdc6-b385-46c9-bb7c-0a8777fdd8b1)



![Screenshot from 2024-10-21 19-34-18](https://github.com/user-attachments/assets/319c9e47-594f-4ac4-bd66-a5b2bdb33487)


![Screenshot from 2024-10-21 19-35-44](https://github.com/user-attachments/assets/28129e55-f943-40ca-bfde-2a827a6cf598)

Multiplication By 9 :


![Screenshot from 2024-10-21 19-40-10](https://github.com/user-attachments/assets/532e97c2-a054-491d-abc8-6431f8c7c390)


![Screenshot from 2024-10-21 19-40-42](https://github.com/user-attachments/assets/4d341c7b-884b-45a3-87fd-e759f8940d00)


![Screenshot from 2024-10-21 19-40-34](https://github.com/user-attachments/assets/273b437f-92dd-4197-9071-a81ff51760c9)


![Screenshot from 2024-10-21 19-41-07](https://github.com/user-attachments/assets/eb6ef501-96f0-4159-87a5-a3f33e7bdad2)


![Screenshot from 2024-10-21 19-41-16](https://github.com/user-attachments/assets/55328586-b5a7-4062-8b1e-1d696501c551)

Day 3 :

Optimization of various designs
Design infers 2 input AND GATE :

![Screenshot from 2024-10-21 20-33-16](https://github.com/user-attachments/assets/e1c0d2dd-5573-46f8-98f7-9772ef7656a8)

![Screenshot from 2024-10-21 20-33-44](https://github.com/user-attachments/assets/ce1fb3e2-7848-4872-ac8c-c5c027843a38)

![Screenshot from 2024-10-21 20-34-02](https://github.com/user-attachments/assets/6117ad2e-11d1-4254-9bdb-2b9d04c15aac)

![Screenshot from 2024-10-21 20-34-58](https://github.com/user-attachments/assets/247eb96e-4c69-40ef-95f9-93754d17117a)

Design infers 2 input OR Gates :

![Screenshot from 2024-10-21 20-38-21](https://github.com/user-attachments/assets/df4706ca-c3df-44b6-b5aa-7042195c5f09)

![Screenshot from 2024-10-21 20-38-26](https://github.com/user-attachments/assets/913f4c23-0a07-43fe-9ee7-3190cb802b2b)

![Screenshot from 2024-10-21 20-38-46](https://github.com/user-attachments/assets/1929b730-68c2-4c5d-81cd-b4de133c9682)

![Screenshot from 2024-10-21 20-38-55](https://github.com/user-attachments/assets/e16fb7c2-5a47-4963-8673-1e8a59a695b2)
![Screenshot from 2024-10-21 20-41-32](https://github.com/user-attachments/assets/cd387f8c-e545-4089-9b8d-1af1821af60a)

Design infers 3 input AND gate :

![Screenshot from 2024-10-21 20-43-42](https://github.com/user-attachments/assets/47992fbd-c34f-45f5-b5be-d6d753e6eeea)

![Screenshot from 2024-10-21 20-44-01](https://github.com/user-attachments/assets/3b5ce902-9561-499f-9b9b-a20375861e42)

![Screenshot from 2024-10-21 20-44-20](https://github.com/user-attachments/assets/a7d1a13a-3b6c-4f83-940a-84679f9f911c)

![Screenshot from 2024-10-21 20-44-38](https://github.com/user-attachments/assets/e61111d0-0686-489a-a290-27064c2ebdc2)

Design infers 2 input XNOR Gate :

![Screenshot from 2024-10-21 20-46-30](https://github.com/user-attachments/assets/64c76146-03d6-44cb-89f2-4214fe91cd6a)

![Screenshot from 2024-10-21 20-46-42](https://github.com/user-attachments/assets/a3afd3e3-8c4c-416a-9b9f-58f62f77d83e)

![Screenshot from 2024-10-21 20-46-56](https://github.com/user-attachments/assets/cf8cf2fa-4c4d-4309-b851-c92e426a6c3e)

![Screenshot from 2024-10-21 20-47-05](https://github.com/user-attachments/assets/ff073ab9-571b-4881-b2b3-b88b63f925c6)

![image](https://github.com/user-attachments/assets/6e9ec96c-7c0b-455d-b797-2955c8d39180)

Multiple Module Optimization 1 :

![Screenshot from 2024-10-21 20-50-27](https://github.com/user-attachments/assets/7b6f6642-1a30-4097-877b-97ca637033da)

![Screenshot from 2024-10-21 20-50-31](https://github.com/user-attachments/assets/4ae90e56-2376-4b8d-a00b-d9e61cbf9cfa)

![Screenshot from 2024-10-21 20-50-43](https://github.com/user-attachments/assets/d6cfdd33-bea0-47b3-b220-b7e5fddb117a)

![Screenshot from 2024-10-21 21-19-32](https://github.com/user-attachments/assets/9740c34a-2d67-4e8a-b629-2cc9510344a4)

![image](https://github.com/user-attachments/assets/3de6e364-f862-41d5-bc01-1682bc48ab6f)

Multiple Module optimization 2 :

![Screenshot from 2024-10-21 21-25-51](https://github.com/user-attachments/assets/5aedc7f4-b7a2-4af9-a588-7c04423946d6)

![Screenshot from 2024-10-21 21-26-22](https://github.com/user-attachments/assets/882daa8c-19f6-41af-a44a-cc5dd105eea7)

![Screenshot from 2024-10-21 21-26-28](https://github.com/user-attachments/assets/b850fcc9-ba64-405c-bfd5-8a1a31f0e7df)

![Screenshot from 2024-10-21 21-26-46](https://github.com/user-attachments/assets/e4ba29c4-8fd8-4e6e-98bb-2104493461f9)

D flip flop constant 1 with asynchronous reset (Active low):
![Screenshot from 2024-10-21 21-29-22](https://github.com/user-attachments/assets/23a05e39-a471-4cb9-a7d7-2b3d2c453d89)

![Screenshot from 2024-10-21 21-29-45](https://github.com/user-attachments/assets/b53b4988-d73f-491e-b405-4c00f8845b6c)

![Screenshot from 2024-10-21 21-30-49](https://github.com/user-attachments/assets/e1251cfb-3681-488b-a8a4-0659e66b509e)

![Screenshot from 2024-10-21 21-30-55](https://github.com/user-attachments/assets/eafa5293-fc55-48b2-b172-fb8c58899afc)

![Screenshot from 2024-10-21 21-31-25](https://github.com/user-attachments/assets/fd1787db-86d4-45eb-8bdc-e94717656e83)

![Screenshot from 2024-10-21 21-31-30](https://github.com/user-attachments/assets/8ac6f193-c057-49db-b593-0f8525353794)

![Screenshot from 2024-10-21 21-31-53](https://github.com/user-attachments/assets/fa562be3-5b71-4e93-a62c-8cff2f2043eb)

D flip flop constant 2 with Asynchronous Reset (Active High):

![Screenshot from 2024-10-21 21-39-05](https://github.com/user-attachments/assets/606be055-de4f-4143-b6b4-b4c63b3cdd0d)

![Screenshot from 2024-10-21 21-38-58](https://github.com/user-attachments/assets/81d508b3-0241-4ae8-8d4a-873027a11eee)


![Screenshot from 2024-10-21 21-40-12](https://github.com/user-attachments/assets/a75aa825-cfa0-4c2c-a360-245aae1608b9)

![Screenshot from 2024-10-21 21-40-16](https://github.com/user-attachments/assets/9e9d838a-8ba4-410b-90a3-801b92e781ed)

![Screenshot from 2024-10-21 21-40-35](https://github.com/user-attachments/assets/3031c849-729f-422b-87f7-a407273fc7bf)

D flip flop constant 3 with Asynchronous Reset (Active low) :

![Screenshot from 2024-10-21 21-50-18](https://github.com/user-attachments/assets/a9983d34-0f18-440c-8d2a-48b4d2f53406)

![Screenshot from 2024-10-21 21-50-46](https://github.com/user-attachments/assets/cf64b474-76be-4e80-94de-ed5e767ccd55)

![Screenshot from 2024-10-21 21-50-59](https://github.com/user-attachments/assets/f36d8ec9-ccba-4791-8085-fa8a47464ff8)

D flip flop constant 4 Asynchronous Reset (Active Low) :

![Screenshot from 2024-10-21 21-53-46](https://github.com/user-attachments/assets/0434d448-b645-4c1c-97bf-a20c55c3f672)

![Screenshot from 2024-10-21 21-54-10](https://github.com/user-attachments/assets/87c014d5-5432-4172-8373-5909d4f97b43)


![Screenshot from 2024-10-21 21-54-25](https://github.com/user-attachments/assets/f0591986-2c00-4ec7-8c7b-0fde01aad3af)

D flip flop constant 5 with Asynchronous Reset :

![Screenshot from 2024-10-21 21-56-22](https://github.com/user-attachments/assets/83ae3950-6c69-4333-9bf3-5c569021e9ab)

![Screenshot from 2024-10-21 21-56-43](https://github.com/user-attachments/assets/f5a3f784-2828-4a6a-908e-1e89e1df8d98)

![Screenshot from 2024-10-21 21-56-53](https://github.com/user-attachments/assets/fd88e430-17e7-4554-9402-4afaf7b5e9b5)

Counter optimization 1 :

![Screenshot from 2024-10-21 21-59-13](https://github.com/user-attachments/assets/dd9e6203-6941-45f5-9d56-da792bb39d13)

![Screenshot from 2024-10-21 21-59-50](https://github.com/user-attachments/assets/b2967312-e598-4b3b-823f-deed51a84dfb)

![Screenshot from 2024-10-21 22-00-04](https://github.com/user-attachments/assets/70ac6e93-5958-4cec-8d2b-5522d383f76b)

Counter Optimization 2 :

![Screenshot from 2024-10-21 22-01-25](https://github.com/user-attachments/assets/2c16a02c-3585-4c80-930f-13728aca208a)

![Screenshot from 2024-10-21 22-02-19](https://github.com/user-attachments/assets/e4f45278-3867-47fd-ab53-2b1ba9d48f4b)

![Screenshot from 2024-10-21 22-02-31](https://github.com/user-attachments/assets/b7a963bb-9426-404c-9df3-a6814c3cf955)


DAY 4 :

Design of 2:1 MUX using Ternary operator :


![Screenshot from 2024-10-21 23-02-02](https://github.com/user-attachments/assets/92487a68-9e7b-4d19-aac8-f706bb0acc91)

![Screenshot from 2024-10-21 23-02-20](https://github.com/user-attachments/assets/5a9efa44-4267-41f8-ba4b-5b29122803d5)

![Screenshot from 2024-10-21 23-05-17](https://github.com/user-attachments/assets/daf7ca16-5d05-4249-8720-1fbdb605956a)

![Screenshot from 2024-10-21 23-06-13](https://github.com/user-attachments/assets/701c0c64-6ab3-404f-82a8-1e9b4384578c)

![Screenshot from 2024-10-21 23-07-02](https://github.com/user-attachments/assets/dc125582-ee0f-4a02-934c-e8d0b70b187e)

![Screenshot from 2024-10-21 23-07-14](https://github.com/user-attachments/assets/02d640a1-0089-42e8-b906-513b77958237)

![Screenshot from 2024-10-21 23-11-01](https://github.com/user-attachments/assets/8c839f6b-d09a-4c90-bfea-8d53930991d6)

![Screenshot from 2024-10-21 23-12-33](https://github.com/user-attachments/assets/3b853f7f-68a7-493c-910d-38018ed8eb79)

![Screenshot from 2024-10-21 23-12-23](https://github.com/user-attachments/assets/09e15a87-36c8-4e6a-8719-95244d5057c4)

Design of a Bad 2:1 Mux :

![Screenshot from 2024-10-21 23-13-57](https://github.com/user-attachments/assets/f9276fa3-6727-46fe-ac6d-1bd3837ff501)

![Screenshot from 2024-10-21 23-14-21](https://github.com/user-attachments/assets/4cdbac18-5da6-43e3-b6f3-3f3f1c81e3fb)

![Screenshot from 2024-10-21 23-15-42](https://github.com/user-attachments/assets/bdb85f54-7b81-45a2-bf91-2a13f8aad523)

![Screenshot from 2024-10-21 23-16-09](https://github.com/user-attachments/assets/a6d880fa-e8aa-49a8-9f32-16774a9c919f)


![Screenshot from 2024-10-21 23-16-26](https://github.com/user-attachments/assets/ad54380a-5983-43d8-b003-2b8dc46c5e5b)

![Screenshot from 2024-10-21 23-16-40](https://github.com/user-attachments/assets/a62506ad-0f36-4701-b1d3-0fbad32e9ad4)

Blocking Caveat :

![Screenshot from 2024-10-21 23-18-59](https://github.com/user-attachments/assets/cdf0ed22-a247-4fd1-a16f-4f6f3d5b91ee)

![Screenshot from 2024-10-21 23-18-46](https://github.com/user-attachments/assets/6a90a00b-d20c-4770-8eb5-268c21e42355)

![Screenshot from 2024-10-21 23-19-22](https://github.com/user-attachments/assets/01a0dec0-a4bb-4eac-8f9d-529f97896463)

![Screenshot from 2024-10-21 23-21-06](https://github.com/user-attachments/assets/44610a6b-c6e6-4a42-9c18-f5ddc84e0eff)


![Screenshot from 2024-10-21 23-22-15](https://github.com/user-attachments/assets/8bfc384f-8803-4676-b3cf-b1a17c2ff78c)

![Screenshot from 2024-10-21 23-22-31](https://github.com/user-attachments/assets/263cce39-9587-46dd-b924-a26fece0ffd2)

![Screenshot from 2024-10-21 23-22-51](https://github.com/user-attachments/assets/41699e21-3df3-4009-87c1-ce5b229a33a9)






</details>

<details>
 <summary> Assignment 12 </summary>
  <br> 
  The following commands were used to generate the netlist and the mapped netlist verilog design from the rvmyth core verilog file:

```
read_liberty -lib ~/Asic_Tasks/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 

read_verilog rvmyth_final.v clk_gate.v 

synth -top rvmyth_final 

abc -liberty ~/Asic_Tasks/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 

write_verilog rvmyth_final_net_map.v

```

  ![Screenshot from 2024-10-23 23-48-16](https://github.com/user-attachments/assets/001f20bd-8e7d-46b1-bb62-caac7185df26)
![Screenshot from 2024-10-23 23-48-52](https://github.com/user-attachments/assets/19d559d4-4653-49ab-836d-199f3b320e91)
![Screenshot from 2024-10-23 23-49-03](https://github.com/user-attachments/assets/98538f13-a19a-439c-a8d2-b6c34c649a5a)

The generated netlist verilog and mapped netlist verilog is shown below :

![Screenshot from 2024-10-23 23-52-50](https://github.com/user-attachments/assets/64c3686c-fb36-48db-a65a-85756425b8f3)

![Screenshot from 2024-10-23 23-56-17](https://github.com/user-attachments/assets/3b4fb68b-284e-4c86-828d-aca265727849)

Top Module " vsdbabysoc" was edited to included to integrated the newly generated netlist verilog :
![Screenshot from 2024-10-24 00-02-42](https://github.com/user-attachments/assets/dee0a810-8ae8-46b3-a120-3526c76257ea)

The testbench has been changed to :

![Screenshot from 2024-10-24 00-03-10](https://github.com/user-attachments/assets/13fb8623-da31-48e8-8cbb-156ad5e01e26)

The following commands were used to simulate the new SOC which includes the synthesized RVMYTH core :

![Screenshot from 2024-10-23 23-51-31](https://github.com/user-attachments/assets/149e9300-e5de-41ac-b4f3-e1b4d91ee016)

The gtkwave window showing the output and the clock is :

![Screenshot from 2024-10-24 01-25-52](https://github.com/user-attachments/assets/a5af2473-ac91-4843-9099-82c8ced96757)


The standard cell highlighted in the image is "7059" the same cell is available in the code as shown in the code :

![Screenshot from 2024-10-23 23-55-45](https://github.com/user-attachments/assets/f7b9278e-9a51-4f8a-904b-4c74a5b94667)

The output for the RTL code for RVMYTH core is shown below :

![Screenshot from 2024-10-24 01-37-29](https://github.com/user-attachments/assets/1a8db0e2-4e10-43e7-a328-5c817fd7948e)


We have successfully demonstrated that the output for the RVMYTH RTL design and the synthesized design are same.

The Heirarchy of the Net list is shown below :

![image](https://github.com/user-attachments/assets/e23930a0-bc82-45ef-9d57-520161373109)

  
</details>
<details>
  <summary> Assignment 13 </summary>
  <br>
  In this task STA was performed on the RV core netlist generated with yosys. The following commands we run to perform the analysis:
  
  ![Screenshot from 2024-10-28 21-33-49](https://github.com/user-attachments/assets/fda39c1c-5ca9-40d7-a7c3-7700952655ec)
  ![Screenshot from 2024-10-28 21-35-42](https://github.com/user-attachments/assets/f6029870-d452-4941-9923-6edd55dc6948)
  ![Screenshot from 2024-10-28 21-36-02](https://github.com/user-attachments/assets/810cd1fd-c8c5-4ffc-8aca-87297148732a)

  As we can see in the above snapshots that for a given clock period the design is showing setup and hold violations.
  
</details>


<details>
  <summary> Assignment 14 </summary>
  <br>
  In this task we are performing STA on the core netlist we generated, using other library files.

  The sdc file is shown below :

  ![Screenshot from 2024-11-04 23-25-34](https://github.com/user-attachments/assets/505db5c8-60b2-454c-a01a-f43b0436e36d)

  The script is shown below :

  ![Screenshot from 2024-11-04 23-27-54](https://github.com/user-attachments/assets/cabfc628-7ef9-463f-a5e1-16ddbbd6761f)

  the output data is shown in the table below :
  ![Screenshot from 2024-11-04 22-29-07](https://github.com/user-attachments/assets/0216272d-ff89-42e7-ae47-f78634c76e9b)

  The plots for the variour outputs is shown below:
  ![Screenshot from 2024-11-04 23-09-29](https://github.com/user-attachments/assets/f923bdf1-1a15-4b19-9b48-8beedbf436a7)

  ![Screenshot from 2024-11-04 23-11-36](https://github.com/user-attachments/assets/95423060-bf5b-4d17-a990-666270fbcc9f)

  ![Screenshot from 2024-11-04 23-13-49](https://github.com/user-attachments/assets/188874df-996a-436b-828c-7bdc5a7a6585)

  ![Screenshot from 2024-11-04 23-08-06](https://github.com/user-attachments/assets/09503483-f989-43f1-8039-37b6c60cbb5a)



</details>

<details>
  <summary> Assignment 15 </summary>
  <br>
Day 1 : Introduction to Open Source EDA, OpenLANE and Sky130 PDK

![Screenshot 2024-11-13 141249](https://github.com/user-attachments/assets/f7ff7423-cceb-44a3-a819-cf832149f4f7)

![Screenshot 2024-11-13 141351](https://github.com/user-attachments/assets/9ecf8b31-88cd-4c22-9842-cd0c2bc7a0b8)

![Screenshot 2024-11-13 160022](https://github.com/user-attachments/assets/ad866101-4840-4ccd-92f4-ca5ce5bc8b11)

![Screenshot 2024-11-13 160900](https://github.com/user-attachments/assets/1116189d-f2be-407e-b5b1-5ea278c014ee)

To calculate the Flop Ratio : Screen shot of the synthesis report is given:

Calculation of Flop Ratio and DFF % from synthesis statistics report file

Flop Ratio = 1613/14876 = 0.108429685 Percentage of DFFs = 0.108429685*100 = 10.8429685


Day 2 : Good floorplan vs bad floorplan and introduction to library cells

1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

   ![Screenshot 2024-11-13 162445](https://github.com/user-attachments/assets/67e2e3f2-05b8-497f-8358-1b2607a7596d)

   ![Screenshot 2024-11-13 162504](https://github.com/user-attachments/assets/4e3d3b03-4b40-472e-a813-caf51af1c5bf)

   ![Screenshot 2024-11-13 162825](https://github.com/user-attachments/assets/6a9c7e7a-b9da-4bc6-ae09-4fb96abfbf3e)

   ![Screenshot 2024-11-13 162857](https://github.com/user-attachments/assets/f7712e20-3a5b-4454-b82c-d5a8278074ad)

2. Calculate the die area in microns from the values in floorplan def.

   ![Screenshot 2024-11-13 164752](https://github.com/user-attachments/assets/b5ad6915-5b8f-43d2-86b2-3c85826ddddb)

   According to Floorplan def

1000 unit distance = 1 Micron Die width in unit distance = 660685-0 = 660685 Die height in unit distance = 671405-0 = 671405 Distance in microns = Value in unit distance/1000 Die width in microns = 660685/1000 = 660.685 Microns Die heigth in microns = 671.405 Microns

3. Load generated floorplan def in magic tool and explore the floorplan.

   ![Screenshot 2024-11-13 165340](https://github.com/user-attachments/assets/7f75327c-f59f-4e6b-a7df-cc530e7f4211)

   ![Screenshot 2024-11-13 184907](https://github.com/user-attachments/assets/90241b7d-09e8-4c55-9081-e710aade42ad)

   ![Screenshot 2024-11-13 184922](https://github.com/user-attachments/assets/8ec0ea4d-4fc7-4d45-bf41-eec2170b7c02)

   ![Screenshot 2024-11-13 185044](https://github.com/user-attachments/assets/e1dab24c-5cda-4f03-9c33-8bae3ecfc02e)

   ![Screenshot 2024-11-13 185153](https://github.com/user-attachments/assets/12e7b0ed-12cf-46f6-b5c5-2b2bae1bd48c)

   ![Screenshot 2024-11-13 185600](https://github.com/user-attachments/assets/53d54e05-1220-40d7-af46-f7ca4c0d5ccd)

   ![Screenshot 2024-11-13 185638](https://github.com/user-attachments/assets/255f715b-618c-476a-ae7a-b934136de8ff)

   ![Screenshot 2024-11-13 185801](https://github.com/user-attachments/assets/5734f7ce-17a0-4788-a6ac-bb55747c1289)

   ![Screenshot 2024-11-13 185845](https://github.com/user-attachments/assets/4118f75d-3ac3-48e3-bbd0-9e469c605043)

4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
   
   ![Screenshot 2024-11-13 190440](https://github.com/user-attachments/assets/5a05b51c-433b-45a0-827f-030df4dd82da)

   ![Screenshot 2024-11-13 190510](https://github.com/user-attachments/assets/607699f1-6f46-4349-b14f-3232af476f77)

   ![Screenshot 2024-11-13 190736](https://github.com/user-attachments/assets/1d6e42c4-0118-41b1-a66e-bcafd0eb1253)

   ![Screenshot 2024-11-13 191244](https://github.com/user-attachments/assets/db07f77c-87e6-487b-aac6-18197903d664)


   ![Screenshot 2024-11-13 190755](https://github.com/user-attachments/assets/31ce9a5c-3545-44be-bf03-0ef586e35abf)
















</details>



