# MAC Address Table – Static Entry + Aging (IOSvL2)

## 1) Static MAC entry
```text
conf t
mac address-table static 0005.5E40.8403 vlan 1 interface gi1/1
end
```

## 2) Change global MAC aging time (seconds)
```text
conf t
mac address-table aging-time 400
end
```

## Verify
```text
show mac address-table static
show mac address-table dynamic
show mac address-table aging-time
```
