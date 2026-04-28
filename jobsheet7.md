# Laporan Praktikum Sistem Operasi Jobsheet 7

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

### Praktikum 7.1 — Mengenali Bash dan Menyiapkan Workspace
#### Prompt
```
echo "Shell login : $SHELL"
echo "Shell aktif : $0"
bash --version | head -n 1
```

#### Hasil
```
echo "Shell aktif : $0"
bash --version | head -n 1
Shell login : /bin/bash
Shell aktif : bash
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
```

#### Prompt
```
echo $$
ps -p $$ -o pid,ppid,args=
```

#### Hasil
```
11719
    PID    PPID 
  11719   11712 bash
```

#### Prompt
```
mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
cd ~/praktikum-os/week04-bash
pwd
```

#### Hasil
```
/home/fafiq/praktikum-os/week07-bash
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ 
```

#### Prompt
```
touch sample-app.conf
touch logs/app-01.log logs/app-02.log logs/app-03.log
touch sampel/catatan-a.txt sampel/catatan-b.txt
touch sampel/backup-01.tar sampel/backup-02.tar
touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan.log
touch "ruang-nama/laporan server april.txt "
touch "ruang-nama/backup [ mingguan ] server.conf "
ls -R
```

#### Hasil
```.:
backup  bin  logs  ruang-nama  sampel  sample-app.conf

./backup:

./bin:

./logs:
app-01.log  app-02.log  app-03.log

./ruang-nama:
'backup [ mingguan ] server.conf '  'laporan server april.txt '

./sampel:
backup-01.tar  backup-02.tar  catatan-a.txt  catatan-b.txt  laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log
```
### Praktikum 7.2 — Membuat Ringkasan Sesi Terminal
#### Prompt
```
cd ~/praktikum-os/week07-bash
```

#### Hasil
```

```

#### Prompt
```
{
    echo "=== RINGKASAN SESI BASH ==="
    date
    echo "User          : $(whoami)"
    echo "Hostname      : $(hostname)"
    echo "Shell login   : $SHELL"
    echo "Shell aktif   : $0"
    echo "PID shell     : $$"
    echo "Direktori     : $(pwd)"
} | tee session - info . txt
```

#### Hasil
```
=== RINGKASAN SESI BASH ===
Fri Apr 17 03:25:02 PM WIB 2026
User : fafiq
Hostname : fafiq-ubuntu
Shell login: /bin/bash
Shell aktif: bash
PID shell : 11719
Direktori : /home/fafiq/praktikum-os/week07-bash
```

#### Prompt
```
cat session - info . txt
```

#### Hasil
```
=== RINGKASAN SESI BASH ===
Fri Apr 17 03:25:02 PM WIB 2026
User : fafiq
Hostname : fafiq-ubuntu
Shell login: /bin/bash
Shell aktif: bash
PID shell : 11719
Direktori : /home/fafiq/praktikum-os/week07-bash
```

### Praktikum 7.3 — Menambahkan Konfigurasi Aman pada .bashrc
#### Prompt
```
ls -la ~ | grep -E 'bashrc|bash_profile|profile'
```

#### Hasil
```
-rw-r--r--  1 fafiq fafiq 3771 Mar 31  2024 .bashrc
-rw-r--r--  1 fafiq fafiq  807 Mar 31  2024 .profile
```

#### Prompt
```
cp ~/.bashrc ~/.bashrc.bak-praktikum
```

#### Hasil
```
Copy file ~/.bashrc ke ~/.bashrc.bak-praktikum
```

#### Prompt
```
cat <<'EOF' >> ~/.bashrc

# --- Praktikum Bash Shell ---
export PRAKTIKUM_BASH_DIR="$HOME/praktikum-os/week07-bash"
export EDITOR=nano
# --- End Praktikum Bash Shell ---

EOF
```

#### Hasil
```
Menambahkan konfigurasi
```

#### Prompt
```
source ~/.bashrc
echo "$PRAKTIKUM_BASH_DIR"
echo "$EDITOR"
```

#### Hasil
```
/home/fafiq/praktikum-os/week07-bash
nano
```

### Praktikum 7.4 — Menyiapkan .bash_profile untuk Shell Login
#### Prompt
```
[ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bash_profile.bak-praktikum
```

#### Prompt
```
cat <<'EOF' >> ~/.bash_profile

# --- Praktikum Bash Login Shell ---
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi

echo "Login Bash pada $(date '+%F %T')" >> "$HOME/praktikum-os/week07-bash/login-audit.log"
# --- End Praktikum Bash Login Shell ---

EOF
```

#### Prompt
```
bash -l
tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
exit
```

#### Hasil
```
Login Bash pada 2026-04-17 15:33:20
```
### Praktikum 7.5 — Membedakan Variabel Shell dan Environment Variable
#### Prompt
```
KELAS_OS="Sistem Operasi A"
echo "$KELAS_OS"
```

#### Hasil
```
Sistem Operasi A
```

#### Prompt
```
bash
echo "$KELAS_OS"
exit
```

#### Hasil
```
Kosong
```

#### Prompt
```
export KELAS_OS="Sistem Operasi A"
bash
echo "$KELAS_OS"
exit
```

#### Hasil
```
Sistem Operasi A
```

#### Prompt
```
echo "$PATH"
which bash
type ls
```

#### Hasil
```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
/usr/bin/bash
ls is aliased to `ls --color=auto'
```

### Praktikum 7.6 — Menambahkan Direktori Script Pribadi ke PATH

#### Prompt
```
cat <<'EOF' >> ~/.bashrc

# --- Praktikum PATH ---
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
# --- End Praktikum PATH ---

EOF

source ~/.bashrc
echo "$PATH"

cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash

echo "Hostname : $(hostname)"
echo "User     : $(whoami)"
echo "Uptime   : $(uptime -p)"
echo "Disk /   :"
df -h /
EOF

chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem

ringkas-sistem
```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ cat <<'EOF' >> ~/.bashrc

# --- Praktikum PATH ---
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
# --- End Praktikum PATH ---

EOF
fafiq@fafiq-ubuntu:~$ source ~/.bashrc
fafiq@fafiq-ubuntu:~$ echo "$PATH"
/home/fafiq/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
fafiq@fafiq-ubuntu:~$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash

echo "Hostname : $(hostname)"
echo "User     : $(whoami)"
echo "Uptime   : $(uptime -p)"
echo "Disk /   :"
df -h /
EOF
fafiq@fafiq-ubuntu:~$ chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
fafiq@fafiq-ubuntu:~$ ringkas-sistem
Hostname : fafiq-ubuntu
User     : fafiq
Uptime   : up 7 minutes
Disk /   :
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   94G   15G   75G  17% /
fafiq@fafiq-ubuntu:~$ 
```
### Praktikum 7.7 — Membuat Alias Produktivitas Dasar
#### Prompt
```
cat <<'EOF' >> ~/.bashrc

# --- Praktikum Alias ---
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
# --- End Praktikum Alias ---

EOF

source ~/.bashrc
ll
hist10
cdbashlab
pwd

```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ cat <<'EOF' >> ~/.bashrc

# --- Praktikum Alias ---
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
# --- End Praktikum Alias ---

