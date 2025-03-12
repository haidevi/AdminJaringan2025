<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Workshop Administrasi Jaringan<br></h1>
  <h2 style="text-align: center;">Instalisasi NTP dan Samba<br></h2>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://i.ibb.co/DC3QHnM/logo-pens.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh :</h3>
  <p style="text-align: center;">
  <strong>Zada Devi Mariama (3123500015)</strong>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2025/2026</h3>
  <hr>
</div> 
<br>

A.	Instalisasi NTP

1.	Melakukan instalisasi package NTPSec

    ![img](/assets/week-3/ntp/1apt.jpeg) 

2.	Jangan lupa masuk ke root terlebih dahulu

    ![img](/assets/week-3/ntp/2aptmasukroot.jpeg) 
    ![img](/assets/week-3/ntp/3apt.jpeg)

3.	Menyesuaikan konfigurasi pool dengan ntp server Indonesia

    ![img](/assets/week-3/ntp/4apt.jpeg) 

4.	Melakukan autentikasi 

    ![img](/assets/week-3/ntp/5aptautentikasi.jpeg) 

5.	Memeriksa sinkronisasi

    ![img](/assets/week-3/ntp/6apt.jpeg) 

B.	Instalisasi Samba
1.	Melakukan instalisasi package Samba

    ![img](/assets/week-3/samba/1samba.jpeg) 

2.	Konfigurasi Samba

    ![img](/assets/week-3/samba/2samba.jpeg) 
    ![img](/assets/week-3/samba/3samba.jpeg)

3.	Membuat file direktori

    ![img](/assets/week-3/samba/4samba.jpeg)
    ![img](/assets/week-3/samba/5samba.jpeg)
    ![img](/assets/week-3/samba/6samba.jpeg)  

4.	Konfigurasi samba

    ![img](/assets/week-3/samba/7samba.jpeg) 

5.	Membuat sebuah file dan menambahkan user baru

    ![img](/assets/week-3/samba/8samba.jpeg)
    ![img](/assets/week-3/samba/9samba.jpeg)
    ![img](/assets/week-3/samba/10samba.jpeg)  

6.	Percobaan akses melalui CLI

    ![img](/assets/week-3/samba/11samba.jpeg)
    ![img](/assets/week-3/samba/12samba.jpeg)
    ![img](/assets/week-3/samba/13samba.jpeg)
    ![img](/assets/week-3/samba/14samba.jpeg)
    ![img](/assets/week-3/samba/15samba.jpeg)
    ![img](/assets/week-3/samba/16samba.jpeg)
    ![img](/assets/week-3/samba/17samba.jpeg)
    ![img](/assets/week-3/samba/18samba.jpeg)
    ![img](/assets/week-3/samba/19.jpeg) 

7.	Percobaan akses di computer lain

    ![img](/assets/week-3/samba/20samba.png) 
    ![img](/assets/week-3/samba/21samba.png)
    ![img](/assets/week-3/samba/22samba.png)


###Rangkuman Package Management:

Package management adalah proses untuk mengelola perangkat lunak yang terinstal pada sistem operasi, termasuk instalisasi, pembaruan, penghapusan dan pemeliharaan depedensi yang dibutuhkan oleh perangkat lunak tersebut. Berdasarkan referensi dari buku the begginers handbook Debian 12, terdapat cara dan alat yang digunakan dalam manajemen paket di sistem Debian dan distribusi berbasis Debian.

###APT (Advanced Package Tool)

APT adalah manajer paket yang digunakan untuk menginstal, memperbarui, dan menghapus paket perangkat lunak dalam sistem Debian dan distribusi berbasis Debian. APT memudahkan penngelolaan perangkat lunak dengan menyediakan perintah seperti sudo apt install nama_paket untuk menginstal aplikasi. Sudo apt update untuk memperbarui daftar paket. Sudo apt upgrade untuk memperbarui aplikasi yang sudah terinstal.  APT menangani ketergantungan secara otomatis, sehingga sistem dapat menjaga konsistensi antara aplikasi yang terinstal dan dependensinya.

###dpkg

Dpkg adalah alat manajemen paket Tingkat rendah untuk menginstall paket berformat .deb. Perintah utama instalisasi dengan dpkg adalah sudo dpkg -I nama_paket.deb untuk menginstal paket .deb dan sudo apt install -f untuk memperbaiki ketergantungan yang hilang setelah instalasi dengan dpkg.
dpkg tidak menangani ketergantungan secara otomatis, sehingga sering kali perlu dilengkapi dengan APT untuk menangani ketergantungan.

