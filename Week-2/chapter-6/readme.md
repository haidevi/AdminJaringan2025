<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Workshop Administrasi Jaringan<br></h1>
  <h2 style="text-align: center;">Chapter 6-Software Installation and Management<br></h2>
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

## Instalasi Sistem Operasi
    Linux dan FreeBSD memiliki prosedur intalisasi dasar yang sederhana. Untuk mesin fisik, booting dapat dilakukan dari CD, DVD, atau USB. Sementara, untuk mesin virtual, cukup pakai file ISO. Adanya GUI yang membantu prosesnya, instalisasi OS menjadi lebih mudah.
## Instalasi dari Jaringan
    Menginstal OS di banyak komputer dengan memakai media lokal akan memakan banyak waktu. Solussinya adalah melakukan instalisasi melalui jaringan, yang umumnya dipakai di pusat data dan cloud. Metode yang sering digunakan yaitu, DHCP dan TFTP untuk booting tanpa media fisik, lalu mengambil file instalisasi OS dari server melalui HTTP, FTP atau NFS. Bisa juga memakai PXE (Preboot eXecution Environment) dari Intel, yang memungkinkan sistem boot langsung dari jaringan tanpa perlu driver khusus untuk setiap kartu jaringan. 
     ![img](/assets/week-2/ch6.png)
## Sistem Manajemen Paket Linux
    Di Linux, terdapat dua format paket utama: RPM(dipakai di Red Hat, CentOS, SUSE,dll) dan .deb (dipakai di Debian dan Ubuntu). Keduanya mirip secara fungsional. RPM menggunakan rpm, sedangkan .deb memakai dpkg untuk instalasi dan pengelolaan paket. Di atasnya, terdapat alat manajemen paket otomatis seperti yum untuk RPM dan APT untuk .deb, yang bisa mencari, mengunduh, serta mengelola dependensi paket dari internet.
## Manajemen Paket Tinngkat Tinggi
    Alat manajemen paket tingkat tinggi sering dipakai untuk install, hapus, dan upgrade paket. Selain itu, bisa dipakai untuk  mencari paket dan melihat daftar paket yang terinstal di sistem.
## Repositori Paket
    Repositori paket adalah tempat penyimpanan perangkat lunak yang dikelola oleh distributor Linux dan terhubung dengan sistem manajemen paket. Secara default, sistem ini diarahkan ke server resmi distributor melalui web atau FTP. Repositori terdiri dari rilis (kumpulan paket yang konsisten), komponen (bagian dari perangkat lunak dalam rilis), dan arsitektur (kelas perangkat keras yang bisa menjalankan biner yang sama), seperti i386 pada Fedora 20.
## APT: Alat Paket Tingkat Lanjut
    APT adalah sekumpulan alat untuk mengelola paket di sistem berbasis Debian dan merupakan sistem manajemen paket yang paling banyak digunakan.

      Beberapa alat dalam APT:
        
        - apt-get → Menginstal, menghapus, dan memperbarui paket.
        - apt-cache → Mencari dan melihat informasi paket di cache APT.
        - apt-file → Mencari file dalam paket.
        - apt-show-versions → Menampilkan versi paket yang tersedia.
        - aptitude → Antarmuka tingkat tinggi untuk manajemen paket, bisa melakukan tugas seperti apt-get dan lebih banyak lagi.
        - apt-mirror → Untuk mencerminkan (mirror) repositori paket.
    
    Di sistem Ubuntu, abaikan dselect, karena alat ini hanya antarmuka lama untuk sistem paket Debian.
## Yum: Pemutakhiran Yellowdog, Dimodifikasi
    YUM adalah manajer paket untuk sistem Linux berbasis RPM. YUM adalah alat tingkat tinggi yang bisa mengelola paket, menyelesaikan dependensi saat instalasi, update, atau penghapusan paket. YUM juga bisa mengambil paket dari repositori yang terinstal atau menjalankan perintah langsung di terminal untuk mengelola paket tertentu.
## Lokalisasi dan Konfigurasi Perangkat Lunak
    Menyesuaikan sistem dengan lingkungan lokal atau cloud adalah tantangan utama dalam administrasi sistem. Pendekatan yang terstruktur dan bisa direplikasi membantu mencegah sistem snowflake yang sulit dipulihkan saat terjadi masalah besar.