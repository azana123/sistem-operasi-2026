# Laporan Praktikum Sistem Operasi Pertemuan Ke-9

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

### Praktikum 7.1 Script Pertama: Laporan Sistem
#### Prompt
```
mkdir -p ~/praktikum-os/week09/{scripts,logs,data}
cd ~/praktikum-os/week09/scripts

nano laporan-sistem.sh

#!/bin/bash
# Script: laporan-sistem.sh

echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam     : $(date '+%H:%M:%S')"
echo "Hostname: $(hostname)"
echo "User    : $(whoami)"
echo "CPU core: $(nproc)"
echo "RAM bebas: $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk /  : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "================================"

chmod +x laporan-sistem.sh
./laporan-sistem.sh
```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ mkdir -p ~/praktikum-os/week09/{scripts,logs,data}
cd ~/praktikum-os/week09/scripts
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano laporan-sistem.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x laporan-sistem.sh
./laporan-sistem.sh
================================
LAPORAN SISTEM
================================
Tanggal : Friday, 01 May 2026
Jam     : 16:55:49
Hostname: fafiq-ubuntu
User    : fafiq
CPU core: 16
RAM bebas: 7.9Gi
Disk /  : 17% terpakai
================================
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

#### Latihan 9.1
#### Prompt
```
nano laporan-sistem.sh

#!/bin/bash

FILE="laporan-$(date +%F).txt"

{
echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam     : $(date '+%H:%M:%S')"
echo "Hostname: $(hostname)"
echo "User    : $(whoami)"
echo "CPU core: $(nproc)"
echo "RAM bebas: $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk /  : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "================================"
} | tee "$FILE"

./laporan-sistem.sh

ls
cat laporan-$(date +%F).txt
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano laporan-sistem.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./laporan-sistem.sh
================================
LAPORAN SISTEM
================================
Tanggal : Friday, 01 May 2026
Jam     : 16:57:18
Hostname: fafiq-ubuntu
User    : fafiq
CPU core: 16
RAM bebas: 7.9Gi
Disk /  : 17% terpakai
================================
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ls
cat laporan-$(date +%F).txt
laporan-2026-05-01.txt  laporan-sistem.sh
================================
LAPORAN SISTEM
================================
Tanggal : Friday, 01 May 2026
Jam     : 16:57:18
Hostname: fafiq-ubuntu
User    : fafiq
CPU core: 16
RAM bebas: 7.9Gi
Disk /  : 17% terpakai
================================
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Praktikum 7.2 Script Info Sistem dengan Argumen####
#### Prompt
```
nano ~/praktikum-os/week09/scripts/info-sistem.sh

#!/bin/bash
# Penggunaan: ./info-sistem.sh [nama-admin] [batas-disk]

ADMIN=${1:-"Tidak dikenal"}
BATAS=${2:-80}

TANGGAL=$(date '+%F %T')
DISK_PERSEN=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Admin   : $ADMIN"
echo "Tanggal : $TANGGAL"
echo "Disk /  : ${DISK_PERSEN}% terpakai"
echo "Batas   : ${BATAS}%"

if [ "$DISK_PERSEN" -gt "$BATAS" ]; then
    echo "STATUS  : PERINGATAN - disk melebihi batas!"
else
    SISA=$((BATAS - DISK_PERSEN))
    echo "STATUS  : Normal (sisa toleransi ${SISA}%)"
fi

chmod +x ~/praktikum-os/week09/scripts/info-sistem.sh

./info-sistem.sh

./info-sistem.sh "Dian" 50

./info-sistem.sh "Dian" 10
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/info-sistem.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/info-sistem.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./info-sistem.sh
Admin   : Tidak dikenal
Tanggal : 2026-05-01 17:05:06
Disk /  : 17% terpakai
Batas   : 80%
STATUS  : Normal (sisa toleransi 63%)
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./info-sistem.sh "Dian" 50
Admin   : Dian
Tanggal : 2026-05-01 17:05:11
Disk /  : 17% terpakai
Batas   : 50%
STATUS  : Normal (sisa toleransi 33%)
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./info-sistem.sh "Dian" 10
Admin   : Dian
Tanggal : 2026-05-01 17:05:17
Disk /  : 17% terpakai
Batas   : 10%
STATUS  : PERINGATAN - disk melebihi batas!
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

