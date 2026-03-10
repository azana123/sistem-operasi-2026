# Laporan Praktikum Sistem Operasi Jobsheet 4

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

## Tugas Pendahuluan

    Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.

    pwd = Menampilkan lokasi direktori kerja saat ini, misalnya /home/Rappizr7/Documents
    cd = Berpindah dari satu direktori ke direktori lain
    mkdir = Membuat direktori baru. Bisa buat banyak direktori sekaligus atau bertingkat
    rmdir = Menghapus direktori kosong, kalau ada isi biasanya si terjadi error

    Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)

    cp = fungsinya itu mencopy file. contoh untuk copy file cp backup backup1, sedangkan copy folder itu contohnya cp -r folder1 folder2
    mv = fungsinya bisa memindahkan file/rename. contoh untuk pindahkan file itu mv contoh1 A/B, dan kalau rename itu mv contoh1 contoh2
    rm = fungsinya untuk menghapus file. contoh rm contoh1

    Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).

    Hard link (direct): nama file kedua menunjuk ke data/inode yang sama → link count naik, perubahan di satu nama ikut di nama lain, tidak bisa beda partisi/filesystem, dan tidak bisa link ke file yang belum ada.

    Soft link (indirect): file bertipe l yang menunjuk ke path/asal file → link count file asal tidak berubah, bisa beda partisi/filesystem, dan bisa dibuat walau target belum ada (tapi bisa jadi broken kalau target hilang).

    Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

    file = Menentukan jenis/tipe suatu file berdasarkan isinya. contohnya file doc1
    find = Mencari file di pohon direktori (real-time scan). contohnya find /home -name "*.txt" -print
    which = Menunjukkan lokasi exec dari sebuah command berdasarkan env PATH. contohnya which ls
    locate = Mencari file dengan cepat memakai index database, lebih cepat dari find tapi tergantug update database. contohnya locate "*.txt"
    grep = mencari teks di dalam file. contohnya grep hallo *.txt

## Percobaan 1: directory
### 1. Melihat directory home
```
pwd
```
Hasil: 
```
/home/fafiq
```


### 2. Melihat directory actual dan parent directory
Prompt:
```
pwd
```
Hasil: 
```
/home/fafiq
```
Prompt:
```
cd .
pwd
```
Hasil:
```
/home/fafiq
```
Prompt:
```
cd ..
pwd
```
Hasil:
```
/home
```
Prompt:
```
cd
```
Hasil: Kembali ke ~/ directory


### 3. Membuat satu directory, lebih dari satu directory atau sub-directory
Prompt:
```
pwd
```
Hasil: 
```
/home/fafiq
```
Prompt:
```
mkdir A B C A/D A/E B/F A/D/A
```
Hasil: membuat directory

Prompt:
```
ls -l
```
Hasil:
```
drwxrwxr-x  4 fafiq fafiq      4096 Mar 10 19:37 A
drwxrwxr-x  3 fafiq fafiq      4096 Mar 10 19:37 B
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 19:37 C
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```
Prompt:
```
ls -l A
```
Hasil:
```
total 8
drwxrwxr-x 3 fafiq fafiq 4096 Mar 10 19:37 D
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 E
```
Prompt:
```
ls -l A/D
```
Hasil:
```
total 4
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 A
```

### 4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya

Prompt:
```
rmdir B
````
Hasil: Terdapat pesan error "rmdir: failed to remove 'B': Directory not empty" karena perintah rmdir hanya bisa dilakukan pada directory kosong. karena B berisi F, maka B tidak kosong sehingga tidak bisa dihapus menggunakan rmdir.
```
rmdir: failed to remove 'B': Directory not empty
```
Prompt:
```
ls -l B
```
hasil
```
total 4
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 F
```

Prompt:
```
rmdir B/F B
```
Hasil: Menghapu directory B beserta isinya (F).

Prompt:
```
ls -l B
```
Hasil: muncul pesan error "ls: cannot access 'B': No such file or directory" karena directory B sudah dihapus, maka ketika mencoba melakukan list akan muncul pesan error seperti itu.
```
cannot access 'B': No such file or directory
```

### 5. Navigasi direktori dengan instruksi cd untuk pindah dari satu direktori ke direktori lain.
Prompt:
```
pwd
```
Hasil:
```
/home/fafiq
```
Prompt:
```
ls -l
```
Hasil:
```
total 123796
drwxrwxr-x  4 fafiq fafiq      4096 Mar 10 19:37 A
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 19:37 C
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```
Prompt:
```
cd A
```
Hasil: (Masuk ke directory A)
```
~/A$
```
Prompt:
```
pwd
```
Hasil:
```
/home/fafiq/A
```
Prompt:
```
cd ..
```
Hasil: (Keluar dari directory A)
```
~$
```
Prompt
```
pwd
```
Hasil:
```
/home/fafiq
```
Prompt: (User = fafiq)
```
cd /home/fafiq/C
```
Hasil: (Masuk directory C)
```
~/C
```
Prompt:
```
pwd
```
Hasil:
```
/home/fafiq/C
```
Prompt:
```
cd /fafiq/C

