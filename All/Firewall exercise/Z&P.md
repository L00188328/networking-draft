# fw10

config system interface
 edit port1
  set mode dhcp
  set alias Outside
  set allowaccess http https ping ssh
  set role wan
end

config system global
 set hostname FW10
end


config system interface
 edit port2
  set ip 192.168.1.1 255.255.255.0
  set allowaccess ping
  set alias Inside
  set role lan
end

config system interface
 edit port3
  set ip 192.168.3.1 255.255.255.0
  set allowaccess ping
  set alias DMZ
  set role dmz
end

config firewall address

  edit InsideLan
   set associated-interface port2
   set subnet 192.168.1.0 255.255.255.0
  end

  config firewall policy
 edit 1
  set name Inside->Outside
  set srcintf port2
  set dstintf port1
  set srcaddr InsideLan
  set dstaddr all
  set action accept
  set schedule always
  set service ALL
  set nat enable
next
end


# fw11
config system interface
 edit port1
  set mode dhcp
  set alias Outside
  set allowaccess http https ping ssh
  set role wan
end

config system global
 set hostname FW11
end

config system interface
 edit port2
  set ip 192.168.2.1 255.255.255.0
  set allowaccess ping
  set alias Inside
  set role lan
end

config system interface
 edit port3
  set ip 192.168.4.1 255.255.255.0
  set allowaccess ping
  set alias DMZ
  set role dmz
end

config firewall address
 
  edit InsideLan
   set associated-interface port2
   set subnet 192.168.2.0 255.255.255.0
   end


config firewall policy
 edit 1
  set name Inside->Outside
  set srcintf port2
  set dstintf port1
  set srcaddr InsideLan
  set dstaddr all
  set action accept
  set schedule always
  set service ALL
  set nat enable
next
end
