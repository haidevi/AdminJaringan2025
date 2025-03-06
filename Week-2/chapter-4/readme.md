<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Workshop Administrasi Jaringan<br></h1>
  <h2 style="text-align: center;">Chapter 4-Process Control<br></h2>
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

## Komponen-Komponen Proses

   Sebuah proses terdiri dari ruang alamat (sekumpulan halaman memori yang digunakan untuk kode, data, dan tumpukan) serta struktur data di dalam kernel yang melacak status dan sumber daya proses. Kernel mengelola berbagai informasi tentang proses, termasuk peta ruang alamat, status, prioritas, sumber daya yang digunakan, file yang dibuka, serta pemilik proses.

Struktur data internal kernel mencatat berbagai informasi tentang setiap proses:

-	Peta ruang alamat proses
-	 Status proses saat ini (sedang berjalan, tidur, dan seterusnya)
-	Prioritas proses
-	Informasi tentang sumber daya yang digunakan proses (CPU, memori, dan sebagainya)
-	Informasi tentang file dan port jaringan yang telah dibuka oleh proses
-	Topeng sinyal proses (sekumpulan sinyal yang saat ini diblokir)
-	Pemilik proses (ID pengguna dari pengguna yang memulai proses)

Selain itu, thread adalah unit eksekusi dalam sebuah proses yang berbagi ruang alamat dan sumber daya yang sama. Thread memungkinkan paralelisme dalam sebuah proses dan lebih ringan dibandingkan dengan proses karena lebih cepat dibuat dan dihancurkan.

Setiap proses memiliki PID (Process ID), yaitu nomor unik yang diberikan oleh kernel saat proses dibuat. PID digunakan untuk merujuk ke proses dalam berbagai panggilan sistem, seperti pengiriman sinyal.
Setiap proses juga memiliki PPID (Parent Process ID), yaitu PID dari proses induknya yang membuat proses tersebut. PPID digunakan untuk merujuk ke proses induk dalam sistem.
Selain itu, terdapat UID (User ID), yaitu ID pengguna yang memulai proses, serta EUID (Effective User ID), yang menentukan hak akses proses terhadap sumber daya seperti file dan port jaringan.

## Daur Hidup Proses
    Daur hidup sebuah proses dimulai ketika sebuah proses membuat salinan dirinya menggunakan panggilan sistem fork. Proses baru ini memiliki PID berbeda dan informasi akuntansi sendiri. Di Linux, fork sebenarnya memanggil clone, yang memiliki fitur tambahan untuk menangani thread.
Saat sistem booting, kernel secara otomatis membuat beberapa proses, termasuk init atau systemd (proses dengan PID 1). Proses ini menjalankan skrip startup sistem dan menjadi induk bagi semua proses lain yang dibuat di sistem.

## Sinyal
Sinyal adalah mekanisme untuk mengirim pemberitahuan ke suatu proses saat terjadi peristiwa tertentu. Ada sekitar 30 jenis sinyal yang digunakan untuk berbagai keperluan, seperti:  

- Komunikasi antarproses.  
- Menghentikan atau menangguhkan proses saat tombol tertentu ditekan di terminal.  
- Digunakan oleh administrator dengan perintah `kill` untuk mengelola proses.  
- Dikirim oleh kernel saat terjadi kesalahan, seperti pembagian dengan nol.  
- Memberi tahu proses tentang kejadian penting, misalnya proses anak yang berakhir atau data yang siap dibaca di I/O.

    ![img](/assets/week-2/ch4-1.png) 

## Kill: Mengirim Sinyal
    Perintah kill digunakan untuk mengirim sinyal ke proses, biasanya untuk menghentikannya. Secara default, `kill` mengirim sinyal TERM, tetapi proses masih bisa menangkap atau mengabaikannya. Jika ingin memastikan proses benar-benar mati, gunakan kill -9, yang mengirim sinyal KILL yang tidak bisa diblokir. Selain itu, ada `killall` yang menghentikan proses berdasarkan nama, meskipun tidak tersedia di semua sistem. Alternatif lain adalah `pkill`, yang lebih fleksibel karena bisa menghentikan proses berdasarkan kriteria tertentu, seperti semua proses milik pengguna tertentu dengan perintah pkill -u user.
