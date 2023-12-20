# Jarkom-Modul-5-E12-2023

## Anggota Kelompok
- Andhika Lingga Mariano (5025211161)
- Beauty Valen Fajri (5025211227)

## Daftar Isi
- [Topologi](#topologi)
    - [GNS3](#gns3)
    - [CPT](#cpt)
    - [Subnet](#subnet)
- [VLSM pada GNS3](#vlsm-pada-gns3)
    - [Tree VLSM](#tree-vlsm)
    - [Pembagian IP VLSM](#pembagian-ip-vlsm)
    - [Config GNS3](#config-gns3)
- [CIDR pada CPT](#cidr-pada-cpt)
    - [Penggabungan Subnet](#penggabungan-subnet)
    - [Tree CIDR](#tree-cidr)
    - [Pembagian IP CIDR](#pembagian-ip-cidr)
    - [Config dan Routing CPT](#config-dan-routing-cpt)

## Topologi
#GNS3
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/50335b09-ba06-4616-81b1-966d8ac23e1c)

CPT
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/a55cbd5d-eba6-42bc-bfa3-177440a44582)

Subnet
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/47b04158-c936-4d57-915c-c1252fba2d05)

## VLSM pada GNS3
Tree VLSM
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/2479d592-6fb2-4bb6-81ca-260671184817)

Pembagian IP VLSM
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/e651b029-10cf-4ddd-8fb9-15e5fdd7b93f)

Config GNS3
- Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.212.0.21
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.212.0.17
	netmask 255.255.255.252
```

- Heiter
```
auto eth0
iface eth0 inet static
	address 192.212.0.22
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.212.8.1
	netmask 255.255.248.0

auto eth2
iface eth2 inet static
	address 192.212.4.1
	netmask 255.255.252.0
```

- Frieren
```
auto eth0
iface eth0 inet static
	address 192.212.0.18
	netmask 255.255.255.252
  
auto eth1
iface eth1 inet static
	address 192.212.0.13
	netmask 255.255.255.252
  
auto eth2
iface eth2 inet static
	address 192.212.0.9
	netmask 255.255.255.252
```

- Himmel
```
auto eth0
iface eth0 inet static
	address 192.212.0.10
	netmask 255.255.255.252
  
auto eth1
iface eth1 inet static
	address 192.212.2.1
	netmask 255.255.254.0
  
auto eth2
iface eth2 inet static
	address 192.212.0.129
	netmask 255.255.255.128
```

- Fern
```
auto eth0
iface eth0 inet static
	address 192.212.0.130
	netmask 255.255.255.128
  
auto eth1
iface eth1 inet static
	address 192.212.0.5
	netmask 255.255.255.252
  
auto eth2
iface eth2 inet static
	address 192.212.0.1
	netmask 255.255.255.252
```

- Sein (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.212.4.2
	netmask 255.255.252.0
gateway 192.212.4.1
```

- Stark (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.212.0.14
	netmask 255.255.255.252
	gateway 192.212.0.13
```

- Richter (DNS Server)
```
auto eth0
iface eth0 inet static
	address 192.212.0.6
	netmask 255.255.255.252
	gateway 192.212.0.5
```

- Revolte (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 192.212.0.2
	netmask 255.255.255.252
	gateway 192.212.0.1
```

- All Client
```
auto eth0
iface eth0 inet dhcp
```



