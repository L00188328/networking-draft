en
conf t
hostname Router10
enable secret r

interface Loopback1
 ip address 192.168.255.10 255.255.255.255

interface GigabitEthernet0/0
 ip address 192.168.238.10  255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit
 
interface GigabitEthernet0/1
 ip address 192.168.1.10 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit
 
interface GigabitEthernet0/2
 ip address 192.168.2.10 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit

router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
 network 192.168.238.0 0.0.0.255 area 0
 exit
exit
wr mem

# Router 11
en
conf t
hostname Router11
enable secret r

interface Loopback1
 ip address 192.168.255.11 255.255.255.255

interface GigabitEthernet0/0
 ip address 192.168.238.11 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit
 
interface GigabitEthernet0/1
 ip address 192.168.2.11 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit
 
interface GigabitEthernet0/2
 ip address 192.168.3.11 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit

router ospf 1
 network 192.168.3.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
 network 192.168.238.0 0.0.0.255 area 0
 exit
exit
wr mem

# show neighbours
show ip ospf neighbor 

# Clear ip ospf info on router 
clear ip ospf process

# show status
show ip protocols 

# route
sh ip route

# change cost
interface GigabitEthernet0/0
 ip address 192.168.238.10 255.255.255.0
 ip ospf cost 10
 duplex auto
 speed auto

 # look into the interface to see cost
 sh ip ospf int gi0/0

# Cloud to router 2
en
conf t
hostname Router2

int gi0/1
 ip address DHCP
 no shut

interface Loopback1
 ip address 192.168.255.2 255.255.255.255

interface GigabitEthernet0/0
 ip address 192.168.238.2 255.255.255.0
 duplex auto
 speed auto
 no shutdown
exit

router ospf 1
 default-information originate always
 network 192.168.238.0 0.0.0.255 area 0
 exit

exit
wr mem

# nat router 2
en
conf t
ip nat inside source list 1 int gi0/1 overload
access-list 1 permit any
int gi0/1
 ip nat outside
int gi0/0
 ip nat inside

 interface GigabitEthernet0/0
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 MyMD5
 exit

 # rputer 10
 interface GigabitEthernet0/0
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 MyMD5
 exit
  
interface GigabitEthernet0/2
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 MyMD5
 exit
exit

# router11
interface GigabitEthernet0/0
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 MyMD5
 exit

interface GigabitEthernet0/1
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 MyMD5
 exit


 # check
 sh ip ospf int gi0/0

 # timers On Router10 do both at once or neighbour down error
int gi0/2
 ip ospf hello-interval 5
 ip ospf dead-interval 20
 exit
exit
On Router11


 # timers On Router11
int gi0/1
 ip ospf hello-interval 5
 ip ospf dead-interval 20
 exit
exit

# interface to become passive.
passive-interface gi0/0


# all interfaces to become passive.
 passive-interface default

# enables the protocol on that interface only.
 no passive-interface gi0/0