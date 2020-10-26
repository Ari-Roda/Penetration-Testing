Modern computers run multiple processes concurrently, but its actually not concurrently. They switch between processes so fast it seems as though its concurrent (called context switch). The OS has to keep track of each processes location including the current instruction to execute.

Memory in the process is organized as :

User Stack : contains the information required to run the program, current program counter, saved registers etc. Has empty memory section below it in case the stack grows(downwards). even though the stack grows downwards, when data is copied/written into the buffer, it is copied from lower to higher addresess. Depending on how data is entered into the buffer, it means that it's possible to overwrite the integer variable.
Shared Library regions : statically/dynamically link libraries that are used by the program
Run Time heap : increases and decreases dynamically depending on whether a program dynamically assigns memory. Also has empty memory above it in the event that the size of the heap increases.
Read/Write Data :
Read Only code/Data : stores the program executable and initialised variables.

The stack is a region of contiguous memory addresses and it is used to make it easy to transfer control and data between functions. The top of the stack is at the lowest memory address and the stack grows towards lower memory addresses. The most common operations of the stack are:

Pushing: used to add data onto the stack with push var

Popping: used to remove data from the stack with pop var

Each compiled program may include multiple functions, where each function would need to store local variables, arguments passed to the function and more. To make this easy to manage, each function has its own separate stack frame, where each new stack frame is allocated when a function is called, and deallocated when the function is complete. 

Once the function is finished executing, it will call the return instruction(retq). This instruction will pop the value of the return address of the stack, deallocate the stack frame for the add function, change the instruction pointer to the value of the return address, change the stack pointer(rsp) to the top of the stack and change the frame pointer(rbp) to the stack frame of calc.

Upto 6 arguments for functions can be stored in the following registers:
(rax is a special register that stores the return values of the functions(if any).)

*rdi
*rsi
*rdx
*rcx
*r8
*r9

We can now see that a caller function may save values in their registers, but what happens if a callee function also wants to save values in the registers? To ensure the values are not overwritten, the callee values first save the values of the registers on their stack frame, use the registers and then load the values back into the registers. The caller function can also save values on the caller function frame to prevent the values from being overwritten. Here are some rules around which registers are caller and callee saved:

*rax is caller saved
*rdi, rsi, rdx, rcx r8 and r9 are called saved(and they are usually arguments for functions)
*r10, r11 are caller saved
*rbx, r12, r13, r14 are callee saved 
*rbp is also callee saved(and can be optionally used as a frame pointer)
*rsp is callee saved

the binary information is represented in hexadecimal format. Different architectures actually represent the same hexadecimal number in different ways, and this is what is referred to as Endianess. Let’s take the value of 0x12345678 as an example. Here the least significant value is the right most value(78) while the most significant value is the left most value(12).
Little Endian is where the value is arranged from the least significant byte to the most significant byte LSB 78 56 34 12 MSB.
Big Endian is where the value is arranged from the most significant byte to the least significant byte MSB 12 34 56 78 LSB.

using gdb
buffer overflows task7 thm

find how much characters are needed to get a segmentation fault on program. eg. at 14 program runs normal, at 15 segmentation fault occurs because you are going over into next part of stack. If you can see the program source you can see this from variables being set and what their length is. 
Once you know how much to overwrite variable can then find out how much space haveto put an address. 
Can do this by using gdb and overwriting buffer to 14 and then put A and the program should go to 41. This happens because you have overwritten buffer and its now going to the address you set which is A (which equals 41). You can increment A by one until you find out how big the buffer is. eg you will keep going to address 0x00414141 (AAA) until eventuall you jump out to completely different address.
This gives you the amount of space you have to put the address you want it to return to. Therefore if it jumps out at 20 we have 14 to fill the variables space and then 6 the address.
find the address you want to go to using radare2 or gdb change it to little endian and then convert to ascii to repliacete some character sequence in ascii like control characters you have to do ctrl + shift + something (cant copy paste).
you can then run the program in gdb and fill the variable space with data and put the ascii converted address in the rest of the space.
