# Initial setup
en
conf t
hostname Switch9B
ip default-gateway 10.0.10.20
no ip domain-lookup


# VLAN
vlan 5
    name Clients
exit

vlan 6
    name Servers
exit

vlan 10
    name NetMan
exit
int vlan 10
    description "interface to NetMan"
    ip address 10.0.10.11 255.255.255.0
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



exit

wr mem






    

