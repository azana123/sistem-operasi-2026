# Laporan Praktikum Sistem Operasi Jobsheet 4

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

## Tugas Pendahuluan

### 1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.

pwd = Menampilkan lokasi direktori kerja saat ini, misalnya /home/Rappizr7/Documents
cd = Berpindah dari satu direktori ke direktori lain
mkdir = Membuat direktori baru. Bisa buat banyak direktori sekaligus atau bertingkat
rmdir = Menghapus direktori kosong, kalau ada isi biasanya si terjadi error

### 2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)

cp = fungsinya itu mencopy file. contoh untuk copy file cp backup backup1, sedangkan copy folder itu contohnya cp -r folder1 folder2
mv = fungsinya bisa memindahkan file/rename. contoh untuk pindahkan file itu mv contoh1 A/B, dan kalau rename itu mv contoh1 contoh2
rm = fungsinya untuk menghapus file. contoh rm contoh1

### 3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).

Hard link (direct): nama file kedua menunjuk ke data/inode yang sama → link count naik, perubahan di satu nama ikut di nama lain, tidak bisa beda partisi/filesystem, dan tidak bisa link ke file yang belum ada.

Soft link (indirect): file bertipe l yang menunjuk ke path/asal file → link count file asal tidak berubah, bisa beda partisi/filesystem, dan bisa dibuat walau target belum ada (tapi bisa jadi broken kalau target hilang).

### 4. uliskan maksud perintah-perintah : file, find, which, locate dan grep.

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
## Percobaan 3: Symbolic Link
### 1. Membuat Shortcut (File link)

Prompt:
```
echo "Halo apakabar" > halo.txt
```
```
ls -l
```
Hasil:
```
total 123792
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
-rw-rw-r--  1 fafiq fafiq        15 Mar 10 20:52 halo.txt
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
ln halo.txt z
```
```
ls -l
```
Hasil:
```
total 123796
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
-rw-rw-r--  2 fafiq fafiq        15 Mar 10 20:52 halo.txt
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
-rw-rw-r--  2 fafiq fafiq        15 Mar 10 20:52 z
```
Prompt:
```
cat z
```
Hasil:
```
Halo apa kabar
```
Prompt:
```
mkdir mydir
```
```
ln z mydir/halo.juga
```
```
cat mydir/halo.juga
```
Hasil:
```
halo apa kabar
```
Prompt
```
ln -s z bye.txt
```
```
ls -l bye.txt
```
Hasil:
```
lrwxrwxrwx 1 fafiq fafiq 1 Mar 10 20:57 bye.txt -> z
```
Prompt:
```
cat bye.txt
```
Hasil:
```
Halo apa kabar
```

## Percobaan 4: Melihat isi file
Prompt:
```
ls -l
```
Hasil;
```
total 123800
lrwxrwxrwx  1 fafiq fafiq         1 Mar 10 20:57 bye.txt -> z
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Desktop
drwxr-xr-x  8 fafiq fafiq      4096 Mar  4 06:54 Documents
drwxr-xr-x  3 fafiq fafiq      4096 Mar  9 22:03 Downloads
-rw-rw-r--  1 fafiq fafiq   5462976 Mar  7 10:42 fastfetch-linux-amd64.deb
drwxrwxr-x  5 fafiq fafiq      4096 Mar  4 10:59 gnome-terminal
-rw-rw-r--  1 fafiq fafiq 121241076 Mar  4 02:12 google-chrome-stable_current_amd64.deb
-rw-rw-r--  3 fafiq fafiq        15 Mar 10 20:52 halo.txt
drwxrwxr-x 10 fafiq fafiq      4096 Mar  4 23:21 i3lock-color
drwxrwxr-x  4 fafiq fafiq      4096 Mar  9 05:21 lwalpapers
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Music
drwxrwxr-x  2 fafiq fafiq      4096 Mar 10 20:55 mydir
drwxr-xr-x  2 fafiq fafiq      4096 Mar  9 06:15 Pictures
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Public
drwx------  8 fafiq fafiq      4096 Mar  5 20:56 snap
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Templates
drwxr-xr-x  2 fafiq fafiq      4096 Mar  4 01:21 Videos
drwxr-xr-x 15 fafiq fafiq      4096 Mar  5 19:22 Visual_Paradigm_CE_18.0
-rw-rw-r--  3 fafiq fafiq        15 Mar 10 20:52 z
```
```
file halo.txt
```
Hasil:
```
halo.txt: ASCII text
```
Prompt:
```
file bye.txt
```
Hasil:
```
bye.txt: symbolic link to z
```
## Perobaan 5: Mencari file
### 1. Perintah Find
Prompt:
```
find /home -name "*.txt" -print > myerror.txt
```
```
cat myerror.txt
```
Hasil
```
/home/fafiq/.local/share/fonts/OFL.txt
/home/fafiq/snap/discord/272/.pki/nssdb/pkcs11.txt
/home/fafiq/snap/discord/272/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
/home/fafiq/snap/discord/272/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
/home/fafiq/snap/discord/273/.pki/nssdb/pkcs11.txt
/home/fafiq/snap/discord/273/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
/home/fafiq/snap/discord/273/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/pkcs11.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/datareporting/glean/client_id.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145064904.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772596832185.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009713810.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642185270.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643896261.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772619606040.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772622940817.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772686612977.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607443718.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607845964.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764457799.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824531808.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773123125758.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772610367206.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620217080.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772623075480.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772618232526.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826340802.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606984282.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773061814491.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772645023761.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773001713106.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607457193.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772628946382.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773037404169.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772825076557.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772604309335.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034586444.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823077012.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643209284.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145000142.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764470606.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644848823.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644900773.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637691289.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637647779.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606773943.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034576771.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773029134851.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826063846.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772609758920.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824153310.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642088878.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712139612.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772613326761.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712236164.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772700051772.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772721992660.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772813323699.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772612176230.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597119916.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823302120.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772804158881.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772601431922.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772611573586.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772641904122.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824935638.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597110067.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009442788.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772977377821.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773002314770.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772581935148.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642396806.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824923766.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607775347.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620183772.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772812682324.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/enumerate_devices.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/serviceworker.txt
/home/fafiq/.pki/nssdb/pkcs11.txt
/home/fafiq/bye.txt
/home/fafiq/myerror.txt
/home/fafiq/halo.txt
/home/fafiq/Visual_Paradigm_CE_18.0/jre/conf/security/policy/README.txt
/home/fafiq/Visual_Paradigm_CE_18.0/jre/lib/server/Xusage.txt
/home/fafiq/Visual_Paradigm_CE_18.0/resources/community.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpmime_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/poi_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axiom_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/crazybeans_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpclient_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/wsdl4j_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jcommon_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlgraphics-commons_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpcore_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlschema_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/foxtrot_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/neethi_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/msv_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jfreechart_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/aspose_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xalan_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axis2_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/batik_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-logging_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javassist_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/avalon-framework_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlbeans_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/gson_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javamail_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/activation_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/sqlite-jdbc_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/velocity_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/trident_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/fop_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/bcel_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/flamingo_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jython_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-io_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-lang.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jackcess-2.1.3.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/truezip_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-httpclient_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-codec_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jxl_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/ant_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/winlaf_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/.install4j/i4j_extf_5_aprh35.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/jre/21.0.10-linux-x86_64/conf/security/policy/README.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/changeSignature.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/dashboard.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/LICENSE.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/node_modules/marked/man/marked.1.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/temp/flag.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/formulahendry.auto-close-tag-0.5.15/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/welcome/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/overview/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/ext-guide/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/formatter-settings/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/beginner-tips/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/project-settings/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/install-jdk/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/dist/extension.bundle.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/dist/extension.bundle.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/tomoki1207.pdf-1.2.2/LICENSE.txt
/home/fafiq/.vscode/extensions/usernamehw.errorlens-3.28.0/LICENSE.txt
/home/fafiq/.vscode/extensions/esbenp.prettier-vscode-12.3.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/oderwat.indent-rainbow-8.3.1/node_modules/signal-exit/LICENSE.txt
/home/fafiq/.vscode/extensions/oderwat.indent-rainbow-8.3.1/LICENSE.txt
/home/fafiq/.vscode/extensions/pkief.material-icon-theme-5.32.0/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/write/node_modules/mkdirp/bin/usage.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/path-is-inside/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/esquery/license.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/signal-exit/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/no-config-found.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/whitespace-found.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/plugin-missing.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/extend-config-missing.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/node_modules/mkdirp/bin/usage.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/circular-json/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/vsls/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/bcryptjs/tests/quickbrown.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/LICENSE.txt
/home/fafiq/.cache/flameshot/flameshot/region.txt
/home/fafiq/.cache/fastfetch/packages/dpkg.txt
/home/fafiq/.cache/tracker3/files/last-crawl.txt
/home/fafiq/.cache/tracker3/files/first-index.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/vocab_en-us.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/enus_denylist_encoded_241007.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/15/E6DC4029A1E4B4C1/CFC76F0125B01B03/VERSION.txt
/home/fafiq/.config/Code/User/globalStorage/vscode-redhat-telemetry/cache/identify.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/indexNamesMap.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
/home/fafiq/.config/Code/WebStorage/1/CacheStorage/index.txt
/home/fafiq/.config/Code/WebStorage/2/CacheStorage/index.txt
/home/fafiq/.config/Code/WebStorage/3/CacheStorage/index.txt
```
Prompt:
```
find . -name "*.txt" -exec wc -l {} \;
```
Hasil:
```
93 ./.local/share/fonts/OFL.txt
5 ./snap/discord/272/.pki/nssdb/pkcs11.txt
4 ./snap/discord/272/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
4 ./snap/discord/272/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
5 ./snap/discord/273/.pki/nssdb/pkcs11.txt
4 ./snap/discord/273/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
4 ./snap/discord/273/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
5 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/pkcs11.txt
0 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/datareporting/glean/client_id.txt
40 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145064904.txt
117 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772596832185.txt
310 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009713810.txt
22 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642185270.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643896261.txt
114 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772619606040.txt
261 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772622940817.txt
108 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772686612977.txt
359 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607443718.txt
136 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607845964.txt
287 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764457799.txt
335 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824531808.txt
106 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773123125758.txt
303 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772610367206.txt
19 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620217080.txt
38 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772623075480.txt
222 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772618232526.txt
301 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826340802.txt
359 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606984282.txt
239 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773061814491.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772645023761.txt
33 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773001713106.txt
287 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607457193.txt
395 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772628946382.txt
166 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773037404169.txt
503 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772825076557.txt
78 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772604309335.txt
38 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034586444.txt
143 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823077012.txt
25 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643209284.txt
40 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145000142.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764470606.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644848823.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644900773.txt
21 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637691289.txt
27 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637647779.txt
582 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606773943.txt
46 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034576771.txt
194 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773029134851.txt
86 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826063846.txt
242 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772609758920.txt
227 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824153310.txt
26 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642088878.txt
417 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712139612.txt
104 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772613326761.txt
76 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712236164.txt
65 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772700051772.txt
27 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772721992660.txt
161 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772813323699.txt
323 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772612176230.txt
133 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597119916.txt
176 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823302120.txt
364 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772804158881.txt
246 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772601431922.txt
305 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772611573586.txt
60 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772641904122.txt
101 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824935638.txt
46 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597110067.txt
234 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009442788.txt
131 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772977377821.txt
151 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773002314770.txt
800 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772581935148.txt
26 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642396806.txt
337 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824923766.txt
242 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607775347.txt
137 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620183772.txt
17 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772812682324.txt
3 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/enumerate_devices.txt
137 ./snap/firefox/common/.mozilla/firefox/obe6z55d.default/serviceworker.txt
5 ./.pki/nssdb/pkcs11.txt
1 ./bye.txt
193 ./myerror.txt
1 ./halo.txt
54 ./Visual_Paradigm_CE_18.0/jre/conf/security/policy/README.txt
22 ./Visual_Paradigm_CE_18.0/jre/lib/server/Xusage.txt
0 ./Visual_Paradigm_CE_18.0/resources/community.txt
182 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpmime_license.txt
463 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/poi_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axiom_license.txt
25 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/crazybeans_license.txt
182 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpclient_license.txt
87 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/wsdl4j_license.txt
56 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jcommon_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlgraphics-commons_license.txt
175 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpcore_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlschema_license.txt
26 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/foxtrot_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/neethi_license.txt
29 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/msv_license.txt
56 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jfreechart_license.txt
42 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/aspose_license.txt
54 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xalan_license.txt
203 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axis2_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/batik_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-logging_license.txt
140 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javassist_license.txt
175 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/avalon-framework_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlbeans_license.txt
13 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/gson_license.txt
119 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javamail_license.txt
119 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/activation_license.txt
201 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/sqlite-jdbc_license.txt
201 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/velocity_license.txt
23 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/trident_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/fop_license.txt
53 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/bcel_license.txt
11 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/flamingo_license.txt
191 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jython_license.txt
203 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-io_license.txt
201 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-lang.txt
201 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jackcess-2.1.3.txt
70 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/truezip_license.txt
175 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-httpclient_license.txt
202 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-codec_license.txt
57 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jxl_license.txt
203 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/ant_license.txt
32 ./Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/winlaf_license.txt
66 ./Visual_Paradigm_CE_18.0/.install4j/i4j_extf_5_aprh35.txt
54 ./.vscode/extensions/redhat.java-1.53.0-linux-x64/jre/21.0.10-linux-x86_64/conf/security/policy/README.txt
41 ./.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/changeSignature.js.LICENSE.txt
61 ./.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/extension.js.LICENSE.txt
41 ./.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/dashboard.js.LICENSE.txt
276 ./.vscode/extensions/redhat.java-1.53.0-linux-x64/LICENSE.txt
86 ./.vscode/extensions/zhuangtongfa.material-theme-3.19.0/node_modules/marked/man/marked.1.txt
0 ./.vscode/extensions/zhuangtongfa.material-theme-3.19.0/temp/flag.txt
20 ./.vscode/extensions/zhuangtongfa.material-theme-3.19.0/LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-maven-0.45.1/dist/extension.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-maven-0.45.1/LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-maven-0.45.1/ThirdPartyNotices.txt
21 ./.vscode/extensions/formulahendry.auto-close-tag-0.5.15/LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/extension.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/welcome/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/overview/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/ext-guide/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/formatter-settings/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/beginner-tips/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/project-settings/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/install-jdk/index.js.LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/LICENSE.txt
0 ./.vscode/extensions/vscjava.vscode-java-pack-0.30.5/ThirdPartyNotices.txt
33 ./.vscode/extensions/vscjava.vscode-java-test-0.44.0/dist/extension.bundle.js.LICENSE.txt
17 ./.vscode/extensions/vscjava.vscode-java-test-0.44.0/LICENSE.txt
1416 ./.vscode/extensions/vscjava.vscode-java-test-0.44.0/ThirdPartyNotices.txt
72 ./.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/dist/extension.bundle.js.LICENSE.txt
21 ./.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/LICENSE.txt
586 ./.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/ThirdPartyNotices.txt
22 ./.vscode/extensions/tomoki1207.pdf-1.2.2/LICENSE.txt
20 ./.vscode/extensions/usernamehw.errorlens-3.28.0/LICENSE.txt
21 ./.vscode/extensions/esbenp.prettier-vscode-12.3.0/LICENSE.txt
17 ./.vscode/extensions/vscjava.vscode-java-debug-0.58.5/dist/extension.js.LICENSE.txt
17 ./.vscode/extensions/vscjava.vscode-java-debug-0.58.5/LICENSE.txt
173 ./.vscode/extensions/vscjava.vscode-java-debug-0.58.5/ThirdPartyNotices.txt
16 ./.vscode/extensions/oderwat.indent-rainbow-8.3.1/node_modules/signal-exit/LICENSE.txt
21 ./.vscode/extensions/oderwat.indent-rainbow-8.3.1/LICENSE.txt
8 ./.vscode/extensions/pkief.material-icon-theme-5.32.0/LICENSE.txt
12 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/write/node_modules/mkdirp/bin/usage.txt
47 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/path-is-inside/LICENSE.txt
24 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/esquery/license.txt
16 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/signal-exit/LICENSE.txt
7 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/no-config-found.txt
3 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/whitespace-found.txt
9 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/plugin-missing.txt
3 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/extend-config-missing.txt
12 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/node_modules/mkdirp/bin/usage.txt
19 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/circular-json/LICENSE.txt
91 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/vsls/LICENSE.txt
150 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/bcryptjs/tests/quickbrown.txt
21 ./.vscode/extensions/ritwickdey.liveserver-5.7.10/LICENSE.txt
0 ./.cache/flameshot/flameshot/region.txt
0 ./.cache/fastfetch/packages/dpkg.txt
0 ./.cache/tracker3/files/last-crawl.txt
0 ./.cache/tracker3/files/first-index.txt
302 ./.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/vocab_en-us.txt
580 ./.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/enus_denylist_encoded_241007.txt
4 ./.config/google-chrome/optimization_guide_model_store/15/E6DC4029A1E4B4C1/CFC76F0125B01B03/VERSION.txt
0 ./.config/Code/User/globalStorage/vscode-redhat-telemetry/cache/identify.txt
0 ./.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
1 ./.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
1 ./.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/indexNamesMap.txt
0 ./.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
5 ./.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
2 ./.config/Code/WebStorage/1/CacheStorage/index.txt
2 ./.config/Code/WebStorage/2/CacheStorage/index.txt
3 ./.config/Code/WebStorage/3/CacheStorage/index.txt
```
### 2. Perintah which
Prompt:
```
which ls
```
Hasil:
```
/usr/bin/ls
```

