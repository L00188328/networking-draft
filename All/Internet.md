# Configure router for nat

int gi0/1
 ip address dhcp
 no shut
 exit


 # check if dchp is working Router1
 show ip interface brief

# dns lookup info
ip domain-lookup
ip name-server 8.8.8.8

# configure nat on router
ip nat inside source list 1 int gi0/1 overload
access-list 1 permit any
int gi0/1
 ip nat outside
int gi0/0.5
 ip nat inside
int gi0/0.10
 ip nat inside

