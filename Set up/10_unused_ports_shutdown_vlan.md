# Unused Ports → Discard / Shutdown VLAN Pattern (IOSvL2)

## 1) Create a discard VLAN
```text
conf t
vlan 1000
 name Discard
end
write memory
```

## 2) Move unused ports into VLAN 1000 and shutdown
```text
conf t
interface gi0/0
 description UNUSED_SHUTDOWN
 switchport mode access
 switchport access vlan 1000
 shutdown
exit

interface range gi0/2-3
 description UNUSED_SHUTDOWN
 switchport mode access
 switchport access vlan 1000
 shutdown
end
write memory
```

## Verify
```text
show interface status
show vlan brief
```

## Optional: Native VLAN definition for trunks
```text
conf t
vlan 999
 name Native
end
write memory
```
