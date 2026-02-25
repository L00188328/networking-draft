

# login to elevated mode
en

# Save congifuration to nvram
copy running-config startup-config

# Ls items
dir
dir nvram:

# configure terminal
conf t

# stop wrong commands taking a long time to resolve. 
no ip domain-lookup


# change host name
host Core1
exit

# shows last changes
show run


# Set password and synchronous
line con 0
 password MyConsole
 logging synchronous
 login 
 history size 10
 exec-timeout 6 50
exit

# Aux device port
line aux 0
 password MyAux
end

 # Enable secure passwords for elevated mode login
 service password-encryption

enable secret MyPassword

# Set 8 password 
username robyn algorithm-type sha256 secret *******

# Login limit attempts
login block-for 60 attempts 3 within 30

# Restrict login via access list
login quite-mode

# Log succesful and fialed logins
login on-success 
login on-failure

# show file systems
show file systems

