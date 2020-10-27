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

#######################################################################

When a function calls another function, it needs to add the return address on the stack so the callee function knows where to transfer control to once it has finished executing. Data will be copied upwards from buffer[0] to buffer[n]. Since we can overflow the buffer, it also follows that we can overflow the return address with our own value. We can control where the function returns and change the flow of execution of a program.

shell code quite literally is code that will open up a shell. More specifically, it is binary instructions that can be executed. Since shellcode is just machine code(in the form of binary instructions), you can usually start off by writing a C program to do what you want, compile it into assembly and extract the hex characters. This shellcode opens up a basic shell:

\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05

The basic idea is that we need to point the overwritten return address to the shellcode, but where do we actually store the shellcode and what actual address do we point it at? Why don’t we store the shellcode in the buffer - because we know the address at the beginning of the buffer, we can just overwrite the return address to point to the start of the buffer.

*Find out the address of the start of the buffer and the start address of the return address

*Calculate the difference between these addresses so you know how much data to enter to overflow

*Start out by entering the shellcode in the buffer, entering random data between the shellcode and the return address, and the address of the buffer in the return address

In theory, this looks like it would work quite well. However, memory addresses may not be the same on different systems, even across the same computer when the program is recompiled. So we can make this more flexible using a NOP instruction. A NOP instruction is a no operation instruction - when the system processes this instruction, it does nothing, and carries on execution. A NOP instruction is represented using \x90. Putting NOPs as part of the payload means an attacker can jump anywhere in the memory region that includes a NOP and eventually reach the intended instructions. This is what an injection vector would look like:

|NOP block |SHELL code|Memory Address|

You’ve probably noticed that shellcode, memory addresses and NOP sleds are usually in hex code. To make it easy to pass the payload to an input program, you can use python:

python -c “print (NOP * no_of_nops + shellcode + random_data * no_of_random_data + memory address)”

Using this format would be something like this for this challenge:

python -c “print(‘\x90’ * 30 +‘\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05’+

‘\x41’ * 60 + 

‘\xef\xbe\xad\xde’) | ./program_name

 ”
