# AAA – Local Users + TACACS+ Group (Lab)

## A) Local-only AAA (quick + reliable)
```text
conf t
aaa new-model

username RLD privilege 15 secret Passw0rd
enable secret cisco

aaa authentication login default local
end
write memory
```

## Allow remote access (SSH/Telnet for testing)
```text
conf t
line vty 0 4
 transport input all
 login authentication default
end
write memory
```

---

## B) TACACS+ server group + local fallback
### 1) Define TACACS server
```text
conf t
tacacs server AAA1
 address ipv4 192.168.0.2
 key gns3
end
```

### 2) Create a TACACS+ group
```text
conf t
aaa group server tacacs+ CP90x
 server name AAA1
end
```

### 3) Use TACACS first, then local fallback
```text
conf t
aaa authentication login default group CP90x local
end
write memory
```

## Verify
```text
show run | section aaa
show run | section tacacs
show aaa servers
```

## Notes
- TACACS must be reachable (routing/gateway) or logins will pause until timeout, then fall back to local (if configured).
- For labs, keep at least one local admin user with privilege 15.
