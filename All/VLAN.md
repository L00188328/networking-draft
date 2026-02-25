# vlan configuration show
show vlan

# delete configuration
write erase

## also delete vlan.dat

# create a vlan
vlan 999

# set up  a vlan with ip address
en
conf t
vlan 10
 name NetMan
 exit
int vlan 10 
 description "interface to NetMan"
 ip address 192.168.10.23 255.255.255.0
 no shut
exit
exit
wr mem

# Switch to trunk port
en
conf t
int range gi3/0-3
 switchport trunk native vlan 999
 switchport trunk encapsulation dot1q
 switchport mode trunk               
 exit
exit
wr mem

# setting a port 
en
conf t
interface gi0/1
 description Netman
 switchport access vlan 10
 switchport mode access 
 exit
exit
wr mem

# see files
dir all-filesystems

# create a lot of vlans on switch 3
en
conf t
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
vlan 7
 name Telephony
 exit
vlan 8
 name HVAC
 exit
vlan 9
 name Storage
 exit
vlan 11
 name Cameras
 exit
vlan 12
 name OOBM
 exit
vlan 13
 name Clusters
 exit
vlan 14
 name Loopbacks
 exit
vlan 15
 name Routers
 exit
exit
wr mem 

# check trunk status
show interface trunk

# configure vtp on switch 1
en
conf t
vtp mode server
 vtp domain DonegalSME
 vtp password DSME
 vtp version 3
 exit
exit
vtp primary vlan

# back on swtich 3 check if it workes
en
show vtp status

show vtp password


# more config for the switch 2 and 3
en
conf t
vtp mode client
 vtp domain DonegalSME
 vtp password DSME
 vtp version 3
exit

# configure ports as clients and servers
en
conf t
int range gi1/0-3
 description Clients
 switchport access vlan 5
 exit
int range gi2/0-3
 description Servers
 switchport access vlan 6
 exit 
exit
wr mem

# turns off negogiate trunk links on the correct ports for be careful
conf t
switchport nonegotiate
exit
wr mem

# check
show int gi0/1 switchport

# create a discard vlan
en
conf  t
vlan 1000
 name Discard
exit
wr mem

# move uinunsed ports into shutdown vlan
en
conf t
int gi0/0
 description Shutdown
 switchport access vlan 1000
 shutdown
exit

int range gi0/2-3
 description Shutdown
 switchport access vlan 1000
 shutdown
exit
exit
wr mem

#  create vlan 999
en
conf t
vlan 999
 name Native
exit
exit
wr mem

## edit many vlan interface address
en
conf t

ip routing

int vlan 2
 description "Hosts Router"
 ip address 192.168.2.23 255.255.255.0
 no shut
 exit

int vlan 3
 description "Radio Router"
 ip address 192.168.3.23 255.255.255.0
 no shut
 exit

int vlan 4
 description "PowerLAN Router"
 ip address 192.168.4.23 255.255.255.0
 no shut
 exit

int vlan 5
 description "Cients Router"
 ip address 192.168.5.23 255.255.255.0
 no shut
 exit
 
int vlan 6
 description "Servers Router"
 ip address 192.168.6.23 255.255.255.0
 no shut
 exit

int vlan 7
 description "Telephony Router"
 ip address 192.168.7.23 255.255.255.0
 no shut
 exit

 int vlan 8
 description "HVAC Router"
 ip address 192.168.8.23 255.255.255.0
 no shut
 exit

 int vlan 9
 description "Storage Router"
 ip address 192.168.9.23 255.255.255.0
 no shut
 exit

 int vlan 10
 description "NETMAN Router"
 ip address 192.168.10.23 255.255.255.0
 no shut
 exit

 int vlan 11
 description "Cameras Router"
 ip address 192.168.11.23 255.255.255.0
 no shut
 exit

 int vlan 12
 description "OOBM Router"
 ip address 192.168.12.23 255.255.255.0
 no shut
 exit

 int vlan 13
 description "Clusters Router"
 ip address 192.168.13.23 255.255.255.0
 no shut
 exit

 int vlan 14
 description "Loopbacks Router"
 ip address 192.168.14.23 255.255.255.0
 no shut
 exit

 int vlan 15
 description "Routers Router"
 ip address 192.168.15.23 255.255.255.0
 no shut
 exit
 
 exit
 wr mem