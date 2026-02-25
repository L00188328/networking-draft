# configure switch 21
en
conf t

hostname Switch21

# Configure VLANs
vlan 2
 name Hosts
 exit
vlan 3
 name StaffRadio
 exit
vlan 4
 name Power
 exit
vlan 5
 name Clients
 exit
vlan 6
 name Servers
 exit
vlan 10
 name NetMan
 exit
vlan 14
 name Loopbacks
 exit
vlan 15
 name Routers
 exit
vlan 999
 name Native
 exit
vlan 1000
 name Discard
 exit

# Configure ports
Interface range GigabitEthernet0/0-3
 description Clients
 switchport access vlan 10
 switchport mode access
 negotiation auto
 exit
 
Interface range GigabitEthernet1/0-3
 description Servers
 switchport access vlan 6
 switchport mode access
 negotiation auto
 exit 

Interface range GigabitEthernet2/0-3
 description Unused
 switchport access vlan 1000
 switchport mode access
 negotiation auto
 shutdown
 exit
 
Interface range GigabitEthernet3/0-3
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 999
 switchport mode trunk
 negotiation auto
 exit

# Configure SVI for management only
interface Vlan10
 description "interface to NetMan"
 ip address 10.1.10.21 255.255.255.0
 no shut
 exit

exit
wr mem


# vpc set address
ip 10.1.10.101 255.255.255.0 10.1.10.1



# router config
en
conf t

hostname Router1

# Enable the physical interface
int gi0/0
 no shut
 exit

# Set up VLANs
int gi0/0.10
 encapsulation dot1Q 10 
 ip address 10.1.10.1 255.255.255.0
 no shut
 exit


# sub interface for vlan 5
int gi0/0.5
 encapsulation dot1Q 5
 ip address 10.1.5.1 255.255.255.0
 no shut
 exit

 # sub interface for vlan 6
int gi0/0.6
 encapsulation dot1Q 6
 ip address 10.1.6.1 255.255.255.0
 no shut
 exit

 # move port Gi0/1 to vlan 5
 conf t
interface GigabitEthernet0/1
 switchport access vlan 5
 exit


# vpc2 set address
ip 10.1.5.102 255.255.255.0 10.1.5.1