#### Latihan 9.2
#### Prompt
```
nano ~/praktikum-os/week09/scripts/kalkulator.sh

#!/bin/bash
# Penggunaan: ./kalkulator.sh <angka1> <operator> <angka2>

if [ $# -ne 3 ]; then
    echo "Penggunaan: $0 <angka1> <operator> <angka2>"
    exit 1
fi

A=$1
OP=$2
B=$3

case $OP in
    +) HASIL=$((A + B)) ;;
    -) HASIL=$((A - B)) ;;
    \*) HASIL=$((A * B)) ;;
    /) 
        if [ "$B" -eq 0 ]; then
            echo "Error: pembagian dengan nol"
            exit 1
        fi
        HASIL=$((A / B)) ;;
    *)
        echo "Operator tidak valid. Gunakan + - * /"
        exit 1
        ;;
esac

echo "Hasil: $HASIL"

chmod +x ~/praktikum-os/week09/scripts/kalkulator.sh

./kalkulator.sh 20 + 5
./kalkulator.sh 10 \* 3
./kalkulator.sh 10 / 0
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/kalkulator.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/kalkulator.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./kalkulator.sh 20 + 5
./kalkulator.sh 10 \* 3
./kalkulator.sh 10 / 0
Hasil: 25
Hasil: 30
Error: pembagian dengan nol
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Praktikum 7.3 Script Grading dan Menu Interaktif
#### Prompt
```
nano ~/praktikum-os/week09/scripts/grading-batch.sh

#!/bin/bash
# Script: grading-batch.sh

MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

echo "=== HASIL GRADING ==="

for ENTRI in "${MAHASISWA[@]}"; do
    NAMA=$(echo "$ENTRI" | cut -d: -f1)
    NILAI=$(echo "$ENTRI" | cut -d: -f2)

    if [ "$NILAI" -ge 85 ]; then
        GRADE="A"
    elif [ "$NILAI" -ge 75 ]; then
        GRADE="B"
    elif [ "$NILAI" -ge 65 ]; then
        GRADE="C"
    elif [ "$NILAI" -ge 55 ]; then
        GRADE="D"
    else
        GRADE="E"
    fi

    printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"
done

echo "====================="

chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
./grading-batch.sh

#!/bin/bash
# Menu interaktif sistem

while true; do
    echo ""
    echo "===== MENU MONITOR ====="
    echo "1) Info disk"
    echo "2) Info memori"
    echo "3) Proses teratas"
    echo "4) Keluar"
    echo -n "Pilih [1-4]: "
    
    read PILIHAN

    case $PILIHAN in
        1) df -h ;;
        2) free -h ;;
        3) ps aux --sort=-%cpu | head -6 ;;
        4) echo "Sampai jumpa!"; exit 0 ;;
        *) echo "Pilihan tidak valid." ;;
    esac
done

chmod +x ~/praktikum-os/week09/scripts/menu-sistem.sh
./menu-sistem.sh
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/grading-batch.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
./grading-batch.sh
=== HASIL GRADING ===
Andi        92 A
Budi        73 C
Citra       55 D
Deni        80 B
Eka         45 E
=====================
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/menu-sistem.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/menu-sistem.sh
./menu-sistem.sh

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 1
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.5G  2.9M  1.5G   1% /run
/dev/nvme0n1p3   94G   15G   75G  17% /
tmpfs           7.5G   23M  7.5G   1% /dev/shm
tmpfs           5.0M   16K  5.0M   1% /run/lock
efivarfs        148K   72K   72K  51% /sys/firmware/efi/efivars
/dev/nvme0n1p1 1022M  111M  912M  11% /boot/efi
tmpfs           1.5G  132K  1.5G   1% /run/user/1000

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 2
               total        used        free      shared  buff/cache   available