EOF
fafiq@fafiq-ubuntu:~$ source ~/.bashrc
fafiq@fafiq-ubuntu:~$ ll
total 140K
drwxr-x--- 24 fafiq fafiq 4.0K Apr 17 15:35 .
drwxr-xr-x  3 root  root  4.0K Apr 14 20:01 ..
-rw-------  1 fafiq fafiq 5.6K Apr 22 13:37 .bash_history
-rw-r--r--  1 fafiq fafiq  220 Mar 31  2024 .bash_logout
-rw-rw-r--  1 fafiq fafiq  214 Apr 17 15:33 .bash_profile
-rw-r--r--  1 fafiq fafiq 4.2K Apr 28 21:21 .bashrc
-rw-r--r--  1 fafiq fafiq 3.7K Apr 17 15:29 .bashrc.bak-praktikum
drwx------ 18 fafiq fafiq 4.0K Apr 17 13:59 .cache
drwx------ 19 fafiq fafiq 4.0K Apr 18 05:10 .config
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 14 20:16 Desktop
drwxrwxr-x  2 fafiq fafiq 4.0K Apr 14 20:34 .dir_colors
drwxr-xr-x  4 fafiq fafiq 4.0K Apr 17 14:19 Documents
drwxrwxr-x  3 fafiq fafiq 4.0K Apr 14 20:40 .dotnet
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 15 00:12 Downloads
-rw-rw-r--  1 fafiq fafiq   57 Apr 15 16:09 .gitconfig
drwxrwxr-x  5 fafiq fafiq 4.0K Apr 14 20:34 gnome-terminal
drwx------  2 fafiq fafiq 4.0K Apr 14 21:07 .gnupg
-rw-------  1 fafiq fafiq   20 Apr 15 16:09 .lesshst
drwx------  4 fafiq fafiq 4.0K Apr 14 20:16 .local
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 14 20:16 Music
drwxr-xr-x  3 fafiq fafiq 4.0K Apr 14 20:28 Pictures
drwx------  3 fafiq fafiq 4.0K Apr 14 20:40 .pki
drwxrwxr-x  3 fafiq fafiq 4.0K Apr 17 15:14 praktikum-os
-rw-r--r--  1 fafiq fafiq  865 Apr 17 15:35 .profile
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 14 20:16 Public
drwx------  6 fafiq fafiq 4.0K Apr 14 21:00 snap
drwx------  2 fafiq fafiq 4.0K Apr 14 20:15 .ssh
-rw-r--r--  1 fafiq fafiq    0 Apr 14 20:17 .sudo_as_admin_successful
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 14 20:16 Templates
drwxrwxr-x  3 fafiq fafiq 4.0K Apr 14 21:04 .themes
drwxr-xr-x  2 fafiq fafiq 4.0K Apr 14 20:16 Videos
drwxrwxr-x  4 fafiq fafiq 4.0K Apr 14 20:40 .vscode
drwxrwxr-x  7 fafiq fafiq 4.0K Apr 17 15:14 week07-bash
-rw-rw-r--  1 fafiq fafiq  180 Apr 14 20:34 .wget-hsts
fafiq@fafiq-ubuntu:~$ hist10
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
# --- End Praktikum Alias ---

EOF

  250  source ~/.bashrc
  251  ll
  252  hist10
fafiq@fafiq-ubuntu:~$ cdbashlab
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ pwd
/home/fafiq/praktikum-os/week07-bash
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ type ll
ll is aliased to `ls -lah --color=auto'
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ 
```

### Praktikum 7.8 — Membuat Fungsi Backup Konfigurasi
#### Prompt
```
echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf
cat ~/praktikum-os/week07-bash/sample-app.conf

cat <<'EOF' >> ~/.bashrc

# --- Praktikum Fungsi Shell ---
backup_conf () {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>"
        return 1
    fi

    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"

    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src"
        return 2
    fi

    mkdir -p "$dst"

    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"

    echo "Backup selesai di $dst"
}
# --- End Praktikum Fungsi Shell ---

EOF

source ~/.bashrc

backup_conf ~/praktikum-os/week07-bash/sample-app.conf

ls -lah ~/praktikum-os/week07-bash/backup

type backup_conf
```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf
fafiq@fafiq-ubuntu:~$ cat ~/praktikum-os/week07-bash/sample-app.conf
PORT=8080
fafiq@fafiq-ubuntu:~$ cat ~/praktikum-os/week07-bash/sample-app.conf
PORT=8080
fafiq@fafiq-ubuntu:~$ cat <<'EOF' >> ~/.bashrc

# --- Praktikum Fungsi Shell ---
backup_conf () {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>"
        return 1
    fi

    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"

    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src"
        return 2
    fi

    mkdir -p "$dst"

    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"

    echo "Backup selesai di $dst"
}
# --- End Praktikum Fungsi Shell ---

EOF
fafiq@fafiq-ubuntu:~$ source ~/.bashrc
fafiq@fafiq-ubuntu:~$ backup_conf ~/praktikum-os/week07-bash/sample-app.conf
Backup selesai di /home/fafiq/praktikum-os/week07-bash/backup
fafiq@fafiq-ubuntu:~$ ls -lah ~/praktikum-os/week07-bash/backup
total 12K
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:25 .
drwxrwxr-x 7 fafiq fafiq 4.0K Apr 17 15:33 ..
-rw-rw-r-- 1 fafiq fafiq   10 Apr 28 21:25 sample-app.conf.2026-04-28-212538.bak
fafiq@fafiq-ubuntu:~$ type backup_conf
backup_conf is a function
backup_conf () 
{ 
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src";
        return 2;
    fi;
    mkdir -p "$dst";
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak";
    echo "Backup selesai di $dst"
}
fafiq@fafiq-ubuntu:~$ 

