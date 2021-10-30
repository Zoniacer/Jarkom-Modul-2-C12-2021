# Jarkom-Modul-2-C12-2021

### C12
Daffa Amanullah Setyawan - 05111940000071\
Satrio Hanif Wicaksono - 05111940000103\
Shidqi Dhaifullah - 05111940000108

### PRAKTIKUM MODUL 2

Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:
![No  1 Screenshot 2021-10-29 234903](https://user-images.githubusercontent.com/73422724/139473071-9ea16174-9f31-4e3a-a720-6cb4c203451a.png)
1. EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet (1).<br>
Jawab:
- Konfigurasi topologi seperti berikut:
1-1
- Lakukan setting network pada masing-masing node sebagai berikut:<br>
<b>Foosha</b>
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.20.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.20.2.1
	netmask 255.255.255.0
```
<b>Loguetown</b>
```
auto eth0
iface eth0 inet static
	address 10.20.1.2
	netmask 255.255.255.0
	gateway 10.20.1.1
```
<b>Alabasta</b>
```
auto eth0
iface eth0 inet static
	address 10.20.1.3
	netmask 255.255.255.0
	gateway 10.20.1.1
```
<b>EniesLobby</b>
```
auto eth0
iface eth0 inet static
	address 10.20.2.2
	netmask 255.255.255.0
	gateway 10.20.2.1
```
<b>Water7</b>
```
auto eth0
iface eth0 inet static
	address 10.20.2.3
	netmask 255.255.255.0
	gateway 10.20.2.1
```
<b>Skypie</b>
```
auto eth0
iface eth0 inet static
	address 10.20.2.4
	netmask 255.255.255.0
	gateway 10.20.2.1
```

-Pada router Foosha, masukkan perintah <code>-t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.20.0.0/16</code><br>
-Pada node lain, masukkan perintah <code>192.168.122.1 > /etc/resolv.conf</code><br>

2. Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.yyy.com
dengan alias www.franky.yyy.com pada folder kaizoku.<br>
Jawab:
-Pada EniesLobby, lakukan perintah <code>cp /etc/bind/db.local /etc/bind/kaizoku/franky.C12.com</code>
-Masukkan konfigurasi berikut pada file franky.c12.com:
2-1
-Lakukan ping pada www.franky.c12.com:
2-2

3. Setelah itu buat subdomain super.franky.yyy.com dengan alias www.super.franky.yyy.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie.
Jawab:
-Pada EniesLobby, masukkan konfigurasi berikut pada file /etc/bind/kaizoku/franky.C12.com:
3-1
kemudian restart bind9
-Pada Loguetown, ping super.frank

6. Setelah itu terdapat subdomain mecha.franky.yyy.com dengan alias www.mecha.franky.yyy.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo.<br>
Jawab:
- Pada node EniesLobby, Edit file franky.c12.com menggunakan nano /etc/bind/kaizoku/franky.c12.com seperti gambar di bawah

![No  6 part 1 lapres Screenshot 2021-10-30 140331](https://user-images.githubusercontent.com/73422724/139526074-9c2cd9eb-b7fd-499a-a6f7-24f161fb47d2.png)

- Pada node EniesLobby, Edit file named.conf.options menggunakan nano /etc/bind/named.conf.options seperti gambar di bawah

![No  6 part 2 lapres Screenshot 2021-10-30 140441](https://user-images.githubusercontent.com/73422724/139526076-f08689e0-2cda-4ab6-bf8c-f438d8a2d1ae.png)

- Pada node EniesLobby, Edit file named.conf.local menggunakan nano /etc/bind/named.conf.local seperti gambar di bawah

![No  6 part 3 lapres Screenshot 2021-10-30 141404](https://user-images.githubusercontent.com/73422724/139526077-f756b547-1339-4a87-b234-e814351cb853.png)

- Pada node EniesLobby, Restart bind9 menggunakan service bind9 restart
- Pada node Water7, Edit file named.conf.options menggunakan nano /etc/bind/named.conf.options seperti gambar di bawah

![No  6 part 4 lapres Screenshot 2021-10-30 141545](https://user-images.githubusercontent.com/73422724/139526078-baa31b1f-5a7c-401f-bd9d-106ff3c09784.png)

- Pada node Water7, Edit file named.conf.local menggunakan nano /etc/bind/named.conf.local seperti gambar di bawah

![No  6 part 5 lapres Screenshot 2021-10-30 141705](https://user-images.githubusercontent.com/73422724/139526079-d7a48a91-6541-44aa-95b1-7d092b8aac7c.png)

- Pada node Water7, Buat folder sunnygo menggunakan mkdir /etc/bind/sunnygo

![No  6 part 6 lapres Screenshot 2021-10-30 141758](https://user-images.githubusercontent.com/73422724/139526080-87701805-7df5-4a6a-9037-8fd1eca264b9.png)

- Pada node Water7, Copy file db.local menggunakan cp /etc/bind/db.local /etc/bind/sunnygo/mecha.franky.c12.com

![No  6 part 7 lapres Screenshot 2021-10-30 141903](https://user-images.githubusercontent.com/73422724/139526081-9e4e0c22-fde1-4c6a-b6a3-83a4ec5a3779.png)

- Pada node Water7, Edit file mecha.franky.c12.com menggunakan nano /etc/bind/sunnygo/mecha.franky.c12.com seperti gambar di bawah

![No  6 part 8 lapres Screenshot 2021-10-30 142807](https://user-images.githubusercontent.com/73422724/139526082-96768433-df39-4657-804b-7d661f7082b6.png)

- Pada node water7, Restart bind9 menggunakan service bind9 restart

![No  6 part 9 lapresScreenshot 2021-10-30 142853](https://user-images.githubusercontent.com/73422724/139526083-7a0a2a25-56e0-4292-af30-c516aa5ed8f5.png)

- Pada node Loguetown, jalankan ping ke mecha.franky.c12.com sehingga ping mecha.franky.c12.com

![No  6 part 10 lapres Screenshot 2021-10-30 143407](https://user-images.githubusercontent.com/73422724/139526084-05922f45-74ab-4330-a608-b6179dbad014.png)

7. Untuk memperlancar komunikasi Luffy dan rekannya, dibuatkan subdomain melalui Water7 dengan nama general.mecha.franky.yyy.com dengan alias www.general.mecha.franky.yyy.com yang mengarah ke Skypie.<br>
Jawab:

- Pada node Water7, Edit file mecha.franky.c12.com menggunakan nano /etc/bind/sunnygo/mecha.franky.c12.com seperti gambar di bawah

![No  7 part 1 lapres Screenshot 2021-10-30 143518](https://user-images.githubusercontent.com/73422724/139526133-0bdd4f21-e16a-40e3-ade0-b158d9e7ff6a.png)

- Pada node water7, Restart bind9 menggunakan service bind9 restart
- Pada node Loguetown, jalankan ping ke general.mecha.franky.c12.com sehingga ping general.mecha.franky.c12.com

![No  7 part 2 lapres Screenshot 2021-10-30 143621](https://user-images.githubusercontent.com/73422724/139526134-f91ef4d6-f7ab-4250-98ad-4584f1c247af.png)

8. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.<br>
Jawab:
- Pada node Skypie, Install apache2 menggunakan apt-get install apache2 -y
- Pada node Skypie, Install php menggunakan apt-get install php -y
- Pada node Skypie, Install libapache2-mod.php7.0 menggunakan apt-get install libapache2-mod.php7.0 -y

![No  8 part 1 lapres Screenshot 2021-10-30 144139](https://user-images.githubusercontent.com/73422724/139526173-81a13ab9-cb3f-4dc0-ae76-4f899dd237b4.png)

![No  8 part 2 lapres Screenshot 2021-10-30 144226](https://user-images.githubusercontent.com/73422724/139526174-80418118-b701-48c5-a596-aa275cf5466a.png)

![No  8 part 3 lapres Screenshot 2021-10-30 144316](https://user-images.githubusercontent.com/73422724/139526176-20500e3b-1783-4dc0-af55-f2b4562fc898.png)

- Pada node Skypie, Copy file 000-default.conf menggunakan cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/franky.c12.com

![No  8 part 4 lapres Screenshot 2021-10-30 144959](https://user-images.githubusercontent.com/73422724/139526178-6f91eaab-c93e-47bd-85d0-0fd4a5295cb0.png)

- Pada node Skypie, Edit file franky.c12.com menggunakan nano /etc/apache2/sites-available/franky.c12.com seperti gambar di bawah

![No  8 part 5 lapres Screenshot 2021-10-30 145420](https://user-images.githubusercontent.com/73422724/139526179-ff47befa-cdac-42ee-ad0a-42c6684fddad.png)

- Pada node Skypie, Jalankan a2ensite untuk franky.c12.com sehingga a2ensite franky.c12.com

![No  8 part 6 lapres Screenshot 2021-10-30 145557](https://user-images.githubusercontent.com/73422724/139526180-0f932522-1f47-40b7-ab00-bd65f8a90757.png)

- Pada node Skypie, Install wget menggunakan apt-get install wget
- Pada node Skypie, Install unzip menggunakan apt-get install unzip
- Pada node Skypie, Unduh file franky.zip menggunakan wget https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom/raw/main/franky.zip
- Pada node Skypie, Unzip franky.zip pada folder /var/www sehingga unzip franky.zip -d /var/www
- Pada node Skypie, Rename folder franky menggunakan mv /var/www/franky /var/www/franky.c12.com
- Pada node Skypie, Restart apache2 menggunakan service apache2 restart
- Pada node Loguetown, Install lynx menggunakan apt-get install lynx -y
- Pada node Loguetown, Jalankan lynx ke www.franky.c12.com sehingga lynx www.franky.c12.com

![No  8 part 9 lapres Screenshot 2021-10-30 150902](https://user-images.githubusercontent.com/73422724/139526185-a01e8571-b82d-4bcb-a02a-265cbb778181.png)

- Hasilnya menampilkan tampilan berikut

![No  8 part 10 lapres Screenshot 2021-10-30 150829](https://user-images.githubusercontent.com/73422724/139526172-6723a6f2-69a6-4b20-9c9f-b4e727d0066d.png)

9. Setelah itu, Luffy juga membutuhkan agar url www.franky.yyy.com/index.php/home dapat menjadi menjadi www.franky.yyy.com/home.<br>
Jawab:
- Pada node Skypie, Edit file franky.c12.com menggunakan nano /etc/apache2/sites-available/franky.c12.com seperti gambar di bawah

![No  9 part 1 lapres Screenshot 2021-10-30 151101](https://user-images.githubusercontent.com/73422724/139526212-c202361b-1c16-4ddd-939b-7b942ded7117.png)

- Pada node Skypie, Restart apache2 menggunakan service apache2 restart
- Pada node Loguetown, Jalankan lynx ke www.franky.c12.com/home sehingga lynx www.franky.c12.com/home

![No  9 part 2 lapres Screenshot 2021-10-30 151211](https://user-images.githubusercontent.com/73422724/139526216-1facc337-d18e-4688-b739-6c02042846e3.png)

- Hasilnya menampilkan tampilan berikut

![No  9 part 3 lapres Screenshot 2021-10-30 151145](https://user-images.githubusercontent.com/73422724/139526217-486e35ca-4435-407b-9b12-a124fe0d566f.png)

10. Setelah itu, pada subdomain www.super.franky.yyy.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.yyy.com .<br>
Jawab:
- Pada node Skypie, Copy file 000-default.conf menggunakan cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/super.franky.c12.com
- Pada node Skypie, Edit file super.franky.c12.com menggunakan nano /etc/apache2/sites-available/super.franky.c12.com seperti gambar di bawah

![No  10 part 1 lapres Screenshot 2021-10-30 151354](https://user-images.githubusercontent.com/73422724/139526238-3bad9ef2-a818-43ae-9beb-2c91d56a52be.png)

- Pada node Skypie, Jalankan a2ensite untuk super.franky.c12.com sehingga a2ensite super.franky.c12.com

![No  10 part 2 lapres Screenshot 2021-10-30 151430](https://user-images.githubusercontent.com/73422724/139526240-bfce631e-7fdb-4e37-a058-3d6fc35759f8.png)

- Pada node Skypie, Unduh file super.franky.zip menggunakan wget https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom/raw/main/super.franky.zip
- Pada node Skypie, Unzip super.franky.zip pada folder /var/www sehingga unzip super.franky.zip -d /var/www
- Pada node Skypie, Rename folder super.franky menggunakan mv /var/www/franky /var/www/super.franky.c12.com
- Pada node Skypie, Restart apache2 menggunakan service apache2 restart
- Pada node Loguetown, Jalankan lynx ke www.franky.c12.com sehingga lynx super.franky.c12.com

![No  10 part 3 lapres Screenshot 2021-10-30 151619](https://user-images.githubusercontent.com/73422724/139526241-b706df42-2ab7-4268-af88-fb87adaad0e6.png)

- Hasilnya menampilkan tampilan berikut

![No  10 part 4 lapres Screenshot 2021-10-30 151707](https://user-images.githubusercontent.com/73422724/139526243-6a17cb39-cc13-4d49-b333-18329474ccd2.png)

11. Akan tetapi, pada folder /public, Luffy ingin hanya dapat melakukan directory listing saja.<br>
Jawaban:
- Dalam node skypie dibuka /etc/apache2/sites-available/super.franky.c12.com.conf dan dilalukan directory listing /public

![image](https://user-images.githubusercontent.com/63639703/139529774-83683a47-5d62-496c-a2ea-d0cc85b0cc9f.png)

- Lalu service apache9 restart dan langsung dicoba lynx super.franky.c12.com/public

![image](https://user-images.githubusercontent.com/63639703/139529748-9e402eb5-cf96-4c58-a675-81e24f43901f.png)

![image](https://user-images.githubusercontent.com/63639703/139529758-106db9d0-ad5f-4236-96b0-801f2133f159.png)

12. Tidak hanya itu, Luffy juga menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache<br>
Jawaban:
- Dalam node skypie dibuka /etc/apache2/sites-available/super.franky.c12.com.conf dan ditambahkan ErrorDocument

![image](https://user-images.githubusercontent.com/63639703/139529622-2ad48783-feba-4570-b008-8df150890a06.png)

- Lalu service apache9 restart dan langsung dicoba lynx super.franky.c12.com/blabla

![image](https://user-images.githubusercontent.com/63639703/139529642-27a0e2b7-e303-49ee-9d07-18a0dc9b8332.png)

![image](https://user-images.githubusercontent.com/63639703/139529651-ddd5a5b1-f26c-4e5e-b713-500c574b7be0.png)

13. Luffy juga meminta Nami untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset www.super.franky.yyy.com/public/js menjadi www.super.franky.yyy.com/js<br>
Jawaban:
- Dalam node skypie dibuka /etc/apache2/sites-available/super.franky.c12.com.conf dan ditambahkan alias

![image](https://user-images.githubusercontent.com/63639703/139529481-173bbc68-8f24-4574-9762-671e7a1c1d4e.png)

- Lalu bisa service apache2 restart dan langsung lynx di node lougetown

![image](https://user-images.githubusercontent.com/63639703/139529512-a0e2c2c6-a8d4-40b9-95e5-fa6ef20dbded.png)

![image](https://user-images.githubusercontent.com/63639703/139529529-19487ad9-baef-47cf-a849-dc0551b70f2a.png)

14. Dan Luffy meminta untuk web www.general.mecha.franky.yyy.com hanya bisa diakses dengan port 15000 dan port 15500<br>
Jawab:
- Dalam node skypie dibuka /etc/apache2/sites-available/general.mecha.c12.com.conf kemudian virtual host diubah menjadi 15000 dan 15500 seperti berikut

![image](https://user-images.githubusercontent.com/63639703/139525512-e245b568-208e-4bc3-8da5-e6a7280f93c4.png)

- restart apache kemudian langsung lynx www.general.mecha.franky.c12.com:15000, karena sudah dibuat username dan password maka hasilnya di no. 15.

15. dengan autentikasi username luffy dan password onepiece dan file di /var/www/general.mecha.franky.yyy<br>
Jawab:
- Dalam node skypie dibuka /var/www/general.mecha.franky.c12 dan digunakan utility ```htpasswd -c /etc/apache2/.htpasswd luffy``` dengan luffy sebagai username dan nanti akan diminta konfirmasi password.

![image](https://user-images.githubusercontent.com/63639703/139525310-38aadc0c-c39d-407f-8011-2ab21102125e.png)


- Restart apache kemudian langsung ke lougetown dan lynx www.general.mecha.franky.c12.com:15000

![image](https://user-images.githubusercontent.com/63639703/139525378-13c404f6-cb35-4942-b7c5-6a66220a251a.png)

![image](https://user-images.githubusercontent.com/63639703/139525391-bebc3760-96e4-460a-b975-3528c1bb9f58.png)

![image](https://user-images.githubusercontent.com/63639703/139525399-786b4fb9-ccf3-4749-8bee-4e8dd1de2412.png)

16.  Dan setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.yyy.com<br>
Jawab:
- Pada node Skypie, Edit file 000-default.conf menggunakan nano /etc/apache2/sites-available/000-default.conf

![No  16 part 1 Screenshot 2021-10-29 230808](https://user-images.githubusercontent.com/73422724/139473459-0449916e-39e9-424d-81f4-35f2189ade64.png)

- Pada node Skypie, restart apache2 menggunakan service apache2 restart

![No  16 part 2 Screenshot 2021-10-29 231026](https://user-images.githubusercontent.com/73422724/139473464-0908d948-61a2-4fc8-a9be-d920ade90a0a.png)

- Pada node Loguetown, jalankan lynx ke IP Skypie sehingga lynx 10.20.2.4

![No  16 part 3 Screenshot 2021-10-29 231125](https://user-images.githubusercontent.com/73422724/139473467-1b5e5ffa-5648-47d4-ae9d-6018fe37aa18.png)

- Hasilnya menampilkan tampilan berikut

![No  16 part 4 Screenshot 2021-10-29 231202](https://user-images.githubusercontent.com/73422724/139473469-d1e22088-d34a-4db5-95d0-a1d075e3e105.png)

17. Dikarenakan Franky juga ingin mengajak temannya untuk dapat menghubunginya melalui website www.super.franky.yyy.com, dan dikarenakan pengunjung web server pasti akan bingung dengan randomnya images yang ada, maka Franky juga meminta untuk mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png. Maka bantulah Luffy untuk membuat konfigurasi dns dan web server ini!<br>
Jawab:
- Pada node Skypie, Jalankan perintah a2enmod rewrite
- Pada node Skypie, Rrestart apache2 menggunakan service apache2 restart
- Pada node Skypie, Tambahkan file .htacces menggunakan nano /var/www/super.franky.c12.com/.htacces

![No  17 part 1 Screenshot 2021-10-29 232754](https://user-images.githubusercontent.com/73422724/139473511-41dcd007-c047-4479-bdfd-bb1ec54d8b41.png)

- Pada node Skypie, Edit file super.franky.c12.com.conf menggunakan /etc/apache2/sites-available/super.franky.c12.com.conf

![No  17 part 2 Screenshot 2021-10-29 232921](https://user-images.githubusercontent.com/73422724/139473520-84c83ee9-70c0-4336-b35c-ae485ab3ff4d.png)

- Pada node Skypie, Restart apache2 menggunakan service apache2 restart

![No  17 part 3 Screenshot 2021-10-29 233001](https://user-images.githubusercontent.com/73422724/139473523-2779d9d7-7c9e-4ab6-a110-693263eaaf99.png)

- Pada node Loguetown, Jalankan lynx ke franky.png sehingga lynx super.franky.c12.com/public/images/franky.png

![No  17 part 4 Screenshot 2021-10-29 233046](https://user-images.githubusercontent.com/73422724/139473526-50c955ec-28f7-4a28-b8b9-cd81029e3565.png)

- Hasilnya menampilkan tampilan berikut berisi perintah mengunduh gambar franky.png

![No  17 part 5 Screenshot 2021-10-29 233154](https://user-images.githubusercontent.com/73422724/139473531-a7dcc715-5c77-4b16-94ea-401ae4bf57a9.png)

- Testing kedua,
- Pada node Loguetown, Jalankan lynx ke super.franky.c12.com sehingga lynx super.franky.c12.com

![No  17 part 6 Screenshot 2021-10-29 233242](https://user-images.githubusercontent.com/73422724/139473534-53294190-2301-4612-a64b-bbb854d5f3d6.png)

- Hasilnya menampilkan tampilan berikut berisi isi website super.franky.c12.com

![No  17 part 7 Screenshot 2021-10-29 233317](https://user-images.githubusercontent.com/73422724/139473535-2527d40e-98ac-4cb4-9019-e16a7484a70c.png)

- Buka folder public

![No  17 part 8 Screenshot 2021-10-29 233403](https://user-images.githubusercontent.com/73422724/139473537-6d57b983-0839-47c3-9df4-24726acb1acc.png)

- Buka folder image

![No  17 part 9 Screenshot 2021-10-29 233504](https://user-images.githubusercontent.com/73422724/139473541-0df156b4-e812-4694-9e60-0b5054e318f0.png)

- Pilih gambar background-frank.jpg untuk diunduh sehingga menampilkan tampilan berikut

![No  17 part 10 Screenshot 2021-10-29 233537](https://user-images.githubusercontent.com/73422724/139473545-4dbc999f-1678-4a34-bfb3-0718fcdc4baf.png)

### SCRIPTING DAN FILE ROOT

EniesLobby

- File root

![image](https://user-images.githubusercontent.com/63639703/139524461-fc114654-2e32-41ef-a58e-9296ed61233e.png)

- Script

![image](https://user-images.githubusercontent.com/63639703/139524479-309d37b6-41fc-48d8-af64-5d64c6ba5da9.png)

Water7

- File root

![image](https://user-images.githubusercontent.com/63639703/139524512-6fba5be7-d1b5-472f-aa4b-2358e28a8b5b.png)

- Script

![image](https://user-images.githubusercontent.com/63639703/139524525-fe8f3c74-84f2-4279-befb-f988590a5003.png)

![image](https://user-images.githubusercontent.com/63639703/139524571-860a06b1-b761-464b-89ca-58ee4e67466c.png)

Skypie

- File root

![image](https://user-images.githubusercontent.com/63639703/139524595-8f2db114-c7aa-4fd6-b098-d4b4da14da40.png)

- Script

![image](https://user-images.githubusercontent.com/63639703/139524611-f8404886-6f25-4bde-89c8-9b185ac03803.png)

![image](https://user-images.githubusercontent.com/63639703/139524630-e528f4af-636e-458f-9670-9e3b1a7a1e70.png)

Lougetown

- File root

![image](https://user-images.githubusercontent.com/63639703/139524672-cc63ccc8-c11c-4c6d-a134-fb2ad2bb0e89.png)

- Script

![image](https://user-images.githubusercontent.com/63639703/139524686-f6be385c-ac9e-4f86-99a2-a34666933a52.png)

![image](https://user-images.githubusercontent.com/63639703/139524726-bf2d1aae-ccbe-491b-8a46-7c428a991890.png)