Mem:            14Gi       4.3Gi       7.9Gi       144Mi       2.8Gi        10Gi
Swap:          4.0Gi          0B       4.0Gi

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 3
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
fafiq       6327  4.6  2.5 1465102044 396156 ?   Sl   16:36   1:37 /usr/share/code/code --type=zygote
fafiq       2901  4.6  2.6 5828148 409228 ?      Ssl  16:27   2:00 /usr/bin/gnome-shell
fafiq       3801  4.2  4.5 12322540 714272 ?     Sl   16:28   1:47 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       5358  2.7  3.0 3052636 480940 ?      Sl   16:31   1:06 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:45068 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {79700def-beb1-4e2d-b7de-3e829ba30fb2} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 11 tab
fafiq       6264  1.4  1.5 51381156 243008 ?     Sl   16:36   0:29 /usr/share/code/code --type=zygote --no-zygote-sandbox

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 4
Sampai jumpa!
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 

```
#### Latihan 9.3
#### Prompt
```
nano ~/praktikum-os/week09/scripts/grading-batch.sh

#!/bin/bash
# Script: grading-batch.sh

MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

echo "=== HASIL GRADING ==="

A=0
B=0
C=0
D=0
E=0

for ENTRI in "${MAHASISWA[@]}"; do
    NAMA=$(echo "$ENTRI" | cut -d: -f1)
    NILAI=$(echo "$ENTRI" | cut -d: -f2)

    if [ "$NILAI" -ge 85 ]; then
        GRADE="A"
    elif [ "$NILAI" -ge 75 ]; then
        GRADE="B"
    elif [ "$NILAI" -ge 65 ]; then
        GRADE="C"
    elif [ "$NILAI" -ge 55 ]; then
        GRADE="D"
    else
        GRADE="E"
    fi

    case $GRADE in
         A) ((A++)) ;;
         B) ((B++)) ;;
         C) ((C++)) ;;
         D) ((D++)) ;;
         E) ((E++)) ;;
    esac
    printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"
done

echo "====================="
echo ""
echo "=== RINGKASAN ==="
echo "A: $A"
echo "B: $B"
echo "C: $C"
echo "D: $D"
echo "E: $E"

./grading-batch.sh
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/grading-batch.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/grading-batch.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./grading-batch.sh
=== HASIL GRADING ===
Andi        92 A
Budi        73 C
Citra       55 D
Deni        80 B
Eka         45 E
=====================

=== RINGKASAN ===
A: 1
B: 1
C: 1
D: 1
E: 1
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Praktikum 7.4 Library Fungsi Validasi
#### Prompt
```
nano ~/praktikum-os/week09/scripts/lib-validasi.sh

#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
    [[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
    [ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
    echo "ERROR: $1" >&2
    exit 1
}

info() {
    echo "[INFO] $1"
}

sukses() {
    echo "[OK] $1"
}


nano ~/praktikum-os/week09/scripts/pakai-library.sh

#!/bin/bash
# pakai-library.sh

# load library (seperti import)
source ~/praktikum-os/week09/scripts/lib-validasi.sh

ANGKA=$1
FILE=$2

# validasi input kosong
[ -z "$ANGKA" ] || [ -z "$FILE" ] && \
error_exit "Penggunaan: $0 <angka> <path-file>"

# cek angka
if adalah_angka "$ANGKA"; then
    sukses "Input '$ANGKA' adalah angka valid"
else
    error_exit "'$ANGKA' bukan angka"
fi

# cek file
if file_bisa_dibaca "$FILE"; then
    sukses "File '$FILE' bisa dibaca"
    info "Jumlah baris: $(wc -l < "$FILE")"
else
    error_exit "File '$FILE' tidak ada atau tidak bisa dibaca"
fi

chmod +x ~/praktikum-os/week09/scripts/pakai-library.sh

./pakai-library.sh 42 /etc/hostname
./pakai-library.sh abc /etc/hostname
./pakai-library.sh 42 tidak-ada.txt
./pakai-library.sh
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/lib-validasi.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/pakai-library.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/pakai-library.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 /etc/hostname
[OK] Input '42' adalah angka valid
[OK] File '/etc/hostname' bisa dibaca
[INFO] Jumlah baris: 1
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./pakai-library.sh abc /etc/hostname
ERROR: 'abc' bukan angka
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 tidak-ada.txt
[OK] Input '42' adalah angka valid
ERROR: File 'tidak-ada.txt' tidak ada atau tidak bisa dibaca
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./pakai-library.sh
ERROR: Penggunaan: ./pakai-library.sh <angka> <path-file>
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

#### Latihan 9.4
#### Prompt
```
nano ~/praktikum-os/week09/scripts/lib-validasi.sh

