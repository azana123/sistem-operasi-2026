# Laporan Praktikum Sistem Operasi Pertemuan Ke-10

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

### Praktikum 10.1 Melihat Penggunaan Memori
#### Prompt
```
mkdir -p ~/praktikum-os/week10-memory
cd ~/praktikum-os/week10-memory

free -h

cat /proc/meminfo | head -n 20
```

#### Hasil
```
fafiq@fafiq-ubuntu:~$ mkdir -p ~/praktikum-os/week10-memory
cd ~/praktikum-os/week10-memory
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ free -h
               total        used        free      shared  buff/cache   available
Mem:            14Gi       4.7Gi       7.3Gi       144Mi       2.9Gi        10Gi
Swap:          4.0Gi          0B       4.0Gi
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ cat /proc/meminfo | head -n 20
MemTotal:       15636212 kB
MemFree:         7647300 kB
MemAvailable:   10743152 kB
Buffers:           92728 kB
Cached:          2825928 kB
SwapCached:            0 kB
Active:          4343608 kB
Inactive:        1581504 kB
Active(anon):    2625596 kB
Inactive(anon):        0 kB
Active(file):    1718012 kB
Inactive(file):  1581504 kB
Unevictable:          32 kB
Mlocked:              32 kB
SwapTotal:       4194300 kB
SwapFree:        4194300 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:              3000 kB
Writeback:             0 kB
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```
#### Analisis
#### Prompt
```
free | awk '/Mem/ {printf "%.2f%%\n", $7/$2*100}'

cat /proc/meminfo
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ free | awk '/Mem/ {printf "%.2f%%\n", $7/$2*100}'
68.23%
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ cat /proc/meminfo
MemTotal:       15636212 kB
MemFree:         7595424 kB
MemAvailable:   10695948 kB
Buffers:           93588 kB
Cached:          2829052 kB
SwapCached:            0 kB
Active:          4399120 kB
Inactive:        1586076 kB
Active(anon):    2681108 kB
Inactive(anon):        0 kB
Active(file):    1718012 kB
Inactive(file):  1586076 kB
Unevictable:          32 kB
Mlocked:              32 kB
SwapTotal:       4194300 kB
SwapFree:        4194300 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:              5408 kB
Writeback:             0 kB
AnonPages:       3062936 kB
Mapped:           937976 kB
Shmem:            148276 kB
KReclaimable:     103080 kB
Slab:             430596 kB
SReclaimable:     103080 kB
SUnreclaim:       327516 kB
KernelStack:       22976 kB
PageTables:        48916 kB
SecPageTables:      3364 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:    12012404 kB
Committed_AS:   14056944 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       88992 kB
VmallocChunk:          0 kB
Percpu:            18112 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:      2048 kB
FilePmdMapped:         0 kB
CmaTotal:              0 kB
CmaFree:               0 kB
Unaccepted:            0 kB
Balloon:               0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:     1630916 kB
DirectMap2M:     8112128 kB
DirectMap1G:     7340032 kB
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```
##### 1. Dari hasil diatas, didapatkan memori yang tersedia adalah 68% yang artinya sistem dalam kondisi normal dan tidak kekurangan ram (diatas 10%)
##### 2. Dari hasil diatas, didapatkan Swap: 4.0Gi total, 0B used dimana 0B used yang artinya tidak pernah menggunakan swap
##### 3. Dari /proc/meminfo didapatkan Buffers: 92728 kB, Cached: 2825928 kB. Dari free -h didapatkan buff/cache: 2.9Gi menunjukan RAM digunakan sebagai cache oleh kernel

