#StackFrame #CS354 #Recursion #Assembly #UWMadison

Make sure you can draw a working model of the stack frame
When writing assembly, the numbers do not automatically match bytes

## Stack Frame
Start with this:
(ebp)
arg = ARGUMENT
ret addr (esp)
In order to offset for parameters, you have to keep track of how many previous inputs there were


### Various assembly
cmp s2, s1 --> s1 - s2, set flag
ret --> pop %eip
jge --> jump greater than
Be careful that when there is a cmpl and a jmp, what sets a flag to 0 or 1 and what jumps away from setting the flag
using a movl operation to get a result will pull the result from memory, so use leal to load the address, not the result
(%eax) would take the address in %eax, follow it, and give the value in that address
choosing a data format suffix (l,w,b) is just finding the operand with the smallest number of bytes

### Addressing Modes
Immediate
- $immediate
Register
- %reg
Memory

### Registers
Single bytes
- ax or ah
- cx or ch
- dx or dh
- bx or bh
- al
- cl
- dl
- bl
Double bytes (words)
- si
- di
- sp
- dp
Quad bytes (double words)
- eax
- ecx
- edx
- ebx
- esi
- edi
- esp
- ebp
You cannot get the address of a register that is less than 32 bit (4 bytes)