#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
    [[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
    [ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
    echo "ERROR: $1" >&2
    exit 1
}

info() {
    echo "[INFO] $1"
}

sukses() {
    echo "[OK] $1"
}

konfirmasi() {
    read -p "$1 (Y/N): " JAWABAN
    case "$JAWABAN" in
        Y|y) return 0 ;;
        *) return 1 ;;
    esac
}

nano ~/praktikum-os/week09/scripts/hapus-file.sh

#!/bin/bash

source ~/praktikum-os/week09/scripts/lib-validasi.sh

FILE=$1

[ -z "$FILE" ] && error_exit "Masukkan nama file"

if konfirmasi "Yakin ingin menghapus $FILE?"; then
    rm -f "$FILE"
    sukses "File dihapus"
else
    info "Dibatalkan"
fi

chmod +x hapus-file.sh
./hapus-file.sh contoh.txt
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/lib-validasi.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/lib-validasi.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/hapus-file.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x hapus-file.sh
./hapus-file.sh contoh.txt
Yakin ingin menghapus contoh.txt? (Y/N): y
[OK] File dihapus
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Praktikum 7.5 Script Backup dengan Opsi
#### Prompt
```
nano ~/praktikum-os/week09/scripts/backup-data.sh

#!/bin/bash
# Penggunaan: ./backup-data.sh [-v] [-c] [-l logfile] <sumber> <tujuan>

VERBOSE=false
COMPRESS=false
LOG_FILE=""

# parsing opsi
while getopts "vcl:" OPSI; do
    case $OPSI in
        v) VERBOSE=true ;;
        c) COMPRESS=true ;;
        l) LOG_FILE="$OPTARG" ;;
        *) echo "Penggunaan: $0 [-v] [-c] [-l logfile] <sumber> <tujuan>"; exit 1 ;;
    esac
done

shift $((OPTIND - 1))

SUMBER=$1
TUJUAN=$2

# fungsi logging
log() {
    local MSG="[ $(date '+%T') ] $1"
    echo "$MSG"
    [ -n "$LOG_FILE" ] && echo "$MSG" >> "$LOG_FILE"
}

# validasi input
[ -z "$SUMBER" ] || [ -z "$TUJUAN" ] && {
    echo "ERROR: sumber dan tujuan wajib diisi"
    exit 1
}

[ ! -d "$SUMBER" ] && {
    log "ERROR: $SUMBER tidak ada"
    exit 2
}

mkdir -p "$TUJUAN"

TANGGAL=$(date '+%F-%H%M%S')

[ "$VERBOSE" = true ] && log "Sumber: $SUMBER | Tujuan: $TUJUAN"

if [ "$COMPRESS" = true ]; then
    ARSIP="$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL.tar.gz"
    tar -czf "$ARSIP" -C "$(dirname "$SUMBER")" "$(basename "$SUMBER")"
    log "Arsip: $ARSIP ($(du -sh "$ARSIP" | cut -f1))"
else
    cp -r "$SUMBER" "$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL"
    log "Backup selesai."
fi

./backup-data.sh ~/praktikum-os/week09/data ~/praktikum-os/week09/logs

./backup-data.sh -v -c -l ../logs/backup.log \
~/praktikum-os/week09/data \
~/praktikum-os/week09/logs

cat ../logs/backup.log
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/backup-data.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/backup-data.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ cd ~/praktikum-os/week09/scripts
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./backup-data.sh ~/praktikum-os/week09/data ~/praktikum-os/week09/logs
[ 17:27:32 ] Backup selesai.
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./backup-data.sh -v -c -l ../logs/backup.log \
~/praktikum-os/week09/data \
~/praktikum-os/week09/logs
[ 17:27:47 ] Sumber: /home/fafiq/praktikum-os/week09/data | Tujuan: /home/fafiq/praktikum-os/week09/logs
[ 17:27:47 ] Arsip: /home/fafiq/praktikum-os/week09/logs/backup-data-2026-05-01-172747.tar.gz (4.0K)
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ cat ../logs/backup.log
[ 17:27:47 ] Sumber: /home/fafiq/praktikum-os/week09/data | Tujuan: /home/fafiq/praktikum-os/week09/logs
[ 17:27:47 ] Arsip: /home/fafiq/praktikum-os/week09/logs/backup-data-2026-05-01-172747.tar.gz (4.0K)
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Praktikum 7.6 Debugging Script
#### Prompt
```
nano ~/praktikum-os/week09/scripts/debug-latihan.sh