```
kill [-signal] pid
```

```
killall firefox
```

```
pkill -u abdoufermat # kill all processes owned by user abdoufermat
```

## PS: Proses Pemantauan
    Perintah ps adalah alat utama untuk memantau proses di sistem. Meskipun tampilannya bisa berbeda antarversi, fungsinya tetap sama, yaitu menampilkan informasi seperti PID, UID, prioritas, penggunaan memori, waktu CPU, dan status proses. Untuk melihat daftar proses secara lengkap, gunakan ps aux. Opsi a menampilkan proses dari semua pengguna, u memberikan detail lebih rinci, dan x menampilkan proses yang tidak terkait dengan terminal.
    ```
    $ ps aux | head -8
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.0  0.0  22556  2584 ?        Ss   2019   0:02 /sbin/init
    root         2  0.0  0.0      0     0 ?        S    2019   0:00 [kthreadd]
    root         3  0.0  0.0      0     0 ?        I<   2019   0:00 [rcu_gp]
    root         4  0.0  0.0      0     0 ?        I<   2019   0:00 [rcu_par_gp]
    root         6  0.0  0.0      0     0 ?        I<   2019   0:00 [kworker/0:0H-kblockd]
    root         8  0.0  0.0      0     0 ?        I<   2019   0:00 [mm_percpu_wq]
    root         9  0.0  0.0      0     0 ?        S    2019   0:00 [ksoftirqd/0]
    ```

    ![img](/assets/week-2/ch4-2.png) 

## Pemantauan Interaktif dengan Top
    
Perintah top menampilkan informasi sistem dan daftar proses secara real-time, dengan pembaruan setiap 1-2 detik. Pengguna dapat menyesuaikan tampilan dan menyimpannya untuk digunakan kembali setelah restart. Alternatifnya, ada htop, yang menawarkan tampilan lebih interaktif dengan kemampuan menggulir vertikal dan horizontal, serta antarmuka yang lebih intuitif dibandingkan top. htop juga memungkinkan pengguna melihat perintah lengkap yang digunakan oleh setiap proses.

## Nice dan Renice: Mengubah Prioritas
    Nice adalah nilai yang menentukan prioritas suatu proses dalam persaingan mendapatkan CPU. Nilai niceness yang lebih tinggi berarti prioritas lebih rendah, sementara nilai lebih rendah atau negatif berarti prioritas lebih tinggi. Di Linux, nilainya berkisar dari -20 hingga +19, sedangkan di FreeBSD dari -20 hingga +20. Proses dengan prioritas tinggi mendapatkan lebih banyak waktu CPU dibandingkan proses dengan prioritas rendah. Jika menjalankan proses yang membutuhkan banyak CPU di latar belakang, menaikkan nilai niceness dapat membantu proses lain tetap berjalan lancar tanpa terganggu.
## Sistem Berkas/Proc
    Versi Linux ps dan top membaca informasi status proses dari direktori /proc, sebuah sistem berkas semu di mana kernel menampilkan berbagai informasi menarik tentang status sistem.

Terlepas dari namanya, /proc berisi informasi lain selain proses (statistik yang dihasilkan oleh sistem, dll).

Proses diwakili oleh direktori dalam /proc, dan setiap proses memiliki direktori yang diberi nama sesuai dengan PID-nya. Direktori /proc berisi berbagai macam berkas yang menyediakan informasi tentang proses, seperti baris perintah, variabel lingkungan, deskriptor berkas, dan sebagainya.
    
    ![img](/assets/week-2/ch4-3.png)

## Strace and Truss
    Untuk mengetahui apa yang sedang dilakukan oleh sebuah proses, Anda dapat menggunakan strace pada Linux atau truss pada FreeBSD. Perintah-perintah ini melacak panggilan sistem dan sinyal. Perintah-perintah ini dapat digunakan untuk men-debug sebuah program atau untuk memahami apa yang dilakukan oleh sebuah program.

