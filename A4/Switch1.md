# Initial setup
en
conf t
hostname Switch1
no ip domain-lookup


# VLAN
vlan 5
    name Clients
exit
int vlan 5
    description "interface to CientsNet"
    ip address 10.0.5.1 255.255.255.0
    vrrp 5 ip 10.0.5.20
    vrrp 5 priority 100
    vrrp 5 preempt
    no shut
    

vlan 6
    name Servers
exit
int vlan 6
    description "interface to ServersNet"
    ip address 10.0.6.1 255.255.255.0
    vrrp 6 ip 10.0.6.20
    vrrp 6 priority 100
    vrrp 6 preempt
    no shut
exit


vlan 10
    name NetMan
exit
int vlan 10
    description "interface to NetMan"
    ip address 10.0.10.1 255.255.255.0
    vrrp 10 ip 10.0.10.20
    vrrp 10 priority 100
    vrrp 10 preempt
    no shut
exit

vlan 1000
    name Discard
exit

vlan 999
    name Native
exit


# Access Ports
int range gi0/0-3
    description Clients
    switchport access vlan 5
    switchport port-security mac-address sticky
    switchport port-security violation protect
    negotiation auto
    spanning-tree portfast edge
    spanning-tree bpduguard enable
    exit
int range gi1/0-3
    description Servers
    switchport access vlan 6
    spanning-tree portfast edge
    spanning-tree bpduguard enable
    exit

# Shutdown Ports      
int range gi2/0-3
    description UNUSED
    switchport mode access
    switchport access vlan 1000
    shutdown
    exit


# Tagged Ports
int range gi3/0-3
    switchport trunk encapsulation dot1q
    switchport mode trunk
    switchport trunk native vlan 999
    switchport trunk allowed vlan 5,6,10,999,1000
exit

ip routing 

exit

wr mem






    

