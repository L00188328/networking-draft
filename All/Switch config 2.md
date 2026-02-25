en
conf t
hostname Switch23
no logging console informational
no ip domain-lookup
exit
wr mem


en
conf t
int vlan 1
ip address 192.168.1.22 255.255.255.0
no shut
exit
exit

# specify static address
mac address-table static 0005.5E40.8403 vlan 1 interface gi1/1

# Set age time 
mac address-table aging-time 400

# Configure a range of ports
int range gi0/1-3
 switchport mode access
 exit 

 # Port securtiy
 conf t
int range gi1/0-3
 switchport mode access
 switchport port-security mac-address sticky
 switchport port-security violation protect
exit
exit

# 

conf t
int range gi2/0-3                          
 switchport mode access
 switchport port-security maximum 3
 switchport port-security violation shutdown
exit
exit

# Check for violation
show port-security interface gi1/3

# More security
interface FastEthernet0/5
 description XXXXXXXXX
 switchport access vlan 5
 switchport mode access
 switchport port-security
 switchport port-security aging time 2
 switchport port-security violation restrict
 switchport port-security aging type inactivity
 macro description cisco-desktop