#!/bin/bash
# Script: debug-latihan.sh
# Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>

DIREKTORI=$1
BATAS=$2

if [ $# -ne 2 ]; then
    echo "Penggunaan: $0 <direktori> <batas-MB>"
    exit 1
fi

UKURAN=$(du -sm "$DIREKTORI" | cut -f1)

echo "Direktori : $DIREKTORI"
echo "Ukuran    : ${UKURAN} MB"
echo "Batas     : ${BATAS} MB"

if [ "$UKURAN" -gt "$BATAS" ]; then
    echo "PERINGATAN: Ukuran melebihi batas!"
    echo "Kelebihan : $((UKURAN - BATAS)) MB"
else
    echo "Status: Normal (sisa: $((BATAS - UKURAN)) MB)"
fi

chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh
cd ~/praktikum-os/week09/scripts

bash -n debug-latihan.sh && echo "Sintaks OK"

bash -x debug-latihan.sh /etc 10

./debug-latihan.sh /var 50

./debug-latihan.sh 
Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/debug-latihan.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh
cd ~/praktikum-os/week09/scripts
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ bash -n debug-latihan.sh && echo "Sintaks OK"
Sintaks OK
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ bash -x debug-latihan.sh /etc 10
+ DIREKTORI=/etc
+ BATAS=10
+ '[' 2 -ne 2 ']'
++ du -sm /etc
++ cut -f1
du: cannot read directory '/etc/ssl/private': Permission denied
du: cannot read directory '/etc/polkit-1/rules.d': Permission denied
du: cannot read directory '/etc/credstore': Permission denied
du: cannot read directory '/etc/sssd': Permission denied
du: cannot read directory '/etc/credstore.encrypted': Permission denied
du: cannot read directory '/etc/cups/ssl': Permission denied
+ UKURAN=12
+ echo 'Direktori : /etc'
Direktori : /etc
+ echo 'Ukuran    : 12 MB'
Ukuran    : 12 MB
+ echo 'Batas     : 10 MB'
Batas     : 10 MB
+ '[' 12 -gt 10 ']'
+ echo 'PERINGATAN: Ukuran melebihi batas!'
PERINGATAN: Ukuran melebihi batas!
+ echo 'Kelebihan : 2 MB'
Kelebihan : 2 MB
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./debug-latihan.sh /var 50
du: cannot read directory '/var/spool/rsyslog': Permission denied
du: cannot read directory '/var/spool/cron/crontabs': Permission denied
du: cannot read directory '/var/spool/cups': Permission denied
du: cannot read directory '/var/cache/private': Permission denied
du: cannot read directory '/var/cache/apparmor/8eeb6286.0': Permission denied
du: cannot read directory '/var/cache/apparmor/70b6ca72.0': Permission denied
du: cannot read directory '/var/cache/apt/archives/partial': Permission denied
du: cannot read directory '/var/cache/ldconfig': Permission denied
du: cannot read directory '/var/cache/cups': Permission denied
du: cannot read directory '/var/snap/cups/1183/var/spool': Permission denied
du: cannot read directory '/var/snap/cups/1183/var/cache': Permission denied
du: cannot read directory '/var/snap/cups/1183/var/run/certs': Permission denied
du: cannot read directory '/var/snap/cups/common/etc/cups/ssl': Permission denied
du: cannot read directory '/var/log/speech-dispatcher': Permission denied
du: cannot read directory '/var/log/private': Permission denied
du: cannot read directory '/var/log/sssd': Permission denied
du: cannot read directory '/var/log/gdm3': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-switcheroo-control.service-3naYfx': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-systemd-logind.service-uk1BzJ': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-fwupd.service-WHng85': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-systemd-resolved.service-PPLcfc': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-colord.service-jCb4Yy': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-power-profiles-daemon.service-KX5FXn': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-polkit.service-o8f8td': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-ModemManager.service-C7boDg': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-bluetooth.service-aFhFHs': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-upower.service-Qg3VBx': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-systemd-oomd.service-YvcjFr': Permission denied
du: cannot read directory '/var/tmp/systemd-private-30ba88492f0548cc917eb5855b62bd3d-systemd-timesyncd.service-nDlOGe': Permission denied
du: cannot read directory '/var/lib/bluetooth': Permission denied
du: cannot read directory '/var/lib/sss/db': Permission denied
du: cannot read directory '/var/lib/sss/keytabs': Permission denied
du: cannot read directory '/var/lib/sss/pipes/private': Permission denied
du: cannot read directory '/var/lib/sss/secrets': Permission denied
du: cannot read directory '/var/lib/sss/deskprofile': Permission denied
du: cannot read directory '/var/lib/polkit-1': Permission denied
du: cannot read directory '/var/lib/private': Permission denied
du: cannot read directory '/var/lib/udisks2': Permission denied
du: cannot read directory '/var/lib/fprint': Permission denied
du: cannot read directory '/var/lib/snapd/cache': Permission denied
du: cannot read directory '/var/lib/snapd/void': Permission denied
du: cannot read directory '/var/lib/snapd/cookie': Permission denied
du: cannot read directory '/var/lib/NetworkManager': Permission denied
du: cannot read directory '/var/lib/saned': Permission denied
du: cannot read directory '/var/lib/colord/.cache': Permission denied
du: cannot read directory '/var/lib/apt/lists/partial': Permission denied
du: cannot read directory '/var/lib/gnome-remote-desktop': Permission denied
du: cannot read directory '/var/lib/update-notifier/package-data-downloads/partial': Permission denied
du: cannot read directory '/var/lib/openvpn/chroot': Permission denied
du: cannot read directory '/var/lib/AccountsService/users': Permission denied
du: cannot read directory '/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial': Permission denied
du: cannot read directory '/var/lib/gdm3': Permission denied
du: cannot read directory '/var/lib/fwupd/gnupg': Permission denied
Direktori : /var
Ukuran    : 3631 MB
Batas     : 50 MB
PERINGATAN: Ukuran melebihi batas!
Kelebihan : 3581 MB
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./debug-latihan.sh
Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

#### Latihan 9.5
#### Prompt
```
nano debug-latihan.sh

#!/bin/bash
set -e

# Script: debug-latihan.sh
# Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>

DIREKTORI=$1
BATAS=$2

# cek jumlah argumen
if [ $# -ne 2 ]; then
    echo "Penggunaan: $0 <direktori> <batas-MB>"
    exit 1
fi

# cek direktori ada atau tidak
if [ ! -d "$DIREKTORI" ]; then
    echo "ERROR: Direktori '$DIREKTORI' tidak ditemukan"
    exit 1
fi

# hitung ukuran (tanpa error permission)
UKURAN=$(du -sm "$DIREKTORI" 2>/dev/null | cut -f1)

echo "Direktori : $DIREKTORI"
echo "Ukuran    : ${UKURAN} MB"
echo "Batas     : ${BATAS} MB"

# cek apakah melebihi batas
if [ "$UKURAN" -gt "$BATAS" ]; then
    echo "PERINGATAN: Ukuran melebihi batas!"
    echo "Kelebihan : $((UKURAN - BATAS)) MB"
else
    echo "Status: Normal (sisa: $((BATAS - UKURAN)) MB)"
fi

chmod +x debug-latihan.sh
./debug-latihan.sh /etc 50
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/debug-latihan.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ cd ~/praktikum-os/week09/scripts
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano debug-latihan.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x debug-latihan.sh
./debug-latihan.sh /etc 50
Direktori : /etc
Ukuran    : 12 MB
Batas     : 50 MB
Status: Normal (sisa: 38 MB)
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Tugas 1 Script Absensi Kelas
#### Prompt
```
nano ~/praktikum-os/week09/scripts/absensi.sh

#!/bin/bash
set -euo pipefail

FILE="../logs/absensi-$(date +%F).txt"
REKAP=false

# fungsi bantuan
usage() {
    echo "Penggunaan:"
    echo "  $0 <nama> <hadir|izin|alpha>"
    echo "  $0 -r   (lihat rekap)"
    echo "  $0 -h   (bantuan)"
    exit 0
}

# parsing opsi
while getopts "rh" opt; do
    case $opt in
        r) REKAP=true ;;
        h) usage ;;
        *) usage ;;
    esac
