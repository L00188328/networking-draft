# set ip address
ip 192.168.1.102/24



# see mac address stored by router
sh mac address-table

# from vpc check ip address from ping
sh arp

# set ip address and gateway
ip 192.168.5.201 255.255.255.0 192.168.5.21

# set the port on swith to talk to port connected to vpc
conf t
int gi0/1
 switchport access vlan 5
 exit
 exit
 wr mem

 # check ip address on switch
show ip interface brief | include Vlan
