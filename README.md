# asic-design-class
Task 1: To compile c code using gcc:
  A c program to calculate the sum of n number was written and was compiled with gcc with the following command:
  
    `gcc -o sum1ton sum1ton.c`

![Screenshot 2024-07-17 160519](https://github.com/user-attachments/assets/f78e0c67-dc60-4f7a-a147-65d616c36c90)

After that `./sum1ton.o ` command was used to print the output.



![Screenshot 2024-07-16 171156](https://github.com/user-attachments/assets/69a193ba-bee9-4067-8827-334c3cd42431)



Task 2: To compile the same c code using RiscV gcc:
  The same c program was then compiled using RiscV gcc with the following command:
  
    `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

  After that, the following command is used to dump the assembly code in terminal:
  
  `riscv64-unknown-elf-objdump -d sum1ton.o | less` 

  
  
![Asic_Design_Task2](https://github.com/user-attachments/assets/1ec2ac62-58e8-4abd-bfac-4732a1a72a64)
