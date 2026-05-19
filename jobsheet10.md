# Laporan Praktikum Sistem Operasi Pertemuan Ke-11

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

### Praktikum 1 Permissions
#### Prompt
```
mkdir ~/lab-permissions && cd ~/lab-permissions
echo "data rahasia" > secret.txt
echo '#!/bin/bash' > myscript.sh
echo 'echo Hello' >> myscript.sh
ls -la

chmod 600 secret.txt
ls -l secret.txt

chmod 755 myscript.sh
ls -l myscript.sh
./myscript.sh

mkdir shared-dir
chmod g+s shared-dir
ls -ld shared-dir

umask
umask 027
touch testfile-027
ls -l testfile-027
```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ mkdir ~/lab-permissions && cd ~/lab-permissions
echo "data rahasia" > secret.txt
echo '#!/bin/bash' > myscript.sh
echo 'echo Hello' >> myscript.sh
ls -la
total 16
drwxrwxr-x  2 fafiq fafiq 4096 May 19 19:08 .
drwxr-x--- 25 fafiq fafiq 4096 May 19 19:08 ..
-rw-rw-r--  1 fafiq fafiq   23 May 19 19:08 myscript.sh
-rw-rw-r--  1 fafiq fafiq   13 May 19 19:08 secret.txt
fafiq@fafiq-ubuntu:~/lab-permissions$ chmod 600 secret.txt
ls -l secret.txt
-rw------- 1 fafiq fafiq 13 May 19 19:08 secret.txt
fafiq@fafiq-ubuntu:~/lab-permissions$ chmod 755 myscript.sh
ls -l myscript.sh
./myscript.sh
-rwxr-xr-x 1 fafiq fafiq 23 May 19 19:08 myscript.sh
Hello
fafiq@fafiq-ubuntu:~/lab-permissions$ mkdir shared-dir
chmod g+s shared-dir
ls -ld shared-dir
drwxrwsr-x 2 fafiq fafiq 4096 May 19 19:09 shared-dir
fafiq@fafiq-ubuntu:~/lab-permissions$ umask
umask 027
touch testfile-027
ls -l testfile-027
0002
-rw-r----- 1 fafiq fafiq 0 May 19 19:09 testfile-027
fafiq@fafiq-ubuntu:~/lab-permissions$ 
```

#### Analisis Praktikum 1: Permissions

##### Jawaban Pertanyaan Analisis
1. **Mengapa `secret.txt` tidak dapat dibaca oleh group dan others setelah `chmod 600`?**
   ***Analisis:** Notasi oktal `600` berarti memberikan izin `rw-` (read, write) untuk owner, `---` (no permission) untuk group, dan `---` untuk others[cite: 47, 125]. Sistem Linux secara ketat memblokir akses baca/tulis bagi pengguna lain di luar owner karena bit permission untuk group dan others bernilai kosong[cite: 18, 47].

2. **Apa perbedaan arti `600` dan `755` terhadap file yang diuji?**
   * **Analisis:** * `600`: File bersifat privat. Hanya owner yang bisa membaca dan mengubah isi file, sedangkan group dan others tidak bisa melakukan apa pun[cite: 50, 125].
     * `755`: File bersifat publik dan executable[cite: 49]. Owner memiliki hak penuh (`rwx`), sedangkan group dan others hanya bisa membaca (`r`) dan mengeksekusi (`x`) file tersebut sebagai program/skrip[cite: 129].

3. **Setelah `umask 027`, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?**
   * **Analisis:** Nilai umask bertindak sebagai masker (pengurang) izin default[cite: 98]. default, pembuatan file reguler baru berangkat dari nilai dasar `666` (bukan `777` karena file baru tidak langsung diberi izin execute)[cite: 98, 110]. 
     * Kalkulasi: `666` dikurangi `027` menghasilkan permission `640` (`rw-r-----`)[cite: 100]. Oleh karena itu, file baru tidak akan pernah bernilai `777`.

### Praktikum 2 Access Control Lists (ACLs)
#### Prompt
```
mkdir ~/lab-acl && cd ~/lab-acl
echo "Data penting" > confidential.txt
chmod 640 confidential.txt
ls -l confidential.txt
getfacl confidential.txt

setfacl -m u:userA:r confidential.txt
ls -l confidential.txt
getfacl confidential.txt