```
### Praktikum 7.9 — Menggunakan Completion Dasar dan Melihat History
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/sampel
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  backup-02.tar  catatan-a.txt  catatan-b.txt  laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat lap
cat: lap: No such file or directory
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat laporan-
laporan-bulanan.log   laporan-harian.log    laporan-mingguan.log  
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat laporan-
laporan-bulanan.log   laporan-harian.log    laporan-mingguan.log  
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat laporan-
laporan-bulanan.log   laporan-harian.log    laporan-mingguan.log  
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat laporan-harian.log 
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ pwd
ls -lah
date
whoami
/home/fafiq/praktikum-os/week07-bash/sampel
total 8.0K
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 17 15:19 .
drwxrwxr-x 7 fafiq fafiq 4.0K Apr 17 15:33 ..
-rw-rw-r-- 1 fafiq fafiq    0 Apr 17 15:19 backup-01.tar
-rw-rw-r-- 1 fafiq fafiq    0 Apr 17 15:19 backup-02.tar
-rw-rw-r-- 1 fafiq fafiq    0 Apr 17 15:19 catatan-a.txt
-rw-rw-r-- 1 fafiq fafiq    0 Apr 17 15:19 catatan-b.txt
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:27 laporan-bulanan.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:27 laporan-harian.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:27 laporan-mingguan.log
Tue Apr 28 09:29:34 PM WIB 2026
fafiq
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ history | tail -n 10
  265  cd ~/praktikum-os/week07-bash/sampel
  266  touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
  267  ls
  268  cat lap
  269  cat laporan-harian.log 
  270  pwd
  271  ls -lah
  272  date
  273  whoami
  274  history | tail -n 10
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ history | grep ls
   11  ls
   50  ls / tmp
   52  ls / direktori - tidak - ada
   55  ls /tmp
   57  ls /direktori - tidak - ada
  175  ls -R
  180  ls -la ~ | grep -E 'bashrc|bash_profile|profile'
  203  ls -la ~ | grep profile
  214  type ls
  231  sudo apt remove --purge -y i3 i3status i3lock suckless-tools rofi feh picom zsh neovim network-manager-gnome pavucontrol brightnessctl playerctl flameshot thunar lxappearance fonts-font-awesome fonts-noto fonts-jetbrains-mono
  235  ls
  237  ls
  240  ls
alias ll='ls -lah --color=auto'
  262  ls -lah ~/praktikum-os/week07-bash/backup
  267  ls
  271  ls -lah
  275  history | grep ls
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ history
    1  fafiq@fafiq-ubuntu:/$ git clone https://github.com/dracula/gnome-terminal
    2  git clone https://github.com/dracula/gnome-terminal
    3  cd gnome-terminal
    4  ./install.sh
    5  sudo apt update
    6  sudo apt install vscode
    7  sudo apt install code
    8  cd Download
    9  cd ~/Download
   10  cd ~/Downloads
   11  ls
   12  cd ..
   13  sudo apt install code_1.115.0-1775600353_amd64.deb
   14  cd ~/Downloads
   15  sudo apt install ./code_1.115.0-1775600353_amd64.deb
   16  git clone https://github.com/D3Ext/aesthetic-wallpapers.git
   17  gsettings set org.gnome.desktop.interface gtk-theme Dracula
   18  gsettings set org.gnome.desktop.wm.preferences theme Dracula
   19  sudo update-grub
   20  sudo nano /etc/grub.d/40_custom
   21  sudo upgrade-grub
   22  sudo update-grub
   23  reboot
   24  sudo nano /etc/default/grub
   25  sudo nano /etc/grub.d/40_custom
   26  sudo nano /etc/default/grub
   27  sudo update-grub
   28  clear
   29  reboot
   30  neofetch
   31  sudo apt install chromium
   32  git config --global user.name "azana123"
   33  git config --global user.email "azanalutfi321@gmail.com"
   34  git config --global --list
   35  ps aux
   36  ps aux -L
   37  echo $$
   38  ps -p $$ -f
   39  pstree -p
   40  ps aux
   41  ps aux | wc -l
   42  pstree -p
   43  pstree -p 43502
   44  clear
   45  ps aux
   46  ps aux -L
   47  clear
   48  sleep 60 &
   49  ps aux | grep sleep
   50  ls / tmp
   51  echo " Sukses : $?"
   52  ls / direktori - tidak - ada
   53  echo " Gagal : $?"
   54  clear
   55  ls /tmp
   56  echo " Sukses : $?"
   57  ls /direktori - tidak - ada
   58  echo " Gagal : $?"
   59  sleep 200 & ps aux
   60  clear
   61  1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
   62  2. Jalankan beberapa perintah yang berhasil da
   63  sleep 200 & ps aux
   64  clear
   65  nice -n 10 sleep 300 &
   66  ps aux | grep sleep
   67  renice -n 15 -p <PID >
   68  ps -p <PID > -o pid ,ni , cmd
   69  renice -n 15 -p <PID>
   70  ps -p <PID> -o pid,ni,cmd
   71  renice -n 15 -p <PID> ps -p <PID> -o pid,ni,cmd
   72  clear
   73  nice -n 10 sleep 300 &
   74  ps aux | grep sleep
   75  renice -n 15 -p 11927
   76  ps -p 11927 -o pid,ni,cmd
   77  nice -n 5 sleep 200 &
   78  ps -p <PID> -o pid,ni,cmd
   79  nice -n 5 sleep 200 & | ps aux | grep sleep
   80  clear
   81  nice -n 5 sleep 200 &
   82  ps aux | grep sleep
   83  ps -p 12726 -o pid,ni,cmd
   84  renice -n 10 -p 12726
   85  clear
   86  nice -n 5 sleep 300 &
   87  renice -n 10 -p 13000
   88  clear
   89  nice -n 5 sleep 300 &
   90  ps aux | grep sleep
   91  ps -p 16964 -o pid,ni,cmd
   92  renice -n 10 -p 16964
   93  ps -p 16964 -o pid,ni,cmd
   94  clear
   95  nice -n 5 sleep 300 &
   96  ps aux | grep sleep
   97  ps -p 12980 -o pid,ni,cmd
   98  renice -n 10 -p 12980
   99  ps -p 12980 -o pid,ni,cmd
  100  renice -n -5 -p 12980
  101  clear
  102  sleep 500 &
  103  sleep 600 &
  104  sleep 700 &
  105  ps aux | grep -v grep | grep sleep
  106  kill 13322
  107  ps aux | grep -v grep | grep sleep
  108  kill -SIGSTOP 13323
  109  ps aux | grep sleep
  110  kill -SIGCONT 13323
  111  ps aux | grep sleep
  112  pkill sleep
  113  sleep 200 &
  114  sleep 300 &
  115  sleep 400 &
  116  jobs
  117  fg %1
  118  bg %1
  119  jobs
  120  kill %1 %2 %3
  121  jobs
  122  top
  123  clear
  124  top
  125  jobs
  126  bg %1 jobs
  127  top
  128  jobs
  129  bg %1 jobs
  130  top
  131  jobs
  132  bg %1
  133  jobs
  134  fg %1
  135  bg %7
  136  fg %7
  137  top
  138  jobs
  139  bg %1
  140  jobs
  141  fg %1
  142  ps aux --sort=-%cpu | head -10
  143  ps aux --sort=-%mem | head -10
  144  top
  145  mkdir -p ~/praktikum-os/ week07-bash/{bin,backup,logs,sampel,ruang-nama}
  146  cd ~/praktikum-os/week04-bash
  147  pwd
  148  mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
  149  cd ~/praktikum-os/week04-bash
  150  pwd
  151  clear
  152  mkdir -p ~/praktikum-os/ week07-bash/{bin,backup,logs,sampel,ruang-nama}
  153  cd ~/praktikum-os/week04-bash
  154  pwd
  155  clear
  156  mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
  157  cd ~/praktikum-os/week07-bash
  158  pwd
  159  cd ..
  160  cd ~
  161  echo "Shell login : $SHELL"
  162  echo "Shell aktif : $0"
  163  bash --version | head -n 1
  164  echo $$
  165  ps -p $$ -o pid,ppid,args=
  166  cd ~/praktikum-os/week09-bash
  167  cd ~/praktikum-os/week07-bash
  168  touch sample-app.conf
  169  touch logs/app-01.log logs/app-02.log logs/app-03.log
  170  touch sampel/catatan-a.txt sampel/catatan-b.txt
  171  touch sampel/backup-01.tar sampel/backup-02.tar
  172  touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan.log
  173  touch "ruang-nama/laporan server april.txt "
  174  touch "ruang-nama/backup [ mingguan ] server.conf "
  175  ls -R
  176  { echo "=== RINGKASAN SESI BASH ==="; date; echo "User : $(whoami)"; echo "Hostname : $(hostname)"; echo "Shell login: $SHELL"; echo "Shell aktif: $0"; echo "PID shell : $$"; echo "Direktori : $(pwd)"; } | tee session-info.txt
  177  cat session-info.txt
  178  clear
  179  cd ~
  180  ls -la ~ | grep -E 'bashrc|bash_profile|profile'
  181  cp ~/.bashrc ~/.bashrc.bak-praktikum
  182  cat <<'EOF' >> ~/.bashrc
  183  # --- Praktikum Bash Shell ---
  184  export PRAKTIKUM_BASH_DIR="$HOME/praktikum-os/week07-bash"
  185  export EDITOR=nano
  186  # --- End Praktikum Bash Shell ---
  187  EOF
  188  source ~/.bashrc
  189  echo "$PRAKTIKUM_BASH_DIR"
  190  echo "$EDITOR"
  191  cd ~/.bashrc
  192  clear
  193  [ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bash_profile.bak-praktikum
  194  cat <<'EOF' >> ~/.bash_profile
  195  # --- Praktikum Bash Login Shell ---
  196  if [ -f ~/.bashrc ]; then
  197  . ~/.bashrc
  198  fi
  199  echo "Login Bash pada $(date '+%F %T')" >> "$HOME/praktikum-os/week07-bash/login-audit.log"
  200  # --- End Praktikum Bash Login Shell ---
  201  EOF
  202  bash -l
  203  ls -la ~ | grep profile
  204  nano ~/.profile
  205  bash -l
  206  clear
  207  KELAS_OS="Sistem Operasi A"
  208  echo "$KELAS_OS"
  209  bash
  210  export KELAS_OS="Sistem Operasi A"
  211  bash
  212  echo "$PATH"
  213  which bash
  214  type ls
  215  source ~/.bash_profile
  216  tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
  217  clear
  218  KELAS_OS="Sistem Operasi A"
  219  echo "$KELAS_OS"
  220  bash
  221  export KELAS_OS="Sistem Operasi A"
  222  bash
  223  export KELAS_OS="Sistem Operasi A"
  224  bash
  225  echo "$KELAS_OS"
  226  exit
  227  sudo apt update
  228  sudo apt install -y i3 i3status i3lock dmenu rofi feh picom zsh git curl neovim network-manager network-manager-gnome pavucontrol brightnessctl playerctl flameshot thunar lxappearance fonts-font-awesome fonts-noto fonts-jetbrains-mono
  229  sudo apt --fix-broken install
  230  sudo dpkg --configure -a
  231  sudo apt remove --purge -y i3 i3status i3lock suckless-tools rofi feh picom zsh neovim network-manager-gnome pavucontrol brightnessctl playerctl flameshot thunar lxappearance fonts-font-awesome fonts-noto fonts-jetbrains-mono
  232  sudo apt autoremove --purge -y
  233  sudo apt clean
  234  sudo apt update
  235  ls
  236  cd praktikum-os
  237  ls
  238  cd week7-bash
  239  cd week07-bash
  240  ls
  241  cd ~/
  242  cat <<'EOF' >> ~/.bashrc

# --- Praktikum PATH ---
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
# --- End Praktikum PATH ---

EOF

  243  source ~/.bashrc
  244  echo "$PATH"
  245  cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash

echo "Hostname : $(hostname)"
echo "User     : $(whoami)"
echo "Uptime   : $(uptime -p)"
echo "Disk /   :"
df -h /
EOF

  246  chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
  247  ringkas-sistem
  248  clear
  249  cat <<'EOF' >> ~/.bashrc

# --- Praktikum Alias ---
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
# --- End Praktikum Alias ---

EOF

  250  source ~/.bashrc
  251  ll
  252  hist10
  253  cdbashlab
  254  pwd
  255  type ll
  256  cd ~/
  257  echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf
  258  cat ~/praktikum-os/week07-bash/sample-app.conf
  259  cat <<'EOF' >> ~/.bashrc

# --- Praktikum Fungsi Shell ---
backup_conf () {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>"
        return 1
    fi

    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"

    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src"
        return 2
    fi

    mkdir -p "$dst"

    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"

    echo "Backup selesai di $dst"
}
# --- End Praktikum Fungsi Shell ---

EOF

  260  source ~/.bashrc
  261  backup_conf ~/praktikum-os/week07-bash/sample-app.conf
  262  ls -lah ~/praktikum-os/week07-bash/backup
  263  type backup_conf
  264  clear
  265  cd ~/praktikum-os/week07-bash/sampel
  266  touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
  267  ls
  268  cat lap
  269  cat laporan-harian.log 
  270  pwd
  271  ls -lah
  272  date
  273  whoami
  274  history | tail -n 10
  275  history | grep ls
  276  history
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ !120
kill %1 %2 %3
bash: kill: %1: no such job
bash: kill: %2: no such job
bash: kill: %3: no such job
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cat ~/praktikum-os/week07-bash/diag-history.txt

  260  source ~/.bashrc
  261  backup_conf ~/praktikum-os/week07-bash/sample-app.conf
  262  ls -lah ~/praktikum-os/week07-bash/backup
  263  type backup_conf
  264  clear
  265  cd ~/praktikum-os/week07-bash/sampel
  266  touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
  267  ls
  268  cat lap
  269  cat laporan-harian.log 
  270  pwd
  271  ls -lah
  272  date
  273  whoami
  274  history | tail -n 10
  275  history | grep ls
  276  history
  277  kill %1 %2 %3
  278  history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ 

```
### Praktikum 7.10 — Menelusuri Perintah Diagnostik dengan History
#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ cd ~
fafiq@fafiq-ubuntu:~$ df -h
free -h
uptime
ps aux | head
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.5G  3.2M  1.5G   1% /run
/dev/nvme0n1p3   94G   15G   75G  17% /
tmpfs           7.5G   23M  7.5G   1% /dev/shm
tmpfs           5.0M   16K  5.0M   1% /run/lock
efivarfs        148K   69K   75K  48% /sys/firmware/efi/efivars
/dev/nvme0n1p1 1022M  111M  912M  11% /boot/efi
tmpfs           1.5G  140K  1.5G   1% /run/user/1000
               total        used        free      shared  buff/cache   available
