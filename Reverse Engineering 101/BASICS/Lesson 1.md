# STEPS
* Seeking approval.....is it legit?
* Using text/hex editors to gather basic information
* Using binary analyzers on the application revealing magic header and much more
* Running application while monitoring the network and log files 
* Disassembling which required assembly knowledge

This is the registry location in windows that tell us which applications are going to be started when the windows start:
![[Pasted image 20230618183939.png]]

they define which apps gonna be started when the user does the login:
![[Pasted image 20230618184028.png]]

when in linux:
![[Pasted image 20230618184057.png]]

Why we use hexadecimal: To simplify the binary representations

The positive number in binary is represented as this:
![[Pasted image 20230618184250.png]]

While the negative numbers need a bit of a work for them to be represented in binary, they have the MSB as '1' representing -ve:
![[Pasted image 20230618184435.png]]

The very definition of the registers to fit your feeble brain:
![[Pasted image 20230618185754.png]]

Their types:
*General Purpose Registers (GPR)*:
* `AX`: Storage for arithmetic operations
* `CX`: Keeps track of the cycles by rotating/shifting or looping
* `DX`:Arithmetic and I/O operations but used for general storage too
* `BX`:Pointer to the data {located in the segment register called `DS`}
* `BP`:locates the parameter passed via the stack
* `SI`:Pointer to the source in string/stream operations
* `DI`:Pointer to destination in string/stream operations
* `SP`:Pointer to the top of the stack.The address held in the SP register is the RAM address where the last byte was stored by a stack operation. When the data is placed 


















