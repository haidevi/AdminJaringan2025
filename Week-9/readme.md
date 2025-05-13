<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan<br>Workshop Administrasi Jaringan<br></h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh :</h3>
  <p style="text-align: center;">
    <strong>Zada Devi Mariama (3123500015)</strong>
  </p>
<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi D3 Teknik Informatika<br>2025/2026</h3>
  <hr>
</div>
<br>

---

## Daftar Isi

- [Gambar Topologi](#gambar-topologi-jaringan-internal)
- [Konfigurasi Bind9](#konfigurasi-bind9)
- [Konfigurasi Web Server (Apache2)](#konfigurasi-web-server-apache2)

---


## Gambar Topologi Jaringan Internal

![img](/assets/week-9/topologi.jpg)<br>

Sebelum konfigurasi Bind9, lakukan setting network untuk mengatur koneksi jaringan secara manual, bukan otomatis dari DHCP. Ini berguna pada server atau sistem yang memerlukan pengaturan jaringan yang konsisten dan tidak berubah.

![img](/assets/week-9/networkinterface.jpg)
<br>

Kemudian setting file `/etc/network/interfaces`

![img](/assets/week-9/setnetwork.jpg)
<br>

Setelah itu lakukan update

![img](/assets/week-9/updatenetwork.jpg)
<br>
<br>

## Konfigurasi Bind9

### Konfigurasi DNS Server (Bind9) Pada Server
1. Instalasi paket dengan menjalankan perintah `apt -y install bind9 bind9utils`

2. Edit dan modifikasi file `/etc/bind/named.conf`

![img](/assets/week-9/namedconf.jpg)
<br>

3. Modifikasi file `/etc/bind/named.conf.options`

![img](/assets/week-9/confoptions.jpg)
<br>

![img](/assets/week-9/confoptions2.jpg)
<br>

4. Konfigurasi internal zone pada file `/etc/bind/named.conf.internal-zones`

![img](/assets/week-9/intzones.jpg)
<br>

5. Konfigurasi file `/etc/default/named`

![img](/assets/week-9/defaultnamed.jpg)
<br>

6. Buat file sesuai dengan domain lokal

![img](/assets/week-9/domainlokal.jpg)
<br>

7. Buat file sesuai dengan IP Address

![img](/assets/week-9/ipaddr.jpg)
<br>
<br>

### Tes DNS Server 1
1. Tes DNS Server dari jaringan dalam kelompok

![img](/assets/week-9/tesdns.jpg)
<br>

![img](/assets/week-9/tesdns2.jpg)
<br>
<br>

## Konfigurasi Web Server (Apache2)
1. Instalasi paket apache2 Jalankan perintah berikut untuk menginstal Apache2

![img](/assets/week-9/installapache2.jpg)
<br>

2. Pengaturan Dasar Apache2
    - ServerTokens: Edit dan ubah /etc/apache2/conf-enabled/security.conf

    ![img](/assets/week-9/confenable.jpg)
    
    Ini digunakan untuk menyembunyikan informasi detail versi Apache pada header HTTP, meningkatkan keamanan.
    <br>

    - DirectoryIndex: Edit /etc/apache2/mods-enabled/dir.conf dan atur urutan file index yang dicari ketika direktori diakses:

    ![img](/assets/week-9/modsenable.jpg)
    <br>

    - ServerName: Edit /etc/apache2/apache2.conf dan tambahkan baris berikut untuk mendefinisikan nama server:

    ![img](/assets/week-9/apache2conf.jpg)

    untuk mencegah munculnya peringatan “Could not reliably determine the server's fully qualified domain name”.
    <br>

    - ServerAdmin: Edit /etc/apache2/sites-enabled/000-default.conf dan ubah baris email admin:

    ![img](/assets/week-9/sitesenable.jpg)
    <br>

    - Pengujian dapat dilakukan dengan mengakses domain melalui browser.

    ![img](/assets/week-9/pengujian.jpg)
    <br>

3. Custom tampilan halaman

![img](/assets/week-9/custom.jpg)
<br>

4. Percobaan Akses

![img](/assets/week-9/successdone.jpg)
<br>
Dari hasil diatas, menunjukkan konfigurasi web server sudah berhasil.

