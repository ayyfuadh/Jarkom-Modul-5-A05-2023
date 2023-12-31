# Jarkom-Modul-5-A05-2023

- Muhammad Febriansyah (5025211164)
- Layyinatul Fuadah (5025211207)

## Pembagian Kelompok Subnet VLSM (Variable Length Subnet Masking)

![Pembagian Subnet](/img/topologi.png)

### Penjelasan

- Richter adalah DNS Server
- Revolte adalah DHCP Server
- Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
- Jumlah Host pada LaubHills adalah 255
- Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

kemudian dilakukan pepentuan jumlah alamat IP yang dibutuhkan oleh tiap subnet.

| **Subnet** | **Jumlah IP** | **Netmask** |
| :--------: | :-----------: | :---------: |
|     A1     |       2       |     /30     |
|     A2     |       2       |     /30     |
|     A3     |     1023      |     /21     |
|     A4     |       2       |     /30     |
|     A5     |       2       |     /30     |
|     A6     |      66       |     /25     |
|     A7     |      514      |     /22     |
|     A8     |      256      |     /24     |
|     A9     |       2       |     /30     |
|    A10     |       2       |     /30     |
| **Total**  |   **1871**    |   **/20**   |

## Tree pembagian IP

Subnet utama/besar dibentuk melalui NID 192.171.0.0 dengan netmask /20. dan diperoleh sebagai berikut:

![Tree IP](/img/tree%20ip%20rian.png)

## Pembagian IP masing masing node

Kemudian dilakukan pembagian IP sesuai dengan subnet yang telah dibagi berdasarkan tree yang telah dibuat.

## Konfigurasi Router + IP pada GNS3

### Konfigurasi ETH

- Revolte

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.2
	netmask 255.255.255.252
	gateway 192.171.0.1
	up echo nameserver 192.171.0.6 > /etc/resolv.conf
```

- Richter

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.6
	netmask 255.255.255.252
	gateway 192.171.0.5
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Fern

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.0.130
	netmask 255.255.255.128
	gateway 192.171.0.129
	up echo nameserver 192.171.0.6 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.171.0.5
	netmask 255.255.255.252


# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.171.0.1
	netmask 255.255.255.252
```

- SchewerMountain1

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- LaubHills

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- Himmel

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.10
         netmask 255.255.255.252
         gateway 192.171.0.9
	 up echo nameserver 192.171.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.171.0.129
         netmask 255.255.255.128

auto eth2
iface eth2 inet static
         address 192.171.1.1
         netmask 255.255.255.0
```

- Frieren

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.18
         netmask 255.255.255.252
         gateway 192.171.0.17
	 up echo nameserver 192.171.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.171.0.13
         netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.171.0.9
         netmask 255.255.255.252
```

- Stark

```
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.171.0.14
         netmask 255.255.255.252
         gateway 192.171.0.13
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Aura

```bash
auto eth0
iface eth0 inet static
    address 192.168.122.2
    netmask 255.255.255.0
    gateway 192.168.122.1

auto eth2
iface eth2 inet static
       address 192.171.0.17
       netmask 255.255.255.252

auto eth1
iface eth1 inet static
      address 192.171.0.21
      netmask 255.255.255.252
```

- Heiter

```bash
auto eth0
iface eth0 inet static
         address 192.171.0.22
         netmask 255.255.255.252
         gateway 192.171.0.21
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth2
iface eth2 inet static
         address 192.171.8.1
         netmask 255.255.248.0

auto eth1
iface eth1 inet static
         address 192.171.4.1
         netmask 255.255.252.0
```

- TurkRegion

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

- Sein

```bash
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.171.4.2
	netmask 255.255.252.0
	gateway 192.171.4.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- GrabForest

```bash
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
```

## Routing

- Himmel

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.130
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.130
```

- Frieren

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.10
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.10
route add -net 192.171.0.128 netmask 255.255.255.128 gw 192.171.0.10
route add -net 192.171.1.0 netmask 255.255.255.0 gw 192.171.0.10
```

- Aura

```
route add -net 192.171.0.0 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.4 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.128 netmask 255.255.255.128 gw 192.171.0.18
route add -net 192.171.1.0 netmask 255.255.255.0 gw 192.171.0.18
route add -net 192.171.0.8 netmask 255.255.255.252 gw 192.171.0.18
route add -net 192.171.0.12 netmask 255.255.255.252 gw 192.171.0.18

route add -net 192.171.8.0 netmask 255.255.248.0 gw 192.171.0.22
route add -net 192.171.4.0 netmask 255.255.252.0 gw 192.171.0.22
```

> Yang lainya tidak perlu karena sudah terhubung dengan router yang lain. Contoh : Sein sudah terhubung dengan Heiter, sehingga tidak perlu di routing lagi. Begitu juga dengan GrabForest dan TurkRegion.