Mem:            14Gi       3.7Gi       8.7Gi        99Mi       2.7Gi        11Gi
Swap:          4.0Gi          0B       4.0Gi
 21:31:35 up 20 min,  1 user,  load average: 0.88, 0.77, 0.56
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0  23436 15096 ?        Ss   21:11   0:01 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    21:11   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    21:11   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   21:11   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   21:11   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   21:11   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   21:11   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   21:11   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I    21:11   0:00 [kworker/0:1-events]
fafiq@fafiq-ubuntu:~$ history | grep -E 'df -h|free -h|uptime|ps aux'
   35  ps aux
   36  ps aux -L
   40  ps aux
   41  ps aux | wc -l
   45  ps aux
   46  ps aux -L
   49  ps aux | grep sleep
   59  sleep 200 & ps aux
   61  1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
   63  sleep 200 & ps aux
   66  ps aux | grep sleep
   74  ps aux | grep sleep
   79  nice -n 5 sleep 200 & | ps aux | grep sleep
   82  ps aux | grep sleep
   90  ps aux | grep sleep
   96  ps aux | grep sleep
  105  ps aux | grep -v grep | grep sleep
  107  ps aux | grep -v grep | grep sleep
  109  ps aux | grep sleep
  111  ps aux | grep sleep
  142  ps aux --sort=-%cpu | head -10
  143  ps aux --sort=-%mem | head -10
