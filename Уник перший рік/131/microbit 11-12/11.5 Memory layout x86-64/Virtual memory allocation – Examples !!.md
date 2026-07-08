 ![[Pasted image 20250210031400.png]]
![[Pasted image 20250210031428.png]]
	BSS UNINTISIALISED DATA
	3 So you know that it's not the global variable that has been initialised or not initialised.So the only other place to store it is the text. So what happens when you run now this code.  
Because the text holds all the instructions as well. So this implies that when the object file becomes an executable and is executed. When intialised this variable would appear in stack
![[Pasted image 20250210031818.png]]So when this is called, all the necessary variables that the function needs will be transferred to the stack. 

heap holds Dynamic memory allocation for variables and the stack runs
Stack holds variables needs by function
![[Pasted image 20250210032042.png]]The extraction pointer contains an address where execution will return to the program when your function completes.
at first main then func1, Sp points to the top of stack, so when func(1) ends our new top of stack will be at main