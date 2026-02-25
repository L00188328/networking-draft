# Access Ports vs Trunks (IOSvL2)

## A) Make an access port in VLAN 10 (host port)

conf t
interface gi0/2
 description NETMAN_HOST
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 # Consider disabling BPDU guard for lab hosts if they trigger err-disable
 # no spanning-tree bpduguard enable
 no shutdown
end


## Verify

show interfaces gi0/2 switchport
show interface status | include Gi0/2


---

## B) Make a trunk port (uplink between switches)

conf t
interface gi3/2
 description UPLINK_TRUNK
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10
 no shutdown
end


## Verify

show interfaces trunk
show interfaces gi3/2 switchport


---

## C) Native VLAN example (optional)

conf t
vlan 999
 name NATIVE
interface gi3/2
 switchport trunk native vlan 999
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,999
end


---

## Common gotchas
- If only VLAN 1 passes and VLAN 10 doesn’t, your uplink is probably **access VLAN 1** instead of trunk.
- If you get “encapsulation auto … cannot be trunk” → set `switchport trunk encapsulation dot1q` first.
