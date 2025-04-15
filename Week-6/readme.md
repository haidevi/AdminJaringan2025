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



## Konfigurasi VM 1 (NoGUI)

1. Penyesuaian network pada adapter 1 dan 2
![img](/assets/week-6/1.png)
![img](/assets/week-6/2.png)

2. Login dan mengecek ip a
![img](/assets/week-6/3.png)

3. Akses ip melalui ssh
![img](/assets/week-6/4.png)

4. Melihat file konfigurasi dan mengatur konfigurasi IP secara manual.
![img](/assets/week-6/5-1.png)
![img](/assets/week-6/5.png)

5. Mengedit file konfigurasi dan mengaktifkan opsi `net.ipv4.ip_forward=1`.
![img](/assets/week-6/6-1.png)
![img](/assets/week-6/6.png)

6. Validasi dengan perintah berikut.
![img](/assets/week-6/7.png)

7. Mengunduh paket iptables dan iptables persistent.
![img](/assets/week-6/8.png)

8. Menambahkan baris kode pada file berikut.
![img](/assets/week-6/9-1.png)
![img](/assets/week-6/9.png)

9. Mengembalikan aturan-aturan iptables dari file konfigurasi yang sebelumnya.
![img](/assets/week-6/10.png)

## Konfigurasi NTP

1. Instalasi NTP client.

![img](/assets/week-6/ntp/1.png)

2. Menambahkan server NTP.
![img](/assets/week-6/ntp/2-1.png)
![img](/assets/week-6/ntp/2.png)

3. Merestart NTP client menggunakan konfigurasi yang baru.
![img](/assets/week-6/ntp/3.png)

4. Mengecek status NTP.
![img](/assets/week-6/ntp/4.png)

## Konfigurasi Samba

1. Mengunduh package samba.
![img](/assets/week-6/samba/1.png)

2. Membuat direktori dan mengubah aksesnya.
![img](/assets/week-6/samba/2.png)

3. Menambahkan unix charset = UTF-8 untuk kompatibilitas dan menambahkan interface.
![img](/assets/week-6/samba/3-1.png)
![img](/assets/week-6/samba/3-2.png)
Menambahkan konfigurasi folder public.
![img](/assets/week-6/samba/3-3.png)
Mengecek akses samba pada VM 1 dengan ip menggunakan VM 2.
![img](/assets/week-6/samba/3-4.png)

4. Merestart dan mengecek status samba.
![img](/assets/week-6/samba/4.png)

## Konfigurasi Bind9

1. Instalasi BIND9 

![img](/assets/week-6/bind/1.png)

2. Mengonfigurasi BIND dan menambahkan `include "/etc/bind/named.conf.internal-zones"`. 

![img](/assets/week-6/bind/2-1.png)
![img](/assets/week-6/bind/2.png)

3. Menambahkan beberapa baris kode dengan perintah berikut.
![img](/assets/week-6/bind/3-1.png)
![img](/assets/week-6/bind/3.png)

4. Menyimpan dan mendefinisikan konfigurasi zona internal.
![img](/assets/week-6/bind/4-1.png)
![img](/assets/week-6/bind/4.png)

5. Menjalankan proses named dengan user bind
![img](/assets/week-6/bind/5-1.png)
![img](/assets/week-6/bind/5.png)

6. Menyimpan record DNS seperti A, NS, MX, dan lainnya untuk domain kelompok5.home.lan
![img](/assets/week-6/bind/6-1.png)
![img](/assets/week-6/bind/6.png)

7. Mengubah nama domain menjadi alamat IP menggunakan perintah berikut.
![img](/assets/week-6/bind/7-1.png)
![img](/assets/week-6/bind/7.png)

## Konfigurasi VM 2

1. Mengubah adapter network menjadi internal network.
![img](/assets/week-6/vm2/1.png)

2. Mengonfigurasi jaringan wired
![img](/assets/week-6/vm2/2.png)

3. Mengecek folder samba.
![img](/assets/week-6/vm2/file.png)

4. Mengecek layanan DNS di VM 2. DNS dianggap berhasil jika hasilnya menampilkan flag ANSWER: 1 atau lebih serta status NOERROR.
![img](/assets/week-6/vm2/3.png)
![img](/assets/week-6/vm2/4.png)


