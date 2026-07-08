![[Pasted image 20251231165447.png]]![[Pasted image 20251231170027.png]]![[Pasted image 20251231170227.png]]![[Pasted image 20251231170240.png]]![[Pasted image 20251231170325.png]]![[Pasted image 20251231170441.png]]
ring 1 guest os that speaks to OS ![[Pasted image 20251231171219.png]]
![[Pasted image 20251231171305.png]]![[Pasted image 20251231171409.png]]### 1. Паравиртуализация (Hypercalls)

Представьте, что Гостевая ОС — это вежливый сотрудник, который знает, что он не начальник.

- **Как это работает:** ОС **знает**, что она виртуальная. В её код (ядро) специально внесены изменения.
    
- **Действие:** Когда ей нужно сделать что-то важное (например, обратиться к памяти), она не пытается сделать это сама. Она специально делает "звонок" (Hypercall) начальнику (Гипервизору): _"Привет, мне нужно выделить память, сделай это за меня, пожалуйста"_.
    
- **Итог:** Это **осознанное общение** через вызовы. Без этих вызовов ничего работать не будет.
    

### 2. Hardware-Assisted (Trap / Ловушка)

Представьте, что Гостевая ОС — это сотрудник, который **думает**, что он тут самый главный (хотя на самом деле он в симуляции).

- **Как это работает:** Мы берем обычную Windows или Linux (без изменений в коде). Она не знает ни про какой гипервизор.
    
- **Действие:** ОС пытается нагло выполнить команду напрямую через процессор: _"Я хочу стереть диск!"_.
    
- **Реакция железа:** Тут вступает в дело **Hardware (процессор)**. У него стоит "сигнализация". Как только ОС пытается сделать что-то запрещенное, процессор **автоматически** срабатывает (это называется **Trap** или "ловушка"), ставит ОС на паузу и вызывает Гипервизор: _"Смотри, она опять пытается лезть к диску, разберись"_.
    
- **Итог:** Вы правы, нам **не нужны Hypercalls** (звонки от самой системы). Процессор (железо) делает всю грязную работу по перехвату управления сам.![[Pasted image 20251231171503.png]]


|**Feature**|**Paravirtualization**|**Hardware-Assisted Virtualization**|
|---|---|---|
|**OS Modification**|**Required.** The Guest OS kernel must be modified to use hypercalls.|**Not Required.** The CPU hardware manages the interception of instructions.|
|**How it works**|The OS explicitly asks the Hypervisor for help (Hypercalls).|The Hardware automatically pauses the OS and wakes the Hypervisor (Traps).|
|**Portability**|**Low.** You are limited to specific, modified Operating Systems.|**High.** You can run unmodified, off-the-shelf Operating Systems.|
|**Performance**|Fast (low overhead), but requires maintenance of modified OS code.|Very Fast (hardware optimized).|
![[Pasted image 20251231171839.png]]