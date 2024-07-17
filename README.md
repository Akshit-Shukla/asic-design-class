# asic-design-class
Task 1: To compile c code using gcc:
  A c program to calculate the sum of n number was written and was compiled with gcc with the following command:
    gcc -o sum1ton sum1ton.c
  
Task 2: To compile the same c code using RiscV gcc:
  The same c program was then compiled using RiscV gcc with the following command:
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c

  After that "riscv-unknown-elf-objdump -d sum1ton.o | less" command was used to dump the assembly code in the terminal. 