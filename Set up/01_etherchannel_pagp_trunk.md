# EtherChannel (PAgP) – L2 Trunk Bundle (IOSvL2)

## Goal
Create Port-Channel 1 using **PAgP** over links (example: `Gi3/0` and `Gi3/2`) and make it a **trunk**.

---

## 1 Pre-checks
# Check available EtherChannel protocols
show etherchannel summary
show pagp neighbor


---

## 2 Create VLANs used on the trunk (example)

conf t
vlan 1
vlan 2
vlan 10
end


---

## 3 Make member links trunks (recommended: configure physical links first)

conf t
interface range gi3/0,gi3/2
 # Some images require this command before trunk mode
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 1,2,10
 no shutdown
end




## 4 Build the EtherChannel with PAgP

conf t
interface range gi3/0,gi3/2
 channel-protocol pagp
 channel-group 1 mode desirable
end


---

## 5 Configure the Port-Channel interface (must match the members)

conf t
interface port-channel 1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 1,2,10
 no shutdown
end


---

## 6 Verify
```text
show etherchannel summary
show interfaces port-channel 1 switchport
show interfaces trunk
show spanning-tree interface port-channel 1
```

---

## 7 Reset / Remove EtherChannel (clean rollback)

conf t
default interface gi3/0
default interface gi3/2
no interface port-channel 1
end

# (Optional) remove VLANs if needed
# conf t
# no vlan 2
# no vlan 10
# end


---

## Common gotchas
- Member ports and Port-Channel must have **matching** trunk settings (allowed VLANs, trunk mode, encapsulation).
- If you see: “encapsulation auto cannot be configured to trunk” → set `switchport trunk encapsulation dot1q` first.