### 3. Perintah locate
Prompt:
```
locate "*.txt"
```
Hasil:
```
/etc/X11/rgb.txt
/etc/brltty/Input/ba/all.txt
/etc/brltty/Input/bd/all.txt
/etc/brltty/Input/bl/18.txt
/etc/brltty/Input/bl/40_m20_m40.txt
/etc/brltty/Input/ec/all.txt
/etc/brltty/Input/ec/spanish.txt
/etc/brltty/Input/eu/all.txt
/etc/brltty/Input/lb/all.txt
/etc/brltty/Input/lt/all.txt
/etc/brltty/Input/mb/all.txt
/etc/brltty/Input/mn/all.txt
/etc/brltty/Input/no/all.txt
/etc/brltty/Input/tn/all.txt
/etc/brltty/Input/tt/all.txt
/etc/brltty/Input/vd/all.txt
/etc/brltty/Input/vr/all.txt
/etc/brltty/Input/vs/all.txt
/etc/java-21-openjdk/security/policy/README.txt
/home/fafiq/bye.txt
/home/fafiq/halo.txt
/home/fafiq/myerror.txt
/home/fafiq/.cache/fastfetch/packages/dpkg.txt
/home/fafiq/.cache/flameshot/flameshot/region.txt
/home/fafiq/.cache/tracker3/files/first-index.txt
/home/fafiq/.cache/tracker3/files/last-crawl.txt
/home/fafiq/.config/Code/User/globalStorage/vscode-redhat-telemetry/cache/identify.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/jdt_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/indexNamesMap.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/javaLikeNames.txt
/home/fafiq/.config/Code/User/workspaceStorage/2625f1a98c94fc6b8f91a2ee865255a7/redhat.java/ss_ws/.metadata/.plugins/org.eclipse.jdt.core/savedIndexNames.txt
/home/fafiq/.config/Code/WebStorage/1/CacheStorage/index.txt
/home/fafiq/.config/Code/WebStorage/2/CacheStorage/index.txt
/home/fafiq/.config/Code/WebStorage/3/CacheStorage/index.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/15/E6DC4029A1E4B4C1/CFC76F0125B01B03/VERSION.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/enus_denylist_encoded_241007.txt
/home/fafiq/.config/google-chrome/optimization_guide_model_store/24/E6DC4029A1E4B4C1/95C6D09368EFEBB0/vocab_en-us.txt
/home/fafiq/.local/share/fonts/OFL.txt
/home/fafiq/.pki/nssdb/pkcs11.txt
/home/fafiq/.vscode/extensions/esbenp.prettier-vscode-12.3.0/LICENSE.txt
/home/fafiq/.vscode/extensions/formulahendry.auto-close-tag-0.5.15/LICENSE.txt
/home/fafiq/.vscode/extensions/oderwat.indent-rainbow-8.3.1/LICENSE.txt
/home/fafiq/.vscode/extensions/oderwat.indent-rainbow-8.3.1/node_modules/signal-exit/LICENSE.txt
/home/fafiq/.vscode/extensions/pkief.material-icon-theme-5.32.0/LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/changeSignature.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/dashboard.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/redhat.java-1.53.0-linux-x64/jre/21.0.10-linux-x86_64/conf/security/policy/README.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/bcryptjs/tests/quickbrown.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/circular-json/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/extend-config-missing.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/no-config-found.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/plugin-missing.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/messages/whitespace-found.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/eslint/node_modules/mkdirp/bin/usage.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/esquery/license.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/path-is-inside/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/signal-exit/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/vsls/LICENSE.txt
/home/fafiq/.vscode/extensions/ritwickdey.liveserver-5.7.10/node_modules/write/node_modules/mkdirp/bin/usage.txt
/home/fafiq/.vscode/extensions/tomoki1207.pdf-1.2.2/LICENSE.txt
/home/fafiq/.vscode/extensions/usernamehw.errorlens-3.28.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-debug-0.58.5/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-dependency-0.27.0/dist/extension.bundle.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/beginner-tips/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/ext-guide/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/formatter-settings/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/install-jdk/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/overview/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/project-settings/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-pack-0.30.5/out/assets/welcome/index.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-java-test-0.44.0/dist/extension.bundle.js.LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/LICENSE.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/ThirdPartyNotices.txt
/home/fafiq/.vscode/extensions/vscjava.vscode-maven-0.45.1/dist/extension.js.LICENSE.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/LICENSE.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/node_modules/marked/man/marked.1.txt
/home/fafiq/.vscode/extensions/zhuangtongfa.material-theme-3.19.0/temp/flag.txt
/home/fafiq/Visual_Paradigm_CE_18.0/.install4j/i4j_extf_5_aprh35.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/activation_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/ant_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/aspose_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/avalon-framework_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axiom_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/axis2_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/batik_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/bcel_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-codec_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-httpclient_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-io_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-lang.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/commons-logging_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/crazybeans_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/flamingo_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/fop_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/foxtrot_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/gson_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpclient_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpcore_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/httpmime_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jackcess-2.1.3.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javamail_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/javassist_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jcommon_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jfreechart_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jxl_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/jython_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/msv_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/neethi_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/poi_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/sqlite-jdbc_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/trident_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/truezip_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/velocity_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/winlaf_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/wsdl4j_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xalan_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlbeans_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlgraphics-commons_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/bundled/3rdPartyLicense/xmlschema_license.txt
/home/fafiq/Visual_Paradigm_CE_18.0/jre/conf/security/policy/README.txt
/home/fafiq/Visual_Paradigm_CE_18.0/jre/lib/server/Xusage.txt
/home/fafiq/Visual_Paradigm_CE_18.0/resources/community.txt
/home/fafiq/snap/discord/272/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
/home/fafiq/snap/discord/272/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
/home/fafiq/snap/discord/272/.pki/nssdb/pkcs11.txt
/home/fafiq/snap/discord/273/.config/discord/Service Worker/CacheStorage/63fc7e4cfcc88165b53fe27bdbf48bdde7611b44/index.txt
/home/fafiq/snap/discord/273/.config/discord/Service Worker/CacheStorage/7d571773fef4871f82ca0457379cf2a39317562f/index.txt
/home/fafiq/snap/discord/273/.pki/nssdb/pkcs11.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/enumerate_devices.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/pkcs11.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/serviceworker.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/datareporting/glean/client_id.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772581935148.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772596832185.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597110067.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772597119916.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772601431922.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772604309335.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606773943.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772606984282.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607443718.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607457193.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607775347.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772607845964.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772609758920.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772610367206.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772611573586.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772612176230.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772613326761.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772618232526.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772619606040.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620183772.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772620217080.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772622940817.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772623075480.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772628946382.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637647779.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772637691289.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772641904122.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642088878.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642185270.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772642396806.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643209284.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772643896261.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644848823.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772644900773.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772645023761.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772686612977.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772700051772.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712139612.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772712236164.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772721992660.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764457799.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772764470606.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772804158881.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772812682324.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772813323699.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823077012.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772823302120.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824153310.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824531808.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824923766.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772824935638.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772825076557.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826063846.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772826340802.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1772977377821.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773001713106.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773002314770.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009442788.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773009713810.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773029134851.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034576771.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773034586444.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773037404169.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773061814491.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773123125758.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145000142.txt
/home/fafiq/snap/firefox/common/.mozilla/firefox/obe6z55d.default/weave/logs/error-sync-1773145064904.txt
/snap/code/227/etc/X11/rgb.txt
/snap/code/227/usr/share/X11/rgb.txt
/snap/code/227/usr/share/code/resources/app/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/extensions/git/dist/main.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/extensions/github/dist/extension.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/extensions/github-authentication/dist/extension.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/extensions/latex/cpp-bailout-license.txt
/snap/code/227/usr/share/code/resources/app/extensions/latex/markdown-latex-combined-license.txt
/snap/code/227/usr/share/code/resources/app/extensions/ms-vscode.js-debug/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/extensions/ms-vscode.js-debug/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/extensions/ms-vscode.js-debug-companion/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/extensions/ms-vscode.js-debug-companion/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/extensions/ms-vscode.vscode-js-profile-table/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/extensions/terminal-suggest/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/extensions/theme-seti/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/deviceid/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/deviceid/NOTICE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/deviceid/owners.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/iconv-lite-umd/lib/iconv-lite-umd.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/vscode-languagedetection/dist/lib/979.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/@vscode/vscode-languagedetection/dist/lib/index.js.LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/native-keymap/License.txt
/snap/code/227/usr/share/code/resources/app/node_modules/native-keymap/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/node_modules/playwright-core/ThirdPartyNotices.txt
/snap/code/227/usr/share/code/resources/app/node_modules/tas-client/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/tslib/CopyrightNotice.txt
/snap/code/227/usr/share/code/resources/app/node_modules/tslib/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/v8-inspect-profiler/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/vscode-oniguruma/LICENSE.txt
/snap/code/227/usr/share/code/resources/app/node_modules/vscode-oniguruma/NOTICES.txt
/snap/code/228/etc/X11/rgb.txt
/snap/code/228/usr/share/X11/rgb.txt
/snap/code/228/usr/share/code/resources/app/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/extensions/git/dist/main.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/extensions/github/dist/extension.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/extensions/github-authentication/dist/extension.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/extensions/latex/cpp-bailout-license.txt
/snap/code/228/usr/share/code/resources/app/extensions/latex/markdown-latex-combined-license.txt
/snap/code/228/usr/share/code/resources/app/extensions/ms-vscode.js-debug/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/extensions/ms-vscode.js-debug/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/extensions/ms-vscode.js-debug-companion/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/extensions/ms-vscode.js-debug-companion/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/extensions/ms-vscode.vscode-js-profile-table/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/extensions/terminal-suggest/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/extensions/theme-seti/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/deviceid/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/deviceid/NOTICE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/deviceid/owners.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/iconv-lite-umd/lib/iconv-lite-umd.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/vscode-languagedetection/dist/lib/979.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/@vscode/vscode-languagedetection/dist/lib/index.js.LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/native-keymap/License.txt
/snap/code/228/usr/share/code/resources/app/node_modules/native-keymap/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/node_modules/playwright-core/ThirdPartyNotices.txt
/snap/code/228/usr/share/code/resources/app/node_modules/tas-client/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/tslib/CopyrightNotice.txt
/snap/code/228/usr/share/code/resources/app/node_modules/tslib/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/v8-inspect-profiler/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/vscode-oniguruma/LICENSE.txt
/snap/code/228/usr/share/code/resources/app/node_modules/vscode-oniguruma/NOTICES.txt
/snap/core20/2717/usr/lib/python3/dist-packages/Jinja2-2.10.1.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/Jinja2-2.10.1.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/Jinja2-2.10.1.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/Jinja2-2.10.1.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/MarkupSafe-1.1.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/MarkupSafe-1.1.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/PyJWT-1.7.1.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/PyJWT-1.7.1.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/PyJWT-1.7.1.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/PyJWT-1.7.1.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/attrs-19.3.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/attrs-19.3.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/attrs-19.3.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/certifi-2019.11.28.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/certifi-2019.11.28.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/chardet-3.0.4.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/chardet-3.0.4.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/chardet-3.0.4.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cloud_init-24.4.1.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cloud_init-24.4.1.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cloud_init-24.4.1.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cloud_init-24.4.1.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cryptography-2.8.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cryptography-2.8.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/cryptography-2.8.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/idna-2.8.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/idna-2.8.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/importlib_metadata-1.5.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/importlib_metadata-1.5.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/importlib_metadata-1.5.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonpatch-1.22.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonpatch-1.22.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonpatch-1.22.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/more_itertools-4.2.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/more_itertools-4.2.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/more_itertools-4.2.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/netifaces-0.10.4.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/netifaces-0.10.4.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/oauthlib-3.1.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/oauthlib-3.1.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/oauthlib-3.1.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyrsistent-0.15.5.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyrsistent-0.15.5.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyrsistent-0.15.5.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyserial-3.4.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyserial-3.4.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyudev-0.21.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyudev-0.21.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/pyudev-0.21.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests-2.22.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests-2.22.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests-2.22.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/setuptools-45.2.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/setuptools-45.2.0.egg-info/entry_points.txt
/snap/core20/2717/usr/lib/python3/dist-packages/setuptools-45.2.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/six-1.14.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/six-1.14.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/urllib3-1.25.8.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/urllib3-1.25.8.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/urllib3-1.25.8.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/urwid-2.0.1.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/urwid-2.0.1.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/dependency_links.txt
/snap/core20/2717/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/requires.txt
/snap/core20/2717/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/top_level.txt
/snap/core20/2717/usr/lib/python3.8/LICENSE.txt
/snap/core20/2717/usr/lib/python3.8/lib2to3/Grammar.txt
/snap/core20/2717/usr/lib/python3.8/lib2to3/PatternGrammar.txt
/snap/core20/2717/usr/lib/python3.9/lib2to3/Grammar.txt
/snap/core20/2717/usr/lib/python3.9/lib2to3/PatternGrammar.txt
/snap/core20/2717/usr/share/doc/mount/mount.txt
/snap/core20/2717/usr/share/subiquity/subiquity-0.0.5.egg-info/dependency_links.txt
/snap/core20/2717/usr/share/subiquity/subiquity-0.0.5.egg-info/entry_points.txt
/snap/core20/2717/usr/share/subiquity/subiquity-0.0.5.egg-info/top_level.txt
/snap/core20/2717/usr/share/vim/vim81/doc/help.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Babel-2.8.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Babel-2.8.0.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Babel-2.8.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Babel-2.8.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Jinja2-3.0.3.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Jinja2-3.0.3.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Jinja2-3.0.3.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/Jinja2-3.0.3.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/PyJWT-2.3.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/PyJWT-2.3.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/PyJWT-2.3.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/PyYAML-5.4.1.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/PyYAML-5.4.1.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/attrs-21.2.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/attrs-21.2.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/attrs-21.2.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/certifi-2020.6.20.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/certifi-2020.6.20.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/chardet-4.0.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/chardet-4.0.0.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/chardet-4.0.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cloud_init-24.4.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cloud_init-24.4.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cloud_init-24.4.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cloud_init-24.4.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/configobj-5.0.6.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cryptography-3.4.8.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cryptography-3.4.8.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/cryptography-3.4.8.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/idna-3.3.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/idna-3.3.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/jsonschema-3.2.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/oauthlib-3.2.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/oauthlib-3.2.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/oauthlib-3.2.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/probert-0.0.18.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyrsistent-0.18.1.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyrsistent-0.18.1.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pytz-2022.1.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pytz-2022.1.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyudev-0.22.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyudev-0.22.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/pyudev-0.22.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests-2.25.1.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests-2.25.1.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests-2.25.1.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/requests_unixsocket-0.2.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/entry_points.txt
/snap/core22/1748/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/six-1.16.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/six-1.16.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/urllib3-1.26.5.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/urllib3-1.26.5.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/urllib3-1.26.5.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/urwid-2.1.2.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/urwid-2.1.2.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/dependency_links.txt
/snap/core22/1748/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/requires.txt
/snap/core22/1748/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/top_level.txt
/snap/core22/1748/usr/lib/python3.10/LICENSE.txt
/snap/core22/1748/usr/lib/python3.10/lib2to3/Grammar.txt
/snap/core22/1748/usr/lib/python3.10/lib2to3/PatternGrammar.txt
/snap/core22/1748/usr/lib/python3.11/lib2to3/Grammar.txt
/snap/core22/1748/usr/lib/python3.11/lib2to3/PatternGrammar.txt
/snap/core22/1748/usr/share/subiquity/subiquity-0.0.5.egg-info/dependency_links.txt
/snap/core22/1748/usr/share/subiquity/subiquity-0.0.5.egg-info/entry_points.txt
/snap/core22/1748/usr/share/subiquity/subiquity-0.0.5.egg-info/top_level.txt
/snap/core22/1748/usr/share/vim/vim82/doc/help.txt
/snap/core24/1349/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/entry_points.txt
/snap/core24/1349/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/MarkupSafe-2.1.5.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/MarkupSafe-2.1.5.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/PyJWT-2.7.0.dist-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/PyYAML-6.0.1.dist-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/certifi-2023.11.17.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/certifi-2023.11.17.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/chardet-5.2.0.dist-info/entry_points.txt
/snap/core24/1349/usr/lib/python3/dist-packages/chardet-5.2.0.dist-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/entry_points.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/configobj-5.0.8.dist-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cryptography-41.0.7.dist-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cryptography.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cryptography.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/cryptography.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/jsonschema-4.10.3.dist-info/entry_points.txt
/snap/core24/1349/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyrsistent-0.20.0.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyrsistent-0.20.0.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/entry_points.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/dependency_links.txt
/snap/core24/1349/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/requires.txt
/snap/core24/1349/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/top_level.txt
/snap/core24/1349/usr/lib/python3.12/LICENSE.txt
/snap/core24/1349/usr/share/vim/vim91/doc/help.txt
/snap/core24/1349/usr/share/vim/vim91/doc/sponsor.txt
/snap/core24/1349/usr/share/vim/vim91/doc/uganda.txt
/snap/core24/1349/usr/share/vim/vim91/doc/version9.txt
/snap/discord/272/etc/X11/rgb.txt
/snap/discord/272/usr/share/X11/rgb.txt
/snap/discord/273/etc/X11/rgb.txt
/snap/discord/273/usr/share/X11/rgb.txt
/snap/gnome-42-2204/202/etc/X11/rgb.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/entry_points.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/entry_points.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/pip/_vendor/vendor.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/pip-22.0.2.dist-info/entry_points.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/pip-22.0.2.dist-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/entry_points.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/entry_points.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/requires.txt
/snap/gnome-42-2204/202/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/top_level.txt
/snap/gnome-42-2204/202/usr/lib/python3.10/LICENSE.txt
/snap/gnome-42-2204/202/usr/share/X11/rgb.txt
/snap/gnome-42-2204/202/usr/share/presage/abbreviations_en.txt
/snap/gnome-42-2204/202/usr/share/presage/abbreviations_it.txt
/snap/gnome-42-2204/247/etc/X11/rgb.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/entry_points.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Mako-1.1.3-py3.10.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/entry_points.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/Markdown-3.3.6.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/MarkupSafe-2.0.1.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/PyGObject-3.42.1.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/dbus_python-1.2.18.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/importlib_metadata-4.6.4.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/more_itertools-8.10.0.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/pip/_vendor/vendor.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/pip-22.0.2.dist-info/entry_points.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/pip-22.0.2.dist-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/entry_points.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/setuptools-59.6.0.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/entry_points.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/wheel-0.37.1.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/dependency_links.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/requires.txt
/snap/gnome-42-2204/247/usr/lib/python3/dist-packages/zipp-1.0.0.egg-info/top_level.txt
/snap/gnome-42-2204/247/usr/lib/python3.10/LICENSE.txt
/snap/gnome-42-2204/247/usr/share/X11/rgb.txt
/snap/gnome-42-2204/247/usr/share/presage/abbreviations_en.txt
/snap/gnome-42-2204/247/usr/share/presage/abbreviations_it.txt
/snap/gnome-46-2404/153/etc/X11/rgb.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/dependency_links.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/top_level.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/distlib-0.3.8.egg-info/dependency_links.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/distlib-0.3.8.egg-info/top_level.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/pip/_vendor/vendor.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/pip-24.0.dist-info/entry_points.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/pip-24.0.dist-info/top_level.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/dependency_links.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/entry_points.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/top_level.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/wheel/vendored/vendor.txt
/snap/gnome-46-2404/153/usr/lib/python3/dist-packages/wheel-0.42.0.dist-info/entry_points.txt
/snap/gnome-46-2404/153/usr/lib/python3.12/LICENSE.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-cli.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-gds-shmem.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-palloc.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pattrs.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pcompress.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pctrl.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pevent.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pfexec-base.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pfexec-linux.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-ploc.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-plookup.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmdl.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-info.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-mca-base.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-mca-var.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-plog.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-psensor-file.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-psensor-heartbeat.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-runtime.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-server.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmix-util.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pmixcc.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pps.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-pquery.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-prm.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/help-ptl-base.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/pmix2/share/pmix/pmixcc-wrapper-data.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkChartsCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonColor-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonComputationalGeometry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonDataModel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonExecutionModel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonMath-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonMisc-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonPython-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonSystem-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkCommonTransforms-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkDomainsChemistry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkDomainsChemistryOpenGL2-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkDomainsParallelChemistry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersAMR-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersExtraction-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersFlowPaths-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersGeneral-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersGeneric-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersGeometry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersHybrid-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersHyperTree-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersImaging-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersModeling-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersParallel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersParallelGeometry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersParallelImaging-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersParallelMPI-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersParallelVerdict-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersPoints-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersProgrammable-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersPython-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersSMP-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersSelection-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersSources-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersStatistics-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersTexture-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersTopology-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkFiltersVerdict-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkGeovisCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOAMR-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOAsynchronous-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOCGNSReader-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOCONVERGECFD-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOChemistry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOCityGML-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOEnSight-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOExodus-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOExport-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOExportGL2PS-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOExportPDF-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOGeometry-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOHDF-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOIOSS-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOImage-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOImport-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOInfovis-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOLSDyna-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOLegacy-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOMINC-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOMPIImage-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOMPIParallel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOMotionFX-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOMovie-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIONetCDF-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOOggTheora-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOPLY-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOParallel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOParallelNetCDF-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOParallelXML-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOSQL-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOSegY-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOTecplotTable-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOVeraOut-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOVideo-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOXML-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkIOXMLParser-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingColor-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingFourier-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingGeneral-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingHybrid-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingMath-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingMorphological-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingSources-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingStatistics-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkImagingStencil-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkInfovisCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkInfovisLayout-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkInteractionImage-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkInteractionStyle-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkInteractionWidgets-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkParallelCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkParallelMPI-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkParallelMPI4Py-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkPythonContext2D-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingAnnotation-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingContext2D-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingContextOpenGL2-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingFreeType-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingGL2PSOpenGL2-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingImage-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingLOD-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingLabel-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingOpenGL2-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingSceneGraph-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingUI-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingVolume-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingVolumeOpenGL2-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkRenderingVtkJS-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkTestingRendering-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkViewsContext2D-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkViewsCore-hierarchy.txt
/snap/gnome-46-2404/153/usr/lib/x86_64-linux-gnu/vtk/hierarchy/VTK/vtkViewsInfovis-hierarchy.txt
/snap/gnome-46-2404/153/usr/share/X11/rgb.txt
/snap/gnome-46-2404/153/usr/share/gdal/pci_datum.txt
/snap/gnome-46-2404/153/usr/share/gdal/pci_ellips.txt
/snap/gnome-46-2404/153/usr/share/licenses/opencv4/SoftFloat-COPYING.txt
/snap/gnome-46-2404/153/usr/share/presage/abbreviations_en.txt
/snap/gnome-46-2404/153/usr/share/presage/abbreviations_it.txt
/snap/libreoffice/366/etc/X11/rgb.txt
/snap/libreoffice/366/etc/java-21-openjdk/security/policy/README.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-af.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-am.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ar.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-as.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ast.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-be.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-bg.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-bn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-br.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-bs.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ca-valencia.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ca.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-cs.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-cy.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-da.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-de.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-dz.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-el.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-en-GB.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-en-US.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-en-ZA.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-eo.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-es.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-et.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-eu.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-fa.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-fi.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-fr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ga.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-gd.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-gl.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-gu.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-gug.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-he.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-hi.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-hr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-hu.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-id.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-is.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-it.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ja.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ka.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-kk.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-km.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-kmr-Latn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-kn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ko.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-lt.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-lv.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-mk.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ml.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-mn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-mr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-nb.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ne.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-nl.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-nn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-nr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-nso.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-oc.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-om.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-or.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-pa-IN.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-pl.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-pt-BR.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-pt.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ro.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ru.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-rw.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-si.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-sk.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-sl.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-sr-Latn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-sr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ss.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-st.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-sv.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-szl.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ta.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-te.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-tg.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-th.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-tn.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-tr.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ts.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ug.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-uk.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-uz.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-ve.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-vi.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-xh.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-zh-CN.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-zh-TW.txt
/snap/libreoffice/366/lib/libreoffice/share/extensions/wiki-publisher/description-zu.txt
/snap/libreoffice/366/lib/libreoffice/share/gallery/personas/personas_list.txt
/snap/libreoffice/366/usr/lib/jvm/java-21-openjdk-amd64/conf/security/policy/README.txt
/snap/libreoffice/366/usr/share/X11/rgb.txt
/snap/libreoffice/366/usr/share/doc/libasound2t64/examples/asoundrc.txt
/snap/libreoffice/366/usr/share/doc/libsdl2-2.0-0/BUGS.txt
/snap/libreoffice/366/usr/share/doc/libsdl2-2.0-0/CREDITS.txt
/snap/libreoffice/366/usr/share/doc/libsdl2-2.0-0/README-SDL.txt
/snap/libreoffice/366/usr/share/doc/mythes-it/th_it_IT_copyright_licenza.txt
/snap/libreoffice/366/usr/share/doc/mythes-it/th_it_IT_lettera_in_inglese.txt
/snap/libreoffice/366/usr/share/openal/presets/presets.txt
/usr/lib/jvm/java-21-openjdk-amd64/conf/security/policy/README.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-af.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-am.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ar.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-as.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ast.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-be.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-bg.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-bn-IN.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-bn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-br.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-bs.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ca-valencia.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ca.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-cs.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-cy.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-da.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-de.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-dz.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-el.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-en-GB.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-en-US.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-en-ZA.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-eo.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-es.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-et.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-eu.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-fa.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-fi.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-fr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ga.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-gd.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-gl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-gu.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-gug.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-he.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-hi.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-hr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-hu.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-hy.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-id.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-is.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-it.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ja.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ka.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-kk.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-km.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-kmr-Latn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-kn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ko.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-lt.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-lv.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-mk.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ml.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-mn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-mr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-nb.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ne.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-nl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-nn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-nr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-nso.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-oc.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-om.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-or.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-pa-IN.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-pl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-pt-BR.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-pt.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ro.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ru.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-rw.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-si.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-sk.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-sl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-sr-Latn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-sr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ss.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-st.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-sv.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-szl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ta.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-te.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-tg.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-th.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-tl.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-tn.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-tr.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ts.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ug.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-uk.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-uz.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-ve.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-vi.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-xh.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-zh-CN.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-zh-TW.txt
/usr/lib/libreoffice/share/extensions/nlpsolver/description-zu.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-af.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-am.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ar.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-as.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ast.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-be.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-bg.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-bn-IN.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-bn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-br.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-bs.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ca-valencia.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ca.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-cs.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-cy.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-da.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-de.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-dz.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-el.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-en-GB.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-en-US.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-en-ZA.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-eo.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-es.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-et.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-eu.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-fa.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-fi.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-fr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ga.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-gd.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-gl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-gu.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-gug.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-he.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-hi.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-hr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-hu.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-hy.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-id.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-is.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-it.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ja.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ka.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-kk.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-km.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-kmr-Latn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-kn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ko.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-lt.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-lv.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-mk.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ml.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-mn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-mr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-nb.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ne.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-nl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-nn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-nr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-nso.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-oc.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-om.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-or.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-pa-IN.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-pl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-pt-BR.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-pt.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ro.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ru.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-rw.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-si.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-sk.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-sl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-sr-Latn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-sr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ss.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-st.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-sv.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-szl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ta.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-te.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-tg.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-th.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-tl.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-tn.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-tr.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ts.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ug.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-uk.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-uz.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-ve.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-vi.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-xh.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-zh-CN.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-zh-TW.txt
/usr/lib/libreoffice/share/extensions/wiki-publisher/description-zu.txt
/usr/lib/libreoffice/share/gallery/personas/personas_list.txt
/usr/lib/python3/dist-packages/Babel-2.10.3.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/Babel-2.10.3.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/Babel-2.10.3.egg-info/requires.txt
/usr/lib/python3/dist-packages/Babel-2.10.3.egg-info/top_level.txt
/usr/lib/python3/dist-packages/Brlapi-0.8.5.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/Brlapi-0.8.5.egg-info/top_level.txt
/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/requires.txt
/usr/lib/python3/dist-packages/Jinja2-3.1.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/MarkupSafe-2.1.5.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/MarkupSafe-2.1.5.egg-info/top_level.txt
/usr/lib/python3/dist-packages/PyJWT-2.7.0.dist-info/top_level.txt
/usr/lib/python3/dist-packages/PyYAML-6.0.1.dist-info/top_level.txt
/usr/lib/python3/dist-packages/bcc-0.29.1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/bcc-0.29.1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/certifi-2023.11.17.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/certifi-2023.11.17.egg-info/top_level.txt
/usr/lib/python3/dist-packages/chardet-5.2.0.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/chardet-5.2.0.dist-info/top_level.txt
/usr/lib/python3/dist-packages/click-8.1.6.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/click-8.1.6.egg-info/requires.txt
/usr/lib/python3/dist-packages/click-8.1.6.egg-info/top_level.txt
/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/requires.txt
/usr/lib/python3/dist-packages/cloud_init-25.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/configobj-5.0.8.dist-info/top_level.txt
/usr/lib/python3/dist-packages/cryptography-41.0.7.dist-info/top_level.txt
/usr/lib/python3/dist-packages/cryptography.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/cryptography.egg-info/requires.txt
/usr/lib/python3/dist-packages/cryptography.egg-info/top_level.txt
/usr/lib/python3/dist-packages/cupshelpers-1.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/cupshelpers-1.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/dbus_python-1.3.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/defer-1.0.6.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/defer-1.0.6.egg-info/top_level.txt
/usr/lib/python3/dist-packages/distro-1.9.0.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/distro-1.9.0.dist-info/top_level.txt
/usr/lib/python3/dist-packages/distro_info-1.7+build1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/distro_info-1.7+build1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/httplib2-0.20.4.dist-info/top_level.txt
/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/requires.txt
/usr/lib/python3/dist-packages/jsonpatch-1.32.egg-info/top_level.txt
/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/jsonpointer-2.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/jsonschema-4.10.3.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/language_selector-0.1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/language_selector-0.1.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/language_selector-0.1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/launchpadlib-1.11.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/launchpadlib-1.11.0.egg-info/requires.txt
/usr/lib/python3/dist-packages/launchpadlib-1.11.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/lazr.restfulclient-0.14.6.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/lazr.restfulclient-0.14.6.egg-info/namespace_packages.txt
/usr/lib/python3/dist-packages/lazr.restfulclient-0.14.6.egg-info/requires.txt
/usr/lib/python3/dist-packages/lazr.restfulclient-0.14.6.egg-info/top_level.txt
/usr/lib/python3/dist-packages/lazr.uri-1.0.6.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/lazr.uri-1.0.6.egg-info/namespace_packages.txt
/usr/lib/python3/dist-packages/lazr.uri-1.0.6.egg-info/requires.txt
/usr/lib/python3/dist-packages/lazr.uri-1.0.6.egg-info/top_level.txt
/usr/lib/python3/dist-packages/louis-3.29.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/louis-3.29.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/markdown_it_py-3.0.0.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/meson-1.3.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/meson-1.3.2.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/meson-1.3.2.egg-info/requires.txt
/usr/lib/python3/dist-packages/meson-1.3.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/mesonbuild/dependencies/data/CMakeLists.txt
/usr/lib/python3/dist-packages/mesonbuild/dependencies/data/CMakeListsLLVM.txt
/usr/lib/python3/dist-packages/mesonbuild/dependencies/data/CMakePathInfo.txt
/usr/lib/python3/dist-packages/netaddr/eui/iab.txt
/usr/lib/python3/dist-packages/netaddr/eui/oui.txt
/usr/lib/python3/dist-packages/netaddr-0.8.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/netaddr-0.8.0.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/netaddr-0.8.0.egg-info/requires.txt
/usr/lib/python3/dist-packages/netaddr-0.8.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/netifaces-0.11.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/requires.txt
/usr/lib/python3/dist-packages/oauthlib-3.2.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/olefile-0.46.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/olefile-0.46.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pexpect-4.9.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pexpect-4.9.0.egg-info/requires.txt
/usr/lib/python3/dist-packages/pexpect-4.9.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pillow-10.2.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pillow-10.2.0.egg-info/requires.txt
/usr/lib/python3/dist-packages/pillow-10.2.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pip/_vendor/vendor.txt
/usr/lib/python3/dist-packages/pip-24.0.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/pip-24.0.dist-info/top_level.txt
/usr/lib/python3/dist-packages/pycups-2.0.1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pycups-2.0.1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pygments-2.17.2.dist-info/entry_points.txt
/usr/lib/python3/dist-packages/pyrsistent-0.20.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pyrsistent-0.20.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/requires.txt
/usr/lib/python3/dist-packages/pyserial-3.5.egg-info/top_level.txt
/usr/lib/python3/dist-packages/python_apt-2.7.7+ubuntu5.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/python_apt-2.7.7+ubuntu5.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/python_dateutil-2.8.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/python_dateutil-2.8.2.egg-info/requires.txt
/usr/lib/python3/dist-packages/python_dateutil-2.8.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/python_debian-0.1.49+ubuntu2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/python_debian-0.1.49+ubuntu2.egg-info/requires.txt
/usr/lib/python3/dist-packages/python_debian-0.1.49+ubuntu2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pytz-2024.1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/pytz-2024.1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/pyxdg-0.28.dist-info/top_level.txt
/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/requires.txt
/usr/lib/python3/dist-packages/requests-2.31.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/setuptools-68.1.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/six-1.16.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/six-1.16.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/systemd_python-235.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/systemd_python-235.egg-info/top_level.txt
/usr/lib/python3/dist-packages/ubuntu_drivers_common-0.0.0.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/ubuntu_drivers_common-0.0.0.egg-info/top_level.txt
/usr/lib/python3/dist-packages/ubuntu_pro_client-8001.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/ubuntu_pro_client-8001.egg-info/entry_points.txt
/usr/lib/python3/dist-packages/ubuntu_pro_client-8001.egg-info/requires.txt
/usr/lib/python3/dist-packages/ubuntu_pro_client-8001.egg-info/top_level.txt
/usr/lib/python3/dist-packages/ufw-0.36.2.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/ufw-0.36.2.egg-info/top_level.txt
/usr/lib/python3/dist-packages/unattended_upgrades-0.1.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/unattended_upgrades-0.1.egg-info/top_level.txt
/usr/lib/python3/dist-packages/wadllib-1.3.6.egg-info/dependency_links.txt
/usr/lib/python3/dist-packages/wadllib-1.3.6.egg-info/requires.txt
/usr/lib/python3/dist-packages/wadllib-1.3.6.egg-info/top_level.txt
/usr/lib/python3/dist-packages/wheel/vendored/vendor.txt
/usr/lib/python3/dist-packages/wheel-0.42.0.dist-info/entry_points.txt
/usr/lib/python3.12/LICENSE.txt
/usr/lib/xorg/protocol.txt
/usr/share/X11/rgb.txt
/usr/share/cmake-3.28/Help/command/DEPRECATED_POLICY_VERSIONS.txt
/usr/share/cmake-3.28/Help/command/DEVICE_LINK_OPTIONS.txt
/usr/share/cmake-3.28/Help/command/FIND_XXX.txt
/usr/share/cmake-3.28/Help/command/FIND_XXX_ORDER.txt
/usr/share/cmake-3.28/Help/command/FIND_XXX_REGISTRY_VIEW.txt
/usr/share/cmake-3.28/Help/command/FIND_XXX_ROOT.txt
/usr/share/cmake-3.28/Help/command/GENEX_NOTE.txt
/usr/share/cmake-3.28/Help/command/LINK_OPTIONS_LINKER.txt
/usr/share/cmake-3.28/Help/command/OPTIONS_SHELL.txt
/usr/share/cmake-3.28/Help/command/SUPPORTED_LANGUAGES.txt
/usr/share/cmake-3.28/Help/command/UNSET_NOTE.txt
/usr/share/cmake-3.28/Help/envvar/ENV_VAR.txt
/usr/share/cmake-3.28/Help/envvar/LANG_FLAGS.txt
/usr/share/cmake-3.28/Help/generator/VS_TOOLSET_HOST_ARCH.txt
/usr/share/cmake-3.28/Help/generator/VS_TOOLSET_HOST_ARCH_LEGACY.txt
/usr/share/cmake-3.28/Help/include/COMPILE_DEFINITIONS_DISCLAIMER.txt
/usr/share/cmake-3.28/Help/include/INTERFACE_INCLUDE_DIRECTORIES_WARNING.txt
/usr/share/cmake-3.28/Help/include/INTERFACE_LINK_LIBRARIES_WARNING.txt
/usr/share/cmake-3.28/Help/manual/ID_RESERVE.txt
/usr/share/cmake-3.28/Help/manual/LINKS.txt
/usr/share/cmake-3.28/Help/manual/OPTIONS_BUILD.txt
/usr/share/cmake-3.28/Help/manual/OPTIONS_HELP.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_DEFINITIONS.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_FLAGS.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_INCLUDES.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_LIBRARIES.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_LINK_OPTIONS.txt
/usr/share/cmake-3.28/Help/module/CMAKE_REQUIRED_QUIET.txt
/usr/share/cmake-3.28/Help/policy/DEPRECATED.txt
/usr/share/cmake-3.28/Help/policy/DISALLOWED_COMMAND.txt
/usr/share/cmake-3.28/Help/prop_gbl/CMAKE_LANG_STD_FLAGS.txt
/usr/share/cmake-3.28/Help/prop_tgt/COMPILE_PDB_NOTE.txt
/usr/share/cmake-3.28/Help/prop_tgt/CUDA_RUNTIME_LIBRARY-VALUES.txt
/usr/share/cmake-3.28/Help/prop_tgt/INTERFACE_BUILD_PROPERTY.txt
/usr/share/cmake-3.28/Help/prop_tgt/INTERFACE_LINK_LIBRARIES_DIRECT.txt
/usr/share/cmake-3.28/Help/prop_tgt/LINK_LIBRARIES_INDIRECTION.txt
/usr/share/cmake-3.28/Help/prop_tgt/MACOS_IMPORT_FILES.txt
/usr/share/cmake-3.28/Help/prop_tgt/MSVC_DEBUG_INFORMATION_FORMAT-VALUES.txt
/usr/share/cmake-3.28/Help/prop_tgt/MSVC_RUNTIME_LIBRARY-VALUES.txt
/usr/share/cmake-3.28/Help/prop_tgt/PDB_NOTE.txt
/usr/share/cmake-3.28/Help/prop_tgt/WATCOM_RUNTIME_LIBRARY-VALUES.txt
/usr/share/cmake-3.28/Help/prop_tgt/XXX_OUTPUT_DIRECTORY.txt
/usr/share/cmake-3.28/Help/prop_tgt/XXX_OUTPUT_NAME.txt
/usr/share/cmake-3.28/Help/release/dev.txt
/usr/share/cmake-3.28/Help/variable/CMAKE_FIND_ROOT_PATH_MODE_XXX.txt
/usr/share/cmake-3.28/Help/variable/CMAKE_LINK_GROUP_USING_FEATURE.txt
/usr/share/cmake-3.28/Help/variable/CMAKE_LINK_LIBRARY_USING_FEATURE.txt
/usr/share/cmake-3.28/Help/variable/CMAKE_OSX_VARIABLE.txt
/usr/share/cmake-3.28/Help/variable/CMAKE_VS_VERSION_BUILD_NUMBER_COMPONENTS.txt
/usr/share/cmake-3.28/Help/variable/CTEST_CUSTOM_XXX.txt
/usr/share/cmake-3.28/Help/variable/IGNORE_SEARCH_LOCATIONS.txt
/usr/share/cmake-3.28/Help/variable/IGNORE_SEARCH_NONSYSTEM.txt
/usr/share/cmake-3.28/Help/variable/IGNORE_SEARCH_PATH.txt
/usr/share/cmake-3.28/Help/variable/IGNORE_SEARCH_PREFIX.txt
/usr/share/cmake-3.28/Help/variable/IGNORE_SEARCH_SYSTEM.txt
/usr/share/cmake-3.28/Help/variable/LINK_GROUP_PREDEFINED_FEATURES.txt
/usr/share/cmake-3.28/Help/variable/LINK_LIBRARY_PREDEFINED_FEATURES.txt
/usr/share/cmake-3.28/Modules/CMakeAddNewLanguage.txt
/usr/share/cmake-3.28/Modules/readme.txt
/usr/share/cmake-3.28/Modules/FortranCInterface/CMakeLists.txt
/usr/share/cmake-3.28/Modules/FortranCInterface/Verify/CMakeLists.txt
/usr/share/cmake-3.28/Modules/IntelVSImplicitPath/CMakeLists.txt
/usr/share/cmake-3.28/Templates/CPack.GenericDescription.txt
/usr/share/cmake-3.28/Templates/CPack.GenericLicense.txt
/usr/share/cmake-3.28/Templates/CPack.GenericWelcome.txt
/usr/share/cups/doc-root/robots.txt
/usr/share/doc/alsa-base/driver/Bt87x.txt
/usr/share/doc/alsa-base/driver/ControlNames.txt
/usr/share/doc/alsa-base/driver/Joystick.txt
/usr/share/doc/alsa-base/driver/MIXART.txt
/usr/share/doc/alsa-base/driver/VIA82xx-mixer.txt
/usr/share/doc/alsa-base/driver/alsa-parameters.txt
/usr/share/doc/alsa-base/driver/emu10k1-jack.txt
/usr/share/doc/alsa-base/driver/powersave.txt
/usr/share/doc/alsa-base/driver/serial-u16550.txt
/usr/share/doc/bpfcc-tools/examples/doc/argdist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/bashreadline_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/bindsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/biolatency_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/biolatpcts_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/biopattern_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/biosnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/biotop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/bitesize_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/bpflist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/btrfsdist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/btrfsslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cachestat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cachetop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/capable_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cobjnew_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/compactsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cpudist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cpuunclaimed_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/criticalstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/cthreads_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/dbslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/dbstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/dcsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/dcstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/deadlock_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/dirtop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/drsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/execsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/exitsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/ext4dist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/ext4slower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/filegone_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/filelife_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/fileslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/filetop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/funccount_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/funcinterval_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/funclatency_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/funcslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/gethostlatency_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/hardirqs_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/inject_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javacalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javaflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javagc_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javaobjnew_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javastat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/javathreads_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/killsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/klockstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/kvmexit_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/llcstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/mdflush_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/memleak_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/mountsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/mysqld_qslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/netqtop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/nfsdist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/nfsslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/nodegc_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/nodestat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/offcputime_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/offwaketime_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/oomkill_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/opensnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/perlcalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/perlflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/perlstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/phpcalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/phpflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/phpstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/pidpersec_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/ppchcalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/profile_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/pythoncalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/pythonflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/pythongc_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/pythonstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rdmaucma_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/readahead_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/reset-trace_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rubycalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rubyflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rubygc_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rubyobjnew_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/rubystat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/runqlat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/runqlen_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/runqslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/shmsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/slabratetop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/sofdsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/softirqs_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/solisten_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/sslsniff_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/stackcount_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/statsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/swapin.txt
/usr/share/doc/bpfcc-tools/examples/doc/swapin_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/syncsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/syscount_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tclcalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tclflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tclobjnew_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tclstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpaccept_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpcong_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpconnect_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpconnlat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpdrop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcplife_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpretrans_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcprtt_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpstates_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpsubnet_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcpsynbl_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcptop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tcptracer_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/threadsnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/tplist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/trace_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/ttysnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/vfscount_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/vfsstat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/virtiostat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/wakeuptime_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/xfsdist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/xfsslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/zfsdist_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/zfsslower_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/ucalls_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/uflow_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/ugc_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/uobjnew_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/ustat_example.txt
/usr/share/doc/bpfcc-tools/examples/doc/lib/uthreads_example.txt
/usr/share/doc/bpfcc-tools/examples/networking/neighbor_sharing/README.txt
/usr/share/doc/bpfcc-tools/examples/networking/vlan_learning/README.txt
/usr/share/doc/bpfcc-tools/examples/tracing/CMakeLists.txt
/usr/share/doc/bpfcc-tools/examples/tracing/biolatpcts_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/bitehist_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/dddos_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/disksnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/kvm_hypercall.txt
/usr/share/doc/bpfcc-tools/examples/tracing/mysqld_query_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/nodejs_http_server_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/stacksnoop_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/tcpv4connect_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/undump_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/urandomread_example.txt
/usr/share/doc/bpfcc-tools/examples/tracing/vfsreadlat_example.txt
/usr/share/doc/bpftrace/examples/bashreadline_example.txt
/usr/share/doc/bpftrace/examples/biolatency_example.txt
/usr/share/doc/bpftrace/examples/biosnoop_example.txt
/usr/share/doc/bpftrace/examples/biostacks_example.txt
/usr/share/doc/bpftrace/examples/bitesize_example.txt
/usr/share/doc/bpftrace/examples/capable_example.txt
/usr/share/doc/bpftrace/examples/cpuwalk_example.txt
/usr/share/doc/bpftrace/examples/dcsnoop_example.txt
/usr/share/doc/bpftrace/examples/execsnoop_example.txt
/usr/share/doc/bpftrace/examples/gethostlatency_example.txt
/usr/share/doc/bpftrace/examples/killsnoop_example.txt
/usr/share/doc/bpftrace/examples/loads_example.txt
/usr/share/doc/bpftrace/examples/mdflush_example.txt
/usr/share/doc/bpftrace/examples/naptime_example.txt
/usr/share/doc/bpftrace/examples/oomkill_example.txt
/usr/share/doc/bpftrace/examples/opensnoop_example.txt
/usr/share/doc/bpftrace/examples/pidpersec_example.txt
/usr/share/doc/bpftrace/examples/runqlat_example.txt
/usr/share/doc/bpftrace/examples/runqlen_example.txt
/usr/share/doc/bpftrace/examples/setuids_example.txt
/usr/share/doc/bpftrace/examples/ssllatency_example.txt
/usr/share/doc/bpftrace/examples/sslsnoop_example.txt
/usr/share/doc/bpftrace/examples/statsnoop_example.txt
/usr/share/doc/bpftrace/examples/swapin_example.txt
/usr/share/doc/bpftrace/examples/syncsnoop_example.txt
/usr/share/doc/bpftrace/examples/syscount_example.txt
/usr/share/doc/bpftrace/examples/tcpaccept_example.txt
/usr/share/doc/bpftrace/examples/tcpconnect_example.txt
/usr/share/doc/bpftrace/examples/tcpdrop_example.txt
/usr/share/doc/bpftrace/examples/tcplife_example.txt
/usr/share/doc/bpftrace/examples/tcpretrans_example.txt
/usr/share/doc/bpftrace/examples/tcpsynbl_example.txt
/usr/share/doc/bpftrace/examples/threadsnoop_example.txt
/usr/share/doc/bpftrace/examples/undump_example.txt
/usr/share/doc/bpftrace/examples/vfscount_example.txt
/usr/share/doc/bpftrace/examples/vfsstat_example.txt
/usr/share/doc/bpftrace/examples/writeback_example.txt
/usr/share/doc/bpftrace/examples/xfsdist_example.txt
/usr/share/doc/cloud-init/status.txt
/usr/share/doc/cloud-init/userdata.txt
/usr/share/doc/cloud-init/var-lib-cloud.txt
/usr/share/doc/cloud-init/examples/boothook.txt
/usr/share/doc/cloud-init/examples/cloud-config-add-apt-repos.txt
/usr/share/doc/cloud-init/examples/cloud-config-ansible-controller.txt
/usr/share/doc/cloud-init/examples/cloud-config-ansible-managed.txt
/usr/share/doc/cloud-init/examples/cloud-config-ansible-pull.txt
/usr/share/doc/cloud-init/examples/cloud-config-apt.txt
/usr/share/doc/cloud-init/examples/cloud-config-archive-launch-index.txt
/usr/share/doc/cloud-init/examples/cloud-config-archive.txt
/usr/share/doc/cloud-init/examples/cloud-config-boot-cmds.txt
/usr/share/doc/cloud-init/examples/cloud-config-ca-certs.txt
/usr/share/doc/cloud-init/examples/cloud-config-chef-oneiric.txt
/usr/share/doc/cloud-init/examples/cloud-config-chef.txt
/usr/share/doc/cloud-init/examples/cloud-config-datasources.txt
/usr/share/doc/cloud-init/examples/cloud-config-disk-setup.txt
/usr/share/doc/cloud-init/examples/cloud-config-gluster.txt
/usr/share/doc/cloud-init/examples/cloud-config-install-packages.txt
/usr/share/doc/cloud-init/examples/cloud-config-launch-index.txt
/usr/share/doc/cloud-init/examples/cloud-config-lxd.txt
/usr/share/doc/cloud-init/examples/cloud-config-mount-points.txt
/usr/share/doc/cloud-init/examples/cloud-config-ntp.txt
/usr/share/doc/cloud-init/examples/cloud-config-reporting.txt
/usr/share/doc/cloud-init/examples/cloud-config-run-cmds.txt
/usr/share/doc/cloud-init/examples/cloud-config-ssh-keys.txt
/usr/share/doc/cloud-init/examples/cloud-config-update-apt.txt
/usr/share/doc/cloud-init/examples/cloud-config-update-packages.txt
/usr/share/doc/cloud-init/examples/cloud-config-user-groups.txt
/usr/share/doc/cloud-init/examples/cloud-config-wireguard.txt
/usr/share/doc/cloud-init/examples/cloud-config-write-files.txt
/usr/share/doc/cloud-init/examples/cloud-config-yum-repo.txt
/usr/share/doc/cloud-init/examples/cloud-config.txt
/usr/share/doc/cloud-init/examples/include-once.txt
/usr/share/doc/cloud-init/examples/include.txt
/usr/share/doc/cloud-init/examples/kernel-command-line.txt
/usr/share/doc/cloud-init/examples/part-handler-v2.txt
/usr/share/doc/cloud-init/examples/part-handler.txt
/usr/share/doc/cloud-init/examples/plain-ignored.txt
/usr/share/doc/cloud-init/examples/user-script.txt
/usr/share/doc/cups/HOWTO_BUGREPORT.txt
/usr/share/doc/dpkg/spec/frontend-api.txt
/usr/share/doc/dpkg/spec/protected-field.txt
/usr/share/doc/dpkg/spec/rootless-builds.txt
/usr/share/doc/dpkg/spec/triggers.txt
/usr/share/doc/fonts-sil-gentium/QUOTES.txt
/usr/share/doc/fonts-ubuntu/CONTRIBUTING.txt
/usr/share/doc/fonts-ubuntu/README.txt
/usr/share/doc/fonts-ubuntu/TRADEMARKS.txt
/usr/share/doc/gawk/examples/network/stoxdata.txt
/usr/share/doc/git/RelNotes/1.5.0.1.txt
/usr/share/doc/git/RelNotes/1.5.0.2.txt
/usr/share/doc/git/RelNotes/1.5.0.3.txt
/usr/share/doc/git/RelNotes/1.5.0.4.txt
/usr/share/doc/git/RelNotes/1.5.0.5.txt
/usr/share/doc/git/RelNotes/1.5.0.6.txt
/usr/share/doc/git/RelNotes/1.5.0.7.txt
/usr/share/doc/git/RelNotes/1.5.0.txt
/usr/share/doc/git/RelNotes/1.5.1.1.txt
/usr/share/doc/git/RelNotes/1.5.1.2.txt
/usr/share/doc/git/RelNotes/1.5.1.3.txt
/usr/share/doc/git/RelNotes/1.5.1.4.txt
/usr/share/doc/git/RelNotes/1.5.1.5.txt
/usr/share/doc/git/RelNotes/1.5.1.6.txt
/usr/share/doc/git/RelNotes/1.5.1.txt
/usr/share/doc/git/RelNotes/1.5.2.1.txt
/usr/share/doc/git/RelNotes/1.5.2.2.txt
/usr/share/doc/git/RelNotes/1.5.2.3.txt
/usr/share/doc/git/RelNotes/1.5.2.4.txt
/usr/share/doc/git/RelNotes/1.5.2.5.txt
/usr/share/doc/git/RelNotes/1.5.2.txt
/usr/share/doc/git/RelNotes/1.5.3.1.txt
/usr/share/doc/git/RelNotes/1.5.3.2.txt
/usr/share/doc/git/RelNotes/1.5.3.3.txt
/usr/share/doc/git/RelNotes/1.5.3.4.txt
/usr/share/doc/git/RelNotes/1.5.3.5.txt
/usr/share/doc/git/RelNotes/1.5.3.6.txt
/usr/share/doc/git/RelNotes/1.5.3.7.txt
/usr/share/doc/git/RelNotes/1.5.3.8.txt
/usr/share/doc/git/RelNotes/1.5.3.txt
/usr/share/doc/git/RelNotes/1.5.4.1.txt
/usr/share/doc/git/RelNotes/1.5.4.2.txt
/usr/share/doc/git/RelNotes/1.5.4.3.txt
/usr/share/doc/git/RelNotes/1.5.4.4.txt
/usr/share/doc/git/RelNotes/1.5.4.5.txt
/usr/share/doc/git/RelNotes/1.5.4.6.txt
/usr/share/doc/git/RelNotes/1.5.4.7.txt
/usr/share/doc/git/RelNotes/1.5.4.txt
/usr/share/doc/git/RelNotes/1.5.5.1.txt
/usr/share/doc/git/RelNotes/1.5.5.2.txt
/usr/share/doc/git/RelNotes/1.5.5.3.txt
/usr/share/doc/git/RelNotes/1.5.5.4.txt
/usr/share/doc/git/RelNotes/1.5.5.5.txt
/usr/share/doc/git/RelNotes/1.5.5.6.txt
/usr/share/doc/git/RelNotes/1.5.5.txt
/usr/share/doc/git/RelNotes/1.5.6.1.txt
/usr/share/doc/git/RelNotes/1.5.6.2.txt
/usr/share/doc/git/RelNotes/1.5.6.3.txt
/usr/share/doc/git/RelNotes/1.5.6.4.txt
/usr/share/doc/git/RelNotes/1.5.6.5.txt
/usr/share/doc/git/RelNotes/1.5.6.6.txt
/usr/share/doc/git/RelNotes/1.5.6.txt
/usr/share/doc/git/RelNotes/1.6.0.1.txt
/usr/share/doc/git/RelNotes/1.6.0.2.txt
/usr/share/doc/git/RelNotes/1.6.0.3.txt
/usr/share/doc/git/RelNotes/1.6.0.4.txt
/usr/share/doc/git/RelNotes/1.6.0.5.txt
/usr/share/doc/git/RelNotes/1.6.0.6.txt
/usr/share/doc/git/RelNotes/1.6.0.txt
/usr/share/doc/git/RelNotes/1.6.1.1.txt
/usr/share/doc/git/RelNotes/1.6.1.2.txt
/usr/share/doc/git/RelNotes/1.6.1.3.txt
/usr/share/doc/git/RelNotes/1.6.1.4.txt
/usr/share/doc/git/RelNotes/1.6.1.txt
/usr/share/doc/git/RelNotes/1.6.2.1.txt
/usr/share/doc/git/RelNotes/1.6.2.2.txt
/usr/share/doc/git/RelNotes/1.6.2.3.txt
/usr/share/doc/git/RelNotes/1.6.2.4.txt
/usr/share/doc/git/RelNotes/1.6.2.5.txt
/usr/share/doc/git/RelNotes/1.6.2.txt
/usr/share/doc/git/RelNotes/1.6.3.1.txt
/usr/share/doc/git/RelNotes/1.6.3.2.txt
/usr/share/doc/git/RelNotes/1.6.3.3.txt
/usr/share/doc/git/RelNotes/1.6.3.4.txt
/usr/share/doc/git/RelNotes/1.6.3.txt
/usr/share/doc/git/RelNotes/1.6.4.1.txt
/usr/share/doc/git/RelNotes/1.6.4.2.txt
/usr/share/doc/git/RelNotes/1.6.4.3.txt
/usr/share/doc/git/RelNotes/1.6.4.4.txt
/usr/share/doc/git/RelNotes/1.6.4.5.txt
/usr/share/doc/git/RelNotes/1.6.4.txt
/usr/share/doc/git/RelNotes/1.6.5.1.txt
/usr/share/doc/git/RelNotes/1.6.5.2.txt
/usr/share/doc/git/RelNotes/1.6.5.3.txt
/usr/share/doc/git/RelNotes/1.6.5.4.txt
/usr/share/doc/git/RelNotes/1.6.5.5.txt
/usr/share/doc/git/RelNotes/1.6.5.6.txt
/usr/share/doc/git/RelNotes/1.6.5.7.txt
/usr/share/doc/git/RelNotes/1.6.5.8.txt
/usr/share/doc/git/RelNotes/1.6.5.9.txt
/usr/share/doc/git/RelNotes/1.6.5.txt
/usr/share/doc/git/RelNotes/1.6.6.1.txt
/usr/share/doc/git/RelNotes/1.6.6.2.txt
/usr/share/doc/git/RelNotes/1.6.6.3.txt
/usr/share/doc/git/RelNotes/1.6.6.txt
/usr/share/doc/git/RelNotes/1.7.0.1.txt
/usr/share/doc/git/RelNotes/1.7.0.2.txt
/usr/share/doc/git/RelNotes/1.7.0.3.txt
/usr/share/doc/git/RelNotes/1.7.0.4.txt
/usr/share/doc/git/RelNotes/1.7.0.5.txt
/usr/share/doc/git/RelNotes/1.7.0.6.txt
/usr/share/doc/git/RelNotes/1.7.0.7.txt
/usr/share/doc/git/RelNotes/1.7.0.8.txt
/usr/share/doc/git/RelNotes/1.7.0.9.txt
/usr/share/doc/git/RelNotes/1.7.0.txt
/usr/share/doc/git/RelNotes/1.7.1.1.txt
/usr/share/doc/git/RelNotes/1.7.1.2.txt
/usr/share/doc/git/RelNotes/1.7.1.3.txt
/usr/share/doc/git/RelNotes/1.7.1.4.txt
/usr/share/doc/git/RelNotes/1.7.1.txt
/usr/share/doc/git/RelNotes/1.7.10.1.txt
/usr/share/doc/git/RelNotes/1.7.10.2.txt
/usr/share/doc/git/RelNotes/1.7.10.3.txt
/usr/share/doc/git/RelNotes/1.7.10.4.txt
/usr/share/doc/git/RelNotes/1.7.10.5.txt
/usr/share/doc/git/RelNotes/1.7.10.txt
/usr/share/doc/git/RelNotes/1.7.11.1.txt
/usr/share/doc/git/RelNotes/1.7.11.2.txt
/usr/share/doc/git/RelNotes/1.7.11.3.txt
/usr/share/doc/git/RelNotes/1.7.11.4.txt
/usr/share/doc/git/RelNotes/1.7.11.5.txt
/usr/share/doc/git/RelNotes/1.7.11.6.txt
/usr/share/doc/git/RelNotes/1.7.11.7.txt
/usr/share/doc/git/RelNotes/1.7.11.txt
/usr/share/doc/git/RelNotes/1.7.12.1.txt
/usr/share/doc/git/RelNotes/1.7.12.2.txt
/usr/share/doc/git/RelNotes/1.7.12.3.txt
/usr/share/doc/git/RelNotes/1.7.12.4.txt
/usr/share/doc/git/RelNotes/1.7.12.txt
/usr/share/doc/git/RelNotes/1.7.2.1.txt
/usr/share/doc/git/RelNotes/1.7.2.2.txt
/usr/share/doc/git/RelNotes/1.7.2.3.txt
/usr/share/doc/git/RelNotes/1.7.2.4.txt
/usr/share/doc/git/RelNotes/1.7.2.5.txt
/usr/share/doc/git/RelNotes/1.7.2.txt
/usr/share/doc/git/RelNotes/1.7.3.1.txt
/usr/share/doc/git/RelNotes/1.7.3.2.txt
/usr/share/doc/git/RelNotes/1.7.3.3.txt
/usr/share/doc/git/RelNotes/1.7.3.4.txt
/usr/share/doc/git/RelNotes/1.7.3.5.txt
/usr/share/doc/git/RelNotes/1.7.3.txt
/usr/share/doc/git/RelNotes/1.7.4.1.txt
/usr/share/doc/git/RelNotes/1.7.4.2.txt
/usr/share/doc/git/RelNotes/1.7.4.3.txt
/usr/share/doc/git/RelNotes/1.7.4.4.txt
/usr/share/doc/git/RelNotes/1.7.4.5.txt
/usr/share/doc/git/RelNotes/1.7.4.txt
/usr/share/doc/git/RelNotes/1.7.5.1.txt
/usr/share/doc/git/RelNotes/1.7.5.2.txt
/usr/share/doc/git/RelNotes/1.7.5.3.txt
/usr/share/doc/git/RelNotes/1.7.5.4.txt
/usr/share/doc/git/RelNotes/1.7.5.txt
/usr/share/doc/git/RelNotes/1.7.6.1.txt
/usr/share/doc/git/RelNotes/1.7.6.2.txt
/usr/share/doc/git/RelNotes/1.7.6.3.txt
/usr/share/doc/git/RelNotes/1.7.6.4.txt
/usr/share/doc/git/RelNotes/1.7.6.5.txt
/usr/share/doc/git/RelNotes/1.7.6.6.txt
/usr/share/doc/git/RelNotes/1.7.6.txt
/usr/share/doc/git/RelNotes/1.7.7.1.txt
/usr/share/doc/git/RelNotes/1.7.7.2.txt
/usr/share/doc/git/RelNotes/1.7.7.3.txt
/usr/share/doc/git/RelNotes/1.7.7.4.txt
/usr/share/doc/git/RelNotes/1.7.7.5.txt
/usr/share/doc/git/RelNotes/1.7.7.6.txt
/usr/share/doc/git/RelNotes/1.7.7.7.txt
/usr/share/doc/git/RelNotes/1.7.7.txt
/usr/share/doc/git/RelNotes/1.7.8.1.txt
/usr/share/doc/git/RelNotes/1.7.8.2.txt
/usr/share/doc/git/RelNotes/1.7.8.3.txt
/usr/share/doc/git/RelNotes/1.7.8.4.txt
/usr/share/doc/git/RelNotes/1.7.8.5.txt
/usr/share/doc/git/RelNotes/1.7.8.6.txt
/usr/share/doc/git/RelNotes/1.7.8.txt
/usr/share/doc/git/RelNotes/1.7.9.1.txt
/usr/share/doc/git/RelNotes/1.7.9.2.txt
/usr/share/doc/git/RelNotes/1.7.9.3.txt
/usr/share/doc/git/RelNotes/1.7.9.4.txt
/usr/share/doc/git/RelNotes/1.7.9.5.txt
/usr/share/doc/git/RelNotes/1.7.9.6.txt
/usr/share/doc/git/RelNotes/1.7.9.7.txt
/usr/share/doc/git/RelNotes/1.7.9.txt
/usr/share/doc/git/RelNotes/1.8.0.1.txt
/usr/share/doc/git/RelNotes/1.8.0.2.txt
/usr/share/doc/git/RelNotes/1.8.0.3.txt
/usr/share/doc/git/RelNotes/1.8.0.txt
/usr/share/doc/git/RelNotes/1.8.1.1.txt
/usr/share/doc/git/RelNotes/1.8.1.2.txt
/usr/share/doc/git/RelNotes/1.8.1.3.txt
/usr/share/doc/git/RelNotes/1.8.1.4.txt
/usr/share/doc/git/RelNotes/1.8.1.5.txt
/usr/share/doc/git/RelNotes/1.8.1.6.txt
/usr/share/doc/git/RelNotes/1.8.1.txt
/usr/share/doc/git/RelNotes/1.8.2.1.txt
/usr/share/doc/git/RelNotes/1.8.2.2.txt
/usr/share/doc/git/RelNotes/1.8.2.3.txt
/usr/share/doc/git/RelNotes/1.8.2.txt
/usr/share/doc/git/RelNotes/1.8.3.1.txt
/usr/share/doc/git/RelNotes/1.8.3.2.txt
/usr/share/doc/git/RelNotes/1.8.3.3.txt
/usr/share/doc/git/RelNotes/1.8.3.4.txt
/usr/share/doc/git/RelNotes/1.8.3.txt
/usr/share/doc/git/RelNotes/1.8.4.1.txt
/usr/share/doc/git/RelNotes/1.8.4.2.txt
/usr/share/doc/git/RelNotes/1.8.4.3.txt
/usr/share/doc/git/RelNotes/1.8.4.4.txt
/usr/share/doc/git/RelNotes/1.8.4.5.txt
/usr/share/doc/git/RelNotes/1.8.4.txt
/usr/share/doc/git/RelNotes/1.8.5.1.txt
/usr/share/doc/git/RelNotes/1.8.5.2.txt
/usr/share/doc/git/RelNotes/1.8.5.3.txt
/usr/share/doc/git/RelNotes/1.8.5.4.txt
/usr/share/doc/git/RelNotes/1.8.5.5.txt
/usr/share/doc/git/RelNotes/1.8.5.6.txt
/usr/share/doc/git/RelNotes/1.8.5.txt
/usr/share/doc/git/RelNotes/1.9.0.txt
/usr/share/doc/git/RelNotes/1.9.1.txt
/usr/share/doc/git/RelNotes/1.9.2.txt
/usr/share/doc/git/RelNotes/1.9.3.txt
/usr/share/doc/git/RelNotes/1.9.4.txt
/usr/share/doc/git/RelNotes/1.9.5.txt
/usr/share/doc/git/RelNotes/2.0.0.txt
/usr/share/doc/git/RelNotes/2.0.1.txt
/usr/share/doc/git/RelNotes/2.0.2.txt
/usr/share/doc/git/RelNotes/2.0.3.txt
/usr/share/doc/git/RelNotes/2.0.4.txt
/usr/share/doc/git/RelNotes/2.0.5.txt
/usr/share/doc/git/RelNotes/2.1.0.txt
/usr/share/doc/git/RelNotes/2.1.1.txt
/usr/share/doc/git/RelNotes/2.1.2.txt
/usr/share/doc/git/RelNotes/2.1.3.txt
/usr/share/doc/git/RelNotes/2.1.4.txt
/usr/share/doc/git/RelNotes/2.10.0.txt
/usr/share/doc/git/RelNotes/2.10.1.txt
/usr/share/doc/git/RelNotes/2.10.2.txt
/usr/share/doc/git/RelNotes/2.10.3.txt
/usr/share/doc/git/RelNotes/2.10.4.txt
/usr/share/doc/git/RelNotes/2.10.5.txt
/usr/share/doc/git/RelNotes/2.11.0.txt
/usr/share/doc/git/RelNotes/2.11.1.txt
/usr/share/doc/git/RelNotes/2.11.2.txt
/usr/share/doc/git/RelNotes/2.11.3.txt
/usr/share/doc/git/RelNotes/2.11.4.txt
/usr/share/doc/git/RelNotes/2.12.0.txt
/usr/share/doc/git/RelNotes/2.12.1.txt
/usr/share/doc/git/RelNotes/2.12.2.txt
/usr/share/doc/git/RelNotes/2.12.3.txt
/usr/share/doc/git/RelNotes/2.12.4.txt
/usr/share/doc/git/RelNotes/2.12.5.txt
/usr/share/doc/git/RelNotes/2.13.0.txt
/usr/share/doc/git/RelNotes/2.13.1.txt
/usr/share/doc/git/RelNotes/2.13.2.txt
/usr/share/doc/git/RelNotes/2.13.3.txt
/usr/share/doc/git/RelNotes/2.13.4.txt
/usr/share/doc/git/RelNotes/2.13.5.txt
/usr/share/doc/git/RelNotes/2.13.6.txt
/usr/share/doc/git/RelNotes/2.13.7.txt
/usr/share/doc/git/RelNotes/2.14.0.txt
/usr/share/doc/git/RelNotes/2.14.1.txt
/usr/share/doc/git/RelNotes/2.14.2.txt
/usr/share/doc/git/RelNotes/2.14.3.txt
/usr/share/doc/git/RelNotes/2.14.4.txt
/usr/share/doc/git/RelNotes/2.14.5.txt
/usr/share/doc/git/RelNotes/2.14.6.txt
/usr/share/doc/git/RelNotes/2.15.0.txt
/usr/share/doc/git/RelNotes/2.15.1.txt
/usr/share/doc/git/RelNotes/2.15.2.txt
/usr/share/doc/git/RelNotes/2.15.3.txt
/usr/share/doc/git/RelNotes/2.15.4.txt
/usr/share/doc/git/RelNotes/2.16.0.txt
/usr/share/doc/git/RelNotes/2.16.1.txt
/usr/share/doc/git/RelNotes/2.16.2.txt
/usr/share/doc/git/RelNotes/2.16.3.txt
/usr/share/doc/git/RelNotes/2.16.4.txt
/usr/share/doc/git/RelNotes/2.16.5.txt
/usr/share/doc/git/RelNotes/2.16.6.txt
/usr/share/doc/git/RelNotes/2.17.0.txt
/usr/share/doc/git/RelNotes/2.17.1.txt
/usr/share/doc/git/RelNotes/2.17.2.txt
/usr/share/doc/git/RelNotes/2.17.3.txt
/usr/share/doc/git/RelNotes/2.17.4.txt
/usr/share/doc/git/RelNotes/2.17.5.txt
/usr/share/doc/git/RelNotes/2.17.6.txt
/usr/share/doc/git/RelNotes/2.18.0.txt
/usr/share/doc/git/RelNotes/2.18.1.txt
/usr/share/doc/git/RelNotes/2.18.2.txt
/usr/share/doc/git/RelNotes/2.18.3.txt
/usr/share/doc/git/RelNotes/2.18.4.txt
/usr/share/doc/git/RelNotes/2.18.5.txt
/usr/share/doc/git/RelNotes/2.19.0.txt
/usr/share/doc/git/RelNotes/2.19.1.txt
/usr/share/doc/git/RelNotes/2.19.2.txt
/usr/share/doc/git/RelNotes/2.19.3.txt
/usr/share/doc/git/RelNotes/2.19.4.txt
/usr/share/doc/git/RelNotes/2.19.5.txt
/usr/share/doc/git/RelNotes/2.19.6.txt
/usr/share/doc/git/RelNotes/2.2.0.txt
/usr/share/doc/git/RelNotes/2.2.1.txt
/usr/share/doc/git/RelNotes/2.2.2.txt
/usr/share/doc/git/RelNotes/2.2.3.txt
/usr/share/doc/git/RelNotes/2.20.0.txt
/usr/share/doc/git/RelNotes/2.20.1.txt
/usr/share/doc/git/RelNotes/2.20.2.txt
/usr/share/doc/git/RelNotes/2.20.3.txt
/usr/share/doc/git/RelNotes/2.20.4.txt
/usr/share/doc/git/RelNotes/2.20.5.txt
/usr/share/doc/git/RelNotes/2.21.0.txt
/usr/share/doc/git/RelNotes/2.21.1.txt
/usr/share/doc/git/RelNotes/2.21.2.txt
/usr/share/doc/git/RelNotes/2.21.3.txt
/usr/share/doc/git/RelNotes/2.21.4.txt
/usr/share/doc/git/RelNotes/2.22.0.txt
/usr/share/doc/git/RelNotes/2.22.1.txt
/usr/share/doc/git/RelNotes/2.22.2.txt
/usr/share/doc/git/RelNotes/2.22.3.txt
/usr/share/doc/git/RelNotes/2.22.4.txt
/usr/share/doc/git/RelNotes/2.22.5.txt
/usr/share/doc/git/RelNotes/2.23.0.txt
/usr/share/doc/git/RelNotes/2.23.1.txt
/usr/share/doc/git/RelNotes/2.23.2.txt
/usr/share/doc/git/RelNotes/2.23.3.txt
/usr/share/doc/git/RelNotes/2.23.4.txt
/usr/share/doc/git/RelNotes/2.24.0.txt
/usr/share/doc/git/RelNotes/2.24.1.txt
/usr/share/doc/git/RelNotes/2.24.2.txt
/usr/share/doc/git/RelNotes/2.24.3.txt
/usr/share/doc/git/RelNotes/2.24.4.txt
/usr/share/doc/git/RelNotes/2.25.0.txt
/usr/share/doc/git/RelNotes/2.25.1.txt
/usr/share/doc/git/RelNotes/2.25.2.txt
/usr/share/doc/git/RelNotes/2.25.3.txt
/usr/share/doc/git/RelNotes/2.25.4.txt
/usr/share/doc/git/RelNotes/2.25.5.txt
/usr/share/doc/git/RelNotes/2.26.0.txt
/usr/share/doc/git/RelNotes/2.26.1.txt
/usr/share/doc/git/RelNotes/2.26.2.txt
/usr/share/doc/git/RelNotes/2.26.3.txt
/usr/share/doc/git/RelNotes/2.27.0.txt
/usr/share/doc/git/RelNotes/2.27.1.txt
/usr/share/doc/git/RelNotes/2.28.0.txt
/usr/share/doc/git/RelNotes/2.28.1.txt
/usr/share/doc/git/RelNotes/2.29.0.txt
/usr/share/doc/git/RelNotes/2.29.1.txt
/usr/share/doc/git/RelNotes/2.29.2.txt
/usr/share/doc/git/RelNotes/2.29.3.txt
/usr/share/doc/git/RelNotes/2.3.0.txt
/usr/share/doc/git/RelNotes/2.3.1.txt
/usr/share/doc/git/RelNotes/2.3.10.txt
/usr/share/doc/git/RelNotes/2.3.2.txt
/usr/share/doc/git/RelNotes/2.3.3.txt
/usr/share/doc/git/RelNotes/2.3.4.txt
/usr/share/doc/git/RelNotes/2.3.5.txt
/usr/share/doc/git/RelNotes/2.3.6.txt
/usr/share/doc/git/RelNotes/2.3.7.txt
/usr/share/doc/git/RelNotes/2.3.8.txt
/usr/share/doc/git/RelNotes/2.3.9.txt
/usr/share/doc/git/RelNotes/2.30.0.txt
/usr/share/doc/git/RelNotes/2.30.1.txt
/usr/share/doc/git/RelNotes/2.30.2.txt
/usr/share/doc/git/RelNotes/2.30.3.txt
/usr/share/doc/git/RelNotes/2.30.4.txt
/usr/share/doc/git/RelNotes/2.30.5.txt
/usr/share/doc/git/RelNotes/2.30.6.txt
/usr/share/doc/git/RelNotes/2.30.7.txt
/usr/share/doc/git/RelNotes/2.30.8.txt
/usr/share/doc/git/RelNotes/2.30.9.txt
/usr/share/doc/git/RelNotes/2.31.0.txt
/usr/share/doc/git/RelNotes/2.31.1.txt
/usr/share/doc/git/RelNotes/2.31.2.txt
/usr/share/doc/git/RelNotes/2.31.3.txt
/usr/share/doc/git/RelNotes/2.31.4.txt
/usr/share/doc/git/RelNotes/2.31.5.txt
/usr/share/doc/git/RelNotes/2.31.6.txt
/usr/share/doc/git/RelNotes/2.31.7.txt
/usr/share/doc/git/RelNotes/2.31.8.txt
/usr/share/doc/git/RelNotes/2.32.0.txt
/usr/share/doc/git/RelNotes/2.32.1.txt
/usr/share/doc/git/RelNotes/2.32.2.txt
/usr/share/doc/git/RelNotes/2.32.3.txt
/usr/share/doc/git/RelNotes/2.32.4.txt
/usr/share/doc/git/RelNotes/2.32.5.txt
/usr/share/doc/git/RelNotes/2.32.6.txt
/usr/share/doc/git/RelNotes/2.32.7.txt
/usr/share/doc/git/RelNotes/2.33.0.txt
/usr/share/doc/git/RelNotes/2.33.1.txt
/usr/share/doc/git/RelNotes/2.33.2.txt
/usr/share/doc/git/RelNotes/2.33.3.txt
/usr/share/doc/git/RelNotes/2.33.4.txt
/usr/share/doc/git/RelNotes/2.33.5.txt
/usr/share/doc/git/RelNotes/2.33.6.txt
/usr/share/doc/git/RelNotes/2.33.7.txt
/usr/share/doc/git/RelNotes/2.33.8.txt
/usr/share/doc/git/RelNotes/2.34.0.txt
/usr/share/doc/git/RelNotes/2.34.1.txt
/usr/share/doc/git/RelNotes/2.34.2.txt
/usr/share/doc/git/RelNotes/2.34.3.txt
/usr/share/doc/git/RelNotes/2.34.4.txt
/usr/share/doc/git/RelNotes/2.34.5.txt
/usr/share/doc/git/RelNotes/2.34.6.txt
/usr/share/doc/git/RelNotes/2.34.7.txt
/usr/share/doc/git/RelNotes/2.34.8.txt
/usr/share/doc/git/RelNotes/2.35.0.txt
/usr/share/doc/git/RelNotes/2.35.1.txt
/usr/share/doc/git/RelNotes/2.35.2.txt
/usr/share/doc/git/RelNotes/2.35.3.txt
/usr/share/doc/git/RelNotes/2.35.4.txt
/usr/share/doc/git/RelNotes/2.35.5.txt
/usr/share/doc/git/RelNotes/2.35.6.txt
/usr/share/doc/git/RelNotes/2.35.7.txt
/usr/share/doc/git/RelNotes/2.35.8.txt
/usr/share/doc/git/RelNotes/2.36.0.txt
/usr/share/doc/git/RelNotes/2.36.1.txt
/usr/share/doc/git/RelNotes/2.36.2.txt
/usr/share/doc/git/RelNotes/2.36.3.txt
/usr/share/doc/git/RelNotes/2.36.4.txt
/usr/share/doc/git/RelNotes/2.36.5.txt
/usr/share/doc/git/RelNotes/2.36.6.txt
/usr/share/doc/git/RelNotes/2.37.0.txt
/usr/share/doc/git/RelNotes/2.37.1.txt
/usr/share/doc/git/RelNotes/2.37.2.txt
/usr/share/doc/git/RelNotes/2.37.3.txt
/usr/share/doc/git/RelNotes/2.37.4.txt
/usr/share/doc/git/RelNotes/2.37.5.txt
/usr/share/doc/git/RelNotes/2.37.6.txt
/usr/share/doc/git/RelNotes/2.37.7.txt
/usr/share/doc/git/RelNotes/2.38.0.txt
/usr/share/doc/git/RelNotes/2.38.1.txt
/usr/share/doc/git/RelNotes/2.38.2.txt
/usr/share/doc/git/RelNotes/2.38.3.txt
/usr/share/doc/git/RelNotes/2.38.4.txt
/usr/share/doc/git/RelNotes/2.38.5.txt
/usr/share/doc/git/RelNotes/2.39.0.txt
/usr/share/doc/git/RelNotes/2.39.1.txt
/usr/share/doc/git/RelNotes/2.39.2.txt
/usr/share/doc/git/RelNotes/2.39.3.txt
/usr/share/doc/git/RelNotes/2.4.0.txt
/usr/share/doc/git/RelNotes/2.4.1.txt
/usr/share/doc/git/RelNotes/2.4.10.txt
/usr/share/doc/git/RelNotes/2.4.11.txt
/usr/share/doc/git/RelNotes/2.4.12.txt
/usr/share/doc/git/RelNotes/2.4.2.txt
/usr/share/doc/git/RelNotes/2.4.3.txt
/usr/share/doc/git/RelNotes/2.4.4.txt
/usr/share/doc/git/RelNotes/2.4.5.txt
/usr/share/doc/git/RelNotes/2.4.6.txt
/usr/share/doc/git/RelNotes/2.4.7.txt
/usr/share/doc/git/RelNotes/2.4.8.txt
/usr/share/doc/git/RelNotes/2.4.9.txt
/usr/share/doc/git/RelNotes/2.40.0.txt
/usr/share/doc/git/RelNotes/2.40.1.txt
/usr/share/doc/git/RelNotes/2.41.0.txt
/usr/share/doc/git/RelNotes/2.42.0.txt
/usr/share/doc/git/RelNotes/2.42.1.txt
/usr/share/doc/git/RelNotes/2.43.0.txt
/usr/share/doc/git/RelNotes/2.5.0.txt
/usr/share/doc/git/RelNotes/2.5.1.txt
/usr/share/doc/git/RelNotes/2.5.2.txt
/usr/share/doc/git/RelNotes/2.5.3.txt
/usr/share/doc/git/RelNotes/2.5.4.txt
/usr/share/doc/git/RelNotes/2.5.5.txt
/usr/share/doc/git/RelNotes/2.5.6.txt
/usr/share/doc/git/RelNotes/2.6.0.txt
/usr/share/doc/git/RelNotes/2.6.1.txt
/usr/share/doc/git/RelNotes/2.6.2.txt
/usr/share/doc/git/RelNotes/2.6.3.txt
/usr/share/doc/git/RelNotes/2.6.4.txt
/usr/share/doc/git/RelNotes/2.6.5.txt
/usr/share/doc/git/RelNotes/2.6.6.txt
/usr/share/doc/git/RelNotes/2.6.7.txt
/usr/share/doc/git/RelNotes/2.7.0.txt
/usr/share/doc/git/RelNotes/2.7.1.txt
/usr/share/doc/git/RelNotes/2.7.2.txt
/usr/share/doc/git/RelNotes/2.7.3.txt
/usr/share/doc/git/RelNotes/2.7.4.txt
/usr/share/doc/git/RelNotes/2.7.5.txt
/usr/share/doc/git/RelNotes/2.7.6.txt
/usr/share/doc/git/RelNotes/2.8.0.txt
/usr/share/doc/git/RelNotes/2.8.1.txt
/usr/share/doc/git/RelNotes/2.8.2.txt
/usr/share/doc/git/RelNotes/2.8.3.txt
/usr/share/doc/git/RelNotes/2.8.4.txt
/usr/share/doc/git/RelNotes/2.8.5.txt
/usr/share/doc/git/RelNotes/2.8.6.txt
/usr/share/doc/git/RelNotes/2.9.0.txt
/usr/share/doc/git/RelNotes/2.9.1.txt
/usr/share/doc/git/RelNotes/2.9.2.txt
/usr/share/doc/git/RelNotes/2.9.3.txt
/usr/share/doc/git/RelNotes/2.9.4.txt
/usr/share/doc/git/RelNotes/2.9.5.txt
/usr/share/doc/git/contrib/buildsystems/CMakeLists.txt
/usr/share/doc/git/contrib/contacts/git-contacts.txt
/usr/share/doc/git/contrib/hg-to-git/hg-to-git.txt
/usr/share/doc/git/contrib/subtree/git-subtree.txt
/usr/share/doc/gnupg/examples/qualified.txt
/usr/share/doc/gnupg/examples/trustlist.txt
/usr/share/doc/gpg-agent/examples/trustlist.txt
/usr/share/doc/hplip/users-guide.txt
/usr/share/doc/libasound2t64/examples/asoundrc.txt
/usr/share/doc/libauthen-sasl-perl/api.txt
/usr/share/doc/libbpfcc/FAQ.txt
/usr/share/doc/libdb5.3t64/build_signature_amd64.txt
/usr/share/doc/libgphoto2-6/OUTDATED.txt
/usr/share/doc/libio-socket-ssl-perl/debugging.txt
/usr/share/doc/libsane-common/leo/leo.txt
/usr/share/doc/libsane-common/plustek/Plustek-PARPORT-TODO.txt
/usr/share/doc/libsane-common/plustek/Plustek-PARPORT.txt
/usr/share/doc/libsane-common/plustek/Plustek-USB-TODO.txt
/usr/share/doc/libsane-common/sceptre/s1200.txt
/usr/share/doc/libsane-common/umax/negative-types.txt
/usr/share/doc/libsynctex2/README.txt
/usr/share/doc/mount/mount.txt
/usr/share/doc/openssl/fingerprints.txt
/usr/share/doc/openssl/HOWTO/keys.txt
/usr/share/doc/powermgmt-base/power_supply.txt
/usr/share/doc/publicsuffix/examples/test_psl.txt
/usr/share/doc/python3-pip/requirements.txt
/usr/share/doc/sssd-common/BUILD.txt
/usr/share/doc/util-linux/00-about-docs.txt
/usr/share/doc/util-linux/PAM-configuration.txt
/usr/share/doc/util-linux/blkid.txt
/usr/share/doc/util-linux/cal.txt
/usr/share/doc/util-linux/col.txt
/usr/share/doc/util-linux/deprecated.txt
/usr/share/doc/util-linux/getopt.txt
/usr/share/doc/util-linux/getopt_changelog.txt
/usr/share/doc/util-linux/howto-build-sys.txt
/usr/share/doc/util-linux/howto-compilation.txt
/usr/share/doc/util-linux/howto-debug.txt
/usr/share/doc/util-linux/howto-man-page.txt
/usr/share/doc/util-linux/howto-tests.txt
/usr/share/doc/util-linux/hwclock.txt
/usr/share/doc/util-linux/modems-with-agetty.txt
/usr/share/doc/util-linux/mount.txt
/usr/share/doc/util-linux/pg.txt
/usr/share/doc/util-linux/release-schedule.txt
/usr/share/doc/vlc/lua/extensions/README.txt
/usr/share/doc/vlc/lua/intf/README.txt
/usr/share/doc/vlc/lua/meta/README.txt
/usr/share/doc/vlc/lua/meta/art/README.txt
/usr/share/doc/vlc/lua/meta/fetcher/README.txt
/usr/share/doc/vlc/lua/meta/reader/README.txt
/usr/share/doc/vlc/lua/playlist/README.txt
/usr/share/doc/vlc/lua/sd/README.txt
/usr/share/doc/x11proto-dev/xwaylandproto.txt
/usr/share/doc/xorg/index.txt
/usr/share/doc/xorg/upstream-features.txt
/usr/share/doc/xorg/faq/general.txt
/usr/share/doc/xorg/howto/report-bugs.txt
/usr/share/doc/xorg/howto/triage-bugs.txt
/usr/share/doc/xorg/reference/experimental.txt
/usr/share/doc/xorg/reference/squeeze-backports.txt
/usr/share/doc/xorg/reference/upstream-contacts.txt
/usr/share/gnupg/help.be.txt
/usr/share/gnupg/help.ca.txt
/usr/share/gnupg/help.cs.txt
/usr/share/gnupg/help.da.txt
/usr/share/gnupg/help.de.txt
/usr/share/gnupg/help.el.txt
/usr/share/gnupg/help.eo.txt
/usr/share/gnupg/help.es.txt
/usr/share/gnupg/help.et.txt
/usr/share/gnupg/help.fi.txt
/usr/share/gnupg/help.fr.txt
/usr/share/gnupg/help.gl.txt
/usr/share/gnupg/help.hu.txt
/usr/share/gnupg/help.id.txt
/usr/share/gnupg/help.it.txt
/usr/share/gnupg/help.ja.txt
/usr/share/gnupg/help.nb.txt
/usr/share/gnupg/help.pl.txt
/usr/share/gnupg/help.pt.txt
/usr/share/gnupg/help.pt_BR.txt
/usr/share/gnupg/help.ro.txt
/usr/share/gnupg/help.ru.txt
/usr/share/gnupg/help.sk.txt
/usr/share/gnupg/help.sv.txt
/usr/share/gnupg/help.tr.txt
/usr/share/gnupg/help.txt
/usr/share/gnupg/help.zh_CN.txt
/usr/share/gnupg/help.zh_TW.txt
/usr/share/ibus-table/tables/template.txt
/usr/share/ieee-data/iab.txt
/usr/share/ieee-data/mam.txt
/usr/share/ieee-data/oui.txt
/usr/share/ieee-data/oui36.txt
/usr/share/libcaca/caca.txt
/usr/share/netpbm/rgb.txt
/usr/share/perl/5.38.2/Unicode/Collate/allkeys.txt
/usr/share/perl/5.38.2/Unicode/Collate/keys.txt
/usr/share/perl/5.38.2/unicore/Blocks.txt
/usr/share/perl/5.38.2/unicore/NamedSequences.txt
/usr/share/perl/5.38.2/unicore/SpecialCasing.txt
/usr/share/snmp/mibs/LM-SENSORS-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-AGENT-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-EXAMPLES-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-EXTEND-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-PASS-MIB.txt
/usr/share/snmp/mibs/NET-SNMP-TC.txt
/usr/share/snmp/mibs/NET-SNMP-VACM-MIB.txt
/usr/share/snmp/mibs/UCD-DEMO-MIB.txt
/usr/share/snmp/mibs/UCD-DISKIO-MIB.txt
/usr/share/snmp/mibs/UCD-DLMOD-MIB.txt
/usr/share/snmp/mibs/UCD-IPFWACC-MIB.txt
/usr/share/snmp/mibs/UCD-SNMP-MIB.txt
/usr/share/vim/vim91/doc/arabic.txt
/usr/share/vim/vim91/doc/autocmd.txt
/usr/share/vim/vim91/doc/builtin.txt
/usr/share/vim/vim91/doc/change.txt
/usr/share/vim/vim91/doc/channel.txt
/usr/share/vim/vim91/doc/cmdline.txt
/usr/share/vim/vim91/doc/debug.txt
/usr/share/vim/vim91/doc/debugger.txt
/usr/share/vim/vim91/doc/develop.txt
/usr/share/vim/vim91/doc/diff.txt
/usr/share/vim/vim91/doc/digraph.txt
/usr/share/vim/vim91/doc/editing.txt
/usr/share/vim/vim91/doc/eval.txt
/usr/share/vim/vim91/doc/farsi.txt
/usr/share/vim/vim91/doc/filetype.txt
/usr/share/vim/vim91/doc/fold.txt
/usr/share/vim/vim91/doc/ft_ada.txt
/usr/share/vim/vim91/doc/ft_context.txt
/usr/share/vim/vim91/doc/ft_mp.txt
/usr/share/vim/vim91/doc/ft_ps1.txt
/usr/share/vim/vim91/doc/ft_raku.txt
/usr/share/vim/vim91/doc/ft_rust.txt
/usr/share/vim/vim91/doc/ft_sql.txt
/usr/share/vim/vim91/doc/gui.txt
/usr/share/vim/vim91/doc/gui_w32.txt
/usr/share/vim/vim91/doc/gui_x11.txt
/usr/share/vim/vim91/doc/hangulin.txt
/usr/share/vim/vim91/doc/hebrew.txt
/usr/share/vim/vim91/doc/help.txt
/usr/share/vim/vim91/doc/helphelp.txt
/usr/share/vim/vim91/doc/howto.txt
/usr/share/vim/vim91/doc/if_cscop.txt
/usr/share/vim/vim91/doc/if_lua.txt
/usr/share/vim/vim91/doc/if_mzsch.txt
/usr/share/vim/vim91/doc/if_ole.txt
/usr/share/vim/vim91/doc/if_perl.txt
/usr/share/vim/vim91/doc/if_pyth.txt
/usr/share/vim/vim91/doc/if_ruby.txt
/usr/share/vim/vim91/doc/if_sniff.txt
/usr/share/vim/vim91/doc/if_tcl.txt
/usr/share/vim/vim91/doc/indent.txt
/usr/share/vim/vim91/doc/index.txt
/usr/share/vim/vim91/doc/insert.txt
/usr/share/vim/vim91/doc/intro.txt
/usr/share/vim/vim91/doc/map.txt
/usr/share/vim/vim91/doc/mbyte.txt
/usr/share/vim/vim91/doc/message.txt
/usr/share/vim/vim91/doc/mlang.txt
/usr/share/vim/vim91/doc/motion.txt
/usr/share/vim/vim91/doc/netbeans.txt
/usr/share/vim/vim91/doc/options.txt
/usr/share/vim/vim91/doc/os_390.txt
/usr/share/vim/vim91/doc/os_amiga.txt
/usr/share/vim/vim91/doc/os_beos.txt
/usr/share/vim/vim91/doc/os_dos.txt
/usr/share/vim/vim91/doc/os_haiku.txt
/usr/share/vim/vim91/doc/os_mac.txt
/usr/share/vim/vim91/doc/os_mint.txt
/usr/share/vim/vim91/doc/os_msdos.txt
/usr/share/vim/vim91/doc/os_os2.txt
/usr/share/vim/vim91/doc/os_qnx.txt
/usr/share/vim/vim91/doc/os_risc.txt
/usr/share/vim/vim91/doc/os_unix.txt
/usr/share/vim/vim91/doc/os_vms.txt
/usr/share/vim/vim91/doc/os_win32.txt
/usr/share/vim/vim91/doc/pattern.txt
/usr/share/vim/vim91/doc/pi_getscript.txt
/usr/share/vim/vim91/doc/pi_gzip.txt
/usr/share/vim/vim91/doc/pi_logipat.txt
/usr/share/vim/vim91/doc/pi_netrw.txt
/usr/share/vim/vim91/doc/pi_paren.txt
/usr/share/vim/vim91/doc/pi_spec.txt
/usr/share/vim/vim91/doc/pi_tar.txt
/usr/share/vim/vim91/doc/pi_vimball.txt
/usr/share/vim/vim91/doc/pi_zip.txt
/usr/share/vim/vim91/doc/popup.txt
/usr/share/vim/vim91/doc/print.txt
/usr/share/vim/vim91/doc/quickfix.txt
/usr/share/vim/vim91/doc/quickref.txt
/usr/share/vim/vim91/doc/quotes.txt
/usr/share/vim/vim91/doc/recover.txt
/usr/share/vim/vim91/doc/remote.txt
/usr/share/vim/vim91/doc/repeat.txt
/usr/share/vim/vim91/doc/rileft.txt
/usr/share/vim/vim91/doc/russian.txt
/usr/share/vim/vim91/doc/scroll.txt
/usr/share/vim/vim91/doc/sign.txt
/usr/share/vim/vim91/doc/spell.txt
/usr/share/vim/vim91/doc/sponsor.txt
/usr/share/vim/vim91/doc/starting.txt
/usr/share/vim/vim91/doc/syntax.txt
/usr/share/vim/vim91/doc/tabpage.txt
/usr/share/vim/vim91/doc/tagsrch.txt
/usr/share/vim/vim91/doc/term.txt
/usr/share/vim/vim91/doc/terminal.txt
/usr/share/vim/vim91/doc/testing.txt
/usr/share/vim/vim91/doc/textprop.txt
/usr/share/vim/vim91/doc/tips.txt
/usr/share/vim/vim91/doc/todo.txt
/usr/share/vim/vim91/doc/uganda.txt
/usr/share/vim/vim91/doc/undo.txt
/usr/share/vim/vim91/doc/userfunc.txt
/usr/share/vim/vim91/doc/usr_01.txt
/usr/share/vim/vim91/doc/usr_02.txt
/usr/share/vim/vim91/doc/usr_03.txt
/usr/share/vim/vim91/doc/usr_04.txt
/usr/share/vim/vim91/doc/usr_05.txt
/usr/share/vim/vim91/doc/usr_06.txt
/usr/share/vim/vim91/doc/usr_07.txt
/usr/share/vim/vim91/doc/usr_08.txt
/usr/share/vim/vim91/doc/usr_09.txt
/usr/share/vim/vim91/doc/usr_10.txt
/usr/share/vim/vim91/doc/usr_11.txt
/usr/share/vim/vim91/doc/usr_12.txt
/usr/share/vim/vim91/doc/usr_20.txt
/usr/share/vim/vim91/doc/usr_21.txt
/usr/share/vim/vim91/doc/usr_22.txt
/usr/share/vim/vim91/doc/usr_23.txt
/usr/share/vim/vim91/doc/usr_24.txt
/usr/share/vim/vim91/doc/usr_25.txt
/usr/share/vim/vim91/doc/usr_26.txt
/usr/share/vim/vim91/doc/usr_27.txt
/usr/share/vim/vim91/doc/usr_28.txt
/usr/share/vim/vim91/doc/usr_29.txt
/usr/share/vim/vim91/doc/usr_30.txt
/usr/share/vim/vim91/doc/usr_31.txt
/usr/share/vim/vim91/doc/usr_32.txt
/usr/share/vim/vim91/doc/usr_40.txt
/usr/share/vim/vim91/doc/usr_41.txt
/usr/share/vim/vim91/doc/usr_42.txt
/usr/share/vim/vim91/doc/usr_43.txt
/usr/share/vim/vim91/doc/usr_44.txt
/usr/share/vim/vim91/doc/usr_45.txt
/usr/share/vim/vim91/doc/usr_50.txt
/usr/share/vim/vim91/doc/usr_51.txt
/usr/share/vim/vim91/doc/usr_52.txt
/usr/share/vim/vim91/doc/usr_90.txt
/usr/share/vim/vim91/doc/usr_toc.txt
/usr/share/vim/vim91/doc/various.txt
/usr/share/vim/vim91/doc/version4.txt
/usr/share/vim/vim91/doc/version5.txt
/usr/share/vim/vim91/doc/version6.txt
/usr/share/vim/vim91/doc/version7.txt
/usr/share/vim/vim91/doc/version8.txt
/usr/share/vim/vim91/doc/version9.txt
/usr/share/vim/vim91/doc/vi_diff.txt
/usr/share/vim/vim91/doc/vim9.txt
/usr/share/vim/vim91/doc/vim9class.txt
/usr/share/vim/vim91/doc/visual.txt
/usr/share/vim/vim91/doc/windows.txt
/usr/share/vim/vim91/doc/workshop.txt
/usr/share/vim/vim91/pack/dist/opt/editorconfig/doc/editorconfig.txt
/usr/share/vim/vim91/pack/dist/opt/matchit/doc/matchit.txt
/usr/share/vim/vim91/tutor/README.ru.utf-8.txt
/usr/share/vlc/lua/http/requests/README.txt
/usr/src/linux-headers-6.17.0-14-generic/scripts/head-object-list.txt
/usr/src/linux-headers-6.17.0-14-generic/scripts/spelling.txt
/usr/src/linux-hwe-6.17-headers-6.17.0-14/arch/sh/include/mach-ecovec24/mach/partner-jet-setup.txt
/usr/src/linux-hwe-6.17-headers-6.17.0-14/arch/sh/include/mach-kfr2r09/mach/partner-jet-setup.txt
/usr/src/linux-hwe-6.17-headers-6.17.0-14/scripts/head-object-list.txt
/usr/src/linux-hwe-6.17-headers-6.17.0-14/scripts/spelling.txt
/var/cache/dictionaries-common/ispell-dicts-list.txt
/var/lib/cloud/instances/iid-datasource-none/cloud-config.txt
/var/lib/cloud/instances/iid-datasource-none/user-data.txt
/var/lib/cloud/instances/iid-datasource-none/vendor-data.txt
/var/lib/cloud/instances/iid-datasource-none/vendor-data2.txt
/var/lib/ieee-data/iab.txt
/var/lib/ieee-data/mam.txt
/var/lib/ieee-data/oui.txt
/var/lib/ieee-data/oui36.txt
/var/lib/systemd/pstore/1772554601/001/dmesg.txt
/var/log/installer/installer-journal.txt
```

## Percobaan 6: Mencari text pada file
Prompt:
```
grep halo *.txt
```
Hasil:
```
myerror.txt:/home/fafiq/halo.txt
```