Sebagai contoh, log berikut ini dihasilkan oleh strace yang dijalankan pada sebuah salinan aktif dari top (yang berjalan sebagai PID 5810):

## Proses yang Berhenti
    Kadang-kadang sebuah proses akan berhenti merespon sistem dan berjalan secara liar. Proses-proses ini mengabaikan prioritas penjadwalan mereka dan bersikeras mengambil 100% dari CPU. Karena proses lain hanya bisa mendapatkan akses terbatas ke CPU, mesin mulai berjalan sangat lambat. Ini disebut proses yang kabur.

Perintah kill dapat digunakan untuk menghentikan proses yang kabur. Jika proses tidak merespon sinyal TERM, Anda dapat menggunakan sinyal KILL untuk menghentikannya

## Proses Berkala
    cron: perintah penjadwalan

Daemon cron (crond pada RedHat: ya, orang aneh!!) adalah alat tradisional untuk menjalankan perintah pada jadwal yang telah ditentukan. Ia dimulai saat sistem melakukan booting dan berjalan selama sistem hidup.

cron membaca berkas konfigurasi yang berisi daftar baris perintah dan waktu pemanggilannya. Baris perintah dieksekusi oleh sh, sehingga hampir semua hal yang dapat Anda lakukan secara manual dari shell juga dapat dilakukan dengan cron.

Sebuah berkas konfigurasi cron disebut “crontab”, kependekan dari “cron table”. Crontab untuk pengguna individual disimpan di bawah /var/spool/cron (Linux) atau /var/cron/tabs (FreeBSD).

Format dari crontab
Sebuah berkas crontab memiliki lima field untuk menentukan hari, tanggal dan waktu yang diikuti oleh perintah yang akan dijalankan pada interval tersebut.


## Pengatur Waktu Systemd
    Timer systemd adalah berkas konfigurasi unit yang namanya berakhiran .timer. timer systemd dapat digunakan sebagai alternatif untuk pekerjaan cron. Mereka lebih fleksibel dan lebih kuat daripada pekerjaan cron.

Sebuah unit timer diaktifkan oleh unit layanan yang sesuai. Unit layanan dipicu oleh unit pengatur waktu pada waktu yang ditentukan dalam unit pengatur waktu. Unit pengatur waktu juga dapat diaktifkan oleh boot sistem atau oleh suatu peristiwa.

Perintah systemctl digunakan untuk mengelola unit systemd. Opsi list-timers digunakan untuk membuat daftar timer yang aktif.

## Penggunaan Umum untuk Tugas Terjadwal
   1. Mengirim Email
      o	Tugas terjadwal dapat digunakan untuk mengirim email otomatis, seperti laporan harian atau hasil eksekusi perintah menggunakan cron atau systemd timers.
      ```
        30 4 25 * * /usr/bin/mail -s "Monthly report"
          abdou@admin.com%Receive the monthly report for the month of July!%%Sincerely,%cron%
      ```
   2. Membersihkan Sistem Berkas
      o	Cron atau systemd timers dapat digunakan untuk menjalankan skrip yang membersihkan sistem file, misalnya menghapus file sampah setiap hari pada tengah malam.
        ```  
        0 0 * * * /usr/bin/find /home/abdou/.local/share/Trash/files -mtime +30 -exec /bin/rm -f {} \;
        ```
   3. Rotasi File Log
      o	Rotasi log membagi file log menjadi beberapa segmen berdasarkan ukuran atau tanggal, menjaga versi lama tetap tersedia. Karena dilakukan secara berkala, tugas ini cocok dijadwalkan secara otomatis.
   4. Menjalankan Pekerjaan Batch
      o	Tugas jangka panjang seperti pemrosesan antrian pesan atau data dapat dijadwalkan menggunakan cron job, misalnya sebagai proses ETL (Extract, Transform, Load) ke gudang data.
   5. Mencadangkan dan Mencerminkan Data
      o	Menggunakan rsync secara terjadwal untuk mencadangkan atau menyinkronkan file antar sistem.
