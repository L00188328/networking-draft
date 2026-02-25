# router 1
en
conf t
hostname Router1
no ip domain lookup

int lo0
ip address 10.255.255.1 255.255.255.255

interface GigabitEthernet0/0
ip address 192.168.12.1 255.255.255.0
no shut

interface GigabitEthernet0/1
ip address 192.168.13.1 255.255.255.0
no shut

interface GigabitEthernet0/2
ip address 192.168.14.1 255.255.255.0
no shut

exit

router bgp 1
neighbor 192.168.12.2 remote-as 2
neighbor 192.168.13.3 remote-as 3
neighbor 192.168.14.4 remote-as 4
network 10.255.255.1 mask 255.255.255.255
exit
exit
wr mem

# router 2
en
conf t
hostname Router2
no ip domain lookup

int lo0
ip address 10.255.255.2 255.255.255.255

interface GigabitEthernet0/0
ip address 192.168.12.2 255.255.255.0
no shut

interface GigabitEthernet0/1
ip address 192.168.24.2 255.255.255.0
no shut

interface GigabitEthernet0/2
ip address 192.168.25.2 255.255.255.0
no shut

interface GigabitEthernet 0/3
ip address 192.168.23.2 255.255.255.0
no shut

exit

router bgp 2
neighbor 192.168.12.1 remote-as 1
neighbor 192.168.23.3 remote-as 3
neighbor 192.168.24.4 remote-as 4
neighbor 192.168.25.5 remote-as 5
network 10.255.255.2 mask 255.255.255.255
exit
exit
wr mem

# router 3
en
conf t
hostname Router3
no ip domain lookup

int lo0
ip address 10.255.255.3 255.255.255.255

interface GigabitEthernet0/0
ip address 192.168.13.3 255.255.255.0
no shut

interface GigabitEthernet0/2
ip address 192.168.36.3 255.255.255.0
no shut

interface GigabitEthernet0/3
ip address 192.168.23.3 255.255.255.0
no shut

exit

router bgp 3
 neighbor 192.168.13.1 remote-as 1
 neighbor 192.168.23.2 remote-as 2
 neighbor 192.168.36.6 remote-as 6
 network 10.255.255.3 mask 255.255.255.255
 exit
exit
wr mem

# router 4
en
conf t
hostname Router4
no ip domain lookup

int lo0
 ip address 10.255.255.4 255.255.255.255

interface GigabitEthernet0/0
 ip address 4.4.4.4 255.255.255.0
 no shut

interface GigabitEthernet0/1
 ip address 192.168.14.4 255.255.255.0
 no shut

interface GigabitEthernet0/2
 ip address 192.168.24.4 255.255.255.0
 no shut

exit

router bgp 4
 neighbor 192.168.14.1 remote-as 1
 neighbor 192.168.24.2 remote-as 2
 network 10.255.255.4 mask 255.255.255.255
 network 4.4.4.0 mask 255.255.255.0
 exit
exit
wr mem


# router 5
en
conf t
hostname Router5
no ip domain lookup

int lo0
 ip address 10.255.255.5 255.255.255.255

interface GigabitEthernet0/0
 ip address 5.5.5.5 255.255.255.0
 no shut

interface GigabitEthernet0/1
 ip address 192.168.25.5 255.255.255.0
 no shut

exit

router bgp 5
 neighbor 192.168.25.2 remote-as 2
 network 10.255.255.5 mask 255.255.255.255
 network 5.5.5.0 mask 255.255.255.0
 exit
exit
wr mem


# router 6
en
conf t
hostname Router6
no ip domain lookup

int lo0
 ip address 10.255.255.6 255.255.255.255

interface GigabitEthernet0/0
 ip address 6.6.6.6 255.255.255.0
 no shut

interface GigabitEthernet0/1
 ip address 192.168.36.6 255.255.255.0
 no shut

exit

router bgp 6
 neighbor 192.168.36.3 remote-as 3
 network 10.255.255.6 mask 255.255.255.255
 redistribute connected
 exit
exit
wr mem


# Show
show ip bgp summary 

show ip bgp neighbour

show ip bgp 

show ip protocols 