### Praktikum 10.2 Mengamati Aktivitas Paging
#### Prompt
```
vmstat 1 5
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 0  0      0 7591220  95076 2945496    0    0   385   189 5640    2  2  0 98  0  0  0
 0  0      0 7590848  95076 2945520    0    0     0   484 1151 1003  1  0 99  0  0  0
 0  0      0 7591292  95100 2945520    0    0     0   144 1011  803  0  0 99  0  0  0
 0  0      0 7595000  95100 2945524    0    0     0     0 10506 10632  6  1 93  0  0  0
 0  0      0 7593312  95100 2945548    0    0     0     0 10357 9122  5  1 94  0  0  0
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```
#### Analisis
##### 1. Dari hasil diatas, didapati bahwa tidak ada aktivitas swap sama sekali
##### 2. Dari hasil diatas, didapati bahwa sistem dalam kondisi normal tanpa memory pressure
##### 3. Dari hasil diatas, didapati bahwa masih tersedia banyak ram, CPU banyak yang berada dalam kondisi idle, dan RAM banyak yang dialokasikan sebagai cache dan baru dilepas kalau sistem membutuhkan lebih banyak ram (Dari hasil analisis nomor 3 inilah bukti kenapa saya suka linux. Sangat hemat resource. Di windows, laptop yang sama akan menggunakan sekitar 60% dari RAM dalam kondisi idle)

### Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
#### Prompt
```
sudo fallocate -l 512M /swapfile-week10

sudo chmod 600 /swapfile-week10

sudo mkswap /swapfile-week10
sudo swapon /swapfile-week10

swapon --show
free -h

cat /proc/sys/vm/swappiness

sudo sysctl vm.swappiness=10

cat /proc/sys/vm/swappiness
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ sudo fallocate -l 512M /swapfile-week10
[sudo] password for fafiq: 
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ sudo chmod 600 /swapfile-week10
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ sudo mkswap /swapfile-week10
sudo swapon /swapfile-week10
Setting up swapspace version 1, size = 512 MiB (536866816 bytes)
no label, UUID=5c605ae4-edf1-4c31-8e79-a6bf6ce4ce11
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ swapon --show
free -h
NAME             TYPE SIZE USED PRIO
/swap.img        file   4G   0B   -2
/swapfile-week10 file 512M   0B   -3
               total        used        free      shared  buff/cache   available
Mem:            14Gi       4.6Gi       7.3Gi       144Mi       2.9Gi        10Gi
Swap:          4.5Gi          0B       4.5Gi
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ cat /proc/sys/vm/swappiness
60
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ sudo sysctl vm.swappiness=10
vm.swappiness = 10
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ cat /proc/sys/vm/swappiness
10
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```

#### Analisis
##### 1. Dari hasil diatas, didapati bahwa nilai default swappiness adalah 60
##### 2. Nilai swappiness kemudian diubah menjadi 10
##### 3. Dari hasil diatas, ada 2 swap yang aktif saat ini, dari sebelumnya 4.0Gi, menjadi 4.5Gi
##### 4. Swap belum pernah digunakan. Artinya sistem tidak pernah kekurangan RAM

