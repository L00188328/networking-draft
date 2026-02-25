# Configure range
int range gi3/0-2

# Check to see what channel protocols are available
channel-protocol ?

# Set tehe protcol to PaGP
channel-protocol pagp
channel-group ?
channel-group 1 mode ?

channel-group 1 mode desirable


# reset switch
conf t
default interface gi3/0
default interface gi3/2
no interface port-channel 1
end

# create vlan
conf t
vlan 1
vlan 2
vlan 10
end

# make the links trunks
conf t
interface range gi3/0,gi3/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 1,2,10
 no shutdown
end

 # create ether channel
 conf t
interface range gi3/0,gi3/2
 channel-protocol pagp
 channel-group 1 mode desirable
end

# configure port channel
conf t
interface port-channel 1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 1,2,10
 no shutdown
end


# enable on each switch with its own ip adddress 
conf t
interface vlan 10
 ip address 192.168.1.21 255.255.255.0
 no shutdown
exit
ip default-gateway 192.168.1.1
