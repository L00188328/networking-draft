# Switch21

en
conf t

hostname Switch21
no logging console informational
no ip domain-lookup

int vlan 1
ip address 192.168.1.21 255.255.255.0
no shut

# Servers
int range gi0/1-3
 switchport mode access
 exit 

# Some clients
int range gi1/0-3
 switchport mode access
 switchport port-security mac-address sticky
 switchport port-security violation protect

# Some other clients
int range gi2/0-3                          
 switchport mode access
 switchport port-security maximum 3
 switchport port-security violation shutdown

exit
exit
wr mem

# Check spaning tree 
show spanning-tree
show spanning-tree summary

# Set as root
spanning-tree vlan 1-4090 root primary

# Set secondary switch.
spanning-tree vlan 1-4090 root secondary

# Set port to not be used for connecting to other switch
int gi0/1
 description Netman
 switchport access vlan 10
 switchport mode access
 negotiation auto
 spanning-tree portfast

# Set port to not be used for connecting to other switch
int range gi0/0-3
 description Netman
 switchport access vlan 10
 switchport mode access
 negotiation auto
 spanning-tree portfast

 # Set ports with guard stop loop error

int range gi2/0-3
 description Netman
 switchport access vlan 10
 switchport mode access
 negotiation auto
 spanning-tree portfast edge
 spanning-tree bpduguard enable

# Defend against this port becoming the root port, stops attacker
int range gi0/0-3 
 spanning-tree guard root
