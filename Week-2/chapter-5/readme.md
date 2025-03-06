<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Workshop Administrasi Jaringan<br></h1>
  <h2 style="text-align: center;">Chapter 5-The Filesystem <br></h2>
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


![img](/assets/week-2/ch5-1.png) 

Sistem berkas berfungsi untuk mengelola penyimpanan dengan empat komponen utama: ruang nama (penamaan & hierarki), API (navigasi & manipulasi), model keamanan (proteksi & berbagi), dan implementasi (penghubung ke hardware). Sistem berkas populer di disk meliputi ext4, XFS, UFS, ZFS, dan Btrfs, sementara FAT & NTFS dipakai di Windows. Sistem berkas modern berusaha meningkatkan kecepatan, keandalan, atau menambahkan fitur baru di atas sistem berkas tradisional.

## Nama Jalan
Dalam dunia teknis, istilah yang benar adalah direktori, bukan folder. Nama path adalah jalur yang menunjukkan lokasi file dalam sistem berkas. Path bisa absolut (misalnya /home/username/file.txt) atau relatif (misalnya ./file.txt).

## Memasang dan Melepas Pemasangan Sistem Berkas
Filesystem terdiri dari beberapa bagian yang lebih kecil, masing-masing berisi satu direktori beserta subdirektori dan file di dalamnya. Struktur keseluruhan disebut file tree, sedangkan filesystem mengacu pada cabang-cabang yang terhubung ke pohon tersebut. Untuk menghubungkan filesystem ke file tree, dapat menggunakan perintah mount. Perintah ini menghubungkan direktori dalam file tree yang ada (mount point) ke root dari filesystem baru.
    
    ```
    # Mount the filesystem on /dev/sda4 to /users
      mount /dev/sda4 /users
    ```

Untuk melepas pemasangan, digunakan perintah umount. Opsi umount -l (lazy unmount) akan menghapus sistem berkas dari hierarki tetapi menunggu hingga tidak digunakan sebelum benar-benar dilepas. Jika sistem berkas masih sibuk, umount -f dapat digunakan untuk memaksa unmount. Alternatifnya, gunakan lsof atau fuser untuk menemukan proses yang masih menggunakan sistem berkas sebelum menghentikannya.
    
    ```
    # Find out which processes are using the filesystem
 
    abdou@debian:~$ lsof /home/abdou

    COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
    bash     1000 abdou  cwd    DIR    8,1     4096  131073 /home/abdou
    bash     1000 abdou  rtd    DIR    8,1     4096  131073 /home/abdou
    bash     1000 abdou  txt    REG    8,1   103752  131072 /bin/bash
    bash     1000 abdou  mem    REG    8,1  1848400  131074 /lib/x86_64-linux-gnu/libc-2.28.so
    bash     1000 abdou  mem    REG    8,1   170864  131075 /lib/x86_64-linux-gnu/ld-2.28.so
    code     1234 abdou  cwd    DIR    8,1     4096  131073 /home/abdou
    msedge   5678 abdou  cwd    DIR    8,1     4096  131073 /home/abdou
    ```

Untuk menyelidiki proses yang menggunakan sistem berkas, dapat menggunakan perintah ps.
   
    ```
    # Investigate the processes that are using the filesystem
    abdou@debian:~$ ps up "1234 5678 91011"

    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    abdou     1234  0.0  0.0  12345  1234 ?        Ssl  00:00   0:00 code
    abdou     5678  0.0  0.0  12345  1234 ?        Ssl  00:00   0:00 msedge
    abdou     91011  0.0  0.0  12345  1234 ?        Ssl  00:00   0:00 chrome
    ```

