# Chapter 1: Creating A DHCP Server With Debian

## Creating DHCP Server

### 1. Membuat IP Address (Debian)
Konfigurasi awal yaitu dengan membuat IP addres pada debian dengan perintah :
```
nano /etc/network/interfaces
```
### 2. Restart konfigurasi
Jika sudah melakukan langkah sebelumnya jangan lupa untuk merestart konfigurasi dengan perintah :
```
service networking restart
```
### 3. Install aplikasi DHCP
selanjutnya adalah menginstal aplikasi DHCP server, tetapi sebelum menginstal, masukan terlebih dahulu CD 2 dan add dengan perintah :
```
apt-cdrom-add
```
setelah semua CD dimasukan, maka sekarang yang dilakukan adalah install aplikasi DHCP dengan perintah :
```
apt-get install isc-dhcp-server
```
Jika sudah terdapat kalimat failed, itu memang wajar karna file DHCP belum dikonfigurasi.

### 4. Konfigurasi File 
Selanjutnya kita akan konfigurasi file dhcp.conf dengan perintah :
```
nano /etc/dhcp/dhcpd.conf
```
Akan terdapat banyak script disana, cari kata yang bertulisan A slightly karena kita akan konfigurasi di deretan tersebut. lalu hapu tanda pagar pada deretan subnet sampai kurung tutup dibawah, keterangan script :
```
subnet = ip network
netmask = ip netmask  
range = rentang ip yang akan dibagikan
option domain-name-server = ip dns server
option domain-name = domain yang dipakai
option routers = ip yang dipakai oleh server/ip gateway yang akan di dapat client
option broadcast = ip broadcast
```
Keterangan = Ubah IP nya sesuai IP yang dipakai, jika belum membuat dns option domain server dan option domin name biarkan saja.

### 5. Memilih Interface 
Selanjutnya yaitu memilih mana yang akan dijadikan dhcp server dengan perintah :
```
nano /etc/default/isc-dhcp-server
```
Pergi ke deretan, bawah dan kolom interfaceisi dengan interface yang dipakai. seluruh konfigurasi sudah selesai restart aplikasi isc-dhcp-server dengan perintah :
```
service isc-dhcp-server restart
```
### Test pada client
Jika sudah, apabila kamu menggunakan virtual, pastikan adapter yang digunakan sama dengan hanya satu adapter virtual yang enable, jika sudah jadikan IPv4 obtain IP automatically pada adapter virtual sehingga mendapat IP otomatis. lalu jalankan test ping menuju server