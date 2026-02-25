# Port Security – Common Patterns (IOSvL2)

## 1) Sticky MAC + Protect (does not shut the port)
```text
conf t
interface range gi1/0-3
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security mac-address sticky
 switchport port-security violation protect
end
```

## 2) Max MACs + Shutdown (shuts on violation)
```text
conf t
interface range gi2/0-3
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 3
 switchport port-security violation shutdown
end
```

## 3) Aging example (inactivity aging)
```text
conf t
interface fa0/5
 description CLIENT
 switchport mode access
 switchport access vlan 5
 switchport port-security
 switchport port-security mac-address sticky
 switchport port-security aging time 2
 switchport port-security aging type inactivity
 switchport port-security violation restrict
end
```

## Verify / Troubleshoot
```text
show port-security interface gi1/3
show port-security address
show interface status err-disabled
```

## Recover from shutdown violation
```text
conf t
interface gi2/0
 shutdown
 no shutdown
end
```