mkdir shared
setfacl -d -m u:userA:rwx shared
setfacl -d -m u:userB:r-x shared
getfacl shared

touch shared/inherited.txt
getfacl shared/inherited.txt

setfacl -m g:readonly-group:r confidential.txt
setfacl -x u:userA confidential.txt
getfacl confidential.txt
```
#### Hasil
```
fafiq@fafiq-ubuntu:~/lab-permissions$ mkdir ~/lab-acl && cd ~/lab-acl
echo "Data penting" > confidential.txt
chmod 640 confidential.txt
ls -l confidential.txt
getfacl confidential.txt
-rw-r----- 1 fafiq fafiq 13 May 19 19:15 confidential.txt
# file: confidential.txt
# owner: fafiq
# group: fafiq
user::rw-
group::r--
other::---

fafiq@fafiq-ubuntu:~/lab-acl$ setfacl -m u:userA:r confidential.txt
ls -l confidential.txt
getfacl confidential.txt
setfacl: Option -m: Invalid argument near character 3
-rw-r----- 1 fafiq fafiq 13 May 19 19:15 confidential.txt
# file: confidential.txt
# owner: fafiq
# group: fafiq
user::rw-
group::r--
other::---

fafiq@fafiq-ubuntu:~/lab-acl$ mkdir shared
setfacl -d -m u:userA:rwx shared
setfacl -d -m u:userB:r-x shared
getfacl shared
setfacl: Option -m: Invalid argument near character 3
setfacl: Option -m: Invalid argument near character 3
# file: shared
# owner: fafiq
# group: fafiq
user::rwx
group::r-x
other::---

fafiq@fafiq-ubuntu:~/lab-acl$ touch shared/inherited.txt
getfacl shared/inherited.txt
# file: shared/inherited.txt
# owner: fafiq
# group: fafiq
user::rw-
group::r--
other::---

fafiq@fafiq-ubuntu:~/lab-acl$ setfacl -m g:readonly-group:r confidential.txt
setfacl -x u:userA confidential.txt
getfacl confidential.txt
setfacl: Option -m: Invalid argument near character 3
setfacl: Option -x: Invalid argument near character 3
# file: confidential.txt
# owner: fafiq
# group: fafiq
user::rw-
group::r--
other::---

fafiq@fafiq-ubuntu:~/lab-acl$ 
```

#### Analisis Praktikum 2: Access Control Lists (ACLs)
##### Jawaban Pertanyaan Analisis
1. **Mengapa `getfacl confidential.txt` awalnya tidak menampilkan user tertentu?**
   * **Analisis:** Karena file tersebut baru dibuat dan hanya menggunakan model permission Unix klasik standar. Sebelum perintah `setfacl` dijalankan, file belum memiliki metadata aturan akses tambahan (named user atau named group).

2. **Setelah `setfacl -m u:userA:r confidential.txt`, apa perbedaan output `ls -l` dan `getfacl`?**
   * **Analisis:** * Pada output `ls -l`, muncul tanda plus (`+`) di akhir string permission (contoh: `-rw-r--+`), yang menandakan bahwa file tersebut kini memiliki aturan ACL aktif.
     * Pada output `getfacl`, sistem menampilkan baris baru yang lebih granular, yaitu `user:userA:r--`, yang menjelaskan secara spesifik bahwa `userA` memiliki hak akses baca.

3. **Mengapa file `inherited.txt` mewarisi ACL dari direktori `shared`?**
   * **Analisis:** Hal ini terjadi karena pada direktori `shared` telah dikonfigurasi **Default ACL** menggunakan opsi `-d` (contoh: `setfacl -d -m ...`). Di Linux, setiap file atau subdirektori baru yang dibuat di dalam direktori ber-Default ACL otomatis akan mewarisi aturan akses tersebut.

### Praktikum 3 Manajemen User, Group, dan Password Policy
#### Prompt
```
sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
sudo passwd userA
sudo passwd userB

id userA
getent passwd userA

sudo usermod -s /bin/zsh userA
getent passwd userA

sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB
sudo groupadd labgroup
sudo groupadd readonly-group

sudo usermod -aG labgroup,readonly-group userA
sudo usermod -aG readonly-group userB

id userA
id userB
getent group labgroup
getent group readonly-group

sudo chage -l userA
sudo chage -M 90 -m 7 -W 14 userA
sudo chage -I 30 userA
sudo chage -E 2026-12-31 userA
sudo chage -d 0 userA
sudo chage -l userA