echo "Uptime   : $(uptime -p)"
df -h /
  282  df -h
  283  free -h
  284  uptime
  285  ps aux | head
  286  history | grep -E 'df -h|free -h|uptime|ps aux'
fafiq@fafiq-ubuntu:~$ !120
kill %1 %2 %3
bash: kill: %1: no such job
bash: kill: %2: no such job
bash: kill: %3: no such job
fafiq@fafiq-ubuntu:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.5G  3.2M  1.5G   1% /run
/dev/nvme0n1p3   94G   15G   75G  17% /
tmpfs           7.5G   23M  7.5G   1% /dev/shm
tmpfs           5.0M   16K  5.0M   1% /run/lock
efivarfs        148K   69K   75K  48% /sys/firmware/efi/efivars
/dev/nvme0n1p1 1022M  111M  912M  11% /boot/efi
tmpfs           1.5G  140K  1.5G   1% /run/user/1000
fafiq@fafiq-ubuntu:~$ history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
fafiq@fafiq-ubuntu:~$ 
```

### Praktikum 7.11 — Mencoba Wildcard Dasar
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/sampel
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  backup-02.tar  catatan-a.txt  catatan-b.txt  laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ ls *.log
laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ ls catatan-?.txt
catatan-a.txt  catatan-b.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ ls backup-0[12].tar
backup-01.tar  backup-02.tar
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ echo *.log
laporan-bulanan.log laporan-harian.log laporan-mingguan.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ echo log-{pagi,siang,malam}.txt
log-pagi.txt log-siang.txt log-malam.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ echo ~
/home/fafiq
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/sampel$ 
```
### Praktikum 7.12 — Mengarsipkan Banyak Log Sekaligus
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/logs
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ touch access-01.log access-02.log access-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls
access-01.log  access-02.log  access-03.log  app-01.log  app-02.log  app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ echo *.log
access-01.log access-02.log access-03.log app-01.log app-02.log app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ echo access-0?.log
access-01.log access-02.log access-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ mkdir -p arsip-log
mv *.log arsip-log/
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls arsip-log
access-01.log  access-02.log  access-03.log  app-01.log  app-02.log  app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ tar -czf arsip-log-$(date +%F).tar.gz fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/logs
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ touch access-01.log access-02.log access-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls
access-01.log  access-02.log  access-03.log  app-01.log  app-02.log  app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ echo *.log
access-01.log access-02.log access-03.log app-01.log app-02.log app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ echo access-0?.log
access-01.log access-02.log access-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ mkdir -p arsip-log
mv *.log arsip-log/
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls arsip-log
access-01.log  access-02.log  access-03.log  app-01.log  app-02.log  app-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ tar -czf arsip-log-$(date +%F).tar.gz arsip-log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls -lah
total 16K
drwxrwxr-x 3 fafiq fafiq 4.0K Apr 28 21:36 .
drwxrwxr-x 7 fafiq fafiq 4.0K Apr 28 21:30 ..
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:36 arsip-log
-rw-rw-r-- 1 fafiq fafiq  220 Apr 28 21:36 arsip-log-2026-04-28.tar.gz
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ 
arsip-log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ ls -lah
total 16K
drwxrwxr-x 3 fafiq fafiq 4.0K Apr 28 21:36 .
drwxrwxr-x 7 fafiq fafiq 4.0K Apr 28 21:30 ..
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:36 arsip-log
-rw-rw-r-- 1 fafiq fafiq  220 Apr 28 21:36 arsip-log-2026-04-28.tar.gz
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/logs$ 
```
### Praktikum 7.13 — Membedakan Single Quote, Double Quote, dan Escape
#### Hasil
```
fafiq@fafiq-ubuntu:~$ echo '$USER bekerja di $HOME'
$USER bekerja di $HOME
fafiq@fafiq-ubuntu:~$ echo "$USER bekerja di $HOME"
fafiq bekerja di /home/fafiq
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/ruang-nama
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ ls
'backup [ mingguan ] server.conf '  'backup [mingguan] server.conf'  'laporan server april.txt'  'laporan server april.txt '
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ ls laporan\ server\ april.txt
'laporan server april.txt'
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ cat "laporan server april.txt"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ 
```
### Praktikum 7.14 — Menangani File dengan Nama Sulit Secara Aman
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash/ruang-nama
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ cp -- "backup [mingguan] server.conf" \
"$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server.conf"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ file_asli="$HOME/praktikum-os/week07-bash/ruang-nama/backup [mingguan] server.conf"
file_salinan="$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf"

cp -- "$file_asli" "$file_salinan"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ ls -lah ~/praktikum-os/week07-bash/backup
total 12K
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:41 .
drwxrwxr-x 7 fafiq fafiq 4.0K Apr 28 21:30 ..
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:41 backup-mingguan-server.conf
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:41 backup-mingguan-server-v2.conf
-rw-rw-r-- 1 fafiq fafiq   10 Apr 28 21:25 sample-app.conf.2026-04-28-212538.bak
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ for file in "$HOME"/praktikum-os/week07-bash/backup/*; do
    printf 'Hasil backup: %s\n' "$file"
done
Hasil backup: /home/fafiq/praktikum-os/week07-bash/backup/backup-mingguan-server.conf
Hasil backup: /home/fafiq/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf
Hasil backup: /home/fafiq/praktikum-os/week07-bash/backup/sample-app.conf.2026-04-28-212538.bak
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/ruang-nama$ 

```
### Tugas Praktikum
#### Tugas Praktikum 1 — Toolkit Bash Administrator Pribadi
#### Hasil
```
fafiq@fafiq-ubuntu:~$ mkdir -p ~/praktikum-os/week07-bash/bin
fafiq@fafiq-ubuntu:~$ cat <<'EOF' >> ~/.bashrc

# ===== TOOLKIT BASH PRAKTIKUM =====

# PATH
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

# Alias
alias ll='ls -lah --color=auto'
alias gs='git status'

# Fungsi
sysinfo() {
    echo "User     : $(whoami)"
    echo "Host     : $(hostname)"
    echo "Uptime   : $(uptime -p)"
}

# ===== END TOOLKIT =====

EOF
fafiq@fafiq-ubuntu:~$ source ~/.bashrc
fafiq@fafiq-ubuntu:~$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash

echo "=== RINGKASAN SISTEM ==="
echo "Tanggal  : $(date)"
echo "User     : $(whoami)"
echo "Hostname : $(hostname)"
echo "Uptime   : $(uptime -p)"
echo "Memori   :"
free -h
echo "Disk /   :"
df -h /
EOF
fafiq@fafiq-ubuntu:~$ chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
fafiq@fafiq-ubuntu:~$ cd ~
ringkas-sistem
=== RINGKASAN SISTEM ===
Tanggal  : Tue Apr 28 09:43:26 PM WIB 2026
User     : fafiq
Hostname : fafiq-ubuntu
Uptime   : up 32 minutes
Memori   :
               total        used        free      shared  buff/cache   available
Mem:            14Gi       3.8Gi       8.5Gi        99Mi       2.7Gi        11Gi
Swap:          4.0Gi          0B       4.0Gi
Disk /   :
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   94G   15G   75G  17% /
fafiq@fafiq-ubuntu:~$ echo "$PATH"
type ll
type sysinfo
type ringkas-sistem
/home/fafiq/praktikum-os/week07-bash/bin:/home/fafiq/praktikum-os/week07-bash/bin:/home/fafiq/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
ll is aliased to `ls -lah --color=auto'
sysinfo is a function
sysinfo () 
{ 
    echo "User     : $(whoami)";
    echo "Host     : $(hostname)";
    echo "Uptime   : $(uptime -p)"
}
ringkas-sistem is hashed (/home/fafiq/praktikum-os/week07-bash/bin/ringkas-sistem)
fafiq@fafiq-ubuntu:~$ {
echo "=== TOOLKIT BASH REPORT ==="
date

echo
echo "PATH:"
echo "$PATH"

echo
echo "TYPE CHECK:"
type ll
type sysinfo
type ringkas-sistem

echo
echo "TEST SCRIPT:"
ringkas-sistem

} | tee ~/praktikum-os/week07-bash/toolkit-bash-report.txt
=== TOOLKIT BASH REPORT ===
Tue Apr 28 09:43:41 PM WIB 2026

