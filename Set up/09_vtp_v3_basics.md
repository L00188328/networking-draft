# VTP v3 Quick Setup (IOSvL2)

## A) VTP Server (Switch 1)
```text
conf t
vtp domain DonegalSME
vtp password DSME
vtp version 3
vtp mode server
end

# Make it the primary server for VLAN changes
vtp primary vlan
```

## Verify
```text
show vtp status
show vtp password
```

---

## B) VTP Client (Switch 2 / 3)
```text
conf t
vtp domain DonegalSME
vtp password DSME
vtp version 3
vtp mode client
end
```

## Verify
```text
show vtp status
```

## Notes
- VTP operates over trunk links. Ensure your inter-switch links are trunks and allow relevant VLANs.
- In labs, VTP can surprise you; use carefully if you don’t want VLANs propagating automatically.
