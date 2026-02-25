# Spanning Tree / Loop Avoidance (PVST) – IOSvL2

## 1) Check STP status

show spanning-tree summary
show spanning-tree vlan 10
show spanning-tree blockedports


---

## 2) Make a switch the root for a VLAN (recommended)
### Root for VLAN 10 (Primary)

conf t
spanning-tree vlan 10 priority 4096
end


### Secondary for VLAN 10
```text
conf t
spanning-tree vlan 10 priority 8192
end
```

> Lower priority = more likely to become root.

---

## 3) Edge / host port settings (use carefully)
### PortFast (host-only)

conf t
interface range gi0/0-3
 spanning-tree portfast
end


### BPDU Guard (protect against accidental loops/rogue switches)

conf t
interface range gi0/0-3
 spanning-tree bpduguard enable
end


### Root Guard (prevent this port becoming root port)

conf t
interface range gi0/0-3
 spanning-tree guard root
end


---

## 4) Recover from err-disabled (BPDU Guard)

show interface status err-disabled

conf t
interface gi0/1
 shutdown
 no shutdown
end


---

## Lab tip
If your Linux “automation” node causes err-disable (sends BPDUs), either:
- disable bpduguard on that specific port, or
- keep bpduguard but connect hosts only to ports that never emit BPDUs.