done

shift $((OPTIND - 1))

# mode rekap
if [ "$REKAP" = true ]; then
    [ ! -f "$FILE" ] && { echo "Belum ada data"; exit 0; }

    echo "=== REKAP ABSENSI ==="
    for STATUS in hadir izin alpha; do
        JUMLAH=$(grep -c " - $STATUS" "$FILE" || true)
        echo "$STATUS : $JUMLAH"
    done
    exit 0
fi

# validasi input
if [ $# -ne 2 ]; then
    usage
fi

NAMA=$1
STATUS=$2

# validasi status
case $STATUS in
    hadir|izin|alpha) ;;
    *)
        echo "Status harus: hadir | izin | alpha"
        exit 1
        ;;
esac

# simpan data
mkdir -p ../logs
echo "[$(date +%H:%M)] $NAMA - $STATUS" >> "$FILE"

echo "Data tersimpan."

chmod +x absensi.sh

./absensi.sh Andi hadir
./absensi.sh Budi izin
./absensi.sh Citra alpha
./absensi.sh Deni hadir
./absensi.sh Eka hadir

cat ../logs/absensi-$(date +%F).txt

./absensi.sh -r
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/absensi.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x absensi.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./absensi.sh Andi hadir
./absensi.sh Budi izin
./absensi.sh Citra alpha
./absensi.sh Deni hadir
./absensi.sh Eka hadir
Data tersimpan.
Data tersimpan.
Data tersimpan.
Data tersimpan.
Data tersimpan.
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ cat ../logs/absensi-$(date +%F).txt
[17:41] Andi - hadir
[17:41] Budi - izin
[17:41] Citra - alpha
[17:41] Deni - hadir
[17:41] Eka - hadir
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./absensi.sh -r
=== REKAP ABSENSI ===
hadir : 3
izin : 1
alpha : 1
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```

### Tugas 2 Script Health Check Sistem
#### Prompt
```
nano ~/praktikum-os/week09/scripts/healthcheck.sh