sudo usermod -aG sudo userA

id userA

sudo su - userA
sudo apt update  
exit             
```

#### Hasil
```
fafiq-ubuntu% sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
sudo passwd userA
sudo passwd userB
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: password updated successfully
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: password updated successfully
fafiq-ubuntu% id userA
getent passwd userA
uid=1001(userA) gid=1001(userA) groups=1001(userA)
userA:x:1001:1001::/home/userA:/bin/bash
fafiq-ubuntu% sudo usermod -s /bin/zsh userA
getent passwd userA
userA:x:1001:1001::/home/userA:/bin/zsh
fafiq-ubuntu% sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB
userB L 2026-05-19 0 99999 7 -1
userB P 2026-05-19 0 99999 7 -1
fafiq-ubuntu% sudo groupadd labgroup
sudo groupadd readonly-group
fafiq-ubuntu% sudo usermod -aG labgroup,readonly-group userA
sudo usermod -aG readonly-group userB
fafiq-ubuntu% id userA
id userB
getent group labgroup
getent group readonly-group
uid=1001(userA) gid=1001(userA) groups=1001(userA),1003(labgroup),1004(readonly-group)
uid=1002(userB) gid=1002(userB) groups=1002(userB),1004(readonly-group)
labgroup:x:1003:userA
readonly-group:x:1004:userA,userB
fafiq-ubuntu% 

fafiq-ubuntu%                                                                
sudo chage -l userA
sudo chage -M 90 -m 7 -W 14 userA
sudo chage -I 30 userA
sudo chage -E 2026-12-31 userA
sudo chage -d 0 userA
sudo chage -l userA
[sudo] password for fafiq: 
Last password change					: May 19, 2026
Password expires					: never
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
Last password change					: password must be changed
Password expires					: password must be changed
Password inactive					: password must be changed
Account expires						: Dec 31, 2026
Minimum number of days between password change		: 7
Maximum number of days between password change		: 90
Number of days of warning before password expires	: 14
fafiq-ubuntu% 

```

#### Analisis Praktikum 3: Manajemen User dan Group
##### Praktikum 3A: Membuat dan Mengelola User
1. **Apa perbedaan output `id userA` sebelum dan sesudah menambah group?**
   * **Analisis:** Sebelum ditambahkan, `id userA` hanya menampilkan group utamanya (Primary Group) yang biasanya memiliki nama yang sama dengan nama user tersebut. Setelah dijalankan `usermod -aG`, output `id` akan bertambah pada bagian `groups=...` yang menunjukkan daftar Supplementary Groups (group tambahan) yang kini diikuti oleh `userA`.

2. **Bagaimana status `passwd -S userB` berubah saat akun di-lock?**
   * **Analisis:** Saat akun `userB` di-lock dengan perintah `usermod -L`, status pada `passwd -S` akan berubah (biasanya ditandai dengan huruf `L` atau tanda seru `!` di depan hash password di `/etc/shadow`), yang menandakan bahwa enkripsi password tersebut telah dimodifikasi oleh sistem sehingga user tidak bisa login menggunakan password tersebut.

##### Praktikum 3B: Group Management
1. **Apa yang ditampilkan `id userA` vs `groups userA`?**
   * **Analisis:** Perintah `groups userA` hanya menampilkan nama-nama group yang diikuti oleh `userA` dalam format teks ringkas. Sementara itu, `id userA` jauh lebih detail karena menampilkan informasi numerik berupa UID (User ID), GID utama (Primary Group ID), serta seluruh GID dari group tambahan (Supplementary Groups) beserta namanya.

2. **Mengapa `-a` pada `usermod -aG` penting?**
   * **Analisis:** Opsi `-a` berarti *append* (menambahkan). Jika kita lupa menyertakan `-a` dan hanya menggunakan `-G`, sistem Linux akan menghapus user tersebut dari semua group tambahan yang lama dan menggantinya secara total dengan group yang baru ditulis. Ini sangat berbahaya jika user tersebut sebelumnya adalah anggota group `sudo` atau `wheel`.

##### Praktikum 3C: Kebijakan Password dan Aging (`chage`)
1. **Apa fungsi dari perintah `chage -l userA` sebelum dan sesudah konfigurasi?**
   * **Analisis:** Perintah `chage -l` berfungsi untuk menampilkan informasi detail mengenai masa aktif password dan akun pengguna (Password Aging Profile). Sebelum konfigurasi, sistem menampilkan nilai default (biasanya password tidak pernah kedaluwarsa). Sesudah dikonfigurasi, output akan berubah secara spesifik menampilkan tanggal pasti kapan password harus diganti, kapan peringatan muncul, hingga kapan akun akan dinonaktifkan.

2. **Apa dampak dari perintah `chage -d 0 userA` terhadap user yang bersangkutan?**
   * **Analisis:** Angka `0` pada opsi `-d` (*last day*) memanipulasi sistem agar menganggap bahwa `userA` terakhir kali mengganti password pada tanggal 1 Januari 1970 (Epoch Unix). Karena sistem menganggap password tersebut sudah sangat usang, `userA` akan dipaksa secara interaktif untuk langsung membuat password baru sesaat setelah berhasil melakukan login berikutnya.

##### Praktikum 3D: Delegasi Hak Akses (`sudo`)
1. **Mengapa memasukkan `userA` ke group `sudo` membuatnya bisa menjalankan perintah administratif?**
   * **Analisis:** Di dalam distribusi Ubuntu, file konfigurasi `/etc/sudoers` secara default telah mengatur bahwa setiap pengguna yang menjadi anggota dari group bernama `sudo` akan diberikan privilese penuh untuk menjalankan perintah apa pun atas nama superuser (root). Oleh karena itu, perintah `usermod -aG sudo userA` secara otomatis mendelegasikan hak administratif tersebut kepada `userA`.

2. **Apakah ada perbedaan keamanan antara membagikan password `root` langsung dengan menggunakan mekanisme `sudo`?**
   * **Analisis:** Menggunakan `sudo` jauh lebih aman karena pengguna (`userA`) cukup menggunakan password milik akunnya sendiri untuk melakukan tugas administratif, sehingga password `root` yang asli tetap rahasia. Selain itu, setiap aktivitas yang dijalankan melalui perintah `sudo` akan dicatat secara mendalam di dalam log sistem (`/var/log/auth.log`), memudahkan proses audit dan pelacakan tindakan jika terjadi kesalahan sistem.

### Praktikum 4 Konfigurasi Sudo
#### Prompt
```
sudo usermod -aG sudo userA
id userA
sudo su - userA
sudo apt update
exit

