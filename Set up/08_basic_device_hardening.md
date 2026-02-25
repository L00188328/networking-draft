# Basic Device Hardening & Useful Commands (IOSvL2)

## 1) Core basics
```text
conf t
hostname Core1
no ip domain-lookup
no logging console
end
write memory
```

## 2) Console line
```text
conf t
line con 0
 password MyConsole
 login
 logging synchronous
 history size 10
 exec-timeout 6 50
end
```

## 3) AUX line (optional)
```text
conf t
line aux 0
 password MyAux
 login
end
```

## 4) Password security
```text
conf t
service password-encryption
enable secret MyPassword
username robyn privilege 15 algorithm-type sha256 secret *****REPLACE*****
end
```

## 5) Login protections (use with care in labs)
```text
conf t
login block-for 60 attempts 3 within 30
end
```

## 6) Useful “show” / filesystem commands
```text
show run
show file systems
dir
dir nvram:
dir all-filesystems
```

## 7) Wipe config (lab reset)
```text
write erase
reload

# Also delete VLAN database if needed:
# delete flash:vlan.dat
# reload
```
