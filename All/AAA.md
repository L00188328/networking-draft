
# AAA setup
# The RADIUS users are alice and bob 
# The TACACS+ user is gns3 All users have a password of gns3

# Switch setup
en
conf t
host Switch10
aaa new-model
int vlan 1
 ip address 192.168.0.10 255.255.255.0
 no shut
no ip domain-lookup
exit

# Switch 10 Configure AAA

en
conf t
aaa new-model
username RLD password Passw0rd
username RLD privilege 15
enable password cisco
aaa authentication login default local
end

# Configure AAA group

conf t
aaa group server tacacs+ CP90x
server name AAA1
end


# Define AAA1

# Switch 10

conf t
tacacs server AAA1
address ipv4 192.168.0.2
key gns3
end

# Configure tell net for testing
# Switch 10

conf t
line vty 0 4
 transport input all
end

# Set up login
# Switch 10

conf t
aaa authentication login default group CP90x local
end

# save
wr mem