###Snap 

Snap adalah sistem paket yang memungkinkan aplikasi dan semua dependensinya berada dalam satu paket. Snap memungkinkan instalasi aplikasi di berbagai distribusi Linux. Untuk menggunakan Snap dapat menggunakan perintah berikut, sudo apt install snapd untuk menginstal Snap,  sudo snap install nama_aplikasi untuk menginstal aplikasi Snap. Snap menawarkan manfaat portabilitas karena aplikasi yang dikemas dengan Snap dapat berjalan di berbagai distribusi Linux tanpa perlu konfigurasi tambahan.

###Flatpak 

Flatpak adalah sistem manajemen aplikasi yang mengisolasi aplikasi dalam "sandbox" untuk meningkatkan keamanan. Untuk menggunakan Flatpak dapat menggunakan perintah seperti, sudo apt install flatpak untuk menginstal Flatpak, flatpak remote-add flathub https://flathub.org/repo/flathub.flatpakrepo untuk menambahkan repositori aplikasi, flatpak install flathub nama_aplikasi untuk menginstal aplikasi Flatpak. Flatpak juga memungkinkan aplikasi berjalan dengan ketergantungan yang terisolasi, mengurangi risiko konflik antar aplikasi.

Menginstal dari paket eksternal “’.deb”
Paket eksternal .deb yang tidak tersedia di repositori APT dapat diinstal dengan menggunakan dpkg atau aplikasi grafis seperti GDebi. Ini berguna untuk menginstal aplikasi yang tidak tersedia di repositori resmi. Menggunakan  GDebi (grafis) atau dpkg (terminal) untuk menginstal file .deb.

![img](/assets/week-3/gdebi.png)

###Membersihkan Sistem 

Pembersihan sistem adalah langkah penting dalam manajemen paket untuk menghemat ruang disk dan menjaga kinerja sistem. Beberapa perintah penting untuk membersihkan sistem seperti, sudo apt clean untuk menghapus cache paket yang diunduh, sudo apt autoremove --purge untuk menghapus paket yang tidak lagi diperlukan, rm -Rf ~/.cache/* untuk menghapus cache aplikasi, rm -Rf ~/.thumbnails untuk menghapus thumbnail yang tidak terpakai.

###Debian Branches (Sid) 

Debian memiliki beberapa cabang distribusi dengan stabilitas yang berbeda:
•	Stable adalah versi stabil yang siap digunakan sehari-hari.
•	Testing adalah versi yang sedang dikembangkan untuk menjadi versi Stable berikutnya.
•	Unstable (Sid) adalah versi yang tidak stabil dengan fitur terbaru, namun dapat berisiko.
Penting untuk memahami perbedaan ini saat memilih distribusi untuk sistem Debian, terutama dalam konteks pembaruan dan stabilitas sistem.

###Mengelola Flatpak 

Flatpak memungkinkan aplikasi berjalan dalam lingkungan terisolasi dan dapat dikelola dengan perintah seperti: flatpak search nama_aplikasi untuk mencari aplikasi, flatpak install flathub nama_aplikasi untuk menginstal aplikasi dari Flathub, flatpak uninstall nama_aplikasi untuk menghapus aplikasi, flatpak update untuk memperbarui aplikasi yang terinstal, flatpak run nama_aplikasi untuk menjalankan aplikasi. Repositori Flatpak seperti Flathub dan KDE Apps menyediakan akses ke berbagai aplikasi dengan dependensi lengkap.

###Kesimpulan

Manajemen paket adalah aspek penting dari pemeliharaan sistem Linux, memastikan perangkat lunak yang terinstal diperbarui, aman, dan tidak mengganggu stabilitas sistem. APT, dpkg, Snap, dan Flatpak adalah alat utama yang digunakan di Debian dan distribusi berbasis Debian, masing-masing dengan keunggulan dan kegunaannya sendiri dalam mengelola perangkat lunak.

##Referensi:

•	https://www.server-world.info/en/note?os=Debian_12&p=ntp&f=1
•	https://www.ntppool.org/en/zone/id
•	https://www.server-world.info/en/note?os=Debian_12&p=samba&f=1
•	The begginers handbook Debian 12: Enterprise Technology Hybrid Online Learning - ETHOL 