#!/bin/bash
set -euo pipefail

BATAS=80
LOG_DIR="../logs"
FILE="$LOG_DIR/healthcheck-$(date +%F).log"

# fungsi bantuan
usage() {
    echo "Penggunaan: $0 [-t batas_disk]"
    exit 0
}

# parsing opsi
while getopts "t:h" opt; do
    case $opt in
        t) BATAS="$OPTARG" ;;
        h) usage ;;
        *) usage ;;
    esac
done

mkdir -p "$LOG_DIR"

# fungsi log (pakai tee)
log() {
    echo "$1" | tee -a "$FILE"
}

log "======================================"
log "HEALTH CHECK SYSTEM"
log "======================================"
log "Tanggal : $(date '+%F %T')"
log "Hostname: $(hostname)"
log "Uptime  : $(uptime -p)"

# CPU (load average)
log "CPU Load: $(uptime | awk -F'load average:' '{print $2}')"

# RAM
RAM=$(free -h | awk '/Mem/ {print $3 "/" $2}')
log "RAM     : $RAM"

# Disk check semua filesystem
log ""
log "=== DISK USAGE ==="

df -h | awk 'NR>1 {print $1, $5, $6}' | while read FS USAGE MOUNT; do
    PERCENT=$(echo "$USAGE" | tr -d '%')

    if [ "$PERCENT" -gt "$BATAS" ]; then
        log "$FS ($MOUNT) : $USAGE ⚠️ WARNING"
    else
        log "$FS ($MOUNT) : $USAGE OK"
    fi
