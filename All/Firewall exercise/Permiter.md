# router 

hostname Router20
ip routing

int gi0/0.105
 description Marketing
 encapsulation dot1Q 105
 ip address 192.168.105.20 255.255.255.0
 no shut
 exit

int gi0/0.106
 description Sales
 encapsulation dot1Q 106
 ip address 192.168.106.20 255.255.255.0
 no shut
 exit

int gi0/0.107
 description Engineering
 encapsulation dot1Q 107
 ip address 192.168.107.20 255.255.255.0
 no shut
 exit
 

interface GigabitEthernet0/0
 no shut 
 exit

interface GigabitEthernet0/1
 ip address 192.168.3.20 255.255.255.0
 no shut 
 exit

exit
wr mem


conf t

interface gi0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 no shut

end
wr mem

# Switch

hostname Switch10
spanning-tree vlan 1-4094 root secondary

vlan 10
 name Netman
vlan 105
 name Marketing
vlan 106
 name Sales
vlan 107
 name Engineering
vlan 999
 name Tagging
vlan 1000
 name Discard
exit

vtp mode server
vtp domain HeadOffice
vtp password Head
vtp version 2

int VLAN 10
 ip address 192.168.10.10 255.255.255.0
 no shut
exit

int range gi0/0-3
 switchport trunk native vlan 999
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit

int range gi1/0-3
 description Marketing
 switchport access vlan 105
 switchport mode access 
exit

int range gi2/0-3
 description Sales
 switchport access vlan 106
 switchport mode access 
exit

int range gi3/0-3
 description Engineering
 switchport access vlan 107
 switchport mode access
 shutdown 
exit

exit
wr mem


conf t
ip default-gateway 192.168.10.1
end
wr

# Router dhcp

ip dhcp excluded-address 192.168.105.0 192.168.105.99
ip dhcp excluded-address 192.168.106.0 192.168.106.99
ip dhcp excluded-address 192.168.107.0 192.168.107.99

ip dhcp pool Marketing
   network 192.168.105.0 255.255.255.0
   default-router 192.168.105.20
   dns-server 8.8.8.8
exit

ip dhcp pool Sales
   network 192.168.106.0 255.255.255.0
   default-router 192.168.106.20
   dns-server 8.8.8.8
exit

ip dhcp pool Engineering
   network 192.168.107.0 255.255.255.0
   default-router 192.168.107.20
   dns-server 8.8.8.8
exit

# Router rip

router rip
 version 2
 redistribute connected
 network 192.168.3.0
 no auto-summary