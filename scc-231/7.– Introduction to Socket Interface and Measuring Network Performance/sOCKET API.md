![[Pasted image 20251030200836.png]]a **socket** is an **API** (Application Programming Interface) that acts like a file, allowing a **process** (application) to send and receive messages over a network.

It's the endpoint for communication, connecting the application (controlled by the developer) to the network layers (controlled by the OS).
![[Pasted image 20251030201105.png]]![[Pasted image 20251030201316.png]]![[Pasted image 20251030201715.png]]![[Pasted image 20251030201908.png]]![[Pasted image 20251030202217.png]]![[Pasted image 20251030202248.png]]![[Pasted image 20251030203043.png]]DGRAm = udp protocol]![[Pasted image 20251030203935.png]]![[Pasted image 20251030203944.png]]![[Pasted image 20251030204059.png]]![[Pasted image 20251030204136.png]]![[Pasted image 20251030204951.png]]
stream tcp 
![[Pasted image 20251030205348.png]]### Setup Phase

`from socket import *`

- **What it does:** Imports all the necessary functions and constants from the Python `socket` module to allow the program to create and manage network connections.
    

`serverPort = 12000`

- **What it does:** Assigns the number `12000` to a variable. This will be the "door number" (port) on the server that the program will listen on for incoming connections.
    

`serverSocket = socket(AF_INET, SOCK_STREAM)`

- **What it does:** This is the most important setup step. It creates the server's main socket.
    
    - `AF_INET`: This constant specifies the address family. It stands for "Address Family - Internet" and means we are using **IPv4** (standard IP addresses like `192.168.1.1`).
        
    - `SOCK_STREAM`: This constant specifies the socket type. It means we are using a **TCP** socket (as opposed to `SOCK_DGRAM` for UDP). TCP is connection-oriented and reliable, like a phone call.
        

`serverSocket.bind(("", serverPort))`

- **What it does:** This "binds" or "assigns" the socket to the specific port on the server.
    
    - `""`: The empty string means "listen on all available IP addresses" this machine has. A client can connect using any of them.
        
    - `serverPort`: This tells the socket to use port `12000` (which we defined earlier).
        
- **Analogy:** This is like a receptionist setting up their desk at the building's main entrance (the IP address) and putting up a sign that says "Desk #12000".
    

`serverSocket.listen()`

- **What it does:** This tells the operating system to start "listening" for connection requests from clients on this socket. It turns the socket from an active one (that makes calls) into a passive, listening one (that accepts calls).
    

`print 'The server is ready to receive'`

- **What it does:** A simple message to the person running the server, letting them know the setup is complete and it's now waiting for a client.
    

---

### Main Server Loop

`while True:`

- **What it does:** This starts an infinite loop, which means the server will run forever (or until you manually stop it). This allows it to handle one client, and then loop back to the `accept()` line to wait for the next client.
    

`connectionSocket, addr = serverSocket.accept()`

- **What it does:** This line **blocks** and waits. The program will pause here until a client tries to connect to port 12000.
    
- When a client _does_ connect, this line creates a **brand new socket** just for that one client.
    
    - `connectionSocket`: This is the new socket, dedicated to this specific client. All `send` and `recv` operations for this client will happen on _this_ socket.
        
    - `addr`: This contains the client's IP address and port number (their "return address").
        
- **Analogy:** The main `serverSocket` is like the receptionist. When a client (visitor) arrives, the receptionist (`.accept()`) tells them to go talk to a specific employee (`connectionSocket`) who will now handle all their needs. The receptionist then goes back to waiting for the next visitor.
    

`sentence = connectionSocket.recv(1024).decode()`

- **What it does:** This line also **blocks** and waits. It listens on the _new_ `connectionSocket` for the client to send data.
    
    - `.recv(1024)`: Receives data from the client, up to a maximum of `1024` bytes. The data arrives as raw **bytes**.
        
    - `.decode()`: Converts the raw bytes into a regular Python **string** (using UTF-8 by default) so we can read it.
        

`connectionSocket.send(sentence.encode())`

- **What it does:** This sends the data back to the client.
    
    - `sentence`: This is the string we just received.
        
    - `.encode()`: This converts the Python **string** back into raw **bytes**, which is the only format that can be sent over the network.
        
    - `.send()`: Transmits those bytes back to the client over the `connectionSocket`.
        

`connectionSocket.close()`

- **What it does:** This closes the dedicated connection to _this specific client_. The "echo" is complete, so the conversation is over.
    
- The `while True:` loop immediately repeats, and the server goes back to waiting at the `serverSocket.accept()` line for a new client to connect.