admin 
Passw0rd

sh sys int

conf sys int

edit port1

set allowaccess ping https ssh http
end

get sys int 

# copy ip address to open UI in browser

# Configure ports on perimeter firewall

 edit "port10"
        set vdom "root"
        set mode dhcp
        set type physical
        set alias "Eir Broadband"
        set lldp-reception enable
        set role wan
        set snmp-index 10
    next

 edit "port9"
        set vdom "root"
        set mode dhcp
        set type physical
        set alias "WAN2 - ENet"
        set lldp-reception enable
        set role wan
        set snmp-index 11
    next