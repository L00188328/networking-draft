# Console 
line con 0
    password MyConsole
    logging synchronous
    login
    history size 10
    exec-timeout 6 50
exit



line vty 0 15
    exec-timeout 5 30
    password MyTelnet
    logging synchronous
    login
    history size 10
exit


# Security
service password-encryption
enable secret MyPassword


# Local Management last port of each switch
interface gi2/3
    description NetMan
    switchport access vlan 10
    switchport mode access
    exit
exit




    
