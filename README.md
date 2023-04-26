#BGP
router BGP 300
net 10.0.0.0 
net 40.0.0.0
neighbor 40.0.0.2 remote-as 600
neighbor 20.0.0.1 remote-as 600
exit 


router BGP 600
net 40.0.0.0 
net 20.0.0.0
net 50.0.0.0
neighbor 40.0.0.1 remote-as 300
neighbor 10.0.0.1 remote-as 300
neighbor 50.0.0.1 remote-as 900
neighbor 30.0.0.1 remote-as 900
exit 
do write memory

router BGP 900
net 30.0.0.0 
net 50.0.0.0
neighbor 50.0.0.2 remote-as 600
neighbor 20.0.0.1 remote-as 600
exit 
do write memory

#OSPF
router ospf 1
network 10.0.0.0 0.255.255.255 area 0
network 40.0.0.0 0.255.255.255 area 0

router ospf 2
network 40.0.0.0 0.255.255.255 area 0
network 20.0.0.0 0.255.255.255 area 1
network 50.0.0.0 0.255.255.255 area 2

router ospf 3
network 30.0.0.0 0.255.255.255 area 2
network 50.0.0.0 0.255.255.255 area 2

#DHCP
config t 
int fa0/0
ip address 10.0.0.1 255.0.0.0
no shutdown
ip dhcp pool net1
network 10.0.0.1 255.0.0.0
exit
int fa1/0
ip address 20.0.0.1 255.0.0.0
no shutdown
ip dhcp pool net2
network 20.0.0.1 255.0.0.0