sudo sed -i '/ \/ / s/defaults/defaults,usrquota,grpquota/' /etc/fstab
sudo mount -o remount /
sudo quotacheck -cumvg /
sudo quotaon -avug
sudo edquota -u userA
sudo quota -v userA
sudo repquota -s /
```

#### Hasil
```
fafiq-ubuntu% sudo usermod -aG sudo userA
[sudo] password for userA: 
fafiq-ubuntu% id userA
uid=1001(userA) gid=1001(userA) groups=1001(userA),27(sudo),1003(labgroup),1004(readonly-group)
fafiq-ubuntu% sudo su - userA
sudo apt update
fafiq-ubuntu% 

fafiq-ubuntu% sudo sed -i '/ \/ / s/defaults/defaults,usrquota,grpquota/' /etc/fstab
fafiq-ubuntu% sudo mount -o remount /
mount: (hint) your fstab has been modified, but systemd still uses
       the old version; use 'systemctl daemon-reload' to reload.
fafiq-ubuntu% systemctl daemon-reload
fafiq-ubuntu% sudo mount -o remount /
fafiq-ubuntu% sudo quotacheck -cumvg /
quotacheck: Your kernel probably supports ext4 quota feature but you are using external quota files. Please switch your filesystem to use ext4 quota feature as external quota files on ext4 are deprecated.
quotacheck: Quota for users is enabled on mountpoint / so quotacheck might damage the file.
Please turn quotas off or use -f to force checking.
fafiq-ubuntu% sudo quotacheck -f -cumvg /
quotacheck: Your kernel probably supports ext4 quota feature but you are using external quota files. Please switch your filesystem to use ext4 quota feature as external quota files on ext4 are deprecated.
quotacheck: Scanning /dev/nvme0n1p3 [/] done
quotacheck: Checked 18712 directories and 200355 files
fafiq-ubuntu% sudo quotaon -avug
quotaon: Your kernel probably supports ext4 quota feature but you are using external quota files. Please switch your filesystem to use ext4 quota feature as external quota files on ext4 are deprecated.
quotaon: using //aquota.group on /dev/nvme0n1p3 [/]: Device or resource busy
quotaon: using //aquota.user on /dev/nvme0n1p3 [/]: Device or resource busy
fafiq-ubuntu% sudo edquota -u userA
fafiq-ubuntu%                      
sudo repquota -s /
*** Report for user quotas on device /dev/nvme0n1p3
Block grace time: 7days; Inode grace time: 7days
                        Space limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --  13593M      0K      0K           182k     0     0       
