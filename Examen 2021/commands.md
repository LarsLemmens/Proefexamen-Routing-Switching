# Adressing Table

## SRV-RTR-1

```
Router(config-if)#interface g0/0/0
Router(config-if)#ip address 172.16.1.2 255.255.255.252
Router(config-if)#no shutdown

Router(config-if)#interface g0/0/1
Router(config-if)#ip address 172.16.3.1 255.255.255.252
Router(config-if)#no shutdown

Router(config)#interface g0/0/2
Router(config-if)#ip address 10.30.255.254 255.255.0.0
Router(config-if)#ipv6 address FE80::1 link-local
Router(config-if)#ipv6 address 2001:DB30:ACAD:1::1/64
Router(config-if)#no shutdown
```

## EHP-RTR-1

```
Router(config)#interface g0/0/0
Router(config-if)#ip address 172.16.2.2 255.255.255.252
Router(config-if)#no shutdown

Router(config-if)#interface g0/0/1
Router(config-if)#ip address 172.16.3.2 255.255.255.252
Router(config-if)#no shutdown

Router(config-if)#interface g0/0/2
Router(config-if)#ip address 10.40.255.254 255.255.0.0
Router(config-if)#ipv6 address FE80::1 link-local
Router(config-if)#ipv6 address 2001:DB40:ACAD:1::1/64
Router(config-if)#no shutdown
```

## COS-RTR-1

```
Router(config)#interface g0/0/0
Router(config-if)#ip address 172.16.1.1 255.255.255.252
Router(config-if)#no shutdown

Router(config-if)#interface g0/0/1
Router(config-if)#ip address 172.16.2.2 255.255.255.252
Router(config-if)#no shutdown

Router(config)#interface g0/0/2.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip address 10.10.255.254 255.255.0.0
Router(config-subif)#ipv6 address 2001:DB10:ACAD:1::1/64
Router(config-subif)#ipv6 address FE80::1 link-local

Router(config)#interface g0/0/2.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 10.20.255.254 255.255.0.0
Router(config-subif)#ipv6 address 2001:DB20:ACAD:1::1/64
Router(config-subif)#ipv6 address FE80::1 link-local
```

## EHP-PC-1

```
IPv4 Address: 10.40.0.1
Subnet Mask: 255.255.0.0
Default Gateway: 10.40.255.254
DNS Server: 10.30.0.100

IPv6 Address 2001:DB40:ACAD:1::2/64
```

## EHP-PC-2

```
IPv4 Address: 10.40.0.2
Subnet Mask: 255.255.0.0
Default Gateway: 10.40.255.254
DNS Server: 10.30.0.100

IPv6 Address 2001:DB40:ACAD:1::3/64
```

# COS-ACCS-1

```
COS-ACCS-1(config)#vlan 10
COS-ACCS-1(config-vlan)#name Sales

COS-ACCS-1(config-vlan)#vlan 20
COS-ACCS-1(config-vlan)#name ICT


COS-ACCS-1(config-if-range)#interface range f0/3-4
COS-ACCS-1(config-if-range)#switchport mode access
COS-ACCS-1(config-if-range)#switchport access vlan 10
```

# COS-ACCS-2
```
COS-ACCS-2(config)#vlan 10
COS-ACCS-2(config-vlan)#name Sales
COS-ACCS-2(config-vlan)#vlan 20
COS-ACCS-2(config-vlan)#name ICT

COS-ACCS-2(config-vlan)#interface range f0/3-4
COS-ACCS-2(config-if-range)#switchport mode access
COS-ACCS-2(config-if-range)#switchport access vlan 20
```

# OSPF

## COS-RTR-1

```
Router(config)#router ospf 10
Router(config-router)#network 10.10.0.0 0.0.255.255 area 0
Router(config-router)#network 10.20.0.0 0.0.255.255 area 0
Router(config-router)#network 172.16.1.0 0.0.0.3 area 0
Router(config-router)#network 172.16.2.0 0.0.0.3 area 0
Router(config-router)#passive-interface GigabitEthernet0/0/2.10
Router(config-router)#passive-interface GigabitEthernet0/0/2.20
Router(config-router)#passive-interface GigabitEthernet0/0/2
```

## SRV-RTR-1

```
Router(config)#router ospf 10
Router(config-router)#network 10.30.0.0 0.0.255.255 area 0
Router(config-router)#network 172.16.1.0 0.0.0.3 area 0
Router(config-router)#network 172.16.3.0 0.0.0.3 area 0
```

## EHP-RTR-1

```
Router(config)#router ospf 10
Router(config-router)#network 10.40.0.0 0.0.255.255 area 0
Router(config-router)#network 172.16.2.0 0.0.0.3 area 0
Router(config-router)#network 172.16.3.0 0.0.0.3 area 0
```

# Links

## COS-ACCS-1

```
COS-ACCS-1(config)#interface range f0/1-2
COS-ACCS-1(config-if-range)#switchport mode trunk
COS-ACCS-2(config-if-range)#channel-group 1 mode active
```

## COS-ACCS-2

```
COS-ACCS-2(config)#interface range f0/1-2
COS-ACCS-2(config-if-range)#switchport mode trunk
COS-ACCS-2(config-if-range)#channel-group 1 mode active
```

# DHCP

## COS-RTR-1

```
Router(dhcp-config)#ip dhcp pool VLAN10_POOL
Router(dhcp-config)#domain-name cosci.local
Router(dhcp-config)#default-router 10.10.0.1
Router(dhcp-config)#default-router 10.10.255.254
Router(dhcp-config)#dns-server 10.30.0.100
Router(dhcp-config)#network 10.10.0.0 255.255.0.0

Router(dhcp-config)#ip dhcp pool VLAN20_POOL
Router(dhcp-config)#domain-name cosci.local
Router(dhcp-config)#dns-server 10.30.0.100
Router(dhcp-config)#default-router 10.20.255.254
Router(dhcp-config)#network 10.20.0.0 255.255.0.0

Router(dhcp-config)#ipv6 dhcp pool VLAN10_POOL_IPV6
Router(config-dhcpv6)#domain-name cosci.local
Router(config-dhcpv6)#dns-server 2001:db30:acad:1::100

Router(config-dhcpv6)#ipv6 dhcp pool VLAN20_POOL_IPV6
Router(config-dhcpv6)#domain-name cosci.local
Router(config-dhcpv6)#dns-server 2001:db30:acad:1::100

Router(config)#ip dhcp excluded-address 10.20.255.254
```