PATH:
/home/fafiq/praktikum-os/week07-bash/bin:/home/fafiq/praktikum-os/week07-bash/bin:/home/fafiq/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin

TYPE CHECK:
ll is aliased to `ls -lah --color=auto'
sysinfo is a function
sysinfo () 
{ 
    echo "User     : $(whoami)";
    echo "Host     : $(hostname)";
    echo "Uptime   : $(uptime -p)"
}
ringkas-sistem is hashed (/home/fafiq/praktikum-os/week07-bash/bin/ringkas-sistem)

TEST SCRIPT:
=== RINGKASAN SISTEM ===
Tanggal  : Tue Apr 28 09:43:41 PM WIB 2026
User     : fafiq
Hostname : fafiq-ubuntu
Uptime   : up 32 minutes
Memori   :
               total        used        free      shared  buff/cache   available
Mem:            14Gi       3.8Gi       8.5Gi        99Mi       2.7Gi        11Gi
Swap:          4.0Gi          0B       4.0Gi
Disk /   :
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   94G   15G   75G  17% /
fafiq@fafiq-ubuntu:~$ 
```
#### Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cd ~/praktikum-os/week07-bash
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ REPORT="audit-konfigurasi-$(date +%F).txt"
ERROR_LOG="audit-error.log"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ {
echo "=== AUDIT FILE KONFIGURASI ==="
date

echo
echo "Daftar file .conf di /etc:"
find /etc -type f -name "*.conf"

echo
echo "Jumlah file:"
find /etc -type f -name "*.conf" | wc -l

echo
echo "Catatan:"
echo "Pemisahan stdout dan stderr penting agar error tidak mengganggu hasil utama."
echo "stdout berisi data utama, stderr berisi error."
echo "Ini membantu analisis lebih bersih dan profesional."

} > "$REPORT" 2> "$ERROR_LOG"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ cat "$REPORT" | tee -a "$REPORT"
=== AUDIT FILE KONFIGURASI ===
Tue Apr 28 09:45:18 PM WIB 2026

