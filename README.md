# Multi-Layer_switch
Configure Layer 3 Switching and Inter-VLAN Routing

These are the command-scripts to setup a MLS (multi-layer-switch) and a layer 2 switch from cisco.

NOTICE: Remember to change the vlans and ips for your specific needs. 

###MLS
enable
config t
ip routing
ipv6 unicast-routing
interface GigabitEthernet0/1
 switchport trunk native vlan 999
 switchport trunk encapsulation dot1q
 switchport mode trunk
interface GigabitEthernet0/2
 no switchport
 ip address 209.165.200.225 255.255.255.252
 ipv6 address 2001:DB8:ACAD:A::1/64vlan 10
 name Staff
vlan 20
 name Student
vlan 30
 name Faculty
interface Vlan10
 ip address 192.168.10.254 255.255.255.0
 ipv6 address 2001:DB8:ACAD:10::1/64
 no shutdown
interface Vlan20
 ip address 192.168.20.254 255.255.255.0 
 ipv6 address 2001:DB8:ACAD:20::1/64
 no shutdown
interface Vlan30
 ip address 192.168.30.254 255.255.255.0
 ipv6 address 2001:DB8:ACAD:30::1/64
 no shutdown
interface Vlan99
 ip address 192.168.99.254 255.255.255.0
 no shutdown
end
########################

###Switch
enable
conf t
int g0/1
switchport mode trunk
switchport trunk native vlan 99
end



######################################################################################################
###Here I will put the "show run"-output on the MLS, Switch 1 (S1), Switch 2 (S2) and Switch (S3)#####
######################################################################################################

MLS#show run
Building configuration...

Current configuration : 1956 bytes
!
version 12.2
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname MLS
!
ip routing
!
ipv6 unicast-routing
!
spanning-tree mode pvst
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
 switchport trunk native vlan 99
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport nonegotiate
!
interface GigabitEthernet0/2
 no switchport
 ip address 209.165.200.225 255.255.255.252
 duplex auto
 speed auto
 ipv6 address 2001:DB8:ACAD:A::1/64
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan10
 mac-address 0002.16a2.cb01
 ip address 192.168.10.254 255.255.255.0
 ipv6 address 2001:DB8:ACAD:10::1/64
!
interface Vlan20
 mac-address 0002.16a2.cb02
 ip address 192.168.20.254 255.255.255.0
 ipv6 address 2001:DB8:ACAD:20::1/64
!
interface Vlan30
 mac-address 0002.16a2.cb03
 ip address 192.168.30.254 255.255.255.0
 ipv6 address 2001:DB8:ACAD:30::1/64
!
interface Vlan99
 mac-address 0002.16a2.cb04
 ip address 192.168.99.254 255.255.255.0
!
ip classless
!
ip flow-export version 9
!
ipv6 route ::/0 GigabitEthernet0/2 2001:DB8:ACAD:A::2

line con 0
 history size 200
 logging synchronous
!
line aux 0
!
line vty 0 4
 login
!
end

MLS#
#####################################################################################
S1#show run
Building configuration...

Current configuration : 1340 bytes
!
version 12.2
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname S1
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
 switchport trunk native vlan 999
 switchport mode trunk
!
interface FastEthernet0/2
 switchport trunk native vlan 999
 switchport mode trunk
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
 switchport trunk native vlan 99
 switchport mode trunk
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 ip address 192.168.99.1 255.255.255.0
!
ip default-gateway 192.168.99.254
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
end


S1#


######################################################################################################

S2#show run
Building configuration...

Current configuration : 2427 bytes
!
version 12.2
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname S2
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport trunk native vlan 999
 switchport mode trunk
!
interface FastEthernet0/2
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/3
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/4
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/5
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/6
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/7
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/8
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/9
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/10
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/11
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/12
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/13
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/14
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/15
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/16
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/17
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/18
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/19
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/20
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/21
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/22
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/23
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/24
 switchport access vlan 30
 switchport mode access
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 ip address 192.168.99.2 255.255.255.0
!
ip default-gateway 192.168.99.254
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
end


S2#

######################################################################################################

S3#sh run
Building configuration...

Current configuration : 2427 bytes
!
version 12.2
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname S3
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/2
 switchport access vlan 10
 switchport trunk native vlan 999
 switchport mode trunk
!
interface FastEthernet0/3
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/4
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/5
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/6
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/7
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/8
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/9
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/10
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/11
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/12
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/13
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/14
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/15
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/16
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/17
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/18
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/19
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/20
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/21
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/22
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/23
 switchport access vlan 30
 switchport mode access
!
interface FastEthernet0/24
 switchport access vlan 30
 switchport mode access
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 ip address 192.168.99.3 255.255.255.0
!
ip default-gateway 192.168.99.254
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
end


S3#

##################################################################################################################################

The end
