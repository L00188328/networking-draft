# VLAN + SVI Management IP (IOSvL2)

## Goal
- Create VLAN(s)
- Assign a **Switch Virtual Interface (SVI)** IP (e.g., VLAN 10 management)
- Set **default gateway** for L2 switch management traffic

---

## 1) Create VLAN(s)

conf t
vlan 10
 name NETMAN
end


---

## 2) Create the SVI + IP address (example)

conf t
interface vlan 10
 ip address 192.168.10.21 255.255.255.0
 no shutdown
end


---

## 3) Set default gateway (for ping/ssh/telnet to other networks)
> Only needed if you will reach off-subnet destinations.  

conf t
ip default-gateway 192.168.10.1
end


---

## 4) Verify

show ip interface brief | include Vlan
show vlan brief
show arp


---

## 5) Notes
- SVI shows **up/up** only when the VLAN exists and there is at least one active port in that VLAN.
- If your host is `192.168.10.103/24`, it can ping `192.168.10.21/24` without a gateway (same subnet).
- Keep VLAN 1 for lab convenience only; prefer management in VLAN 10+.
