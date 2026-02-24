# Laporan Praktikum Sistem Operasi Jobsheet 2

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

## Latihan 1.1
Jelaskan 5 fungsi utama sistem operasi dengan contoh konkret dari minimal 2 OS berbeda (Windows, macOS, atau Linux).

## Jawaban Latihan 1.1
A. Manajemen Proses
Sistem operasi mengatur jalannya program yang sedang berjalan, termasuk multitasking, prioritas proses, dan penjadwalan CPU

B. Manajemen Memory
OS mengatur penggunaan RAM agar setiap program mendapat ruang memori yang cukup dan tidak saling mengganggu

C. Manajemen Sistem Berkas
OS mengatur penyimpanan, pengorganisasian, dan akses file di perangkat

D. Manajemen Perangkat Keras
OS bertugas menjadi perantara antara software dan hardware seperti printer, keyboard, GPU, dan disk

E. Antarmuka Pengguna
OS menyediakan cara pengguna berinteraksi dengan komputer, baik GUI maupun CLI

## Latihan 1.2
Kapan sebaiknya menggunakan Windows vs Linux vs macOS? Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.

## Jawaban Latihan 1.2
Ketika tujuan utama menggunakan komputer adalah untuk bisnis dan gaming, maka windows adalah os yang tepat untuk tipe pengguna     tersebut, karena untuk bisnis, windows menawarka user friendly dan berbagai macam aplikasi yang menunjang bisnis mereka. sedangkan untuk gaming, memang banyak game yang kompatibel dijalankan pada os windows, sehingga membuat windows menjadi os yang cocok untuk bermain game.

Jika tujuan utama menggunakan komputer untuk software development, maka macOS atau linux adalah os yang cocok. Linux adalah opsi yang sangat populer untuk software fevelopment karena memiliki environment yang mirip dengan server production, package management yang kuat.
macOS sangat cocok untuk software development karena macOS berbasis unix yang mirip dengan linux dan memiliki tool dev yang lengkap, dan satu satunya OS untuk iOS dev sehingga macOS menjadi favorit ketika digunakan untuk software development

Jika tujuan utama dari komputer adalah sebagai server industry, maka linux adalah os yang paling cocok karena stabil, hemat resource, opensource dan digunakan oleh mayoritas cloud.
## Latihan 1.3
Install Ubuntu Server 22.04 LTS di VirtualBox dengan langkah berikut:
1. Download Ubuntu Server ISO dari website resmi
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
3. Install dengan automatic partitioning (guided)
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
6. Dokumentasikan proses instalasi dengan screenshot key steps
![neofetch.png](pict_jobsheet2/neofetch.png)
## Jawaban Latihan 1.3
![UbuntuLogin.png](pict_jobsheet2/UbuntuLogin.png)
Disini saya menggunakan metode dual boot ubuntu.

## Latihan 1.4
Setelah instalasi Ubuntu Server, lakukan tasks berikut:
A. Update package list: sudo apt update
B. Upgrade packages: sudo apt upgrade
C. Install neofetch: sudo apt install neofetch
D. Jalankan neofetch dan screenshot hasilnya
E. Check disk usage dengan df -h
F. Check memory dengan free -h
G. Dokumentasikan output dari setiap command

## Jawaban Latihan 1.4
A. ![1.4.1.png](pict_jobsheet2/1.4.1.png)
B. ![1.4.2.png](pict_jobsheet2/1.4.2.png)
C. ![1.4.3.png](pict_jobsheet2/1.4.3.png)
D. ![1.4.4.png](pict_jobsheet2/1.4.4.png)
E. ![1.4.5.png](pict_jobsheet2/1.4.5.png)
F. ![1.4.5.png](pict_jobsheet2/1.4.5.png)

## Latihan 1.5
Eksplorasi sistem yang baru diinstall:
A. Tampilkan informasi OS: cat /etc/os-release
B. Tampilkan versi kernel: uname -r
C. Check network connectivity: ping -c 4 google.com
D. Install dan jalankan htop untuk melihat resource usage
E. Buat laporan singkat tentang konfigurasi sistem Anda

## Jawaban Latihan 1.5
A. ![1.5.1.png](pict_jobsheet2/1.5.1.png)
B. ![1.5.2.png](pict_jobsheet2/1.5.2.png)
C. ![1.5.3.png](pict_jobsheet2/1.5.3.png)
D. ![1.5.4.png](pict_jobsheet2/1.5.4.png)
E. ![1.5.5.png](pict_jobsheet2/1.5.5.png)

Sistem saya menggunakan Ubuntu 24.04.4 LTS x86_64 dengan kernel 6.17.0-14-generic. Sistem ini menggunakan processor AMD Ryzen AI 7 350 dengan integrated GPU Radeon 860M. Sistem ini meiliki total memori 16gb yang terpotong menjadi 15gb karena terbagi untuk vram gpu.Sistem environment desktop ini menggunakan gnome 46.0 Theme Orchis-Dark-Compact [GTK2/3]. Karena sistem ini dual boot, saya melakukan partisi untuk windows 450gb dan ubuntu 50gb.

## Latihan 1.6
Ceritakan pengalaman Anda dengan sistem operasi:
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS, Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi?
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan pengalaman Anda.
6. Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin Anda coba? Mengapa?
Tulis refleksi Anda dalam 300-500 kata disertai dengan dokumentasi.
## Jawaban Latihan 1.6
Untuk saat ini, saya menggunakan Linux sebagai daily driver karena saya pada awalnya tertarik mencoba untuk menggunakan sistem operasi lain selain windows. Saya mulai menggunakan Linux (ubuntu) sekitar bulan desember hingga sekarang. Saya suka bagaimana Linux (ubuntu) memberikan pengalaman baru. mulai dari proses instalasi sampai menggunakannya sebagai daily driver. Selain itu, saya dapat melakukan customisasi terhadap tampilannya menjadi seperti yang saya inginkan. Tantangan yang saya hadapi ketika menggunakan linux banyak terjadi ketika baru meng-install. Mulai dari pembagian partisi, hingga benar benar ter-install. Kemudian saya harus beradaptasi untuk menggunakan command prompt. Menurut saya command prompt terlihat sangat menakutkan untuk pemula. Saya juga menemukan banyak error ketika instalasi tema. Saya harus banyak membaca dari reddit dan forum forum untuk menemukan jawabannya. 
Sebelum saya menggunakan Linux, saya menggunakan windows 11. menurut saya, windows 11 dan linux memiliki keunggulan yang berbeda. Windows unggul pada kompabilitasnya dengan banyak sekali game, sedangkan linux sangat cocok untuk software development. Hal yang membuat saya beralih menggunakan linux adalah karena windows 11 memakan banyak sumberdaya. Ketika kondisi idle, windows dapat memakan 60% dari penggunaan ram dari sistem dengan kapasitas ram 16gb. Sementara pada linux, idle hanya memakan sekitar 8 hingga 10% ram. 
Setelah mempelajari bab ini, saya ingin mencoba menggunakan distro lain, seperti fedora atau arch linux. 
E. ![dokumentasi.png](pict_jobsheet2/dokumentasi.png)
