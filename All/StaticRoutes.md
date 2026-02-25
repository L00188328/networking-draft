# vpc config
ip 192.168.1.101/24 gateway 192.168.1.1


# vpc 2
ip 192.168.2.101/24 gateway 192.168.2.2


# router 1
conf t
hostname Router1

int gi0/1
 ip address 192.168.1.1 255.255.255.0
 no shut
 exit
int gi0/0
 ip address 192.168.3.1 255.255.255.0
 no shut
 exit
exit

# router 2
conf t
hostname Router2

int gi0/1
 ip address 192.168.2.2 255.255.255.0
 no shut
 exit
int gi0/0
 ip address 192.168.3.2 255.255.255.0
 no shut
 exit
exit

# on router 1
ip route 192.168.2.0 255.255.255.0 192.168.3.2

# on router 2
ip route 192.168.1.0 255.255.255.0 192.168.3.1