### Praktikum 10.4 Monitoring Memory
#### Prompt
```
ps aux --sort=-%mem | head

top
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ ps aux --sort=-%mem | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
fafiq       3801  6.5  5.0 12647696 782848 ?     Sl   16:28   7:17 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       9152  4.4  4.4 3520404 691404 ?      Sl   17:31   2:08 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:45070 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {6d5c18f4-ae85-4f65-83dd-61d081b52790} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 17 tab
fafiq       6327  5.5  2.6 1465117768 422092 ?   Sl   16:36   5:40 /usr/share/code/code --type=zygote
fafiq       2901  7.3  2.6 5836072 412660 ?      Ssl  16:27   8:13 /usr/bin/gnome-shell
fafiq       4796  0.9  2.5 7219968 397272 ?      Sl   16:28   1:00 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44603 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {e5aec762-c31c-48d1-96e9-5da2ed287189} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 7 tab
fafiq       4831  0.2  1.9 2892400 311752 ?      Sl   16:28   0:18 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44603 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {faf21793-576d-437b-bfe0-b4f79ff8517f} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 9 tab
fafiq       6211  0.7  1.6 1461671024 253712 ?   SLl  16:36   0:47 /usr/share/code/code
fafiq       6264  1.6  1.5 51390504 245324 ?     Sl   16:36   1:43 /usr/share/code/code --type=zygote --no-zygote-sandbox
fafiq       6364  0.5  1.4 1461350880 230048 ?   Sl   16:36   0:36 /proc/self/exe --type=utility --utility-sub-type=node.mojom.NodeService --lang=en-US --service-sandbox-type=none --render-node-override=/dev/dri/renderD128 --dns-result-order=ipv4first --experimental-network-inspection --inspect-port=0 --js-flags=--nodecommit_pooled_pages --crashpad-handler-pid=6241 --enable-crash-reporter=9f087d08-a067-4f53-bfef-10d3b83556b8,no_channel --user-data-dir=/home/fafiq/.config/Code --standard-schemes=vscode-webview,vscode-file --enable-sandbox --secure-schemes=vscode-webview,vscode-file --cors-schemes=vscode-webview,vscode-file --fetch-schemes=vscode-webview,vscode-file --service-worker-schemes=vscode-webview --code-cache-schemes=vscode-webview,vscode-file --shared-files=v8_context_snapshot_data:100 --field-trial-handle=3,i,4758719632583030802,13021146008621061858,262144 --enable-features=DocumentPolicyIncludeJSCallStacksInCrashReports,EarlyEstablishGpuChannel,EstablishGpuChannelAsync --disable-features=CalculateNativeWinOcclusion,LocalNetworkAccessChecks,ScreenAIOCREnabled,SpareRendererForSitePerProcess,TraceSiteInstanceGetProcessCreation --variations-seed-version --trace-process-track-uuid=3190708992871164437


fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ top
top - 18:19:28 up  1:52,  1 user,  load average: 0.69, 0.68, 0.60
Tasks: 399 total,   1 running, 398 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.4 us,  0.4 sy,  0.0 ni, 98.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem : 32.2/15269.7  [||||||||||||||||||||||||||||||||                                                                    ] 
MiB Swap:  0.0/4096.0   [                                                                                                    ] 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                                
   2901 fafiq     20   0 5825872 412840 178352 S  14.0   2.6   8:15.82 gnome-shell                                                                                                            
   9152 fafiq     20   0 3520404 699908 135052 S   6.0   4.5   2:09.55 Isolated Web Co                                                                                                        
   3801 fafiq     20   0   12.1g 782996 366284 S   5.3   5.0   7:18.83 firefox                                                                                                                
    778 root     -51   0       0      0      0 S   0.7   0.0   0:28.43 irq/105-rtw89_pci                                                                                                      
   4796 fafiq     20   0 7219968 397436 166472 S   0.7   2.5   1:00.35 Isolated Web Co                                                                                                        
  10193 root      20   0       0      0      0 I   0.7   0.0   0:08.57 kworker/u64:3-gfx_0.0.0                                                                                                
   3229 fafiq     20   0  429204  29796  18604 S   0.3   0.2   0:05.16 ibus-extension-                                                                                                        
   3496 fafiq     20   0 2635844 224676 120368 S   0.3   1.4   0:03.11 xdg-desktop-por                                                                                                        
   4067 fafiq     20   0 2698536 175436  98488 S   0.3   1.1   0:10.42 Privileged Cont                                                                                                        
   6264 fafiq     20   0   49.0g 244428 133952 S   0.3   1.6   1:43.66 code                                                                                                                   
   8894 root      20   0       0      0      0 D   0.3   0.0   0:09.97 kworker/u64:4+events_unbound                                                                                           
  10801 root      20   0       0      0      0 I   0.3   0.0   0:00.04 kworker/8:1-mm_percpu_wq                                                                                               
  10965 root      20   0       0      0      0 I   0.3   0.0   0:00.01 kworker/9:1-mm_percpu_wq                                                                                               
  11177 root      20   0       0      0      0 I   0.3   0.0   0:00.84 kworker/u64:0-comp_1.3.1                                                                                               
  11248 fafiq     20   0   23228   6208   3932 R   0.3   0.0   0:00.03 top                                                                                                                    
      1 root      20   0   23500  14928   9848 S   0.0   0.1   0:01.42 systemd                                                                                                                
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.03 kthreadd                                                                                                               
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                                                                                                 
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp                                                                                                       
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-sync_wq                                                                                                      
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kvfree_rcu_reclaim                                                                                           
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_flushwq                                                                                                 
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns                                                                                                        
     11 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri                                                                                            
     13 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_percpu_wq                                                                                                 
     14 root      20   0       0      0      0 S   0.0   0.0   0:00.06 ksoftirqd/0                                                                                                            
     15 root      20   0       0      0      0 I   0.0   0.0   0:07.27 rcu_preempt                                                                                                            
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_exp_par_gp_kthread_worker/0                                                                                        
     17 root      20   0       0      0      0 S   0.0   0.0   0:00.02 rcu_exp_gp_kthread_worker                                                                                              
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.31 migration/0                                                                                                            
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/0                                                                                                          
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/0                                                                                                                
     21 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/1                                                                                                                
     22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/1                                                                                                          
     23 root      rt   0       0      0      0 S   0.0   0.0   0:00.83 migration/1                                                                                                            
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.02 ksoftirqd/1                                                                                                            
     26 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/1:0H-events_highpri                                                                                            
     27 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/2                                                                                                                
     28 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/2                                                                                                          
     29 root      rt   0       0      0      0 S   0.0   0.0   0:00.82 migration/2                                                                                                            
     30 root      20   0       0      0      0 S   0.0   0.0   0:00.01 ksoftirqd/2                                                                                                            
     32 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/2:0H-events_highpri                                                                                            
     33 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/3                                                                                                                
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```
#### Analisis
##### 1. Dari hasil diatas, didapati bahwa proses dengan penggunaan memori terbesar adalah firefox (sekitar 782848 KB / 1024 = 764 MB)
##### 2. Perbedaan VSZ dengan RSS adalah VSZ adalah total memori yang dialokasikan, sedangkan RSS adalah memori fisik yang terpakai atau yang benar benar digunakan
##### 3. Perbandingan PS dengan top adalah PS mengambil data sekali sedangkan top mengambil data secara real-time

