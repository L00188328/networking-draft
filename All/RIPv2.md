# Router1 config
en
conf t
hostname Router1

int gi0/0
 description LAN
 ip address 192.168.1.1 255.255.255.0
 no shut
 exit

int gi0/1
 description Router2
 ip address 192.168.101.1 255.255.255.0
 no shut
 exit

int gi0/2
 description Router3
 ip address 192.168.102.1 255.255.255.0
 no shut
 exit
 
 int gi0/3
 description Router4
 ip address 192.168.103.1 255.255.255.0
 no shut
 exit
exit
wr mem

 # Router2 config
en
conf t
hostname Router2

int gi0/0
 description LAN2
 ip address 192.168.2.2 255.255.255.0
 no shut
 exit

int gi0/1
 description Router1
 ip address 192.168.101.2 255.255.255.0
 no shut
 exit

int gi0/2
 description Router4
 ip address 192.168.104.2 255.255.255.0
 no shut
 exit
 
int gi0/3
 description Router3
 ip address 192.168.105.2 255.255.255.0
 no shut
 exit
exit
wr mem

 # Router3 config
en
conf t
hostname Router3

int gi0/0
 description LAN3
 ip address 192.168.3.3 255.255.255.0
 no shut
 exit

int gi0/1
 description Router4
 ip address 192.168.106.3 255.255.255.0
 no shut
 exit

int gi0/2
 description Router1
 ip address 192.168.102.3 255.255.255.0
 no shut
 exit
 
 int gi0/3
 description Router2
 ip address 192.168.105.3 255.255.255.0
 no shut
 exit
 exit
wr mem


 # Router4 config
en
conf t 
hostname Router4

int gi0/0
 description LAN4
 ip address 192.168.4.4 255.255.255.0
 no shut
 exit

int gi0/1
 description Router3
 ip address 192.168.106.4 255.255.255.0
 no shut
 exit

int gi0/2
 description Router2
 ip address 192.168.104.4 255.255.255.0
 no shut
 exit
 
 int gi0/3
 description Router1
 ip address 192.168.103.4 255.255.255.0
 no shut
 exit
exit
wr mem


# vpcs
ip 192.168.1.101/24 gateway 192.168.1.1

# VPCS2
ip 192.168.2.101/24 gateway 192.168.2.2

# VPCS3
ip 192.168.3.101/24 gateway 192.168.3.3

# VPCS4
ip 192.168.4.101/24 gateway 192.168.4.4


# Turn on the RIP per router
hostname Router1

router rip
 version 2
 no auto-summary
 network 192.168.1.0
 network 192.168.101.0
 network 192.168.102.0
 network 192.168.103.0
 exit

# hostname Router2

router rip
 version 2
 no auto-summary
 network 192.168.2.0
 network 192.168.101.0
 network 192.168.104.0
 network 192.168.105.0
 exit

# hostname Router3

router rip
 version 2
 no auto-summary
 network 192.168.3.0
 network 192.168.106.0
 network 192.168.102.0
 network 192.168.105.0
 exit


# hostname Router4

router rip
 version 2
 no auto-summary
 network 192.168.4.0
 network 192.168.106.0
 network 192.168.104.0
 network 192.168.103.0
 exit
