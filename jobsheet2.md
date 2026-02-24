# Laporan Praktikum Sistem Operasi Jobsheet 2

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>


## 2.1 Percobaan 1: Identifikasi CPU dan Memori
![step1.png](pict_jobsheet2/step1.png)

### Latihan 2.1
Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

### Jawaban latihan 2.1
1. Jumlah CPU(s) pada perangkat adalah 16, jumlah corenya adalah 8, dan jumlah thread nya adalah 2 setiap core, yang artinya perangkat ini memiliki 16 thread.

## 2.2 Percobaan 2: Identifikasi Perangkat PCI/USB dan Driver
![step2.png](pict_jobsheet2/step2.png)

### Latihan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

### Jawaban latihan 2.2
Perangkat         : Network controller (NIC Wi-Fi)
Vendor:Device ID  : 10ec:8922
10ec              : vendor Realtek Semiconductor
8922              : ID perangkat Wi-Fi Realtek
Driver            : rtw89_8922a
Perangkat ini adalah kartu jaringan nirkabel atau Wi-Fi yang memungkinkan laptop terhubung ke internet melalui router atau access point tanpa menggunakan kabel. Selain itu, perangkat ini juga sering kali mendukung fitur Bluetooth yang diintegrasikan dalam chipset yang sama.

## 2.3 Percobaan 3: Identifikasi Storage dan Filesystem
![step3.1.png](pict_jobsheet2/step3.1.png)
![step3.2.png](pict_jobsheet2/step3.2.png)

## 2.4 Percobaan 4: Melihat Modul Aktif dan Informasinya
![step4.png](pict_jobsheet2/step4.png)

## 2.5 Percobaan 5: Konfigurasi Auto-load dan Blacklist
![step5.png](pict_jobsheet2/step5.png)

## 2.6 Percobaan 6 Mengenali Block vs Character Device
![step6.1.png](pict_jobsheet2/step6.1.png)
![step6.2.png](pict_jobsheet2/step6.2.png)
![step6.3.png](pict_jobsheet2/step6.3.png)

### Latihan 2.3
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan character device. (Hint: karakter pertama pada permission string)

### Jawaban Latihan 2.3
Pada ls -l karakter pertama pada permission String menunjukan tipe file
jika karakter pertama c berarti character device. yaitu perangkat yang mengirim dan menerima data dalam bentuk aliran karakter secara berurutan, seperti terminal, keyboard, atau port serial.
jika karakter pertama b berarti block device. yaitu perangkat yang memproses data dalam blok-blok sehingga mendukung akses acak dan buffering, seperti hard disk, SSD, atau flashdisk.
Dengan demikian, perbedaan utama antara penanda c dan b pada output ls -l terletak pada cara perangkat menangani data

## 2.7 Percobaan 7: Melihat Informasi udev
![step7.png](pict_jobsheet2/step7.png)

## 2.8 Percobaan 8: Membuat Workspace Praktikum
![step8.1.png](pict_jobsheet2/step8.1.png)
![step8.2.png](pict_jobsheet2/step8.2.png)

## 2.9 Percobaan 9: Pencarian Pola dengan grep
![step9.png](pict_jobsheet2/step9.png)

### Latihan 2.4
Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

### Jawaban Latihan 2.4
![latihan2.4.png](pict_jobsheet2/latihan2.4.png)

## 2.10 Percobaan 10: Substitusi dengan sed (Aman di File Latihan)
![step10.png](pict_jobsheet2/step10.png)

## 2.11 Percobaan 11: Ekstraksi Kolom dengan awk
![step11.png](pict_jobsheet2/step11.png)

## 2.12 Percobaan 12: Melihat Proses dengan ps
![step12.png](pict_jobsheet2/step12.png)

## 2.13 Percobaan 13: Monitoring Real-time dengan top
![step13.png](pict_jobsheet2/step13.png)

## 2.14 Percobaan 14: Menghentikan Proses dengan kill
![step14.png](pict_jobsheet2/step14.png)

## 2.15 Percobaan 15: Cek Disk, Load, dan Service
![step15.1.png](pict_jobsheet2/step15.1.png)

## 2.16 Percobaan 16: Monitoring Port dan Koneksi
![step16.png](pict_jobsheet2/step16.png)

### Latihan 2.5
Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu
tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut
secara singkat

### Jawaban Latihan 2.5
Port    : 127.0.0.1:3306
Service : Biasanya digunakan oleh mySql atau maria database server yang berjalan di komputer dan karena muncul kata kunci 'LISTEN' maka hanya bisa diakses lewat localhost

## Latihan 1.9

### Latihan 2A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat,
ID vendor:device, dan kernel driver in use

### Jawaban Latihan 2A
Nama Perangkat        : Non-Volatile memory controller (NVMe SSD)
ID Vendor             : device: 15b7:5035
Kernel Driver in Use  : device: 15b7:5035

### Latihan 2B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan
lsblk -f dan tuliskan tipe filesystem serta UUID-nya

### Jawaban Latihan 2B
Device root filesystem  : /dev/nvme0n1p5
Tipe filesystem         : ext4
UUID                    : a7d53045-c480-4910-9536-7b85ceb4bcfe

### Latihan 2C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO,
WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.

### Jawaban Latihan 2C
![latihan2c.png](pict_jobsheet2/latihan2c.png)

### Latihan 2D
Gunakan sed untuk mengganti semua kata server menjadi node pada file
latihan. Tunjukkan sebelum dan sesudah

### Jawaban Latihan 2D
![latihan2d.png](pict_jobsheet2/latihan2d.png)
bagian atas adalah sebelum mengganti kata server menjadi node. Bagian bawah setelah diganti dengan node.

### Latihan 2E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk
di atas 70%.

### Jawaban Latihan 2E
![latihan2e.png](pict_jobsheet2/latihan2e.png)
output tersebut menunjukan bahwa tidak ada filesystem yang penggunaan disk nya di atas 70%

### Latihan 2F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan
SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.

### Jawaban Latihan 2F
![latihan2f.png](pict_jobsheet2/latihan2f.png)
PID proses sleep dapat ditemukan menggunakan perintah ps, misalnya PID 113855. Proses dapat dihentikan menggunakan perintah kill yang secara default mengirim sinyal SIGTERM sehingga proses berhenti secara normal. Jika proses tidak merespons, dapat digunakan SIGKILL untuk memaksa proses berhenti secara langsung tanpa proses cleanup.
### Jawaban Latihan 2G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service
aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.

### Jawaban Latihan 2G
![latihan2g.1.png](pict_jobsheet2/latihan2g.1.png)
![latihan2g.2.png](pict_jobsheet2/latihan2g.2.png)