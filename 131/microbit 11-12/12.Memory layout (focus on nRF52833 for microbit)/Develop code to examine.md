![[Pasted image 20250210175825.png]]
![[Pasted image 20250210175957.png]]
### **Terminal Tab**

- **Purpose:**
    
    - Displays the **serial output** sent by the Micro:bit using the `uBit.serial.printf()` function in the code.
    - The output shows the results of the program as it runs on the Micro:bit hardware.
- **Configuration:**
    
    - The terminal connects to the Micro:bit's **serial port** using the `screen` command:  
        `screen /dev/ttyACM0 115200`
        - `/dev/ttyACM0` refers to the Micro:bit's serial communication port on the computer.
        - `115200` is the baud rate (speed of communication).
- **Displayed Output:**
    
    - Any text printed with `uBit.serial.printf()` in the code is sent to the terminal. For example:
        - **"entered func1"** from the function `func1`.
        - **"hello world"** from the `main` function.
![[Pasted image 20250210180416.png]]![[Pasted image 20250210180538.png]]![[Pasted image 20250210180606.png]]![[Pasted image 20250210180626.png]]

