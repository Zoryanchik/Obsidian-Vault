![[Pasted image 20251230200807.png]]![[Pasted image 20251230200935.png]]## 1. Line Termination (Physical Layer)

This is the "entry gate."

- **What happens:** The router receives raw electrical, optical, or radio signals from the physical cable.
    
- **The Goal:** It converts these physical signals back into digital bits (0s and 1s) that the computer can understand.
    

## 2. Link Layer Protocol (Data Link Layer)

This is the "envelope opener."

- **What happens:** It handles protocols like Ethernet. It checks for errors to make sure the data wasn't corrupted during transmission and strips off the outer layer of the data "envelope."
    
- **The Goal:** To get the data ready for the actual decision-making process.
    

## 3. Lookup, Forwarding, & Queuing (Network Layer)

This is the "brain" of the input port, often called **Decentralized Switching**.

- **Lookup:** The port looks at the destination address in the packet header. It uses a local **forwarding table** (a copy of the master list) to decide which output port this packet needs to go to. This is called **"match plus action."**
    
- **Queuing:** If the "switch fabric" (the internal highway) is busy or if packets are arriving too fast, the packets wait in a line (the red bars in the image).
    
- **The Goal:** Processing everything at **'line speed'**—meaning the router works so fast that it doesn't slow down the incoming traffic.
    

---

### Why "Decentralized"?

Instead of every packet waiting for one central "boss" (the CPU) to tell it where to go, each input port has its own copy of the forwarding table. This allows the router to handle millions of packets per second simultaneously.

**Would you like me to explain what happen**
![[Pasted image 20251230201533.png]]![[Pasted image 20251230201620.png]]*![[Pasted image 20251230203634.png]]*![[Pasted image 20251230204111.png]]![[Pasted image 20251230204209.png]]### Коммутация через память (Memory)

Это самый старый и простой способ, когда пакеты копируются в оперативную память процессора.

- **Как работает:** Пакет поступает на вход, процессор копирует его в память, определяет порт вывода и копирует пакет на нужный выход.
    
- **Минус:** Скорость ограничена пропускной способностью памяти (нужно два обращения к памяти на один пакет). Только один пакет может обрабатываться в один момент времени.
    

### 2. Коммутация через шину (Bus)

Входные и выходные порты соединены одной общей шиной.

- **Как работает:** Входной порт добавляет к пакету специальную метку (заголовок), пакет идет по шине, и только нужный выходной порт его забирает.
    
- **Минус:** **Конфликт шины.** Поскольку шина одна, только один пакет может передаваться в конкретный момент. Если придет сразу несколько пакетов на разные выходы, им придется стоять в очереди. Скорость ограничена скоростью самой шины.
    

### 3. Коммутация через полносвязную сеть (Interconnection Network / Crossbar)

Самый продвинутый и быстрый вариант, который используется в современных мощных роутерах.

- **Как работает:** Это сетка (матрица) путей. В узлах сетки стоят переключатели, которые могут открываться и закрываться.
    
- **Главный плюс:** **Параллелизм.** Несколько пакетов могут передаваться одновременно, если они идут на разные выходы. Например, пакет из Входа А в Выход Б не мешает пакету из Входа В в Выход Г.
    
- **Эффективность:** Это позволяет достичь той самой «желаемой скорости» ($N \times \text{line rate}$), о которой написано в тексте на слайде.
![[Pasted image 20251230204446.png]]
![[Pasted image 20251230204520.png]]