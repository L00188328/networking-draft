# Hostname - change the hostname
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

# Set up the terminal

# Configure the client ports 
# Basic port security
# Set up loop avoidance

# check the status of interfaces
show interface status

# make vlan
conf t
vlan 10
 name NETMAN
exit
end

# make interface
conf t
interface Vlan10
 ip address 192.168.10.23 255.255.255.0
 no shutdown
exit
end
wr mem

# Check interface ips 
en
show ip interface brief | include Vlan

# make a port trunk so other clan traffic can pass
conf t
interface gi3/3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10
 no spanning-tree bpduguard enable
 no spanning-tree guard root
end


