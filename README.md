# Jarkom-Modul-2-A09-2021
Laporan Resmi Praktikum Jarkom Modul 2

# Anggota Kelompok
Anggota  | NRP
---------|-------
Arvel Gavrilla Raissananda | 05111940000040
Johnivan Aldo Sudiono | 05111940000051
Vincent Yonathan | 05111940000186

## Link-link
- [Soal](https://docs.google.com/document/d/11_xDG1yHMIOAZVPksRV0VDwx8S4KIgtAMCLh3UD5-qM/edit)

## Pengantar
Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:
<br>
![image](https://user-images.githubusercontent.com/72689610/139518846-4cd861ac-0104-4924-96a8-ea0fe6aa0203.png)

# --- No 1 ---
EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet.  

### Langkah Penyelesaian : 
1. Klik ```servers``` di kiri atas.
2. Klik ```local```.
3. Klik ```Add blank project```.
4. Masukkan nama ```project``` yang diinginkan.
5. Klik ```Add project```.
6. Klik tombol `Add a node` di samping kiri.
7. Lalu tarik `ubuntu-1` ke area kosong di halaman.
8. Tunggu hingga proses loading selesai.
9. Jika berhasil, maka akan menampilkan tampilan seperti berikut : <br>
![image](https://user-images.githubusercontent.com/72689610/139519228-16e8c278-119a-4ce7-8ad9-5e7be93f418d.png)

10. Klik kanan dan `change hostname` menjadi `Foosha` <br>
![image](https://user-images.githubusercontent.com/72689610/139519257-cb16ec5d-26a4-4303-8a5f-7d9896c02b99.png)

11. Klik kanan kembali dan `change symbol` menjadi symbol `router` <br>
![image](https://user-images.githubusercontent.com/72689610/139519288-b2fbdf95-b299-42ae-9474-cceba9f5941d.png)

12. Lakukanlah semua langkah di atas untuk node `LogueTown`, `Alabasta`, `EniesLobby`, `Water7`, dan `Skypie` sehingga didapatkan tampilan sebagai berikut : <br>
![image](https://user-images.githubusercontent.com/72689610/139519455-de053ca7-3729-45c4-a7fd-6e2ba58b9c08.png)

13. Klik tombol `Add a node` di samping kiri.
14. Tarik `NAT` dan dua `Switch` ke area kosong di halaman. <br>
![image](https://user-images.githubusercontent.com/72689610/139521001-800c996a-09fa-461c-877b-80565eb2646a.png)

15. Klik `Add a Link` dan tambahkan link untuk menghubungkan setiap node dan switch sehingga didapatkan tampilan sebagai berikut: <br>
![image](https://user-images.githubusercontent.com/72689610/139521043-a0eab14b-bc8d-446a-bf52-a9780d6dcec9.png)

16. Kita perlu melakukan setting network pada masing-masing node dengan fitur `Edit network configuration`, untuk konfigurasi network pada masing - masing node diisi dengan setting sebagai berikut :
- Foosha
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.173.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.173.2.1
	netmask 255.255.255.0
```
- Loguetown
```
auto eth0
iface eth0 inet static
	address 192.173.1.2
	netmask 255.255.255.0
	gateway 192.173.1.1
```
- Alabasta
```
auto eth0
iface eth0 inet static
	address 192.173.1.3
	netmask 255.255.255.0
	gateway 192.173.1.1
```
- EniesLobby
```
auto eth0
iface eth0 inet static
	address 192.173.2.2
	netmask 255.255.255.0
	gateway 192.173.2.1
```
- Water7
```
auto eth0
iface eth0 inet static
	address 192.173.2.3
	netmask 255.255.255.0
	gateway 192.173.2.1
```
- Skypie
```
auto eth0
iface eth0 inet static
	address 192.173.2.4
	netmask 255.255.255.0
	gateway 192.173.2.1
```
17. Restart semua node.
18. Topologi sudah bisa berjalan secara lokal, namun untuk mengakses jaringan keluar maka perlu dilakukan beberapa konfigurasi sebagai berikut :
- Ketikkan `vim .bashrc` pada router `Foosha` dan masukkan command berikut :
```
   iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.173.0.0/16
```
- Ketikkan command `cat /etc/resolv.conf` di `Foosha` kemudian isi dengan nameserver yang sesuai
```
   nameserver 192.168.122.1
```
- Pada node LogueTown, Alabasta, EniesLobby, Water7, dan Skypie. Ketikkan command `vim .bashrc` kemudian masukkan command berikut : 
```
   echo nameserver 192.168.122.1 > /etc/resolv.conf
```
- Restart kembali semua node.
19. Semua node sekarang sudah bisa melakukan ping ke ww.google.com, yang artinya topologi sudah bisa mengakses jaringan keluar. <br>
![image](https://user-images.githubusercontent.com/72689610/139521735-03b25203-0121-4caa-a1af-d504c3b9cf1d.png)

# --- No 2 ---
Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.A09.com dengan alias www.franky.A09.com pada folder kaizoku 

### Langkah Penyelesaian : 
1. Buka WebConsole `EniesLobby`, dan `Water7`. Ketikkan `vim .bashrc` dan masukkan command berikut
  ```
  apt-get update
  apt-get install bind9 -y
  ```
2. Buka WebConsole `LogueTown` ,dan `Alabasta`. Ketikkan `vim .bashrc` dan masukkan command berikut
 ```
 apt-get update
 apt-get install dnsutils -y
 ```
3. Restart semua node.
4. Masukkan command berikut pada `EniesLobby`
  ```
 vim /etc/bind/named.conf.local
  ```
5. Isikan configurasi zone domain **franky.A09.com** sesuai dengan syntax berikut:
  ```
  zone "franky.A09.com" {
	type master;
	file "/etc/bind/kaizoku/franky.A09.com";
};
  ```
6. Buat folder **kaizoku** di dalam /etc/bind
  ```
  mkdir /etc/bind/kaizoku
  ```
7. Copy file `db.local` pada path `/etc/bind` ke dalam folder **kaizoku** yang baru saja dibuat dan ubah namanya menjadi `franky.A09.com`
  ```
  cp /etc/bind/db.local /etc/bind/kaizoku/franky.A09.com
  ```
8. Buka file **franky.A09.com** dan edit seperti gambar berikut dengan IP 192..173.2.2 dan IP 192.173.2.4 serta record CNAME `www` <br>
   ![image](https://user-images.githubusercontent.com/72689610/139524491-93177e54-e24b-4616-ab77-de2a3dd20fab.png)
   
9. Restart bind9 dengan command `service bind9 restart`
10. Comment nameserver `Foosha` pada `etc/resolv.conf` di node `LogueTown` dan `Alabasta` kemudian tambahkan `nameserver 192.173.2.2` <br>
![image](https://user-images.githubusercontent.com/72689610/139524542-4f1b938d-bd0b-4a83-bcef-c59e1d91a129.png)

12. Kemudian test dengan cara ping IP `franky.A09.com` dan `www.franky.A09.com` pada `Loguetown` atau `Alabasta` <br>
![image](https://user-images.githubusercontent.com/72689610/139524566-5fd737a5-af47-41c6-bae2-1c1c0a56d541.png)
![image](https://user-images.githubusercontent.com/72689610/139524573-8fb489a3-63f3-4948-8e48-c90b25b0fe9b.png)
![image](https://user-images.githubusercontent.com/72689610/139524619-714cfe56-7c9c-4c7d-a229-57a5d630f109.png)
![image](https://user-images.githubusercontent.com/72689610/139524636-3cf6b5f5-4a1b-4167-9ccd-f5788e346d7b.png)

# --- No 3 ---
Setelah itu buat subdomain super.franky.yyy.com dengan alias www.super.franky.yyy.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

### Langkah Penyelesaian : 
1. Jalankan command `vim /etc/bind/kaizoku/franky.A09.com` dan masukkan data seperti gambar berikut untuk membuat subdomain dan aliasnya <br>
  ![image](https://user-images.githubusercontent.com/72689610/139524756-2c785ab4-b109-485d-b96e-59fa0037cef2.png)
  
2. Restart bind9 dengan menggunakan command `service bind9 restart`
3. Kemudian test dengan cara ping IP `super.franky.A09.com` dan `www.super.franky.A09.com` pada `Loguetown` atau `Alabasta` <br>
![image](https://user-images.githubusercontent.com/72689610/139524831-cc74e70c-dd70-4459-8147-2acb53c04c98.png)
![image](https://user-images.githubusercontent.com/72689610/139524855-ff3e6a3e-673e-4e1b-9c9d-7b932948652c.png)

# --- No 4 ---
Buat juga reverse domain untuk domain utama.

### Langkah Penyelesaian : 
1. Jalankan command `vim /etc/bind/named.conf.local` pada `EniesLobby`
2. Lalu tambahkan konfigurasi berikut ke dalam file `named.conf.local` dibawah zone `franky.A09.com`. Tambahkan reverse IP `192.173.2` yaitu `2.173.192`. 
 ```
 zone "2.173.192.in-addr.arpa" {
    type master;
    file "/etc/bind/kaizoku/2.173.192.in-addr.arpa";
};
 ```
![image](https://user-images.githubusercontent.com/72689610/139524997-3bb15586-5200-4593-be54-53e990cebdab.png) <br>

3. Copykan file `db.local` pada path `/etc/bind` ke dalam folder **kaizoku** yang baru saja dibuat dan ubah namanya menjadi `2.173.192.in-addr.arpa`
4. Edit file `2.173.192.in-addr.arpaa` menggunakan command `vim /etc/bind/kaizoku/2.173.192.in-addr.arpa` menjadi seperti gambar di bawah ini <br>
![image](https://user-images.githubusercontent.com/72689610/139525061-6a0eeb61-06af-4c35-a863-5b72ffc67080.png)

5. Restart bind9 dengan command `service bind9 restart`
6. Test dengan cara mengetikkan command `host -t PTR "10.18.2.2"` pada `Loguetown`. Jika muncul seperti pada gambar berikut berarti sudah benar. <br>
![image](https://user-images.githubusercontent.com/72689610/139525306-a84b4e5a-85e8-4013-a14c-67ad7be33722.png)
  
# --- No 5 ---
Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama.

### Langkah Penyelesaian : 
1. Edit file `/etc/bind/named.conf.local` pada `EniesLobby` tepatnya pada zone `franky.A09.com` dan sesuaikan dengan syntax berikut
 ```
 zone "franky.A09.com" {
        type master;
        notify yes;
        also-notify { 192.173.2.3; };
        allow-transfer { 192.173.2.3; };
        file "/etc/bind/kaizoku/franky.A09.com";
};
 ```
 ![image](https://user-images.githubusercontent.com/72689610/139525471-d817f897-c2b8-49ca-9d9c-d12adb4e05cf.png)

2. Restart bind9 `EniesLobby` dengan command `service bind9 restart`
3. Kemudian buka file `/etc/bind/named.conf.local` pada `Water7` dan tambahkan syntax berikut:
 ```
 zone "franky.A09.com" {
    type slave;
    masters { 192.173.2.2; };
    file "/var/lib/bind/franky.A09.com";
};
 ```
 ![image](https://user-images.githubusercontent.com/72689610/139525509-72dcf532-b04c-4059-9258-0231bd49a48f.png)

4. Restart bind9 `Water7` dengan command `service bind9 restart`
5. Test dengan cara mematikan bind9 pada `EniesLobby` yaitu dengan mengetikkan comman `service bind9 stop`
6. Di node `LogueTown` dan `Alabasta` tambahkan `nameserver 192.173.2.3`.
7. Lalu ping ke semua domain atau subdomain yang telah dibuat.

# --- No 6 ---
Setelah itu terdapat subdomain mecha.franky.A09.com dengan alias www.mecha.franky.A09.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo.

### Langkah Penyelesaian : 
1. Pada `EniesLobby`, edit file `/etc/bind/kaizoku/franky.A09.com` dan ubah menjadi seperti di bawah ini. <br>
![image](https://user-images.githubusercontent.com/72689610/139525654-20301647-53da-49f4-9362-091fba4ca754.png)

2. Kemudian edit file `/etc/bind/named.conf.options` pada `EniesLobby`, comment `dnssec-validation auto;` dan tambahkan `allow-query{any;};` <br>
![image](https://user-images.githubusercontent.com/72689610/139525694-3eb7116e-d66d-463f-b978-846a3de33335.png)

3. Restart bind9 `EniesLobby` dengan command `service bind9 restart`
4. Lakukan langkah kedua pada `Water7`
5. Lalu edit file `/etc/bind/named.conf.local` pada `Water7` tambahkan syntax berikut:
 ```
 zone "mecha.franky.A09.com" {
        type master;
        file "/etc/bind/sunnygo/mecha.franky.A09.com";
};
 ```
 ![image](https://user-images.githubusercontent.com/72689610/139525742-9d717b45-54f3-411d-9832-8544fea46e95.png)

6. Kemudian buatlah folder `sunnygo` pada `Water7` dengan mengetikkan command `mkdir /etc/bind/sunnygo`
7. Dan ketikkan command `cp /etc/bind/db.local /etc/bind/sunnygo/mecha.franky.A09.com` pada `Water7`
8. Kemudian edit file `mecha.franky.A09.com` pada `Water7` menjadi seperti dibawah ini <br>
![image](https://user-images.githubusercontent.com/72689610/139525780-0c2bfe3a-dee9-4240-ad72-9344af0659cf.png)

9. Restart bind9 `Water7` dengan command `service bind9 restart`
10. Kemudian test dengan cara ping IP `mecha.franky.A09.com` dan `www.mecha.franky.A09.com` pada `Loguetown` atau `Alabasta` <br>
![image](https://user-images.githubusercontent.com/72689610/139525829-568c395d-af95-4992-871a-a6b717146ae5.png)
![image](https://user-images.githubusercontent.com/72689610/139525877-6200141e-b189-496b-a36c-9e7a7e3ea8e0.png)

# --- No 7 ---
Untuk memperlancar komunikasi Luffy dan rekannya, dibuatkan subdomain melalui Water7 dengan nama general.mecha.franky.A09.com dengan alias www.general.mecha.franky.A09.com yang mengarah ke Skypie.

### Langkah Penyelesaian : 
1. Jalankan command `vim /etc/bind/kaizoku/mecha.franky.A09.com` pada `Water7` dan edit seperti gambar berikut untuk membuat subdomain dan aliasnya <br>
![image](https://user-images.githubusercontent.com/72689610/139526330-a46a364c-d598-4d24-8af2-364a90d3ba74.png)

2. Restart bind9 `Water7` dengan command `service bind9 restart`
3. Kemudian test dengan cara ping IP `general.mecha.franky.A09.com` dan `www.general.mecha.franky.A09.com` pada `Loguetown` atau `Alabasta` <br>
![image](https://user-images.githubusercontent.com/72689610/139526502-743df139-3aa8-4f08-a875-f1e0b2eae18c.png)
![image](https://user-images.githubusercontent.com/72689610/139526561-e9a52f7f-f1cd-49b2-8619-dca9427524cb.png)
![image](https://user-images.githubusercontent.com/72689610/139526596-c615b6f3-e88b-4329-969b-02c795775f0c.png)

# --- No 8 ---
Cari paket yang menunjukan pengambilan file dari FTP tersebut!

### Langkah Penyelesaian : 
- Membuka file yang telah didownload dari drive (8-10)
- Menjalankan command `ftp-data.command==RETR` pada display filter
- Tidak muncul list packet apapun
![image](https://user-images.githubusercontent.com/72689610/134615449-ef430ba4-f7d5-4bfc-aa29-070ecac22f06.png)

# --- No 9 ---
Cari paket-paket yang menuju FTP terdapat inidkasi penyimpanan beberapa file. Salah satunya adalah sebuah file berisi data rahasia dengan nama "secret.zip". Simpan dan buka file tersebut!

### Langkah Penyelesaian : 
- Buka File yang ada pada Drive (8-10)
-	Mengisi display filter dengan `ftp-data.command contains “secret.zip” `
![soal9a](https://user-images.githubusercontent.com/73924235/134495308-37954fbb-b986-474d-bb72-a9d3ab0d784c.png)
-	Memilih follow dan follow TCP
![soal9b](https://user-images.githubusercontent.com/73924235/134495323-231862f6-0754-43e1-9883-6c5665d8d910.png)
-	Kemudian terlihat data yang masih ASCII, diganti menjadi raw
![soal9c](https://user-images.githubusercontent.com/73924235/134495340-8b42127e-0b23-41a3-a1f4-e30d65c327bc.png)
-	Lalu melakukan Save As dengan nama secret.zip
![soal9d](https://user-images.githubusercontent.com/73924235/134495387-90141451-90d1-4113-8036-4a2015f81bfd.png)
-	Kemudian membuka Folder berisi Wanted.pdf, namun belum bisa dibuka karena memiliki password
![soal9e](https://user-images.githubusercontent.com/73924235/134495398-cbc2d07c-0753-4461-bc83-75ff403bdfb7.png)

# --- No 10 --- 
Selain itu terdapat "history.txt" yang kemungkinan berisi history bash server tersebut! Gunakan isi dari "history.txt" untuk menemukan password untuk membuka file rahasia yang ada di "secret.zip"!

### Langkah Penyelesaian : 
-	Buka File yang ada pada Drive (8-10)
-	Mengisi display filter dengan `ftp-data.command contains “history.txt”`
![soal10a](https://user-images.githubusercontent.com/73924235/134495482-4160e7ce-84a6-46bd-90da-d782ed36d3d4.png)

-	Memilih follow dan follow TCP
 ![soal10b](https://user-images.githubusercontent.com/73924235/134495514-e77d24b3-267e-4c72-8f5b-ccf5dea56330.png)

-	Kemudian terlihat data yang menunjukan bahwa password (key) ada pada file bukanapaapa.txt dari tail-1 (yaitu 1 dari yang paling bawah)
 ![soal10c](https://user-images.githubusercontent.com/73924235/134495528-d335ccb8-2ea4-430f-a902-fba2badb0115.png)

-	Mengisi display filter lagi dengan ftp-data.command contains “bukanapaapa.txt”
 ![soal10d](https://user-images.githubusercontent.com/73924235/134495547-ace13651-282d-42d4-b1f7-f772f514e399.png)

-	Kemudian melakukan follow TCP lagi
 ![soal10e](https://user-images.githubusercontent.com/73924235/134495563-ee65f051-8b93-4d4c-90ac-9c16e60f3a20.png)

-	Terlihat password untuk Wanted.pdf yaitu d1b1langbukanapaapajugagapercaya
 ![soal10f](https://user-images.githubusercontent.com/73924235/134495573-fc36dd2e-6e26-42e0-9cab-5b5fa99d9d46.png)

-	Memasukan password ke wanted.pdf.
![soal10g](https://user-images.githubusercontent.com/73924235/134495603-11783db4-7b98-400e-91ce-e850967bbf4f.png)

# --- No 11 --- 
Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!

### Langkah Penyelesaian :
- Mengisi capture filter dengan "src port 80" kemudian enter
![image](https://user-images.githubusercontent.com/72689610/134629218-62fc01c3-f740-4cc1-9ecc-fa54c00750a3.png)

- Membuka wireshark kembali, namun kali ini memilih `WIFI`
- Mengisi capture filter dengan "src port 80" kemudian enter
- Kemudian buka sebuah website, kali ini kami menggunakan website `http://monta.if.its.ac.id/index.php/progres/tugasakhir`
- Maka di wireshark akan muncul sebagai berikut :
![image](https://user-images.githubusercontent.com/72689610/134629869-4ffa8691-367b-4579-aa97-ad8ee3e71388.png)

# --- No 12 --- 
Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!

### Langkah Penyelesaian :
- Mengisi Capture Filter dengan `port 21` pada Adapter for Loopback Traffic
![soal12a](https://user-images.githubusercontent.com/73924235/134495705-648736d6-9354-45e8-aebc-7c2d11fae484.png)
- Hasil Kosong, karena port 21 harus menggunakan FTP yang bisa diakses melalui filezilla
![soal12b](https://user-images.githubusercontent.com/73924235/134495753-49286cf9-422e-43fe-af40-032200e1e0ed.png)
- Ketika XAMPP dinyalakan dan Filezilla diconnect maka akan menghasilkan hasil berikut
![soal12c](https://user-images.githubusercontent.com/73924235/134642277-6e7a9cf6-aaf7-4ae9-98b9-a69d7546dee8.JPG)

# --- No 13 --- 
Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!

### Langkah Penyelesaian :
- Mengisi capture filter dengan `dst port 443` kemudian enter
![image](https://user-images.githubusercontent.com/72689610/134630498-2dc8b4cd-9b90-444d-9e64-37394adc1cd2.png)

- Membuka wireshark kembali, namun kali ini memilih `WIFI`
- Mengisi capture filter dengan `dst port 443` kemudian enter
![image](https://user-images.githubusercontent.com/72689610/134630498-2dc8b4cd-9b90-444d-9e64-37394adc1cd2.png)

- Kemudian buka sebuah website, kali ini kami menggunakan website `http://monta.if.its.ac.id/index.php/progres/tugasakhir`
- Maka di wireshark akan muncul sebagai berikut :
![image](https://user-images.githubusercontent.com/72689610/134630813-acf1189e-b1ca-47a2-83d8-990101ce3e54.png)

# --- No 14 --- 
Filter sehingga wireshark hanya mengambil paket yang tujuannya ke kemenag.go.id!

### Langkah Penyelesaian :
- Mengisi capture filter dengan `dst host kemenag.go.id` kemudian enter
![image](https://user-images.githubusercontent.com/72689610/134632321-a70faa64-3571-42a2-8bf3-430370c82568.png)

- Membuka website `https://www.kemenag.go.id/`
![image](https://user-images.githubusercontent.com/72689610/134631528-9a25d2b3-15af-4a4f-ad09-6eabbf1f4138.png)

# --- No 15 --- 
Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!

### Langkah Penyelesaian :
- Mencari ip dengan membuka `command prompt` dan mengetikkan `ipconfig`
![image](https://user-images.githubusercontent.com/72689610/134631809-fd0fadf9-76bc-4a57-912b-90181c97378c.png)

- Membuka wireshark dan mengisi capture filter dengan `src host 192.168.1.4`
![image](https://user-images.githubusercontent.com/72689610/134632067-f600b66c-4d91-4ef6-bccd-136176b2bf66.png)

- Output :
![image](https://user-images.githubusercontent.com/72689610/134632169-5379cc0b-6cf3-4632-a5ec-af7d3735c261.png)

## Kendala Pengerjaan
- Saat dijalankan, terkadang output tidak keluar



