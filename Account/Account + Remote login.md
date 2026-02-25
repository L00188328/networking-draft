# account set password
conf t
user RLD password RLD
enable password RLD
exit

# Remote login set password
conf t
line vty 0 4
password RLD
exit
exit
wr mem

# remote login from other machine
telnet 192.168.10.21