man       --   2140K      0K      0K            175     0     0       
_apt      --     32K      0K      0K              6     0     0       
systemd-network --     16K      0K      0K              4     0     0       
systemd-timesync --      4K      0K      0K              2     0     0       
messagebus --      4K      0K      0K              1     0     0       
syslog    --  32624K      0K      0K              5     0     0       
uuidd     --      4K      0K      0K              1     0     0       
tss       --      4K      0K      0K              1     0     0       
dnsmasq   --      4K      0K      0K              1     0     0       
speech-dispatcher --     12K      0K      0K              6     0     0       
fwupd-refresh --      4K      0K      0K              1     0     0       
saned     --      4K      0K      0K              1     0     0       
geoclue   --      4K      0K      0K              1     0     0       
cups-browsed --      8K      0K      0K              2     0     0       
hplip     --      4K      0K      0K              1     0     0       
gnome-remote-desktop --     24K      0K      0K              7     0     0       
colord    --     64K      0K      0K              7     0     0       
gdm       --   3100K      0K      0K            146     0     0       
nm-openvpn --      4K      0K      0K              1     0     0       
fafiq     --   3934M      0K      0K          37025     0     0       
userA     --     72K      0K      0K              7     0     0       
userB     --     16K      0K      0K              4     0     0       


fafiq-ubuntu% 
```

#### Analisis Praktikum 4: Manajemen Delegasi Akses dan Disk Quota

##### Praktikum 4A: Pengelolaan Hak Sudo
1. **Mengapa memasukkan `userA` ke group `sudo` membuatnya bisa menjalankan perintah administratif?**
   * **Analisis:** Di dalam konfigurasi bawaan sistem operasi Ubuntu, berkas pengatur keamanan `/etc/sudoers` telah menetapkan aturan secara global bahwa setiap pengguna yang terdaftar sebagai anggota kelompok (`group`) `sudo` akan diberikan pelimpahan wewenang penuh untuk mengeksekusi seluruh perintah setingkat *superuser* atau root. Oleh sebab itu, memasukkan nama `userA` ke dalam kelompok tersebut secara otomatis mengaktifkan hak istimewa administratifnya.

2. **Apa kegunaan instruksi `sudo su - userA` dalam pengujian hak akses tersebut?**
   * **Analisis:** Instruksi ini berfungsi untuk mensimulasikan perpindahan sesi login terminal dari akun utama menuju lingkungan kerja milik `userA` secara menyeluruh, termasuk memuat seluruh berkas profil konfigurasi shell miliknya. Metode pengujian ini sangat krusial digunakan oleh administrator sistem untuk memvalidasi bahwa hak akses ataupun pembatasan yang baru saja diterapkan telah bekerja dengan semestinya pada akun pengguna target.

##### Praktikum 4B: Manajemen Disk Quota
1. **Mengapa muncul pesan eror `quotacheck: Mountpoint (or device) / not found or has no quota enabled` saat pertama kali dijalankan?**
   * **Analisis:** Pesan eror tersebut muncul karena kernel Linux mendeteksi bahwa sistem berkas pada direktori root (`/`) belum mengaktifkan opsi pembatasan kapasitas. Agar fitur ini berfungsi, parameter `usrquota` (untuk user) dan `grpquota` (untuk group) harus didaftarkan terlebih dahulu pada tabel konfigurasi sistem berkas di `/etc/fstab`, diikuti dengan melakukan proses muat ulang (*remount*) sistem berkas terkait.

2. **Apa perbedaan mendasar antara batasan berjenis *Soft Limit* dan *Hard Limit* pada konfigurasi berkas saat mengedit `edquota`?**
   * **Analisis:** * *Soft Limit* bertindak sebagai batas ambang peringatan awal, di mana pengguna masih diperbolehkan untuk melewati kapasitas penyimpanan tersebut untuk sementara waktu dalam masa tenggang tertentu (*grace period*).
     * *Hard Limit* bertindak sebagai batas maksimal absolut sistem, di mana pengguna sama sekali tidak akan diizinkan untuk menulis data baru ke dalam ruang penyimpanan apabila kapasitasnya telah menyentuh angka batasan tersebut.

### Praktikum 5 Perintah Bash
#### Prompt
```
id userA
id userB
sudo userdel -r userA
sudo userdel -r userB
sudo groupdel labgroup
sudo groupdel readonly-group
```

#### Hasil
```
fafiq-ubuntu% id userA
id userB
sudo userdel -r userA
sudo userdel -r userB
sudo groupdel labgroup
sudo groupdel readonly-group
uid=1001(userA) gid=1001(userA) groups=1001(userA),27(sudo),1003(labgroup),1004(readonly-group)
uid=1002(userB) gid=1002(userB) groups=1002(userB),1004(readonly-group)
userdel: user userA is currently used by process 14990
userdel: userB mail spool (/var/mail/userB) not found
fafiq-ubuntu% 
```

#### Analisis Praktikum 5: Audit Akhir dan Pembersihan Sistem (Cleanup)

##### Praktikum 5A: Proses Deaktivasi dan Keamanan Pasca-Lab
1. **Mengapa penghapusan user uji coba menggunakan opsi `userdel -r` sangat direkomendasikan setelah praktikum selesai?**
   * **Analisis:** Opsi `-r` (*remove*) memastikan bahwa sistem tidak hanya menghapus data akun dari berkas `/etc/passwd`, melainkan juga menghapus direktori rumah (*home directory*) `/home/userA` beserta seluruh berkas sementara di dalamnya secara permanen. Jika opsi ini diabaikan, direktori usang akan tertinggal di dalam sistem penyimpanan (*orphan files*), yang berpotensi memboroskan kapasitas ruang disk dan menimbulkan celah keamanan di kemudian hari.

2. **Apa yang terjadi pada file-file yang pernah dibuat oleh `userA` di luar home directory (misal di `/tmp` atau direktori bersama) setelah akunnya dihapus?**
   * **Analisis:** Berkas-berkas tersebut akan tetap ada di dalam sistem berkas, namun kepemilikannya (*ownership*) akan berubah. Karena nama `userA` sudah tidak terdaftar, sistem Linux akan menampilkan pemilik file tersebut dalam bentuk angka UID numeriknya saja (misalnya `1001`). Berkas tanpa pemilik yang valid ini disebut sebagai berkas yatim piatu (*orphaned files*) dan harus dibersihkan secara manual oleh administrator menggunakan perintah `find / -nouser` demi menjaga kebersihan lingkungan sistem.

### Latihan A
#### Prompt
```
find / -perm -4000 -type f 2>/dev/null
find / -perm -0002 -type d 2>/dev/null
sudo mkdir -p /srv/webapp/
sudo groupadd webapp-team
sudo chown root:webapp-team /srv/webapp/
sudo chmod 2770 /srv/webapp/
sudo setfacl -d -m u:deploy:r /srv/webapp/
sudo setfacl -m u:deploy:r /srv/webapp/
```

#### Hasil
```
fafiq-ubuntu% find / -perm -4000 -type f 2>/dev/null
find / -perm -0002 -type d 2>/dev/null
sudo mkdir -p /srv/webapp/
sudo groupadd webapp-team
sudo chown root:webapp-team /srv/webapp/
sudo chmod 2770 /srv/webapp/
sudo setfacl -d -m u:deploy:r /srv/webapp/
sudo setfacl -m u:deploy:r /srv/webapp/
/usr/sbin/pppd
/usr/bin/passwd
/usr/bin/newgrp
/usr/bin/umount
/usr/bin/pkexec
/usr/bin/sudo
/usr/bin/su
/usr/bin/chfn
/usr/bin/fusermount3
/usr/bin/chsh
/usr/bin/gpasswd
/usr/bin/mount
/usr/share/code/chrome-sandbox
/usr/lib/polkit-1/polkit-agent-helper-1
/usr/lib/xorg/Xorg.wrap
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/openssh/ssh-keysign
/snap/chromium/3411/usr/lib/chromium-browser/chrome-sandbox
/snap/core24/1643/usr/bin/chfn
/snap/core24/1643/usr/bin/chsh
/snap/core24/1643/usr/bin/gpasswd
/snap/core24/1643/usr/bin/mount
/snap/core24/1643/usr/bin/newgrp
/snap/core24/1643/usr/bin/passwd
/snap/core24/1643/usr/bin/su
/snap/core24/1643/usr/bin/sudo
/snap/core24/1643/usr/bin/umount
/snap/core24/1643/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core24/1643/usr/lib/openssh/ssh-keysign
/snap/core24/1643/usr/lib/polkit-1/polkit-agent-helper-1
/snap/core24/1587/usr/bin/chfn
/snap/core24/1587/usr/bin/chsh
/snap/core24/1587/usr/bin/gpasswd
/snap/core24/1587/usr/bin/mount
/snap/core24/1587/usr/bin/newgrp
/snap/core24/1587/usr/bin/passwd
/snap/core24/1587/usr/bin/su
/snap/core24/1587/usr/bin/sudo
/snap/core24/1587/usr/bin/umount
/snap/core24/1587/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core24/1587/usr/lib/openssh/ssh-keysign
/snap/core24/1587/usr/lib/polkit-1/polkit-agent-helper-1
/snap/core22/2292/usr/bin/chfn
/snap/core22/2292/usr/bin/chsh
/snap/core22/2292/usr/bin/gpasswd
/snap/core22/2292/usr/bin/mount
/snap/core22/2292/usr/bin/newgrp
/snap/core22/2292/usr/bin/passwd
/snap/core22/2292/usr/bin/su
/snap/core22/2292/usr/bin/sudo
/snap/core22/2292/usr/bin/umount
/snap/core22/2292/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core22/2292/usr/lib/openssh/ssh-keysign
/snap/core22/2292/usr/libexec/polkit-agent-helper-1
/snap/core22/2411/usr/bin/chfn
/snap/core22/2411/usr/bin/chsh
/snap/core22/2411/usr/bin/gpasswd
/snap/core22/2411/usr/bin/mount
/snap/core22/2411/usr/bin/newgrp
/snap/core22/2411/usr/bin/passwd
/snap/core22/2411/usr/bin/su
/snap/core22/2411/usr/bin/sudo
/snap/core22/2411/usr/bin/umount
/snap/core22/2411/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core22/2411/usr/lib/openssh/ssh-keysign
/snap/core22/2411/usr/libexec/polkit-agent-helper-1
/snap/core24/1643/run/lock
/snap/core24/1643/tmp
/snap/core24/1643/var/tmp
/snap/core24/1587/run/lock
/snap/core24/1587/tmp
/snap/core24/1587/var/tmp
/snap/core22/2292/run/lock
/snap/core22/2292/tmp
/snap/core22/2292/var/tmp
/snap/core22/2411/run/lock
/snap/core22/2411/tmp
/snap/core22/2411/var/tmp
/dev/mqueue
/dev/shm
/run/lock
/tmp
/tmp/.font-unix
/tmp/.ICE-unix
/tmp/.X11-unix
/tmp/.XIM-unix
/var/crash
/var/snap/cups/1183/tmp
/var/tmp
/var/lib/BrlAPI
/var/metrics
setfacl: Option -m: Invalid argument near character 3
setfacl: Option -m: Invalid argument near character 3
fafiq-ubuntu% 
```

### Latihan B
#### Prompt
```
sudo useradd -m -s /bin/bash intern
sudo usermod -aG labgroup intern
sudo chage -M 45 -W 7 intern
echo "intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *" | sudo tee /etc/sudoers.d/intern-status
sudo edquota -u intern
```

#### Hasil
```
fafiq-ubuntu% sudo useradd -m -s /bin/bash intern
sudo usermod -aG labgroup intern
sudo chage -M 45 -W 7 intern
echo "intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *" | sudo tee /etc/sudoers.d/intern-status
sudo edquota -u intern
usermod: group 'labgroup' does not exist
intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *
fafiq-ubuntu% sudo groupadd labgroup
sudo usermod -aG labgroup intern
id intern
uid=1003(intern) gid=1004(intern) groups=1004(intern),1005(labgroup)
fafiq-ubuntu% sudo useradd -m -s /bin/bash intern
sudo usermod -aG labgroup intern
sudo chage -M 45 -W 7 intern
echo "intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *" | sudo tee /etc/sudoers.d/intern-status
sudo edquota -u intern
useradd: user 'intern' already exists
intern ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *
fafiq-ubuntu% 
```