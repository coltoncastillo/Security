# la da da da da dada da da da da

There are 16 general purpose 64-bit registers
  - %rax : The first return register
  - %rbp : the base pointer that keeps track of the base of the stack
  - %rsp : the stack pointer that points to the top of the stack 
      - You will see arguments passed to functions as something like `%ebp-0x8`
  

Heap - Memory that can be allocated and deallocated

Stack - A contiguous section of memory used for passing arguments

General Register - A multipurpose register that can be used by either programmer or user to store data or a memory location address

Control Register - A processor register that changes or controls the behavior of a CPU

Flags Register - Contains the current state of the processor


- MOV - move source to destination
- PUSH - push source onto stack
- POP - Pop top of stack to destination
- INC - Increment source by 1
- DEC - Decrement source by 1
- ADD - Add source to destination
- SUB - Subtract source from destination
- CMP - Compare 2 values by subtracting them and setting the %RFLAGS register. ZeroFlag set means they are the same.
- JMP - Jump to specified location
- JLE - Jump if less than or equal
- JE - Jump if equal


