done

log "======================================"
log "Selesai."

chmod +x ~/praktikum-os/week09/scripts/healthcheck.sh

./healthcheck.sh

./healthcheck.sh -t 50

cat ../logs/healthcheck-$(date +%F).log
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/healthcheck.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/healthcheck.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./healthcheck.sh
======================================
HEALTH CHECK SYSTEM
======================================
Tanggal : 2026-05-01 17:43:11
Hostname: fafiq-ubuntu
Uptime  : up 1 hour, 15 minutes
CPU Load:  0.73, 0.83, 0.75
RAM     : 4.7Gi/14Gi

=== DISK USAGE ===
tmpfs (/run) : 1% OK
/dev/nvme0n1p3 (/) : 17% OK
tmpfs (/dev/shm) : 1% OK
tmpfs (/run/lock) : 1% OK
efivarfs (/sys/firmware/efi/efivars) : 51% OK
/dev/nvme0n1p1 (/boot/efi) : 11% OK
tmpfs (/run/user/1000) : 1% OK
======================================
Selesai.
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ ./healthcheck.sh -t 50
======================================
HEALTH CHECK SYSTEM
======================================
Tanggal : 2026-05-01 17:43:24
Hostname: fafiq-ubuntu
Uptime  : up 1 hour, 15 minutes
CPU Load:  0.72, 0.82, 0.75
RAM     : 4.7Gi/14Gi

=== DISK USAGE ===
tmpfs (/run) : 1% OK
/dev/nvme0n1p3 (/) : 17% OK
tmpfs (/dev/shm) : 1% OK
tmpfs (/run/lock) : 1% OK
efivarfs (/sys/firmware/efi/efivars) : 51% ⚠️ WARNING
/dev/nvme0n1p1 (/boot/efi) : 11% OK
tmpfs (/run/user/1000) : 1% OK
======================================
Selesai.
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ cat ../logs/healthcheck-$(date +%F).log
======================================
HEALTH CHECK SYSTEM
======================================
Tanggal : 2026-05-01 17:43:11
Hostname: fafiq-ubuntu
Uptime  : up 1 hour, 15 minutes
CPU Load:  0.73, 0.83, 0.75
RAM     : 4.7Gi/14Gi

=== DISK USAGE ===
tmpfs (/run) : 1% OK
/dev/nvme0n1p3 (/) : 17% OK
tmpfs (/dev/shm) : 1% OK
tmpfs (/run/lock) : 1% OK
efivarfs (/sys/firmware/efi/efivars) : 51% OK
/dev/nvme0n1p1 (/boot/efi) : 11% OK
tmpfs (/run/user/1000) : 1% OK
======================================
Selesai.
======================================
HEALTH CHECK SYSTEM
======================================
Tanggal : 2026-05-01 17:43:24
Hostname: fafiq-ubuntu
Uptime  : up 1 hour, 15 minutes
CPU Load:  0.72, 0.82, 0.75
RAM     : 4.7Gi/14Gi

=== DISK USAGE ===
tmpfs (/run) : 1% OK
/dev/nvme0n1p3 (/) : 17% OK
tmpfs (/dev/shm) : 1% OK
tmpfs (/run/lock) : 1% OK
efivarfs (/sys/firmware/efi/efivars) : 51% ⚠️ WARNING
/dev/nvme0n1p1 (/boot/efi) : 11% OK
tmpfs (/run/user/1000) : 1% OK
======================================
Selesai.
fafiq@fafiq-ubuntu:~/praktikum-os/week09/scripts$ 
```