## Pengroganisasian Pohon Berkas
Sistem UNIX memiliki struktur pohon berkas yang kurang terorganisir dengan baik, dengan berbagai konvensi penamaan yang tidak seragam dan penyebaran file yang acak. Hal ini membuat proses upgrade sistem operasi menjadi sulit. Root filesystem mencakup direktori root (/) dan sejumlah file serta subdirektori minimal. Kernel OS biasanya berada di /boot, meskipun lokasinya bisa berbeda-beda. Direktori penting lainnya meliputi:
    - /etc untuk konfigurasi sistem,
    - /sbin dan /bin untuk utilitas penting,
    - /tmp untuk file sementara,
    - /dev sebagai sistem berkas virtual yang dimount terpisah,
    - /lib atau /lib64 untuk pustaka bersama, yang pada beberapa sistem dipindahkan ke /usr/lib.
    - /usr menyimpan program standar yang tidak bersifat kritis bagi sistem, dokumentasi, dan pustaka 
    - /var berisi log sistem dan data yang sering berubah. 
    
/usr dan /var, kedua direktori ini harus tersedia agar sistem dapat masuk ke mode multiuser.

![img](/assets/week-2/ch5-2.png)


## Jenis-Jenis File

Sebagian besar implementasi sistem berkas mendefinisikan tujuh jenis berkas:

- File biasa
- Direktori
- File perangkat karakter
- File perangkat blokir
- Soket domain lokal
- Pipa bernama (FIFO)
- Tautan simbolik

Anda dapat menentukan jenis suatu file dengan menggunakan perintah file (ketik man file untuk informasi lebih lanjut).
    
    ```
    $ file /bin/bash
    bin/bash: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=33a5554034feb2af38e8c75872058883b2988bc5, for GNU/Linux 3.2.0, stripped
    ```
Anda juga dapat menggunakan ls -ld, di mana opsi -d memaksa ls untuk menampilkan informasi tentang direktori itu sendiri, bukan isi direktori tersebut.

    ![img](/assets/week-2/ch5-3.png)

File biasa menyimpan data tanpa struktur tertentu. Direktori berfungsi sebagai referensi ke file lain. Hard link memungkinkan satu file memiliki banyak nama, dan bisa dibuat menggunakan perintah ln.
contoh:
    ```
    $ ln /etc/passwd /tmp/passwd
    ```

File perangkat (device files) memungkinkan program berkomunikasi dengan perangkat keras dan periferal sistem. Kernel memuat driver untuk mengelola perangkat ini agar tetap abstrak dan tidak bergantung pada perangkat keras tertentu.
File perangkat dibedakan menjadi character device dan block device, tetapi perbedaannya tidak terlalu penting untuk dibahas secara rinci. Setiap file perangkat memiliki major number (menentukan driver perangkat) dan minor number (menentukan unit fisik yang dikontrol). Misalnya, pada Linux, major number 4 digunakan untuk driver serial, di mana /dev/tty0 memiliki minor number 0 dan /dev/tty1 memiliki minor number 1.
Dulu, perangkat dalam /dev dibuat dengan mknod dan dihapus dengan rm, tetapi sistem ini tidak efisien karena banyaknya perangkat dan driver yang muncul seiring waktu. Kini, /dev biasanya dimount sebagai sistem file khusus yang dikelola otomatis oleh kernel dan daemon pengguna.
Local domain sockets memungkinkan komunikasi antarproses dalam satu host, mirip dengan network sockets tetapi terbatas di sistem lokal. Contohnya, Syslog dan X Window System menggunakan local domain sockets.
Named pipes bekerja seperti local domain sockets untuk komunikasi antarproses dalam satu sistem.
Symbolic links (soft links) adalah referensi ke file berdasarkan nama, lebih fleksibel dibanding hard links karena dapat menunjuk ke file di sistem file berbeda dan juga ke direktori. Misalnya, /usr/bin sering kali merupakan symbolic link ke /bin, yang membantu menghemat ruang root filesystem dan memungkinkan berbagi perangkat lunak antar host dengan lebih mudah.
 
    ```
    $ ln -s /bin /usr/bin

    $ ls -l /usr/bin
    lrwxrwxrwx 1 root root 4 Mar  1  2020 /usr/bin -> /bin
    ```
