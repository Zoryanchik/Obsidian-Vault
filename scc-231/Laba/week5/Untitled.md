# SCC.231 Week 5&6 Lab activity: Socket Programming

## Part 1: Implementing an echo service

### Task 1: Implement an Echo Server & Task 3: Implementing I/O Multiplexing with `select`

```
import select
import socket
import time

HOST = '0.0.0.0'  # Listen on all available interfaces
PORT = 12345       # Port to listen on


def main():
    # Create a TCP socket
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Set socket options to handle TIME_WAIT better
    server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEPORT, 1)

    # Bind the socket to the specified host and port
    server_socket.bind((HOST, PORT))

    # Initialize list of sockets to monitor for incoming data
    rfds = [server_socket]

    # Start listening for incoming connections
    server_socket.listen()

    # Use an infinite loop to handle incoming connections and data
    while True:

        # Use select to wait for any socket to be ready for processing
        rlist, _, _ = select.select(rfds, [], [])

        # Check if there is a new connection request
        if server_socket in rlist:
            # Accept a new client connection
            client_socket, client_address = server_socket.accept()
            print(f"Accepted connection from {client_address}")
            # Add the new client socket to the list of monitored sockets
            rfds.append(client_socket)

            # Remove the server socket from the ready list to avoid processing it again in the next step
            rlist.remove(server_socket)

        for client_socket in rlist:
            # Basic check to ensure the client_socket is still valid
            if client_socket not in rfds:
                continue

            # Receive data from the client
            data = client_socket.recv(1024)

            # If the data starts with byte 0xff or if no data is received, close the connection
            if data.startswith(b'\xff') or len(data) == 0:
                # Close the client socket
                client_socket.close()
                rfds.remove(client_socket)
                break

            # Get the port number and the IP of the client socket
            client_port = client_socket.getpeername()[1]
            client_ip = client_socket.getpeername()[0]

            # Add timestamp when data is received and prepare response
            timestamp = time.time()
            print(f"[{client_ip}:{client_port}] {timestamp}:{data}")
            timestamped_response = f"{timestamp}:{data.decode()}"

            # Echo back with timestamp
            client_socket.sendall(timestamped_response.encode())


if __name__ == "__main__":
    main()
```

### Task 2: Implement an Echo Client

```
import socket
import time

# You may need to change the HOST to the server's IP address, in task 2
HOST = '10.0.0.1'  # Listen on all available interfaces
PORT = 12345       # Port to listen on


def main():
    # Create a TCP socket
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Connect to the server
    server_socket.connect((HOST, PORT))

    print("Type messages and press Enter")
    print("To quit: Ctrl+C or Ctrl+D")

    while True:
        try:
            # read user input
            message = input("> ")
        except EOFError:
            print("Ctrl+D detected. Exiting...")
            break
        except KeyboardInterrupt:
            print("Ctrl+C detected. Exiting...")
            break
        if not message:
            # empty message, exit loop
            break

        # Append timestamp to message and send to server
        message = f'{time.time()}:{message}'
        server_socket.sendall(message.encode())

        # Receive response from server and print formatted output
        response = server_socket.recv(1024)
        print(f"{time.time()}:{response.decode()}")

    # Close the socket
    server_socket.close()


if __name__ == "__main__":
    main()
```

### Part 2: Static Routing in Mininet

```
from mininet.topo import Topo
from mininet.node import Node


class LinuxRouter(Node):
    def config(self, **params):
        super(LinuxRouter, self).config(**params)
        if 'routes' in params:
            for (ip, gateway) in params['routes']:
                self.cmd('ip route add {} via {}'.format(ip, gateway))
        self.cmd('sysctl net.ipv4.ip_forward=1')

    def terminate(self):
        self.cmd('sysctl net.ipv4.ip_forward=0')
        super(LinuxRouter, self).terminate()


class TutorialTopology(Topo):

    def build(self):
        # add two host to the network
        h1 = self.addHost('h1', ip='10.0.0.2/24', defaultRoute='via 10.0.0.1')
        h2 = self.addHost('h2', ip='10.0.0.1/24', cls=LinuxRouter, routes=[
                          ('10.1.0.0/24', '192.168.0.1')])
        h3 = self.addHost('h3', ip='10.1.0.1/24', cls=LinuxRouter, routes=[
                          ('10.0.0.0/24', '192.168.0.2')])
        h4 = self.addHost('h4', ip='10.1.0.2/24', defaultRoute='via 10.1.0.1')

        # add a switch to the network
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')

        # add a link between the hosts `h1` and `h2` and the `s1` switch
        self.addLink(h1, s1, intfName1='h1-eth0',
                     params1={'ip': '10.0.0.2/24'}, bw=100, delay="30ms", loss=1)
        self.addLink(h2, s1, intfName1='h2-eth0',
                     params1={'ip': '10.0.0.1/24'}, bw=10, delay="10ms", loss=1)
        self.addLink(h3, s2, intfName1='h3-eth0',
                     params1={'ip': '10.1.0.2/24'}, bw=100, delay="100ms", loss=0)
        self.addLink(h4, s2, intfName1='h4-eth0',
                     params1={'ip': '10.1.0.1/24'}, bw=100, delay="100ms", loss=0)
        self.addLink(h2, h3, intfName1='h2-eth1', intfName2='h3-eth1',
                     params1={'ip': '192.168.0.2/24'}, params2={
                         'ip': '192.168.0.1/24'})


# the topologies accessible to the mn tool's `--topo` flag
# note: if using the Dockerfile, this must be the same as in the Dockerfile
topos = {'tutorialTopology': (lambda: TutorialTopology())}

if __name__ == '__main__':

    # With the code below, you can run the topology directly, using the command `python3 topology.py`
    from mininet.net import Mininet
    from mininet.cli import CLI
    from mininet.log import setLogLevel
    from mininet.nodelib import LinuxBridge
    from mininet.link import TCLink

    setLogLevel('debug')

    topo = TutorialTopology()
    net = Mininet(topo=topo, controller=None,
                  autoSetMacs=True, build=True, switch=LinuxBridge, link=TCLink)
    net.start()
    CLI(net)
    net.stop()
```