```
Hasil: Muncul pesan error karena linux membaca path dari root /. sehingga yang dibaca adalah root->fafiq->C. Sedangkan yang benar adalah root->home->fafiq->C.
```
bash: cd: /fafiq/C: No such file or directory
```
Prompt:
```
pwd
```
Hasil:
```
/home/fafiq/C
```

## Percobaan 2: Manipulasi file
### 1. Perintah cp untuk mengkopi file atau seluruh direktori
prompt: 
```
cat > contoh
```
Hasil: (Membuat file dengan nama contoh dan mengisi langsung di terminal)
```
contoh
```
Prompt:
```
cp contoh contoh1
```
Hasil: (Menggandakan file contoh dengan nama contoh1)
```
contoh1
```
Prompt:
```
ls -l
```
Hasil:
```
total 123804
drwxrwxr-x  4 fafiq fafiq      4096 Mar 10 19:37 A
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 19:37 C
-rw-rw-r--  1 fafiq fafiq         2 Mar 10 20:13 contoh
-rw-rw-r--  1 fafiq fafiq         2 Mar 10 20:14 contoh1
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```
Prompt:
```
cp contoh A
```
Hasil: (Karena sudah ada directory A, maka file contoh digandakan ke dalam directory A)
```
A->contoh
```
Prompt:
```
ls -l A
```
Hasil:
```
total 12
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:18 contoh
drwxrwxr-x 3 fafiq fafiq 4096 Mar 10 19:37 D
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 E
```
Prompt:
```
cp contoh contoh1 A/D
```
Hasil: (Melakukan copy terhadap file contoh dan contoh1 kedalam directory A/D)
```
```
Prompt:
```
ls -l A/D
```
Hasil:
```
total 12
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 A
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:21 contoh
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:21 contoh1
```

### 2 Perintah untuk memindahkan file
Prompt:
```
mv contoh contoh2
```
Hasil: (Mengubah nama file contoh menjadi contoh 2)
```
contoh -> contoh2
```
Prompt:
```
ls -l
```
Hasil:
```
total 123804
drwxrwxr-x  4 fafiq fafiq      4096 Mar 10 20:18 A
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 19:37 C
-rw-rw-r--  1 fafiq fafiq         2 Mar 10 20:14 contoh1
-rw-rw-r--  1 fafiq fafiq         2 Mar 10 20:13 contoh2
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```
Prompt:
```
mv contoh1 contoh2 A/D
```
Hasil: (Memindah contoh1 dan contoh2 ke dalam A/D)
```
A/D -> contoh1, contoh2
```
Prompt:
```
ls -l A/D
```
Hasil:
```
total 16
drwxrwxr-x 2 fafiq fafiq 4096 Mar 10 19:37 A
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:21 contoh
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:14 contoh1
-rw-rw-r-- 1 fafiq fafiq    2 Mar 10 20:13 contoh2
```
Prompt:
```
mv contoh contoh1 C
```
Hasil: (Memindahkan file contoh dan contoh1 ke directory C)
```
C -> contoh, contoh1
```
Prompt: (sebenarnya ini error karena file contoh dan contoh1 sudah tidak berada di root)
```
mv contoh contoh1 C
```
Prompt (Yang benar jika ingin memindahkan contoh dan contoh1 ke C)
```
mv A/D/contoh A/D/contoh1 C
```
Hasil: (Memindahkan file contoh dan contoh1 dari A/D ke C)
```
C -> contoh, contoh1
```
Prompt:
```
ls -l C
```
Hasil:
```
total 8
-rw-rw-r-- 1 fafiq fafiq 2 Mar 10 20:21 contoh
-rw-rw-r-- 1 fafiq fafiq 2 Mar 10 20:14 contoh1
```

### 3. Perintah rm untuk menghapus file
Prompt: (Sebenarnya ini salah karena contoh2 sudah tidak ada di root lagi)
```
rm contoh2
```
Prompt: (Yang benar)
```
rm A/D/contoh2
```
Hasil:
```
menghapus file contoh2 pada directory A/D
```
Prompt:
```
ls -l
```
Hasil:
```
total 123796
drwxrwxr-x  4 fafiq fafiq      4096 Mar 10 20:18 A
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 20:32 C
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```
Prompt: (Sebenarnya ini salah karena file contoh sudah tidak ada di root)
```
rm -i contoh
```
Prompt: (Yang benar)
```
rm -i A/contoh
```
Hasil: 
```
rm: remove regular file 'A/contoh'? yes
```
Prompt:
```
rm -rf A C
```
Hasil:
```
Menghapus directory A dan C beserta isinya
```
Prompt:
```
ls -l
```
Hasil:
```
total 123788
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
```


