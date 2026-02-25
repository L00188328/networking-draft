# set up each switch to for redundancy: the number 1 means vlan 1
en
conf t
interface vlan 5
 standby 1 ip 192.168.5.20
end
wr mem

# check each router
show standby brief

# set priority
en
conf t
int vlan 2
 standby 2 priority 200
 exit
exit