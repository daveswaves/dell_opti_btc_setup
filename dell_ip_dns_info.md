# Dell IP / DNS Info

```
When installing Linux Ubuntu Server 23.04 LTS onto the Dell Optiplex 9020M (i5 processor / 8GB RAM) it defaults to a
dynamic IP address. This results in losing the abilty to access the server remotely via SSH.

The following demonstrates modifying the '00-installer-config.yaml' file to set a static IP address.
*** NOTE: If the routes address is incorrect, the server can still be accessed via SSH, but is unable to connect
to the internet. ***
```

## /etc/netplan/00-installer-config.yaml

```
# This is the network config written by 'subiquity'
network:
  ethernets:
    eno1:
      addresses: [192.168.1.193/24]
      routes:
        - to: default
          via: 192.168.1.254
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
  version: 2

```

*** Remember to apply the changes: ***

```
$ sudo netplan apply
```


## Get IP address: ip a

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 64:00:6a:6a:89:78 brd ff:ff:ff:ff:ff:ff
    altname enp0s25
    inet 192.168.1.193/24 metric 100 brd 192.168.1.255 scope global dynamic eno1
       valid_lft 85972sec preferred_lft 85972sec
    inet 192.168.1.120/24 brd 192.168.1.255 scope global secondary eno1
       valid_lft forever preferred_lft forever
    inet6 fd2d:60d4:9416:0:6600:6aff:fe6a:8978/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 7115sec preferred_lft 1715sec
    inet6 fe80::6600:6aff:fe6a:8978/64 scope link 
       valid_lft forever preferred_lft forever
```

## Get DNS: ip r

```
default via 192.168.1.254 dev eno1 proto static 
default via 192.168.1.254 dev eno1 proto dhcp src 192.168.1.193 metric 100 
192.168.1.0/24 dev eno1 proto kernel scope link src 192.168.1.193 metric 100 
192.168.1.254 dev eno1 proto dhcp scope link src 192.168.1.193 metric 100  
```