## Atribut File
Setiap file dalam sistem Unix dan Linux memiliki **mode file**, terdiri dari **9 bit izin akses** (baca, tulis, eksekusi) dan **3 bit tambahan** untuk eksekusi program. Ditambah **4 bit tipe file**, yang tetap sejak file dibuat. Pemilik file atau superuser dapat mengubah mode file dengan `chmod`.

![img](/assets/week-2/ch5-4.png)

Permission bits terdiri dari tiga kelompok: **owner (u)**, **group (g)**, dan **others (o)**, yang dapat diingat dengan "Hugo". Izin juga bisa dinyatakan dalam **notasi oktal**, di mana setiap digit mewakili tiga bit: **400, 200, 100** untuk owner, **40, 20, 10** untuk group, dan **4, 2, 1** untuk others.  

Pada file biasa, **read (r)** memungkinkan membaca file, **write (w)** memungkinkan mengubah atau menghapus isinya, dan **execute (x)** memungkinkan menjalankan file, baik sebagai **biner** yang dieksekusi langsung oleh CPU maupun **skrip** yang dijalankan oleh interpreter seperti shell atau Python. Skrip biasanya diawali dengan **shebang (`#!`)** untuk menentukan interpreter yang digunakan.
    
    ```
    #!/usr/bin/perl
    ```

