# GNS3 Cisco IOSvL2 – Config Cheat Sheets (Organized)

Open any file below and copy/paste the command blocks into your switches/routers.

## Files
1. `01_etherchannel_pagp_trunk.md` – Build/Reset a Layer2 EtherChannel (PAgP) as a trunk
2. `02_vlan_svi_management.md` – Create VLANs + SVIs (management IP) + default gateway
3. `03_trunking_access_ports.md` – Access ports vs trunks (and common gotchas)
4. `04_spanning_tree_loop_avoidance.md` – PVST checks + root bridge control + edge-port protection
5. `05_port_security_basics.md` – Sticky MAC, violation modes, aging, verification
6. `06_aaa_local_and_tacacs.md` – AAA local auth + TACACS+ server group (lab-friendly)
7. `07_mac_table_static_aging.md` – Static MAC entry + aging timer
8. `08_basic_device_hardening.md` – Basic CLI hardening & login controls
9. `09_vtp_v3_basics.md` – VTP v3 server/client quick setup
10. `10_unused_ports_shutdown_vlan.md` – “Discard/Shutdown VLAN” pattern for unused ports

## Notes (important)
- **Do not mix subnets**: if your switch SVI is `192.168.10.21/24`, your host must be in `192.168.10.0/24` too.
- On some IOSvL2 images, you must set: `switchport trunk encapsulation dot1q` before `switchport mode trunk`.
- **BPDU Guard** will err-disable ports if it sees BPDUs. Use it on true host ports only (or disable for lab hosts that emit BPDUs).
