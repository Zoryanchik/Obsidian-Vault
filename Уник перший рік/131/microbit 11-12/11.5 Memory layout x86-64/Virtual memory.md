 top![[Pasted image 20250210025313.png]]
(MMU)So what happens is that your program, when you compile it and you obtain the object file, the object file contains virtual addresses.But when your program becomes a process and is about to be executed. Those virtual addresses are mapped onto physical addresses. TLB

So to give you now an analogy. Imagine that your program, after it's compiled and it's becomes an object file.It's like a book. And the books have pages and lines, right?And now assume that you have 20 books and every book has a different number of pages. But when I go to book number three and edit pages one and two only, so one and two virtual pages one and two of the other book will become pages.  I'm calling the process in such a way. So I'm creating another book which contains all the pages of those books in a seemingly random order.So the final book that I create will actually the pages will be renumbered.So you have from 1 to 5000, for example. And this will be the actual physical pages. but initial will have original

![[Pasted image 20250210030535.png]]
![[Pasted image 20250210031039.png]]
So then when the red line is executed, your program will attempt to access memory that has not been allocated to your program anymore.
So when you add code to your program pre devs, you request for more pages.Depending on the number of print devs you ask. When you.So you may be accessing memory that actually has beginning has been given to your program by mistake because of the print depth, but when no printf we will have bug because there is no memory anymore