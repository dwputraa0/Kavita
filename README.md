# [<img src="/Logo/kavita.svg" width="32" alt="">]() Kavita
<div align="center">

![new_github_preview_stills](https://user-images.githubusercontent.com/735851/169657008-37812c18-5490-4e2a-9dcb-4806f8c87c69.gif)

Kavita is a fast, feature rich, cross platform reading server. Built with a focus for being a full solution for all your reading needs. Setup your own server and share
your reading collection with your friends and family!

[![Release](https://img.shields.io/github/release/Kareadita/Kavita.svg?style=flat&maxAge=3600)](https://github.com/Kareadita/Kavita/releases)
[![License](https://img.shields.io/badge/license-GPLv3-blue.svg?style=flat)](https://github.com/Kareadita/Kavita/blob/master/LICENSE)
[![Downloads](https://img.shields.io/github/downloads/Kareadita/Kavita/total.svg?style=flat)](https://github.com/Kareadita/Kavita/releases)
[![Docker Pulls](https://img.shields.io/docker/pulls/kizaing/kavita.svg)](https://hub.docker.com/r/kizaing/kavita/)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=Kareadita_Kavita&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=Kareadita_Kavita)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=Kareadita_Kavita&metric=security_rating)](https://sonarcloud.io/dashboard?id=Kareadita_Kavita)
[![Backers on Open Collective](https://opencollective.com/kavita/backers/badge.svg)](#backers)
[![Sponsors on Open Collective](https://opencollective.com/kavita/sponsors/badge.svg)](#sponsors)
<a href="https://hosted.weblate.org/engage/kavita/">
<img src="https://hosted.weblate.org/widgets/kavita/-/ui/svg-badge.svg" alt="Translation status" />
</a>
<img src="https://img.shields.io/endpoint?url=https://stats.kavitareader.com/api/ui/shield-badge"/>
</div>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang

**Kavita** adalah sebuah server manga, komik, dan buku yang lengkap, cepat, lintas platform, dan sumber terbuka. Dibangun dari awal dengan fokus pada manga dan tujuan menjadi solusi lengkap untuk kebutuhan membaca Anda. Server **Kavita** dapat dibentuk secara pribadi maupun bersama yang dapat membagikan koleksi bacaan dengan teman serta keluarga.

Fitur yang ada pada kavita adalah
- manage library

  ![manage_lib](https://github.com/dwputraa0/Kavita/blob/main/kavita/manage_lib.png)

- Manage User

  ![manage_user](https://github.com/dwputraa0/Kavita/blob/main/kavita/manage_user.png)
- info dan baca file

  ![desc](https://github.com/dwputraa0/Kavita/blob/main/kavita/desc_book.png)
  ![open_book](https://github.com/dwputraa0/Kavita/blob/main/kavita/open_book.png)

- bookmark, add collection and reading list, dan sebagainya.
  
  ![read_list](https://github.com/dwputraa0/Kavita/blob/main/kavita/read_list.png)
  ![want_to_read](https://github.com/dwputraa0/Kavita/blob/main/kavita/want_to_read.png)



# Instalasi

#### Kebutuhan Sistem :
- web browser
- Unix, Linux atau Windows.
- Docker
- VPS yang bisa diakses menggunakan SSH dan SFTP


#### Proses Instalasi :
1. login ke dalam server ssh yang ingin digunakan. untuk windows, disarankan untuk menggunakan  wsl
    ```
    $ ssh tim1@159.65.143.175
    ```
2. update dan install docker dengan command berikut
    ```
    $ ssh tim1@159.65.143.175
    $ sudo snap install docker
    ```
3. buat file docker-compose.yml yang diisikan
   - **image** `kizaing/kavita:latest`
   - **container** name bisa diisi sesuka hati, dalam hal ini kami menggunakan nama `kavita`
   - **volumes** untuk membuat direktori jenis buku yang diinginkan
   - **environment** untuk menentukan `timezone`
   - **port**, dalam hal ini kami menggunakan `10000`

    Hasil akhir file `docker-compose.yml` adalah sebagai berikut
    ```
    services:
        kavita:
            image: kizaing/kavita:latest    
            container_name: kavita
            volumes:
                - ./manga:/manga          
                - ./comics:/comics       
                - ./books:/books         
                - ./data:/kavita/config  
            environment:
                - TZ=Your/Timezone
            ports:
                - "10000:5000" other services
            restart: unless-stopped
    ```




4. jalankan file docker compose
    ```
    $ sudo docker-compose up -d
    ```
   cek apakah docker berhasil dijalankan

    ```
    $ sudo docker ps
    ```
    
![docker_run](https://github.com/dwputraa0/Kavita/blob/main/kavita/docker_run.png)

5. setelah berhasil dijalankan, kunjungi alamat `web server` dan buat akun `admin`.

	![admin_dashboard](https://github.com/dwputraa0/Kavita/blob/main/kavita/admin_UI.png)


# Konfigurasi

**Server**
  	
   ![manage_lib](https://github.com/dwputraa0/Kavita/blob/main/kavita/digitalocean.png)

Menggunakan layanan server Digital ocean dengan spesifikasi:
1 GB Memory / 1 Intel vCPU / 35 GB Disk / SGP1 - Ubuntu 22.04 (LTS) x64


**Masukkan Buku**
1. login ke `SSH`, dan buat direktori nama buku yang ingin kita masuki

   	![dirname](https://github.com/dwputraa0/Kavita/blob/main/kavita/konf_dirname.png)
2. keluar dari `SSH` , lalu masuk ke dalam file yang ingin kita masuki, lalu login kembali dengan `SFTP`

  	![sftp](https://github.com/dwputraa0/Kavita/blob/main/kavita/konf_sftp.png)
   
4. masukkan file ke direktori yang kalian mau dan jalankan command
    ```
    $ put <nama-file>
    ```

   
**Buat Library**
1. masuk ke admin dashboard dan pilih add library

  	![lib](https://github.com/dwputraa0/Kavita/blob/main/kavita/konf_admdashboard.png)
   
3. isi data yang kalian inginkan, seperti direktori library, nama library, cover, restriksi dan sebagainya
4. scan isi direktori agar tampil ke layar

	![lib](https://github.com/dwputraa0/Kavita/blob/main/kavita/manage_lib.png)

**Buat akun user**
1. Untuk menambahkan user agar bisa masuk ke server, kita bisa setting ke dashboard admin=> user
   
   ![buat_akun_user](https://github.com/dwputraa0/Kavita/blob/main/kavita/konf_buatakunuser.png)
   
3. invite dan masukkan email, role restriksi nya
4. undangan nantinya akan dikirim ke email, dan nantinya kita akan membuat akun user
5. untuk mencoba akun user, kalian dapat login dengan
    ```    
    username : user
    password : 123456
    ```


# Cara Pemakaian

Fitur utama **Kavita** adalah manajemen baca buku, dimana kita bisa membuat user lain melihat *reading list* buku yang sudah atau ingin kita baca.   :
1. Login bisa menggunakan akun user atau admin

	![login](https://github.com/dwputraa0/Kavita/blob/main/kavita/login.png)
   
2. Kita bisa melihat list buku-buku di **home**

	![home](https://github.com/dwputraa0/Kavita/blob/main/kavita/home.png)

3. Buku-buku tersebut bisa kita tambahkan ke **Want to Read**, **Collection**, dan **Bookmarks**

	![add](https://github.com/dwputraa0/Kavita/blob/main/kavita/add.png)

5. kita bisa membuat list **Want to Read**, dan **Collection** sesuai keinginan kita sendiri

	![collection](https://github.com/dwputraa0/Kavita/blob/main/kavita/collectiom.png)

	![wanttoread](https://github.com/dwputraa0/Kavita/blob/main/kavita/wanttoread.png)

7. Kita bisa meletakkan info atau deskripsi dari buku

	![desc](https://github.com/dwputraa0/Kavita/blob/main/kavita/desc_book.png)
	
8. Kita bisa membaca buku langsung dari website

	![open](https://github.com/dwputraa0/Kavita/blob/main/kavita/open_book.png)

9. Kita bisa memberikan seseorang akun dan mengubah role mereka sesuai yang kita mau.

	![role](https://github.com/dwputraa0/Kavita/blob/main/kavita/userrole.png)

10. Kita Bisa lihat Statistik dari pengunaan website tersebut

   ![statistic](https://github.com/dwputraa0/Kavita/blob/main/kavita/statistic.png)


# Pembahasan

**Kavita** ditulis dalam bahasa pemrograman `C#`. Sebagai salah satu aplikasi manajemen buku, aplikasi ini menawarkan berbagai kelebihan, diantaranya :
- Mudah untuk di deploy
- Fitur yang banyak
- Mendukung berbagai macam jenis file
- Desain yang bagus
- Open Source

Tentu saja, sebuah aplikasi pasti memiliki kekurangan. Kekurangan yang dimiliki **Prestashop** antara lain :
- Memakan Resource yang lumayan banyak

	![lib](https://github.com/dwputraa0/Kavita/blob/main/kavita/resources.png)

- Agak lambat


# Referensi

1. [About Kavita](https://github.com/Kareadita/Kavita) - Kavita
2. [How to install Kavita](https://wiki.kavitareader.com/en/install) - Kavita
3. [How to Install WSL in Windows](https://learn.microsoft.com/en-us/windows/wsl/install) - Microsoft
5. [App Preview](http://159.65.143.175:10000/) - Kavita