Daftar file .conf di /etc:
/etc/ucf.conf
/etc/ipp-usb/ipp-usb.conf
/etc/bluetooth/input.conf
/etc/bluetooth/network.conf
/etc/bluetooth/main.conf
/etc/speech-dispatcher/clients/emacs.conf
/etc/speech-dispatcher/modules/epos-generic.conf
/etc/speech-dispatcher/modules/mary-generic.conf
/etc/speech-dispatcher/modules/dtk-generic.conf
/etc/speech-dispatcher/modules/mimic3-generic.conf
/etc/speech-dispatcher/modules/espeak-ng.conf
/etc/speech-dispatcher/modules/flite.conf
/etc/speech-dispatcher/modules/espeak-ng-mbrola-generic.conf
/etc/speech-dispatcher/modules/espeak-ng-mbrola.conf
/etc/speech-dispatcher/modules/espeak.conf
/etc/speech-dispatcher/modules/swift-generic.conf
/etc/speech-dispatcher/modules/openjtalk.conf
/etc/speech-dispatcher/modules/festival.conf
/etc/speech-dispatcher/modules/espeak-mbrola-generic.conf
/etc/speech-dispatcher/modules/llia_phon-generic.conf
/etc/speech-dispatcher/modules/cicero.conf
/etc/speech-dispatcher/speechd.conf
/etc/selinux/semanage.conf
/etc/UPower/UPower.conf
/etc/logrotate.conf
/etc/pam.conf
/etc/environment.d/90qt-a11y.conf
/etc/environment.d/90atk-adaptor.conf
/etc/ghostscript/fontmap.d/10fonts-urw-base35.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan2.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-cns1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-gb1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-korea1.conf
/etc/brltty.conf
/etc/fprintd.conf
/etc/modprobe.d/blacklist-modem.conf
/etc/modprobe.d/blacklist-firewire.conf
/etc/modprobe.d/amd64-microcode-blacklist.conf
/etc/modprobe.d/blacklist.conf
/etc/modprobe.d/intel-microcode-blacklist.conf
/etc/modprobe.d/blacklist-rare-network.conf
/etc/modprobe.d/blacklist-ath_pci.conf
/etc/modprobe.d/iwlwifi.conf
/etc/modprobe.d/alsa-base.conf
/etc/modprobe.d/blacklist-framebuffer.conf
/etc/gtk-3.0/im-multipress.conf
/etc/ca-certificates.conf
/etc/apparmor/parser.conf
/etc/depmod.d/ubuntu.conf
/etc/rsyslog.d/20-ufw.conf
/etc/rsyslog.d/50-default.conf
/etc/rsyslog.d/21-cloudinit.conf
/etc/fonts/snap-override/10-prefer-noto.conf
/etc/fonts/fonts.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-serif.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans.conf
/etc/fonts/conf.avail/30-droid-noto.conf
/etc/fonts/conf.avail/57-dejavu-sans-mono.conf
/etc/fonts/conf.avail/57-dejavu-sans.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/57-dejavu-serif.conf
/etc/fonts/conf.avail/65-droid-sans-fallback.conf
/etc/fonts/conf.avail/58-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/30-droid-noto-mono.conf
/etc/rygel.conf
/etc/security/group.conf
/etc/security/access.conf
/etc/security/pam_env.conf
/etc/security/limits.conf
/etc/security/faillock.conf
/etc/security/namespace.conf
/etc/security/limits.d/25-pw-rlimits.conf
/etc/security/limits.d/10-gamemode.conf
/etc/security/pwquality.conf
/etc/security/pwhistory.conf
/etc/security/sepermit.conf
/etc/security/capability.conf
/etc/security/time.conf
/etc/snmp/snmp.conf
/etc/udisks2/udisks2.conf
/etc/apport/crashdb.conf
/etc/deluser.conf
/etc/nsswitch.conf
/etc/adduser.conf
/etc/avahi/avahi-daemon.conf
/etc/PackageKit/Vendor.conf
/etc/PackageKit/PackageKit.conf
/etc/initramfs-tools/initramfs.conf
/etc/initramfs-tools/update-initramfs.conf
/etc/e2scrub.conf
/etc/modules-load.d/cups-filters.conf
/etc/apg.conf
/etc/libaudit.conf
/etc/geoclue/geoclue.conf
/etc/libao.conf
/etc/sudo.conf
/etc/kerneloops.conf
/etc/sensors3.conf
/etc/nftables.conf
/etc/ld.so.conf
/etc/usb_modeswitch.conf
/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
/etc/NetworkManager/NetworkManager.conf
/etc/dbus-1/system.d/com.ubuntu.WhoopsiePreferences.conf
/etc/dbus-1/system.d/com.redhat.NewPrinterNotification.conf
/etc/dbus-1/system.d/kerneloops.conf
/etc/dbus-1/system.d/org.debian.apt.conf
/etc/dbus-1/system.d/com.ubuntu.SoftwareProperties.conf
/etc/dbus-1/system.d/org.opensuse.CupsPkHelper.Mechanism.conf
/etc/dbus-1/system.d/com.hp.hplip.conf
/etc/dbus-1/system.d/com.ubuntu.LanguageSelector.conf
/etc/dbus-1/system.d/com.redhat.PrinterDriversInstaller.conf
/etc/systemd/timesyncd.conf
/etc/systemd/sleep.conf
/etc/systemd/oomd.conf
/etc/systemd/resolved.conf
/etc/systemd/pstore.conf
/etc/systemd/journald.conf
/etc/systemd/system.conf
/etc/systemd/networkd.conf
/etc/systemd/user.conf
/etc/systemd/logind.conf
/etc/sane.d/sceptre.conf
/etc/sane.d/apple.conf
/etc/sane.d/canon_lide70.conf
/etc/sane.d/u12.conf
/etc/sane.d/kvs1025.conf
/etc/sane.d/snapscan.conf
/etc/sane.d/net.conf
/etc/sane.d/fujitsu.conf
/etc/sane.d/agfafocus.conf
/etc/sane.d/artec_eplus48u.conf
/etc/sane.d/sharp.conf
/etc/sane.d/hp5400.conf
/etc/sane.d/hp4200.conf
/etc/sane.d/sp15c.conf
/etc/sane.d/epsonds.conf
/etc/sane.d/cardscan.conf
/etc/sane.d/mustek_pp.conf
/etc/sane.d/abaton.conf
/etc/sane.d/saned.conf
/etc/sane.d/hp.conf
/etc/sane.d/hpsj5s.conf
/etc/sane.d/gphoto2.conf
/etc/sane.d/microtek2.conf
/etc/sane.d/epson2.conf
/etc/sane.d/pie.conf
/etc/sane.d/sm3840.conf
/etc/sane.d/ibm.conf
/etc/sane.d/epson.conf
/etc/sane.d/xerox_mfp.conf
/etc/sane.d/avision.conf
/etc/sane.d/microtek.conf
/etc/sane.d/epjitsu.conf
/etc/sane.d/umax1220u.conf
/etc/sane.d/coolscan3.conf
/etc/sane.d/dll.conf
/etc/sane.d/umax_pp.conf
/etc/sane.d/tamarack.conf
/etc/sane.d/umax.conf
/etc/sane.d/plustek_pp.conf
/etc/sane.d/canon630u.conf
/etc/sane.d/plustek.conf
/etc/sane.d/teco2.conf
/etc/sane.d/rts8891.conf
/etc/sane.d/escl.conf
/etc/sane.d/s9036.conf
/etc/sane.d/dmc.conf
/etc/sane.d/pixma.conf
/etc/sane.d/airscan.conf
/etc/sane.d/test.conf
/etc/sane.d/teco3.conf
/etc/sane.d/leo.conf
/etc/sane.d/genesys.conf
/etc/sane.d/qcam.conf
/etc/sane.d/dc240.conf
/etc/sane.d/hp3900.conf
/etc/sane.d/artec.conf
/etc/sane.d/bh.conf
/etc/sane.d/dc25.conf
/etc/sane.d/magicolor.conf
/etc/sane.d/dc210.conf
/etc/sane.d/stv680.conf
/etc/sane.d/ricoh.conf
/etc/sane.d/canon_dr.conf
/etc/sane.d/p5.conf
/etc/sane.d/coolscan.conf
/etc/sane.d/dell1600n_net.conf
/etc/sane.d/hs2p.conf
/etc/sane.d/matsushita.conf
/etc/sane.d/kodakaio.conf
/etc/sane.d/mustek.conf
/etc/sane.d/ma1509.conf
/etc/sane.d/mustek_usb.conf
/etc/sane.d/canon.conf
/etc/sane.d/coolscan2.conf
/etc/sane.d/kodak.conf
/etc/sane.d/lexmark.conf
/etc/sane.d/teco1.conf
/etc/sane.d/pieusb.conf
/etc/sane.d/canon_pp.conf
/etc/sane.d/nec.conf
/etc/sane.d/gt68xx.conf
/etc/sane.d/st400.conf
/etc/cracklib/cracklib.conf
/etc/fuse.conf
/etc/apt/apt.conf.d/20apt-esm-hook.conf
/etc/apt/apt.conf.d/20snapd.conf
/etc/ldap/ldap.conf
/etc/mke2fs.conf
/etc/host.conf
/etc/dhcpcd.conf
/etc/init/whoopsie.conf
/etc/pnm2ppa.conf
/etc/gai.conf
/etc/udev/iocost.conf
/etc/udev/udev.conf
/etc/sudo_logsrvd.conf
/etc/ufw/ufw.conf
/etc/ufw/sysctl.conf
/etc/rsyslog.conf
/etc/hdparm.conf
/etc/hp/hplip.conf
/etc/debconf.conf
/etc/xattr.conf
/etc/locale.conf
/etc/ubuntu-advantage/uaclient.conf
/etc/sysctl.d/10-network-security.conf
/etc/sysctl.d/10-magic-sysrq.conf
/etc/sysctl.d/10-kernel-hardening.conf
/etc/sysctl.d/10-zeropage.conf
/etc/sysctl.d/10-console-messages.conf
/etc/sysctl.d/10-map-count.conf
/etc/sysctl.d/10-ptrace.conf
/etc/sysctl.d/10-bufferbloat.conf
/etc/sysctl.d/10-ipv6-privacy.conf
/etc/ld.so.conf.d/libc.conf
/etc/ld.so.conf.d/x86_64-linux-gnu.conf
/etc/gdm3/custom.conf
/etc/pulse/client.conf
/etc/sysctl.conf
/etc/xdg/user-dirs.conf
/etc/cups/snmp.conf
/etc/cups/cups-files.conf
/etc/cups/cupsd.conf
/etc/cups/printers.conf
/etc/cups/subscriptions.conf
/etc/cups/cups-browsed.conf
/etc/gtk-2.0/im-multipress.conf
/etc/fwupd/fwupd.conf
/etc/fwupd/remotes.d/lvfs.conf
/etc/fwupd/remotes.d/vendor-directory.conf
/etc/fwupd/remotes.d/lvfs-testing.conf

