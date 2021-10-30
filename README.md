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
Konfigurasi Webserver dengan domain www.franky.A09.com dan DocumentRoot pada /var/www/franky.A09.com.

### Langkah Penyelesaian : 
1. Pada Skypie, pindah ke direktori `/etc/apache2/sites-available` lalu copy file **000-default.conf** ke **franky.A09.com.conf** dengan perintah
   `
   cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/franky.A09.com.conf
   `
2. Edit file **franky.A09.com.conf** sehingga menjadi 
![image](https://user-images.githubusercontent.com/36225278/139530010-3e9bbaa4-5b72-446a-942d-c3bb147da559.png)

3. Aktifkan konfigurasi `a2ensite franky.A09.com.conf`
4. Pindah ke direktori `/var/www` lalu download file dengan command `git config --global http.sslVerify false` lalu `git clone https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom.git` dan unzip file
![image](https://user-images.githubusercontent.com/36225278/139530029-7aa6fd56-40c0-4e95-abd0-395b5373fe7d.png)

5. Restart apache dengan `service apache2 restart`
6. Ketika mengakses www.franky.A09.com atau www.franky.A09.com/index.php/home maka akan mendapat tampilan seperti berikut
![image](https://user-images.githubusercontent.com/36225278/139530038-8e4e5105-90a2-44a9-836f-6abe5abb9a78.png)


# --- No 9 ---
Mengubah url www.franky.A09.com/index.php/home dapat menjadi menjadi www.franky.A09.com/home

### Langkah Penyelesaian : 
1. Jalankan perintah a2enmod rewrite
2. Melakukan konfigurasi pada server dengan menambahkan pada **franky.A09.com.conf** 
   ```
   <Directory /var/www/franky.A09.com>
      Options +FollowSymLinks -Multiviews
      AllowOverride All
   </Directory>
   ```
   ![image](https://user-images.githubusercontent.com/36225278/139530242-defa4f6a-b85a-4b8a-aa56-d06f6a4118ce.png)
   
3. Pindah ke direktori `/var/www/franky.A09.com` dan buat file **.htaccess** lalu masukkan
   ```
   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule ^home$ index.php/home
    ```
4. Restart apache dengan `service apache2 restart`
5. Ketika mengakses www.franky.A09.com/home maka akan mendapat tampilan seperti berikut
![image](https://user-images.githubusercontent.com/36225278/139530038-8e4e5105-90a2-44a9-836f-6abe5abb9a78.png)
    
# --- No 10 --- 
Konfigurasi subdomain www.super.franky.A09.com Setelah itu, pada subdomain www.super.franky.A09.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.A09.com.

### Langkah Penyelesaian : 
1. Edit file **super.franky.A09.com.conf** sehingga menjadi
![image](https://user-images.githubusercontent.com/36225278/139530672-a210e485-9c57-490b-a5bd-260eefce4760.png)

2. Restart apache dengan `service apache2 restart`
3. Ketika mengakses www.super.franky.A09.com maka akan mendapat tampilan seperti berikut
![image](https://user-images.githubusercontent.com/36225278/139530821-aaf34422-9f11-4c93-b7d4-cb6c4e4b2a35.png)

# --- No 11 --- 
Akan tetapi, pada folder /public hanya dapat melakukan directory listing saja.

1. Konfigurasi file **super.franky.A09.com.conf** dengan menambahkan
   ``` 
   <Directory /var/www/super.franky.A09.com/public>
       Options +Indexes
   </Directory>
   ```
   sehingga menjadi 
   ![image](https://user-images.githubusercontent.com/36225278/139530984-2f0c3179-fe63-4a8a-98c1-de2f2a23a286.png)

2. Ketika mengakses www.super.franky.A09.com/public maka akan mendapat tampilan seperti berikut
![image](https://user-images.githubusercontent.com/36225278/139531082-39435ddd-3a85-4ae3-ba01-9e8f1e34937c.png)

# --- No 12 --- 
Mengganti error default dari apache menjadi error file 404.html pada folder/error.

### Langkah Penyelesaian :
1. Menambahkan konfigurasi berikut pada **suoer.franky.A09.com.conf**
   `ErrorDocument 404 /error/404.html`
   Sehingga menjadi
   ![image](https://user-images.githubusercontent.com/36225278/139531160-2d792071-fac5-4896-a814-37ca859bdb51.png)

2. Ketika mengakses url invalid seperti www.super.franky.A09.com/hai maka akan mendapat tampilan seperti berikut
   ![image](https://user-images.githubusercontent.com/36225278/139531212-e9f78f14-8e23-4956-926b-e70acae270ba.png)

# --- No 13 --- 
Konfigurasi virtual host agar dapat mengakses file asset www.super.franky.A09.com/public/js menjadi www.super.franky.A09.com/js.

### Langkah Penyelesaian :
1. Jika mengakses www.super.franky.A09.com/public/js maka mendapatkan tampilan sebagai berikut
   ![image](https://user-images.githubusercontent.com/36225278/139531302-81a456be-0362-42e0-852b-4d46f5b54674.png)
2. Edit file **super.franky.A09.com.conf** dengan menambahkan
   `Alias "/js" "/var/www/super.franky.A09.com/public/js"`
   sehinggan menjadi
   ![image](https://user-images.githubusercontent.com/36225278/139531444-5c1d9492-155b-48a1-867d-365fc2081799.png)

   Ketika mengakses www.super.franky.A09.com/js maka akan mendapatkan tampilan seperti berikut
   ![image](https://user-images.githubusercontent.com/36225278/139531487-69bcabbe-fe53-432d-90d6-8f41e629b082.png)

# --- No 14 --- 
Mengatur web www.general.mecha.franky.A09.com hanya bisa diakses dengan port 15000 dan port 15500

### Langkah Penyelesaian :
1. Membuat konfigurasi Web Server di /etc/apache2/sites-available/general.mecha.franky.A09.com.conf, tambahkan potongan kode berikut.
   ```
   <VirtualHost *:15000 *:15500>
        ServerName general.mecha.franky.A09.com
        ServerAlias www.general.mecha.franky.A09.com
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/general.mecha.franky.A09.com
    </VirtualHost>
    ```
     ![image](https://user-images.githubusercontent.com/36225278/139531766-57eeedde-24d8-4d85-a327-d1cd2cbc68ff.png)

2. Tambahkan port yang akan di listen pada /etc/apache2/ports.conf
   ```
   Listen 15000
   Listen 15500
   ```
![image](https://user-images.githubusercontent.com/36225278/139531859-edd92fa6-fdfc-4502-8ca3-11abe20eabac.png)

3. Buat folder baru di /var/www dengan nama general.mecha.franky.A09.com
   `mkdir /var/www/general.mecha.franky.A09.com`
   
4. Copy file - file lampiran github ke folder yang telah dibuat
   `cp -R /root/general.mecha.franky/* /var/www/general.mecha.franky.A09.com`
   
5. Restart apache2 dengan `service apache2 restart`

6. general.mecha.franky.A09.com dan Alias nya sudah bisa diakses melalui client menggunakan Lynx pada port 15000 atau 15500

# --- No 15 --- 
Memberi autentikasi pada www.general.mecha.franky.A09.com dengan username **luffy** dan password **onepiece**

### Langkah Penyelesaian :
1. Tambahkan code berikut pada file /etc/apache2/sites-available/general.mecha.franky.A09.com.conf di bagian web server general.mecha.franky.A09.com
   ![image](https://user-images.githubusercontent.com/36225278/139532054-05d94aec-7856-416b-9787-02ccbd5acffa.png)

2. Buat user baru dengan command berikut sehingga memunculkan file **.htpasswd** pada direktori /etc/apache2
   `htpasswd -c /etc/apache2/.htpasswd luffy`
   
3. Akan diminta memasukan password, masukkan **onepiece**
4. Ketika web server general.mecha.franky.A09.com diakses, akan diminta authentikasi username dan password

# --- No 16 --- 
Setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.A09.com

### Langkah Penyelesaian :
1. Tambahkan file .htaccess pada folder /var/www/html, lalu isikan berikut
   ```
   RewriteEngine On
   RewriteBase /
   RewriteCond %{HTTP_HOST} ^192\.173\.2\.4$
   RewriteRule ^(.*)$ http://www.franky.A09.com/$1 [L,R=301]
   ```
 
2. Ketika mengakses ip Skypie (192.173.2.4), akan langsung redirect ke http://www.franky.A09.com

# --- No 17 --- 
Mengganti request gambar yang memiliki substring**franky** akan diarahkan menuju **franky.png** ketika mengakses www.super.franky.A09.com

### Langkah Penyelesaian :
1. Tambahkan code berikut pada file .htaccess pada folder /var/www/general.mecha.franky.A09.com, lalu isikan berikut
   ```
   RewriteEngine On
   RewriteRule ^(.*)franky(.*)$ http://www.super.franky.A09.com/public/images/franky.png [L,R=301]
   ```
    
2. Ketika mengakses image yang memiliki substring **franky**, akan langsung redirect ke http://www.super.franky.A09.com/public/images/franky.png

## Kendala Pengerjaan
- Saat dijalankan, terkadang output tidak keluar
- Terkadang virtual box tidak bisa dibuka
- Penggunaan script.sh yang masih membingungkan di awalnya, sehingga harus mengulang dari awal, karena belum terbiasa



