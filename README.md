# Jarkom-Modul-5-E12-2023

## Anggota Kelompok
- Andhika Lingga Mariano (5025211161)
- Beauty Valen Fajri (5025211227)

## Daftar Isi
- [GNS3](#gns3)
	- [Topologi](#topologi)
	- [Subnet](#subnet)
- [VLSM](#vlsm)
	- [Tree](#tree)
	- [Pembagian IP](#pembagian-ip)
- [Config](#config)
- [Routing dan DHCP](#routing-dan-dhcp)

# GNS3
## Topologi
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/50335b09-ba06-4616-81b1-966d8ac23e1c)

## Subnet
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/47b04158-c936-4d57-915c-c1252fba2d05)

# VLSM
## Tree
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/2479d592-6fb2-4bb6-81ca-260671184817)

## Pembagian IP
![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/114421539/e651b029-10cf-4ddd-8fb9-15e5fdd7b93f)

# Config 
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

- All Client (LaubHills, SchwerMountain, TurkRegion, GrobeForest)
```
auto eth0
iface eth0 inet dhcp
```

# Routing dan DHCP
- Aura
```
#Kanan
route add -net 192.212.8.0 netmask 255.255.248.0 gw 192.212.0.22 #A9
route add -net 192.212.4.0 netmask 255.255.252.0 gw 192.212.0.22 #A10

#Bawah
route add -net 192.212.0.0 netmask 255.255.255.252 gw 192.212.0.18 #A1
route add -net 192.212.0.4 netmask 255.255.255.252 gw 192.212.0.18 #A2
route add -net 192.212.0.128 netmask 255.255.255.128 gw 192.212.0.18 #A3
route add -net 192.212.2.0 netmask 255.255.254.0 gw 192.212.0.18 #A4
route add -net 192.212.0.8 netmask 255.255.255.252 gw 192.212.0.18 #A5
route add -net 192.212.0.12 netmask 255.255.255.252 gw 192.212.0.18 #A6
```

- Heiter (DHCP Relay)
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.212.0.21 #default

#DHCP Relay
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo '
SERVERS="192.212.0.2"
INTERFACES="eth1 eth2"
OPTIONS=' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```

- Frieren
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.212.0.17 #default
route add -net 192.212.0.0 netmask 255.255.255.252 gw 192.212.0.10 #A1
route add -net 192.212.0.4 netmask 255.255.255.252 gw 192.212.0.10 #A2
route add -net 192.212.0.128 netmask 255.255.255.128 gw 192.212.0.10 #A3
route add -net 192.212.2.0 netmask 255.255.254.0 gw 192.212.0.10 #A4
```

- Himmel (DHCP Relay)
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.212.0.9 #default
route add -net 192.212.0.0 netmask 255.255.255.252 gw 192.212.0.130 #A1
route add -net 192.212.0.4 netmask 255.255.255.252 gw 192.212.0.130 #A2

#DHCP Relay
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo '
SERVERS="192.212.0.2"
INTERFACES="eth1 eth2"
OPTIONS=' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```

- Fern
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.212.0.129 #default
```

- Revolte (DHCP Server)
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo '
# A1
subnet 192.212.0.0 netmask 255.255.255.252 {

}

# A2
subnet 192.212.0.4 netmask 255.255.255.252 {

}

# A5
subnet 192.212.0.8 netmask 255.255.255.252 {

}

# A6
subnet 192.212.0.12 netmask 255.255.255.252 {

}

# A7
subnet 192.212.0.16 netmask 255.255.255.252 {

}

# A8
subnet 192.212.0.20 netmask 255.255.255.252 {

}

# SchwerMountain
subnet 192.212.0.128 netmask 255.255.255.128 {
    range 192.212.0.131 192.212.0.194;
    option routers 192.212.0.129;
    option broadcast-address 192.212.0.255;
    option domain-name-servers 192.212.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}

# LaubHills
subnet 192.212.2.0 netmask 255.255.254.0 {
    range 192.212.2.2 192.212.3.1;
    option routers 192.212.2.1;
    option broadcast-address 192.212.3.255;
    option domain-name-servers 192.212.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}

# TurkRegion
subnet 192.212.8.0 netmask 255.255.248.0 {
    range 192.212.8.2 192.212.11.255;
    option routers 192.212.8.1;
    option broadcast-address 192.212.15.255;
    option domain-name-servers 192.212.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}

# GrobeForest
subnet 192.212.4.0 netmask 255.255.252.0 {
    range 192.212.4.3 192.212.6.2;
    option routers 192.212.4.1;
    option broadcast-address 192.212.7.255;
    option domain-name-servers 192.212.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
# Soal 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## Jawab
Pada aura, jalankan command iptables berikut.
```
IPETH0="$(ip -br a | grep eth0 | awk '{print $NF}' | cut -d'/' -f1)"
iptables -t nat -A POSTROUTING -o eth0 -j SNAT -s 192.212.0.0/20 --to-source "$IPETH0"
```

# Soal 2
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.


## Jawab
Di sini kami menjalankan command iptables pada client LaubHills, lalu melakukan testing dari client SchwerMountain.

- LaubHills
```
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
```

### Testing
Install netcat pada kedua client dengan command
```
apt-get update
apt-get install netcat -y
```

Untuk testing port 8080, jalankan command `nc -l -p 8080` pada LaubHills dan command `nc [IP LaubHills] 8080` pada client SchwerMountain. Pada port 8080, koneksi akan berhasil.

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/8865dd40-ce81-4f8d-a08a-4d4640279e1d)

Sementara untuk port selain 8080, maka koneksi akan didrop.

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/16b94875-6562-49a6-bc3c-20d700f39c6d)

# Soal 3
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

## Jawab
Jalankan command berikut pada Revolte dan Richter
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

### Testing
Lakukan ping dari client ke Revolte dan Richter. Client ke-4 yang melakukan ping akan didrop.

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/cc80f389-3e99-449b-aa0a-5704959f3470)

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/0060c6b1-52aa-4164-9a8b-08336fb617a4)

# Soal 4
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

## Jawab
Jalankan command berikut pada Sein dan Stark
```
iptables -A INPUT -p tcp --dport 22 ! -s [IP GrobeForest] -j REJECT
```

### Testing
Gunakan netcat untuk mencoba koneksi ke Sein dan Stark, di mana hanya GrobeForest saja yang dapat terhubung.

- GrobeForest

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/9e707895-7b72-4d70-92b5-d6e576a0f284)

- Selain GrobeForest

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/aeccc935-7d63-4e1b-8f47-8b972b94896e)


# Soal 5
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

## Jawab
Jalankan command berikut pada Sein dan Stark
```
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```

### Testing
Lakukan ping ke Sein dan Stark

- Pukul 10.00 (berhasil)

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/b9dd1c71-968f-40cf-a42a-9b4d3a10dab0)

- Pukul 00.15 (gagal)

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/23c75f55-6fd8-4bb3-a365-4bb2f5e644fb)



# Soal 6
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## Jawab
Jalankan command berikut pada Sein dan Stark
```
iptables -I INPUT 1 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j REJECT
iptables -I INPUT 1 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j REJECT
```

### Testing
Lakukan ping ke Sein dan Stark

- Hari Jumat pukul 10.06 (berhasil)

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/be9793a1-7b5e-4e87-b6a5-070883d7b397)


- Hari Jumat pukul 12.30 (gagal)

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/5a2d3c34-99e6-437c-81e9-ca63ee543041)


# Soal 7
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## Jawab


# Soal 8
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## Jawab
Jalankan command berikut pada Sein dan Stark untuk menolak semua koneksi dari subnet Revolte (/30) mulai dari tanggal 14/02/2024 sampai 26/06/2024.
```
iptables -A INPUT -s 192.212.0.0/30 -m time --datestart 2024-02-14 --datestop 2024-06-26 -j REJECT
```
### Testing
Lakukan ping ke Sein dan Stark pada tanggal pemilu dan koneksinya akan ditolak.

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/4f8d2b92-abdc-4954-a3fc-18517c8e9a0c)

# Soal 9
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)

## Jawab
Jalankan command berikut pada Sein dan Stark 
```
iptables -N portscan

iptables -I INPUT 1 -m recent --name portscan --set -j ACCEPT
iptables -I FORWARD 1 -m recent --name portscan --set -j ACCEPT

iptables -I INPUT 1 -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
iptables -I FORWARD 1 -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
```

### Testing
Lakukan ping ke Sein dan Stark sebanyak 25 kali. Ping yang masuk hanya sebanyak 20, sementara selebihnya akan didrop

![image](https://github.com/Deekuh/Jarkom-Modul-5-E12-2023/assets/90295688/d84ca7ab-2bfc-442a-b648-5cdb11ea2448)

# Soal 10
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 

## Jawab
