# Chapter 1: Creating A DHCP Server With Cisco

## Creating A DHCP Server

### 1. Akses Command Line Interface:
Anda dapat menghubungkan perangkat Cisco melalui kabel konsol atau SSH/Telnet.

### 2. Masuk ke mode Eksekutif Berhak:
Jika Anda belum berada dalam Mode Eksekutif Berhak, gunakan perintah enable dan masukkan kata sandi jika diperlukan.

### 3. Masuk ke mode Konfigurasi Global:
Masuk ke Mode Konfigurasi Global dengan perintah configure terminal atau conf t

### 4. Tentukan Pool DHCP:
Anda perlu mengkonfigurasi pool DHCP, dengan menentukan rentang alamat IP yang akan kepada klien. Gunakan perintah berikut untuk menentukan pool:
```
ip dhcp pool [nama-pool]
network [alamat-jaringan] [subnet-mask]
default-router [alamat-gateway]
dns-server [alamat-DNS]
```
Gantilah variabel yag berada dalam [] dengaan alamat yang ingin anda masukan contoh:
```
ip dhcp pool my-pool
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
```
### 5. Tentukan parameter lease (opsional):
Anda dapat mengkonfigurasi waktu lease untuk alamat IP jika Anda ingin mengendalikan berapa lama perangkat klien memegang alamat IP yang diberikan. Gunakan perintah berikut:

Untuk mengatur waktu lease dalam hari, gunakan lease [day]. Untuk mengatur waktu lease dalam jam, gunakan lease [hour]. Untuk mengatur waktu lease dalam menit, gunakan lease [minutes]. Sebagai contoh, untuk mengatur waktu lease:

```
lease 1 #untuk hari
lease 2 0 #untuk jam 
lease 30 #untuk menit
```
### 6. Aktifkan layanan DHCP 
Keluar dari konfigurasi pool DHCP dengan mengetik exit untuk keluar dari mode konfigurasi pool DHCP, Aktifkan layanan DHCP pada Interface:

Anda perlu mengaktifkan layanan DHCP pada Interface tertentu (misalnya, Interface Ethernet) di mana permintaan DHCP akan diterima. masukan konfigurasi:
```
interface [jenis-antarmuka] [nomor-antarmuka]
ip address [alamat-IP] [subnet-mask]
ip helper-address [IP-server-DHCP]
```
Dalam contoh di atas, ip helper-address menentukan alamat IP server DHCP.

Sebagai contoh, jika Anda ingin mengaktifkan DHCP pada antarmuka GigabitEthernet:
```
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
ip helper-address 192.168.1.2
```
### 7. Simpan Konfigurasi 
Untuk menyimpan konfigurasi Anda, gunakan perintah write memory atau copy running-config startup-config.

Router Cisco Anda sekarang telah dikonfigurasi sebagai server DHCP. Router ini akan memberikan alamat IP kepada perangkat klien dalam pool DHCP yang telah ditentukan saat mereka meminta alamat. Pastikan parameter pool DHCP sesuai dengan kebutuhan jaringan Anda.