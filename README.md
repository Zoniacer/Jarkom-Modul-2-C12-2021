# Jarkom-Modul-2-C12-2021

### C12
Daffa Amanullah Setyawan - 05111940000071\
Satrio Hanif Wicaksono - 05111940000103\
Shidqi Dhaifullah - 05111940000108

### PRAKTIKUM MODUL 2

Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:
![No  1 Screenshot 2021-10-29 234903](https://user-images.githubusercontent.com/73422724/139473071-9ea16174-9f31-4e3a-a720-6cb4c203451a.png)
EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet (1).

<br><br><br>
<br><br><br>


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

- Pada node Skypie, Rrestart apache2 menggunakan service apache2 restart 

![No  17 part 3 Screenshot 2021-10-29 233001](https://user-images.githubusercontent.com/73422724/139473523-2779d9d7-7c9e-4ab6-a110-693263eaaf99.png)

- Pada node Loguetown, jalankan lynx ke franky.png sehingga lynx super.franky.c12.com/public/images/franky.png

![No  17 part 4 Screenshot 2021-10-29 233046](https://user-images.githubusercontent.com/73422724/139473526-50c955ec-28f7-4a28-b8b9-cd81029e3565.png)

- Hasilnya menampilkan tampilan berikut berisi perintah mengunduh gambar franky.png

![No  17 part 5 Screenshot 2021-10-29 233154](https://user-images.githubusercontent.com/73422724/139473531-a7dcc715-5c77-4b16-94ea-401ae4bf57a9.png)

- Testing kedua,
- Pada node Loguetown, jalankan lynx ke super.franky.c12.com sehingga lynx super.franky.c12.com

![No  17 part 6 Screenshot 2021-10-29 233242](https://user-images.githubusercontent.com/73422724/139473534-53294190-2301-4612-a64b-bbb854d5f3d6.png)

- Hasilnya menampilkan tampilan berikut berisi isi website super.franky.c12.com

![No  17 part 7 Screenshot 2021-10-29 233317](https://user-images.githubusercontent.com/73422724/139473535-2527d40e-98ac-4cb4-9019-e16a7484a70c.png)

- Buka folder public

![No  17 part 8 Screenshot 2021-10-29 233403](https://user-images.githubusercontent.com/73422724/139473537-6d57b983-0839-47c3-9df4-24726acb1acc.png)

- Buka folder image

![No  17 part 9 Screenshot 2021-10-29 233504](https://user-images.githubusercontent.com/73422724/139473541-0df156b4-e812-4694-9e60-0b5054e318f0.png)

- Pilih gambar background-frank.jpg untuk diunduh sehingga menampilkan tampilan berikut

![No  17 part 10 Screenshot 2021-10-29 233537](https://user-images.githubusercontent.com/73422724/139473545-4dbc999f-1678-4a34-bfb3-0718fcdc4baf.png)