### Praktikum 10.5 Script Monitor Memori
#### Prompt
```
cd ~/praktikum-os/week10-memory
nano monitor-memori.sh

#!/bin/bash
set -euo pipefail

THRESHOLD=20

echo "=== Monitor Memori ==="
date
echo

free -h
echo

AVAIL=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')

if [ "$AVAIL" -lt "$THRESHOLD" ]; then
    echo "PERINGATAN: Memori tersedia hanya ${AVAIL}%!"
else
    echo "Status: Memori tersedia ${AVAIL}% (normal)"
fi

echo
echo "--- 5 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 6 | tail -n 5

chmod +x monitor-memori.sh
bash monitor-memori.sh

```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ cd ~/praktikum-os/week10-memory
nano monitor-memori.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ chmod +x monitor-memori.sh
bash monitor-memori.sh
=== Monitor Memori ===
Fri May  1 06:25:17 PM WIB 2026

               total        used        free      shared  buff/cache   available
Mem:            14Gi       4.8Gi       7.1Gi       144Mi       2.9Gi        10Gi
Swap:          4.0Gi          0B       4.0Gi

Status: Memori tersedia 67% (normal)

--- 5 Proses Memori Tertinggi ---
fafiq       9152  5.0  5.0 3537912 787232 ?      Sl   17:31   2:43 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:45070 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {6d5c18f4-ae85-4f65-83dd-61d081b52790} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 17 tab
fafiq       3801  6.6  5.0 12629180 787200 ?     Sl   16:28   7:42 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       6327  5.7  2.7 1465112584 424120 ?   Sl   16:36   6:14 /usr/share/code/code --type=zygote
fafiq       2901  7.5  2.6 5836432 412904 ?      Ssl  16:27   8:48 /usr/bin/gnome-shell
fafiq       4796  0.8  2.5 7219968 397676 ?      Sl   16:28   1:01 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44603 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {e5aec762-c31c-48d1-96e9-5da2ed287189} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 7 tab
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```

#### Analisis
##### 1. Variabel THRESHOLD digunakan sebagai batas minimum persentase memori tersedia.
##### 2. Cara menghitung presentase memori adalah free | awk '/Mem/ {printf "%d", $7/$2*100}'. Dimana %7 adalah memori tersedia, %2 adalah total RAM dan dikali dengan 100%
##### 3. Pada perulangan, Jika AVAIL < THRESHOLD maka tampilkan peringatan,jika tidak, tampilkan status normal
##### 4. Dari hasil diatas, Status: Memori tersedia 67% (normal) maka memori jauh diatas 20% (threshold) artinya masih tersedia banyak memori kosong
### Praktikum 10.6 Mengamati System Call dengan strace
#### Prompt
```
strace ls 2>&1 | head -n 30