Nonbinary executable files tanpa interpreter diasumsikan sebagai sh scripts. Kernel mengenali shebang (#!), tetapi jika interpreter tidak ditentukan dengan benar, kernel menolak file tersebut, dan shell mencoba menjalankannya sebagai shell script.
Pada direktori, execute bit memungkinkan masuk atau melewati direktori tanpa menampilkan isinya. Kombinasi read + execute memungkinkan melihat isi direktori, sedangkan write + execute memungkinkan membuat, menghapus, dan mengganti nama file di dalamnya.

The setuid and setgid bits

Setuid (4000) dan setgid (2000) adalah bit izin khusus di Unix. Setuid: Saat diaktifkan pada file, eksekusi file akan menggunakan hak akses pemilik file, bukan pengguna yang menjalankannya. Setgid: Saat diaktifkan pada file, eksekusi file akan menggunakan hak akses grup file. Jika diterapkan pada direktori, file baru di dalamnya akan mewarisi grup direktori, bukan grup default pembuat file. Setgid pada direktori mempermudah berbagi file dalam satu grup pengguna.

The sticky bit

Sticky bit (1000) mencegah pengguna menghapus atau mengganti nama file yang bukan miliknya dalam direktori bersama seperti **`/tmp`**, meskipun memiliki izin menulis.

ls: membuat daftar dan memeriksa file

Perintah ls digunakan untuk menampilkan dan memeriksa file serta direktori. Ls -l menampilkan detail file dalam format panjang, termasuk izin, jumlah hard link, pemilik, grup, ukuran, waktu modifikasi, dan nama file. Setiap direktori memiliki minimal dua hard link: . (diri sendiri) dan .. (induknya). Output ls untuk file perangkat berbeda dari file biasa.
    
    ```
    $ ls -l /dev/tty0
    crw--w---- 1 root tty 4, 0 Mar  1  2020 /dev/tty0
    ```

chmod: ubah hak akses

Perintah chmod mengubah mode sebuah berkas. Anda dapat menggunakan notasi oktal atau notasi simbolik.
     ![img](/assets/week-2/ch5-5.png)
    
Contoh-contoh dari sintaks mnemonic chmod:

| Specifier  | Meaning                                                                  |
| ---------- | -------------------------------------------------------------------      |
| u+w        | Menambahkan izin menulis untuk pemilik berkas                            |
| ug=rw,o=r  | Memberikan izin r/w kepada pemilik dan grup, dan izin r kepada orang lain|
| a-x        | Menghapus izin eksekusi untuk semua pengguna                             |
| ug=srx, o= | Mengatur setuid, setgid, dan bit lengket untuk pemilik dan grup (r/x)    |
| g=u        | Membuat izin grup sama dengan pemilik                                    |

chown: mengubah kepemilikan

Perintah chown mengubah pemilik dan grup sebuah berkas. Opsi -R menyebabkan chown mengubah kepemilikan isi berkas secara rekursif.

```
$ chown -R abdou:users /home/abdou
```

chgrp: mengubah grup

Perintah chgrp mengubah grup sebuah berkas. Opsi -R menyebabkan chgrp mengubah grup isi berkas secara rekursif.

```
$ chgrp -R users /home/abdou
```

umask: mengatur izin default

Perintah umask menetapkan perizinan default untuk berkas dan direktori baru. Perintah umask adalah sebuah bit mask yang dikurangkan dari perizinan default untuk menentukan perizinan yang sebenarnya.

Contoh:

```
$ umask 022
```

| Octal | Binary | Perms | Octal | Binary | Perms |
| ----- | ------ | ----- | ----- | ------ | ----- |
| 0     | 000    | rwx   | 4     | 100    | -wx   |
| 1     | 001    | rw-   | 5     | 101    | -w-   |
| 2     | 010    | r-x   | 6     | 110    | --x   |
| 3     | 011    | r--   | 7     | 111    | ---   |
 
## Daftar Kontrol Akses
Model perizinan Unix tradisional memiliki keterbatasan, seperti sulitnya menetapkan banyak pemilik untuk satu file atau memberikan izin berbeda ke grup pengguna tertentu. Access Control Lists (ACL) memperluas model ini dengan memungkinkan file memiliki beberapa pemilik dan izin yang bervariasi untuk tiap grup pengguna.
Setiap aturan dalam ACL disebut Access Control Entry (ACE), yang terdiri dari penentu pengguna/grup, topeng izin, dan tipe (izinkan atau tolak). Untuk melihat ACL suatu file, gunakan perintah getfacl, sedangkan untuk mengaturnya gunakan setfacl.
    
    ```
    $ getfacl /etc/passwd
    ```

    ```
    $ setfacl -m u:abdou:rw /etc/passwd
    ```
Ada dua jenis ACL: ACL POSIX dan ACL NFSv4. ACL POSIX adalah ACL Unix tradisional, dan ACL NFSv4 adalah jenis ACL yang lebih baru dan lebih kuat.

## Implementasi ACL 
ACL dapat dikelola oleh kernel, sistem berkas, atau perangkat lunak tingkat tinggi seperti NFS dan SMB untuk mengontrol akses ke file dan direktori.
## POSIX ACLs
POSIX ACLs adalah ACL tradisional di Unix dan didukung oleh sebagian besar sistem operasi berbasis Unix, termasuk Linux, FreeBSD, dan Solaris.

  | Format                | Example         | Sets permissions for      |
  | --------------------- | --------------- | ------------------------- |
  | user::perms           | user:rw-        | Pemilik file              |
  | user:username:perms   | user:abdou:rw-  | Pengguna tertentu         |
  | group::perms          | group:r-x       | Grup pemilik file         |
  | group:groupname:perms | group:users:r-x | Grup tertentu             |
  | mask::perms           | mask::rwx       | Maksimum yang diberikan   |
  | other::perms          | other::r--      | Semua pengguna lain       |

    ```
    $ setfacl -m user:abdou:rwx,group:users:rwx,other::r /home/abdou

    $ getfacl --omit-header /home/abdou

    user::rwx
    user:abdou:rwx
    group::r-x
    group:users:r-x
    mask::rwx
    other::r--
    ```

## ACL NFSv4
    
ACL NFSv4 adalah jenis ACL yang lebih baru dan lebih kuat, didukung oleh beberapa sistem operasi berbasis Unix seperti Linux dan FreeBSD. Mirip dengan POSIX ACLs, tetapi memiliki fitur tambahan, seperti default ACL, yang secara otomatis menetapkan izin untuk file dan direktori baru.