Jumlah file:
259

Catatan:
Pemisahan stdout dan stderr penting agar error tidak mengganggu hasil utama.
stdout berisi data utama, stderr berisi error.
Ini membantu analisis lebih bersih dan profesional.
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ cat "$ERROR_LOG"
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/rules.d’: Permission denied
find: ‘/etc/credstore’: Permission denied
find: ‘/etc/sssd’: Permission denied
find: ‘/etc/credstore.encrypted’: Permission denied
find: ‘/etc/cups/ssl’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/rules.d’: Permission denied
find: ‘/etc/credstore’: Permission denied
find: ‘/etc/sssd’: Permission denied
find: ‘/etc/credstore.encrypted’: Permission denied
find: ‘/etc/cups/ssl’: Permission denied
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ ls -lah audit-konfigurasi-*.txt
-rw-rw-r-- 1 fafiq fafiq 17K Apr 28 21:45 audit-konfigurasi-2026-04-28.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ ls -lah audit-error.log
-rw-rw-r-- 1 fafiq fafiq 578 Apr 28 21:45 audit-error.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash$ 
```
#### Tugas Praktikum 3 — Mini Health Check Harian Server
#### Hasil
```
fafiq@fafiq-ubuntu:~$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/daily-healthcheck
#!/usr/bin/env bash

LOGFILE="$HOME/praktikum-os/week07-bash/healthcheck-$(date +%F).log"

{
echo "=== DAILY HEALTH CHECK ==="
echo "Tanggal   : $(date)"
echo "Hostname  : $(hostname)"
echo "User      : $(whoami)"
echo "Shell     : $0"
echo

echo "=== UPTIME ==="
uptime -p
echo

echo "=== MEMORY ==="
free -h
echo

echo "=== DISK ROOT ==="
df -h /
echo

echo "=== HISTORY TERAKHIR ==="
history | tail -n 10

} | tee "$LOGFILE"

# cek exit status
if [ ${PIPESTATUS[0]} -eq 0 ]; then
    echo "Health check sukses"
else
    echo "Ada error saat health check"
fi
EOF
fafiq@fafiq-ubuntu:~$ chmod +x ~/praktikum-os/week07-bash/bin/daily-healthcheck
fafiq@fafiq-ubuntu:~$ daily-healthcheck
=== DAILY HEALTH CHECK ===
Tanggal   : Tue Apr 28 09:47:40 PM WIB 2026
Hostname  : fafiq-ubuntu
User      : fafiq
Shell     : /home/fafiq/praktikum-os/week07-bash/bin/daily-healthcheck

=== UPTIME ===
up 36 minutes

=== MEMORY ===
               total        used        free      shared  buff/cache   available
Mem:            14Gi       3.9Gi       8.4Gi        99Mi       2.8Gi        11Gi
Swap:          4.0Gi          0B       4.0Gi

=== DISK ROOT ===
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   94G   15G   75G  17% /

=== HISTORY TERAKHIR ===
Health check sukses
fafiq@fafiq-ubuntu:~$ ls -lah ~/praktikum-os/week07-bash/healthcheck-*.log
-rw-rw-r-- 1 fafiq fafiq 572 Apr 28 21:47 /home/fafiq/praktikum-os/week07-bash/healthcheck-2026-04-28.log
fafiq@fafiq-ubuntu:~$ cat ~/praktikum-os/week07-bash/healthcheck-*.log
=== DAILY HEALTH CHECK ===
Tanggal   : Tue Apr 28 09:47:40 PM WIB 2026
Hostname  : fafiq-ubuntu
User      : fafiq
Shell     : /home/fafiq/praktikum-os/week07-bash/bin/daily-healthcheck

=== UPTIME ===
up 36 minutes

=== MEMORY ===
               total        used        free      shared  buff/cache   available
Mem:            14Gi       3.9Gi       8.4Gi        99Mi       2.8Gi        11Gi
Swap:          4.0Gi          0B       4.0Gi

=== DISK ROOT ===
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   94G   15G   75G  17% /

=== HISTORY TERAKHIR ===
fafiq@fafiq-ubuntu:~$ 
```
#### Tugas Praktikum 4 — Penanganan File dengan Nama Kompleks dan Arsip Aman
#### Hasil
```
fafiq@fafiq-ubuntu:~$ mkdir -p ~/praktikum-os/week07-bash/tugas4
cd ~/praktikum-os/week07-bash/tugas4
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ touch "laporan harian.txt"
touch "laporan mingguan.txt"
touch "backup [server].conf"
touch data-01.log data-02.log data-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ ls -lah
total 8.0K
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:48  .
drwxrwxr-x 8 fafiq fafiq 4.0K Apr 28 21:48  ..
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48 'backup [server].conf'
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48  data-01.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48  data-02.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48  data-03.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48 'laporan harian.txt'
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:48 'laporan mingguan.txt'
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ cat "laporan harian.txt"
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ echo *.log
data-01.log data-02.log data-03.log
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ mkdir -p backup
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ cp -- "laporan harian.txt" backup/
cp -- "laporan mingguan.txt" backup/
cp -- "backup [server].conf" backup/
cp -- *.log backup/
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ ls -lah backup
total 8.0K
drwxrwxr-x 2 fafiq fafiq 4.0K Apr 28 21:50  .
drwxrwxr-x 3 fafiq fafiq 4.0K Apr 28 21:50  ..
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50 'backup [server].conf'
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50  data-01.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50  data-02.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50  data-03.log
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50 'laporan harian.txt'
-rw-rw-r-- 1 fafiq fafiq    0 Apr 28 21:50 'laporan mingguan.txt'
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ tar -czf backup-arsip-$(date +%F).tar.gz backup
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ history | tail -n 30 > riwayat-arsip.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ cat riwayat-arsip.txt
if [ ${PIPESTATUS[0]} -eq 0 ]; then
    echo "Health check sukses"
else
    echo "Ada error saat health check"
fi
EOF

  319  chmod +x ~/praktikum-os/week07-bash/bin/daily-healthcheck
  320  daily-healthcheck
  321  ls -lah ~/praktikum-os/week07-bash/healthcheck-*.log
  322  cat ~/praktikum-os/week07-bash/healthcheck-*.log
  323  clear
  324  mkdir -p ~/praktikum-os/week07-bash/tugas4
  325  cd ~/praktikum-os/week07-bash/tugas4
  326  touch "laporan harian.txt"
  327  touch "laporan mingguan.txt"
  328  touch "backup [server].conf"
  329  touch data-01.log data-02.log data-03.log
  330  ls -lah
  331  cat laporan harian.txt
  332  cat "laporan harian.txt"
  333  echo *.log
  334  mkdir -p backup
  335  cp -- "laporan harian.txt" backup/
  336  cp -- "laporan mingguan.txt" backup/
  337  cp -- "backup [server].conf" backup/
  338  cp -- *.log backup/
  339  ls -lah backup
  340  tar -czf backup-arsip-$(date +%F).tar.gz backup
  341  history | tail -n 30 > riwayat-arsip.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week07-bash/tugas4$ 
```
