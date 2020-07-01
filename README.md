# Статическая и динамическая маршрутизация

Схема стенда:

![alt-текст](https://github.com/awesomenmi/net_route/blob/master/Untitled%20Diagram.png)

Вывод команды _ip a_:
### R1
```
[root@R1 vagrant]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:8a:fe:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic eth0
       valid_lft 85269sec preferred_lft 85269sec
    inet6 fe80::5054:ff:fe8a:fee6/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:2d:17:49 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::e5d7:c81a:a0a3:fcff/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:f8:5d:fb brd ff:ff:ff:ff:ff:ff
    inet6 fe80::e335:6cf0:44a8:95a5/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
5: eth3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:2b:75:28 brd ff:ff:ff:ff:ff:ff
    inet 10.1.0.1/24 brd 10.1.0.255 scope global noprefixroute eth3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe2b:7528/64 scope link 
       valid_lft forever preferred_lft forever
6: vlan12@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:2d:17:49 brd ff:ff:ff:ff:ff:ff
    inet 192.168.12.1/30 brd 192.168.12.3 scope global noprefixroute vlan12
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe2d:1749/64 scope link 
       valid_lft forever preferred_lft forever
7: vlan13@eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:f8:5d:fb brd ff:ff:ff:ff:ff:ff
    inet 192.168.13.1/30 brd 192.168.13.3 scope global noprefixroute vlan13
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef8:5dfb/64 scope link 
       valid_lft forever preferred_lft forever

```
### R2
```
[root@R2 vagrant]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:8a:fe:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic eth0
       valid_lft 85435sec preferred_lft 85435sec
    inet6 fe80::5054:ff:fe8a:fee6/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:50:29:6c brd ff:ff:ff:ff:ff:ff
    inet6 fe80::8b93:5fc3:25c3:407b/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:37:ed:15 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::1e8d:3250:83a3:e2f5/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
5: eth3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:0e:14:be brd ff:ff:ff:ff:ff:ff
    inet 10.2.0.1/24 brd 10.2.0.255 scope global noprefixroute eth3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe0e:14be/64 scope link 
       valid_lft forever preferred_lft forever
6: vlan12@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:50:29:6c brd ff:ff:ff:ff:ff:ff
    inet 192.168.12.2/30 brd 192.168.12.3 scope global noprefixroute vlan12
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe50:296c/64 scope link 
       valid_lft forever preferred_lft forever
7: vlan23@eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:37:ed:15 brd ff:ff:ff:ff:ff:ff
    inet 192.168.23.1/30 brd 192.168.23.3 scope global noprefixroute vlan23
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe37:ed15/64 scope link 
       valid_lft forever preferred_lft forever
```
### R3
```
[root@R3 vagrant]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:8a:fe:e6 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic eth0
       valid_lft 85675sec preferred_lft 85675sec
    inet6 fe80::5054:ff:fe8a:fee6/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:5c:d8:d6 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::da24:caef:1fec:df3b/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:e7:32:b3 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::b53e:43fb:2f3:145d/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
5: eth3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:a2:ca:fc brd ff:ff:ff:ff:ff:ff
    inet 10.3.0.1/24 brd 10.3.0.255 scope global noprefixroute eth3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea2:cafc/64 scope link 
       valid_lft forever preferred_lft forever
6: vlan13@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:5c:d8:d6 brd ff:ff:ff:ff:ff:ff
    inet 192.168.13.2/30 brd 192.168.13.3 scope global noprefixroute vlan13
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe5c:d8d6/64 scope link 
       valid_lft forever preferred_lft forever
7: vlan23@eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:e7:32:b3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.23.2/30 brd 192.168.23.3 scope global noprefixroute vlan23
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fee7:32b3/64 scope link 
       valid_lft forever preferred_lft forever
```

Для того, чтобы изобразить __ассиметричный роутинг__, достаточно изменить файл /etc/quagga/ospfd.conf на одном из роутеров, добавив строчку ```ip ospf cost 300``` 
Например, содержимое файла для R1:
```
hostname R1

router ospf
    ospf router-id 192.168.12.1
    network 192.168.12.0/30 area 0
    network 192.168.13.0/30 area 0
    network 10.1.0.0/24 area 1
    redistribute connected

interface vlan13
ip ospf cost 300

log file /var/log/quagga/ospfd.log
```

Для симметричного роутинга с дорогим линком, необходимо изменить "стоимость" интерфейсов для одного влана, например для VLAN13, то есть для роутеров R1 и R3.
Например, содержимое файла для R3:
```
hostname R3

router ospf
    ospf router-id 192.168.13.2
    network 192.168.13.0/30 area 0
    network 192.168.23.0/30 area 0
    network 10.3.0.0/24 area 3
    redistribute connected

interface vlan13
ip ospf cost 300

log file /var/log/quagga/ospfd.log
```