## Konfigurasi DHCP

### DHCP Server

Pada DHCP Server, kita akan menginstall isc-dhcp-server dengan perintah

```bash
apt-get update
wait
apt-get install isc-dhcp-server -y
wait

echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

cp ~/dhcpd.conf /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

Kemudian pada file dhcpd.conf, kita akan mengkonfigurasi seperti berikut

```bash

option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 192.171.0.0 netmask 255.255.255.252 {
}

subnet 192.171.0.128 netmask 255.255.255.128 {
    range 192.171.0.131 192.171.0.254;
    option routers 192.171.0.129;
    option broadcast-address 192.171.0.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.1.0 netmask 255.255.255.0 {
    range 192.171.1.2 192.171.1.254;
    option routers 192.171.1.1;
    option broadcast-address 192.171.1.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.8.0 netmask 255.255.248.0 {
    range 192.171.8.2 192.171.15.254;
    option routers 192.171.8.1;
    option broadcast-address 192.171.15.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.171.4.0 netmask 255.255.252.0 {
    range 192.171.4.3 192.171.7.254;
    option routers 192.171.4.1;
    option broadcast-address 192.171.7.255;
    option domain-name-servers 192.171.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}
```

- `option domain-name-servers` adalah DNS Server yang akan digunakan
- `default-lease-time` adalah waktu lease default
- `max-lease-time` adalah waktu lease maksimal
- `subnet` adalah subnet yang akan digunakan
- `range` adalah range IP yang akan digunakan
- `option routers` adalah IP dari router yang akan digunakan
- `option broadcast-address` adalah IP broadcast yang akan digunakan

### DHCP Relay

Install isc-dhcp-relay pada route **Himmel dan Heiter** dengan perintah

```bash
# Configuration DHCP Relay
apt-get update
wait
apt-get install isc-dhcp-relay -y
wait

echo '
SERVERS="192.171.0.2"
INTERFACES="eth0 eth1 eth2"
OPTIONS="-m replace"
' >  /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' >  /etc/sysctl.conf
```

- `SERVERS` adalah IP dari DHCP Server yang akan digunakan
- `INTERFACES` adalah interface yang akan digunakan untuk DHCP Relay
- `OPTIONS` adalah opsi yang digunakan untuk DHCP Relay
- `net.ipv4.ip_forward=1` adalah opsi untuk mengaktifkan ip forwarding

## Konfigurasi DNS

```
apt-get update
wait

apt-get install bind9 -y
wait
cp ~/named.conf.options /etc/bind/

service bind9 restart
```

- `named.conf.options` adalah konfigurasi DNS Server

Berikut adalah isi dari file `named.conf.options`

```bash
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
};
```

- `forwarders` adalah DNS Server yang akan digunakan untuk forward
- `allow-query` adalah opsi untuk mengizinkan query dari semua IP
- `auth-nxdomain no` adalah opsi untuk mengizinkan domain yang tidak ada

## Konfigurasi Web Server

Untuk konfigurasi web server, kita akan menginstall nginx pada node **Sein dan Stark** dengan perintah

```bash
apt-get update
wait
apt-get install nginx -y
wait
cp ~/index.nginx-debian.html /var/www/html
service nginx start
apt-get install netcat -y
```

- `index.nginx-debian.html` adalah file html yang akan ditampilkan pada web server nanti
- `netcat` adalah aplikasi yang digunakan untuk mengirimkan data ke web server

## Soal

### Pemasalah 1

Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

### Solusi

Pada node **Aura**, kita akan mengkonfigurasi iptables dengan perintah

```bash
iptables -t nat -A POSTROUTING -s 192.171.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.2
```

- `-t nat` adalah opsi untuk menambahkan rule pada tabel nat
- `-A POSTROUTING` adalah opsi untuk menambahkan rule pada chain POSTROUTING
- `-s` adalah opsi untuk menentukan source IP
- `-o` adalah opsi untuk menentukan interface
- `-j SNAT` adalah opsi untuk melakukan SNAT
- `--to-source` adalah opsi untuk menentukan IP yang akan digunakan untuk SNAT

### Testing

Pada node **Client**, kita akan melakukan ping ke google.com dengan perintah

```bash
ping google.com
```

![output jawaban](</img/soal%201%20(1).png>)
![output jawaban](</img/soal%201%20(2).png>)
![output jawaban](</img/soal%201%20(3).png>)

### Pemasalah 2

Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

### Solusi

Untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP, kita akan mengkonfigurasi iptables pada node **SchewerMountain** dengan perintah

```bash
# Berisikhkan semua aturan yang ada jika diperlukan
iptables -F
# Izinkan koneksi yang masuk pada port 8080 TCP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

# Jatuhkan semua koneksi TCP yang tidak menuju ke port 8080
iptables -A INPUT -p tcp ! --dport 8080 -j DROP

# Jatuhkan semua koneksi UDP
iptables -A INPUT -p udp -j DROP
```

- `iptables -F` adalah opsi untuk menghapus semua rule yang ada

- `iptables -A INPUT -p tcp --dport 8080 -j ACCEPT` adalah opsi untuk menambahkan rule pada chain INPUT untuk menerima koneksi TCP pada port 8080

- `iptables -A INPUT -p tcp ! --dport 8080 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi TCP yang tidak menuju ke port 8080

### Testing

Untuk melakukan testing, kita akan menggunakan node **SchewerMountain** dan **Revolte**. Untuk membuat perbandingan antara port yang belum di drop dan port yang sudah di drop, kita akan menggunakan netcat pada node **Revolte** dengan perintah

Perhatikan video berikut untuk melihat perbandingan antara port yang belum di drop dan port yang sudah di drop

https://github.com/robbypambudi/Jarkom-Modul-5-B13-2023/assets/34505233/25ea1a47-510a-4dec-bce0-f743b125f805

### Pemasalah 3

Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

### Solusi

Untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, kita akan mengkonfigurasi iptables pada node **Revolte** dan **Richter** dengan perintah

```bash
# Soal No 3
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

- `iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi ICMP yang lebih dari 3
- `--connlimit-above 3` adalah opsi untuk menentukan batas koneksi
- `--connlimit-mask 0` adalah opsi untuk menentukan mask

### Testing

Untuk melakukan testing, kita akan menggunakan node **Revolte** dan **Richter**. Untuk membuat perbandingan antara koneksi yang belum di batasi dan koneksi yang sudah di batasi, kita akan menggunakan netcat pada node **Revolte** dan **Richter** dengan perintah

- Testing pada node **Revolte**

`ping ping 192.171.0.2` dan mendapatkan hasil sebagai berikut :

https://github.com/robbypambudi/Jarkom-Modul-5-B13-2023/assets/34505233/77e97ae5-3f1f-49e7-a45b-bce04083ca75

    - Dari video diatas, kita dapat melihat bahwa koneksi ICMP yang lebih dari 3 akan di drop

- Testing pada node **Richter**

`ping 192.171.0.2` dan mendapatkan hasil sebagai berikut :

https://github.com/robbypambudi/Jarkom-Modul-5-B13-2023/assets/34505233/d058e54a-a097-4e40-85bc-81d66602dfdb

    - Dari video diatas, kita dapat melihat bahwa koneksi ICMP yang lebih dari 3 akan di drop

### Pemasalah 4

Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

### Solusi

Untuk melakukan pembatasan koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest, kita akan mengkonfigurasi iptables pada node **Sein** dan **Stark** dengan perintah

```bash
# Soal No 4
iptables -A INPUT -p tcp --dport 22 -s 192.171.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

- -s `192.171.4.0/22` adalah opsi untuk menentukan source IP yang diizinkan pada kali ini adalah subnet `192.171.4.0/22` yaitu di block A10 yang merupakan GrobeForest
- `iptables -A INPUT -p tcp --dport 22 -j DROP` adalah opsi untuk menambahkan rule pada chain INPUT untuk menolak koneksi TCP pada port 22 yang tidak berasal dari subnet A10

### Testing

Untuk melakukan testing tersebut kita akan menggunakan netcat pada node **Sein** dan **Stark** dengan perintah

```
nmap 192.171.4.2 -p 22
```

https://github.com/robbypambudi/Jarkom-Modul-5-B13-2023/assets/34505233/ede8e197-09da-4f4b-9378-6dbfd150a8a0

- Dari video diatas, kita dapat melihat bahwa koneksi SSH yang berasal dari subnet A10 akan diizinkan sedangkan yang berasal dari subnet lainnya akan di drop.

### Pemasalah 5

Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

### Solusi

Untuk melakukan pembatasan akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00, kita akan mengkonfigurasi iptables pada node **Sein** dan **Stark** dengan perintah

```bash
# Izinkan akses ke Web Server pada Senin-Jumat pukul 08.00-16.00
iptables -A INPUT -p tcp --dport 80 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

# Menolak akses selain dari aturan yang telah ditentukan
iptables -A INPUT -p tcp --dport 80 -j DROP
```

### Testing

Untuk melakukan testing tersebut kita akan menggunakan netcat pada node **Sein** dan **Stark** dengan perintah

```
nc -l -p 80
```

dan melakukan akses pada node **Aura** dengan perintah

```
curl 192.171.4.2 -v
```

- **Time : 02:00**
  ![Time : 02:00](/assets/time.png)

- **Time : 09:00**