strace -c ls

strace -c ls /etc 2>&1 | tail -5
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ strace ls 2>&1 | head -n 30
execve("/usr/bin/ls", ["ls"], 0x7ffe1bf7ce10 /* 51 vars */) = 0
brk(NULL)                               = 0x57d5ddbc2000
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x77497e43e000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=64207, ...}) = 0
mmap(NULL, 64207, PROT_READ, MAP_PRIVATE, 3, 0) = 0x77497e42e000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=174472, ...}) = 0
mmap(NULL, 181960, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x77497e401000
mmap(0x77497e407000, 118784, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x77497e407000
mmap(0x77497e424000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x23000) = 0x77497e424000
mmap(0x77497e42a000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x29000) = 0x77497e42a000
mmap(0x77497e42c000, 5832, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x77497e42c000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\243\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
fstat(3, {st_mode=S_IFREG|0755, st_size=2125328, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x77497e000000
mmap(0x77497e028000, 1605632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x77497e028000
mmap(0x77497e1b0000, 323584, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0x77497e1b0000
mmap(0x77497e1ff000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1fe000) = 0x77497e1ff000
mmap(0x77497e205000, 52624, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x77497e205000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ strace -c ls
monitor-memori.sh
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 33.55    0.000203         203         1           execve
 22.15    0.000134           7        18           mmap
  7.11    0.000043          21         2           getdents64
  5.79    0.000035           5         7           openat
  5.29    0.000032           6         5           read
  5.29    0.000032           6         5           mprotect
  3.80    0.000023           2         9           close
  3.80    0.000023           2         8           fstat
  2.48    0.000015          15         1           munmap
  2.48    0.000015           7         2         2 statfs
  1.49    0.000009           3         3           brk
  1.32    0.000008           4         2         2 access
  1.16    0.000007           7         1           write
  0.99    0.000006           3         2           ioctl
  0.99    0.000006           3         2           pread64
  0.50    0.000003           3         1           arch_prctl
  0.50    0.000003           3         1           getrandom
  0.33    0.000002           2         1           set_tid_address
  0.33    0.000002           2         1           set_robust_list
  0.33    0.000002           2         1           prlimit64
  0.33    0.000002           2         1           rseq
------ ----------- ----------- --------- --------- ----------------
100.00    0.000605           8        74         4 total
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ strace -c ls /etc 2>&1 | tail -5
  0.22    0.000002           2         1           getrandom
  0.22    0.000002           2         1           rseq
  0.11    0.000001           1         1           set_robust_list
------ ----------- ----------- --------- --------- ----------------
100.00    0.000891          11        76         5 total
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```
#### Analisis
##### 1. System call yang dominan adalah mmap, diikuti openat, read, dan getdents64. mmap digunakan untuk memuat library ke memori, getdents64 digunakan untuk membaca isi direktori, openat, read, close untuk akses file.
##### 2. Fungsi system call utama execve adalah menjalankan program ls, mmap adalah load library ke RAM, getdents64 adalah membaca daftar file dalam direktori, openat adalah membuka file, read adalah membaca isi file, close adalah menutup file
##### 3. Dari hasil "errors = 4" terdapat error kecil, contohnya access atau statfs, dimana merupakan error yang tidak fatal dan program berjalan dengan baik
##### 4. ls berisi 74 system call, ls/etc berisi 76 system call artinya direktory etc berisi lebih banyak file

### Tugas
#### Prompt
```
nano diagnosa-server.sh

#!/bin/bash

LAPORAN="diagnosa-server-lambat.txt"
WARN_MEM=false
WARN_SWAP=0

cek_memori() {
    echo "--- Kondisi Memori ---"
    free -h
    echo

    AVAIL_PCT=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')

    if [ "$AVAIL_PCT" -lt 20 ]; then
        echo "PERINGATAN: Memori tersedia hanya ${AVAIL_PCT}%"
        WARN_MEM=true
    fi
}

cek_swap() {
    echo "--- Penggunaan Swap ---"
    swapon --show 2>/dev/null || echo "Tidak ada swap aktif"
    echo

    WARN_SWAP=$(free | awk '/Swap/ {print $3}')

    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "INFO: Swap digunakan (${WARN_SWAP} kB)"
    fi
}

cek_proses() {
    echo "--- 10 Proses Memori Tertinggi ---"
    ps aux --sort=-%mem | head -n 11
    echo
}

cek_paging() {
    echo "--- Aktivitas Paging (5 sampel) ---"
    vmstat 1 5
    echo
}

ringkasan() {
    echo "=== RINGKASAN ==="

    if [ "$WARN_MEM" = true ]; then
        echo "- Memori: KRITIS - perlu tindakan segera"
    else
        echo "- Memori: normal"
    fi

    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "- Swap: aktif - pantau aktivitas paging"
    else
        echo "- Swap: tidak digunakan"
    fi
}

{
    echo "=== LAPORAN DIAGNOSA SERVER ==="
    date
    echo

    cek_memori
    cek_swap
    cek_proses
    cek_paging
    ringkasan

} | tee "$LAPORAN"

echo
echo "Laporan disimpan ke: $LAPORAN"

chmod +x diagnosa-server.sh
bash diagnosa-server.sh
```

#### Hasil
```
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ nano diagnosa-server.sh
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ chmod +x diagnosa-server.sh
bash diagnosa-server.sh
=== LAPORAN DIAGNOSA SERVER ===
Fri May  1 06:44:38 PM WIB 2026

--- Kondisi Memori ---
               total        used        free      shared  buff/cache   available
Mem:            14Gi       5.0Gi       6.9Gi       116Mi       2.9Gi         9Gi
Swap:          4.0Gi          0B       4.0Gi

--- Penggunaan Swap ---
NAME      TYPE SIZE USED PRIO
/swap.img file   4G   0B   -2

--- 10 Proses Memori Tertinggi ---
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
fafiq       9152  6.3  5.5 3612748 873756 ?      Sl   17:31   4:38 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:45070 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {6d5c18f4-ae85-4f65-83dd-61d081b52790} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 17 tab
fafiq       3801  6.7  5.0 12500772 786724 ?     Sl   16:28   9:14 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       6327  5.9  2.8 1465112584 442756 ?   Sl   16:36   7:41 /usr/share/code/code --type=zygote
fafiq       2901  7.7  2.6 5836432 413536 ?      Ssl  16:27  10:33 /usr/bin/gnome-shell
fafiq       4796  0.8  2.2 7193080 357888 ?      Sl   16:28   1:10 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44603 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {e5aec762-c31c-48d1-96e9-5da2ed287189} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 7 tab
fafiq       4831  0.2  1.9 2892416 311836 ?      Sl   16:28   0:19 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44603 -prefMapHandle 1:283801 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {faf21793-576d-437b-bfe0-b4f79ff8517f} -parentPid 3801 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 9 tab
fafiq       6211  0.8  1.6 1461669936 254136 ?   SLl  16:36   1:03 /usr/share/code/code
fafiq       6264  1.7  1.5 51391400 244872 ?     Sl   16:36   2:18 /usr/share/code/code --type=zygote --no-zygote-sandbox
fafiq       6364  0.6  1.4 1461350880 233736 ?   Sl   16:36   0:49 /proc/self/exe --type=utility --utility-sub-type=node.mojom.NodeService --lang=en-US --service-sandbox-type=none --render-node-override=/dev/dri/renderD128 --dns-result-order=ipv4first --experimental-network-inspection --inspect-port=0 --js-flags=--nodecommit_pooled_pages --crashpad-handler-pid=6241 --enable-crash-reporter=9f087d08-a067-4f53-bfef-10d3b83556b8,no_channel --user-data-dir=/home/fafiq/.config/Code --standard-schemes=vscode-webview,vscode-file --enable-sandbox --secure-schemes=vscode-webview,vscode-file --cors-schemes=vscode-webview,vscode-file --fetch-schemes=vscode-webview,vscode-file --service-worker-schemes=vscode-webview --code-cache-schemes=vscode-webview,vscode-file --shared-files=v8_context_snapshot_data:100 --field-trial-handle=3,i,4758719632583030802,13021146008621061858,262144 --enable-features=DocumentPolicyIncludeJSCallStacksInCrashReports,EarlyEstablishGpuChannel,EstablishGpuChannelAsync --disable-features=CalculateNativeWinOcclusion,LocalNetworkAccessChecks,ScreenAIOCREnabled,SpareRendererForSitePerProcess,TraceSiteInstanceGetProcessCreation --variations-seed-version --trace-process-track-uuid=3190708992871164437
fafiq       3496  0.0  1.4 2635844 224676 ?      Ssl  16:27   0:03 /usr/libexec/xdg-desktop-portal-gnome

--- Aktivitas Paging (5 sampel) ---
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0 7265956 106604 2942448    0    0   273   174 5816    3  2  0 98  0  0  0
 0  0      0 7276380 106604 2942504    0    0     0     0 5523 3479  1  0 99  0  0  0
 0  0      0 7257256 106604 2946752    0    0     0     0 9492 6516  3  1 97  0  0  0
 0  0      0 7254724 106612 2946760    0    0     0   328 8785 10007  5  1 94  0  0  0
 1  0      0 7263552 106644 2946784    0    0     0   224 4357 4292  3  1 96  0  0  0

=== RINGKASAN ===
- Memori: normal
- Swap: tidak digunakan

Laporan disimpan ke: diagnosa-server-lambat.txt
fafiq@fafiq-ubuntu:~/praktikum-os/week10-memory$ 
```

#### Analisis
##### 1. cek_memori Berfungsi untuk menampilkan kondisi memori dan menghitung persentase memori tersedia. Jika di bawah threshold (20%), maka akan memberikan peringatan. cek_swap Berfungsi untuk menampilkan status penggunaan swap dan mendeteksi apakah swap sedang digunakan. cek_proses Menampilkan 10 proses dengan penggunaan memori tertinggi untuk mengetahui aplikasi yang paling banyak menggunakan RAM. cek_paging Menggunakan vmstat untuk memantau aktivitas paging (swap in dan swap out). ringkasan Memberikan kesimpulan kondisi sistem berdasarkan hasil pengecekan memori dan swap.
##### 2. Kondisi sistem normal. Memori tersedia sekitar 9Gi, threshold 20%, dan swap 0
##### 3. tee digunakan untuk menampilkan output ke layar sekaligus menyimpan ke file, sedangkan > hanya menyimpan ke file tanpa menampilkan ke layar
##### 4. Dari hasil vmstat, didapati si = 0, so = 0 artinya tidak ada aktivitas paging