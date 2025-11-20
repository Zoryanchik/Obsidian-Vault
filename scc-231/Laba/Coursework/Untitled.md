![[Pasted image 20251119234637.png]]![[Pasted image 20251119235053.png]]![[Pasted image 20251119235112.png]]![[Pasted image 20251119235154.png]]
``` Python 

```from mininet.topo import Topo
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


class courseworkTopo(Topo):

    def build(self):
        # Add hosts with IP addresses and default routes
        host1 = self.addHost('host1', ip='192.168.0.2/24',
                             defaultRoute='via 192.168.0.1')
        
        host2 = self.addHost('host2', ip='192.168.0.3/24',
                             defaultRoute='via 192.168.0.1')
        
        host3 = self.addHost('host3', ip='192.168.2.2/24',
                             defaultRoute='via 192.168.2.1')
        
        host4 = self.addHost('host4', ip='192.168.2.3/24',
                             defaultRoute='via 192.168.2.1')
        
        host5 = self.addHost('host5', ip='192.168.3.2/24',
                             defaultRoute='via 192.168.3.1')

        # Add routers with static routes using LinuxRouter class
        router1 = self.addHost('router1', cls=LinuxRouter, ip=None,
                               routes=[
                                   ('192.168.3.0/24', '10.10.1.2'),
                                   ('192.168.2.0/24', '10.10.0.1')
                               ])
        
        router2 = self.addHost('router2', cls=LinuxRouter, ip=None,
                               routes=[
                                   ('192.168.0.0/24', '10.10.0.2'),
                                   ('10.10.1.0/24', '10.10.0.2'),
                                   ('192.168.3.0/24', '10.10.0.2')
                               ])
        
        router3 = self.addHost('router3', cls=LinuxRouter, ip=None,
                               routes=[
                                   ('192.168.0.0/24', '10.10.1.1'),
                                   ('10.10.0.0/24', '10.10.1.1'),
                                   ('192.168.2.0/24', '10.10.1.1')
                               ])

        # Add switches
        switch1 = self.addSwitch('switch1')
        switch2 = self.addSwitch('switch2')

        # Add links: hosts to switches (no bandwidth/delay/loss constraints)
        self.addLink(host1, switch1, intfName1='host1-eth0',
                     params1={'ip': '192.168.0.2/24'})
        
        self.addLink(host2, switch1, intfName1='host2-eth0',
                     params1={'ip': '192.168.0.3/24'})
        
        self.addLink(host3, switch2, intfName1='host3-eth0',
                     params1={'ip': '192.168.2.2/24'})
        
        self.addLink(host4, switch2, intfName1='host4-eth0',
                     params1={'ip': '192.168.2.3/24'})

        # Add link: router1-eth1 to switch1
        self.addLink(router1, switch1, intfName1='router1-eth1',
                     params1={'ip': '192.168.0.1/24'})
        
        # Add link: router2-eth1 to switch2
        self.addLink(router2, switch2, intfName1='router2-eth1',
                     params1={'ip': '192.168.2.1/24'})

        # Add link: router1-eth2 to router2-eth2 (10ms delay, 1% loss)
        self.addLink(router1, router2, 
                     intfName1='router1-eth2', intfName2='router2-eth2',
                     params1={'ip': '10.10.0.2/24'}, 
                     params2={'ip': '10.10.0.1/24'},
                     delay='10ms', loss=1)

        # Add link: router1-eth3 to router3-eth2 (100 Mbit/s, 100ms delay)
        self.addLink(router1, router3,
                     intfName1='router1-eth3', intfName2='router3-eth2',
                     params1={'ip': '10.10.1.1/24'}, 
                     params2={'ip': '10.10.1.2/24'},
                     bw=100, delay='100ms', loss=0)

        # Add link: router3-eth0 to host5 (direct connection)
        self.addLink(router3, host5,
                     intfName1='router3-eth0', intfName2='host5-eth0',
                     params1={'ip': '192.168.3.1/24'},
                     params2={'ip': '192.168.3.2/24'})


# the topologies accessible to the mn tool's `--topo` flag
# note: if using the Dockerfile, this must be the same as in the Dockerfile
topos = {'courseworkTopo': (lambda: courseworkTopo())}


if __name__ == '__main__':
    # With the code below, you can run the topology directly, using the command `python3 topology.py`
    from mininet.net import Mininet
    from mininet.cli import CLI
    from mininet.log import setLogLevel
    from mininet.nodelib import LinuxBridge
    from mininet.link import TCLink

    setLogLevel('info')

    topo = courseworkTopo()
    net = Mininet(topo=topo, controller=None,
                  autoSetMacs=True, build=True, switch=LinuxBridge, link=TCLink)
    net.start()
    CLI(net)
    net.stop()
    
    
    
    *** Ping: testing ping reachability host1 -> host2 X X X X X X  host2 -> host1 X X X X X X  host3 -> X X host4 X X X X  host4 -> X X host3 X X X X  host5 -> X X X X X X router3  router1 -> X X X X X X X  router2 -> X X X X X X X  router3 -> X X X X host5 X X  *** Results: 89% dropped (6/56 received)
	    now all good