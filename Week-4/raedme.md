<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Workshop Administrasi Jaringan<br></h1>
  <h2 style="text-align: center;"><br></h2>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://i.ibb.co/DC3QHnM/logo-pens.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh :</h3>
  <p style="text-align: center;">
  <strong>Zada Devi Mariama</strong>
  </p>
  <p style="text-align: center;">
  <strong>3123500015</strong>
  </p>
  <p style="text-align: center;">
  <strong> D3 Teknik Informatika A</strong>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2025/2026</h3>
  <hr>
</div> 
<br>

## Ekosistem Internet dan Konsep DNS

Fungsi nsswitch.conf, mengatur bagaimana sistem Linux mencari berbagai jenis informasi. Dengan perintah `less /etc/nsswitch.conf` sistem Linux akan menentukan urutan pencarian berbagai jenis layanan.
![img](/assets/week-4/dns/1nsswitch.jpeg)
![img](/assets/week-4/dns/2etc.png)

Perintah `less /etc/hosts` digunakan untuk melihat isi file /etc/hosts, yang berisi penyesuaian alamat ip ke nama host secara lokal.
![img](/assets/week-4/dns/etchost1.jpeg)
![img](/assets/week-4/dns/etchost.jpeg)

Uji koneksi dengan melakukan ping sesuai nama yang diberikan ke alamat ip.
![img](/assets/week-4/dns/pinghw.jpeg)

Perintah `ip a` untuk mengecek alamat ip.
![img](/assets/week-4/dns/ip.jpeg)


File `/etc/resolv.conf` digunakan untuk mengonfigurasi server DNS yang digunakan oleh sistem untuk melakukan pencarian nama domain. Perintah `less etc/resolv.conf` digunakan untuk melihat konfigurasi.
```
    less etc/resolv.conf
```
Perintah `ping www` mencoba menghubungi host bernama "www". Jika ada konfigurasi `search` di `/etc/resolv.conf`, sistem akan menambahkan domain, misalnya `www.pens.ac.id`. Jika tidak ditemukan, sistem akan meminta server DNS yang terdaftar untuk mencari alamat IP.
![img](/assets/week-4/dns/www.jpeg)

File **`root.hints`** adalah daftar server root DNS yang membantu server DNS mencari alamat IP sebuah domain. Jika tidak ada data di cache, server menggunakan file ini untuk menemukan server yang bisa menjawab permintaan. Dengan **`root.hints`**, server DNS tetap dapat berfungsi meskipun ada perubahan pada jaringan global.
![img](/assets/week-4/dns/hints.jpeg)
![img](/assets/week-4/dns/hints2.jpeg)
![img](/assets/week-4/dns/hints3.jpeg)


## instalasi dan Konfigurasi Bind9

Perintah `apt -y install bind9 bind9utils` digunakan untuk menginstal BIND9, sebuah server DNS di sistem berbasis Debian atau ubuntu.  
![img](/assets/week-4/bind9/1.png) 

File `/etc/bind/named.conf` adalah pusat konfigurasi utama BIND9, yang mengarahkan sistem ke file konfigurasi lainnya untuk mengelola layanan DNS. Pada file ini menambahkan `named.conf.internal-zones`sebagai file konfigurasi baru.
![img](/assets/week-4/bind9/2_1.png) 
![img](/assets/week-4/bind9/2.png) 

Mengecek internal network.
![img](/assets/week-4/bind9/3inet.png) 

Menambahkan ACL (Access Control List) dengan nama internal-network untuk jaringan 192.168.100.0/24 di BIND9. Dengan menambahkan ACL internal-network, hanya perangkat dalam jaringan 192.168.100.0/24 yang dapat melakukan query dan rekursi ke server DNS. Ini meningkatkan keamanan dengan mencegah akses dari jaringan luar.
![img](/assets/week-4/bind9/4_1.png) 
![img](/assets/week-4/bind9/4.png) 

Konfigurasi untuk zona forward dan zona reverse yang sesuai dengan domain kelompok5.home dan subnet 192.168.100.0/24 di BIND9. Zona forward (kelompok5.home) menerjemahkan nama domain ke IP.
Zona reverse (100.168.192.in-addr.arpa) menerjemahkan IP ke nama domain.
![img](/assets/week-4/bind9/5_1.png)
![img](/assets/week-4/bind9/5.png)  

Menambahkan -u bind -4 di `/etc/default/named` memastikan BIND9 berjalan dengan pengguna bind untuk keamanan dan hanya menggunakan IPv4, menghindari potensi masalah dengan IPv6.
![img](/assets/week-4/bind9/6_1.png) 
![img](/assets/week-4/bind9/6.png) 

Konfigurasi file zona forward (kelompok5.home.lan) yang telah disesuaikan dengan domain kelompok5.home dan jaringan 192.168.100.0/24. File kelompok5.home.lan digunakan untuk forward lookup di BIND9.
Nama domain seperti www.kelompok5.home akan diterjemahkan ke alamat IP di jaringan 192.168.100.0/24.
Konfigurasi ini memastikan server dapat merespons permintaan DNS dengan benar dalam jaringan internal.
![img](/assets/week-4/bind9/7_1.png) 
![img](/assets/week-4/bind9/7.png) 

Konfigurasi file zona reverse (100.168.192.db) yang sesuai dengan domain kelompok5.home dan jaringan 192.168.100.0/24. File 100.168.192.db digunakan untuk reverse lookup (menerjemahkan alamat IP ke nama domain) di jaringan 192.168.100.0/24.
Dengan konfigurasi ini, 192.168.100.10 akan di-resolve sebagai www.kelompok5.home
![img](/assets/week-4/bind9/8_1.png) 
![img](/assets/week-4/bind9/8.png) 

Perintah berikut digunakan untuk me-restart layanan BIND9 setelah melakukan perubahan konfigurasi DNS.
![img](/assets/week-4/bind9/9.png) 

Konfigurasi /etc/resolv.conf memastikan sistem menggunakan DNS lokal (192.168.100.166) untuk menyelesaikan domain internal seperti www.kelompok5.home.
![img](/assets/week-4/bind9/10_1.png)
![img](/assets/week-4/bind9/10.png)

Perintah `dig dlp.kelompok5.home` digunakan untuk melakukan query DNS terhadap dlp.kelompok5.home menggunakan dig (Domain Information Groper).
![img](/assets/week-4/bind9/11.png)

Perintah `dig -x 192.168.100.166
` digunakan untuk melakukan reverse DNS lookup pada IP 192.168.100.166 menggunakan dig.
![img](/assets/week-4/bind9/12.png)    

Referensi

- [Configure for Internal Network](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=1)
- [Configure for Zone Files](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=3)
- [Verify Resolution ](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=4)