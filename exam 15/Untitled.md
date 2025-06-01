111
Encapsulation is a fundamental concept in (OOP)** that refers to bundling data (variables) and methods (functions) that operate on the data into a single unit, typically a **class**.
Class = blueprint (a specification of an object someone might build)
OOP is a way of writing programs using "objects." 
What supports modularity : class, encapsulation, constructor,  method, modularity relies on standarts (API)
Methods are functions that are declared within class
private can be accessed only from methods inside the class
Class Car 
Namespaces provide space where we can define or d3eclare identifires
{
    int miles: this is varible
    public:
    void drive(int miles);
};

void Car::drive(int miles)  set method                             to get something from private   char *Car::getColour(){
{                                                                                        return colour     }
    milesdriven = milesdriven +miles;
}
int main()
{
    Car nameofcar;            
    nameofcar.respray(18)                                     
}

Constructor (no return type)  helps intialize our objects
Class Car 
{ public:
cqar(char *b);};

Car::Cqar(char *b){
        brand = b;}
Int main ()
Car newcar ((char *) double dot 'Bmw', 312312312 not in our class but still true);

reference   
void goononhl(Car *C)                   Garage::Garage(Car &c): ownedCar(c) is valid as void Garage(Car &c) {Car &sameCar =c;     }
{
    c->drive(1000);
}
int main ()
{
    Car newCar ((char *)) 'White');                     
    goonHoliday(&newCar);
    newCar.show();
}

121.
HAshing transforms keys into numerical inices using a hash fuction to store and retrive data efficiently
a b c d e f g h i j k l
Index A[1] = a
A[2] = b
-1 bc no 8 literu
Algorithm isa set od computational steps that trasnform input to output
operation counting: 1+1
Tn  = if we have 1 o3 N, N-1, if we have 0 03 N+1, N
while and log, than our while will logn2 + 1
when quadratic wqe times only one n to the previous one

Sigma  NsigI=1 i = N(n+1)podilt na 2;       NsigI=1 1 = N; 

bsigI=a 1 = b - a + 1
for (i = a; i <=b; i ++)

Worst case in array our i < N, N+1
            BigO the growth of function   Once n is biogger than n0, tn is alwaysn smaller or eqeual to m F(n)

Slowest to fastetst GROWTH
constant<logn<(nTOc, 0 < c <1)<nlogn<nto2<2ton<n!
So complete the fastest is reverse





131
If radio is turn on our memory on mirobict is smaller
Datagrams 

ubit.diaplay.scroll(b[0])   PacketBuffer4 b(2) sequence of 2 bytes
b[0] = 255;
ubit.radio.datagram.send(b)

Heap(malloc) = dynamiclly memory for variables that known at runtime, with heap top is up and read from top to bottom

Stack = stores all loal variables and functrions arguments
#So when this is called, all the necessary variables that the function needs will be transferred to the stack. 

Display on sreenccccccccccccccccc screen /dev/ttyACM0 115200`

Why, if we go from 64 bits to 48 bits, why is this equivalent to using the lower half and the high half of the full memory? Because if you remove the first, if you ignore the first four digit hexadecimal digits. mmediately you drop from 16 hexadecimal to 12, which is equivalent to 48 bits. so from 0 to 7
So the next one is. So if you add one here, everything will become zero and the same one will become eight.But the virtually what happens is you go from seven on that on and all lives to the next to this, which is eight and all zeros.

How to read addresses
In stack top is down, and we read from top to bottom if little endian we read from biggest to smallest
if he we doing in revers 

(gdb) info stack
#0  func1 (a=7) at SCC131_example2.c:5  
#1  0x00005555555551b3 in main () at SCC131_example2.c:10  
(gdb) info frame 0              //Display information abouit staqk frame 0, which corresponds to func 1
Stack frame at 0x7fffffffdf60:          //Addres that signifies the begining of the fram 0, andd the end of frame 1
 rip = 0x55555555517f in func1 (SCC131_example2.c:5); //addres of the next instructions pointer, that frame will return when func1 resumes
 saved rip = 0x5555555551b3  //Address and location in the stack   this frame will return to at the end of func1, when control returns to the previous frame
 called by frame at 0x7fffffffdf80  // addres of the frame that called this frame
 source language c.  

 Arglist at 0x7fffffffdf50, args: a=7  
 Locals at 0x7fffffffdf50,              Previous frame's sp is 0x7fffffffdf60   //When executtion of frame 1 is completed, this frame will pop up and this addres will become the new stack pointer

 Saved registers:  
  rbp at 0x7fffffffdf50, rip at 0x7fffffffdf58 // location

131.Assembly 
when shifting 4 biys - > hex

Mvn Flips
MOVT R0, #0x5678  ; Sets upper 16 bits, lower 16 bits remain unchanged (unpredictable value)
MOV  R0, #0x1234  ; Overwrites the lower 16 bits, but upper 16 bits are cleared
