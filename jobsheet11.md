# Laporan Praktikum Sistem Operasi Pertemuan Ke-12

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

## Service Management
### Prakitkum 1 Amati Layanan Aktif Saat Boot
#### Langkah 1
##### Prompt
```
systemctl list-units --type=service --state=running
```

##### Hasil
```
fafiq-ubuntu% systemctl list-units --type=service --state=running
  UNIT                           LOAD   ACTIVE SUB     DESCRIPTION                                                     
  accounts-daemon.service        loaded active running Accounts Service
  avahi-daemon.service           loaded active running Avahi mDNS/DNS-SD Stack
  bluetooth.service              loaded active running Bluetooth service
  colord.service                 loaded active running Manage, Install and Generate Color Profiles
  cron.service                   loaded active running Regular background program processing daemon
  cups-browsed.service           loaded active running Make remote CUPS printers available locally
  cups.service                   loaded active running CUPS Scheduler
  dbus.service                   loaded active running D-Bus System Message Bus
  fwupd.service                  loaded active running Firmware update daemon
  gdm.service                    loaded active running GNOME Display Manager
  gnome-remote-desktop.service   loaded active running GNOME Remote Desktop
  kerneloops.service             loaded active running Tool to automatically collect and submit kernel crash signatures
  ModemManager.service           loaded active running Modem Manager
  NetworkManager.service         loaded active running Network Manager
  polkit.service                 loaded active running Authorization Manager
  power-profiles-daemon.service  loaded active running Power Profiles daemon
  rsyslog.service                loaded active running System Logging Service
  rtkit-daemon.service           loaded active running RealtimeKit Scheduling Policy Service
  snap.cups.cups-browsed.service loaded active running Service for snap application cups.cups-browsed
  snap.cups.cupsd.service        loaded active running Service for snap application cups.cupsd
  snapd.service                  loaded active running Snap Daemon
  switcheroo-control.service     loaded active running Switcheroo Control Proxy service
  systemd-journald.service       loaded active running Journal Service
  systemd-logind.service         loaded active running User Login Management
  systemd-oomd.service           loaded active running Userspace Out-Of-Memory (OOM) Killer
  systemd-resolved.service       loaded active running Network Name Resolution
  systemd-timesyncd.service      loaded active running Network Time Synchronization
  systemd-udevd.service          loaded active running Rule-based Manager for Device Events and Files
  udisks2.service                loaded active running Disk Manager
  unattended-upgrades.service    loaded active running Unattended Upgrades Shutdown
  upower.service                 loaded active running Daemon for power management
  user@1000.service              loaded active running User Manager for UID 1000
  wpa_supplicant.service         loaded active running WPA supplicant

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization of SUB.
        SUB    → The low-level unit activation state, values depend on unit type.

33 loaded units listed.
```

#### Langkah 2
##### Prompt
```
systemctl list-unit-files --type=service | head -30
```

##### Hasil
```
fafiq-ubuntu% systemctl list-unit-files --type=service | head -30
UNIT FILE                                    STATE           PRESET
accounts-daemon.service                      enabled         enabled
alsa-restore.service                         static          -
alsa-state.service                           static          -
alsa-utils.service                           masked          enabled
anacron.service                              enabled         enabled
apparmor.service                             enabled         enabled
apport-autoreport.service                    static          -
apport-coredump-hook@.service                static          -
apport-forward@.service                      static          -
apport.service                               enabled         enabled
apt-daily-upgrade.service                    static          -
apt-daily.service                            static          -
apt-news.service                             static          -
autovt@.service                              alias           -
avahi-daemon.service                         enabled         enabled
bluetooth.service                            enabled         enabled
bolt.service                                 static          -
brltty-udev.service                          static          -
brltty.service                               disabled        enabled
cloud-config.service                         enabled         enabled
cloud-final.service                          enabled         enabled
cloud-init-hotplugd.service                  static          -
cloud-init-local.service                     enabled         enabled
cloud-init.service                           enabled         enabled
colord.service                               static          -
configure-printer@.service                   static          -
console-getty.service                        disabled        disabled
console-setup.service                        enabled         enabled
container-getty@.service                     static          -
```

#### Langkah 3
##### Prompt
```
systemd-analyze blame | sort -rh | head -3
```

##### Hasil
```
698ms fwupd.service
649ms boot-efi.mount
418ms NetworkManager.service
```
### Praktikum 2 Kelola Layanan SSH
#### Langkah 1
##### Prompt
```
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
```

##### Hasil
```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Sun 2026-06-07 13:16:46 WIB; 25s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 28435 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 28436 (sshd)
      Tasks: 1 (limit: 18078)
     Memory: 1.2M (peak: 1.7M)
        CPU: 13ms
     CGroup: /system.slice/ssh.service
             └─28436 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Jun 07 13:16:46 fafiq-ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Jun 07 13:16:46 fafiq-ubuntu sshd[28436]: Server listening on 0.0.0.0 port 22.
Jun 07 13:16:46 fafiq-ubuntu sshd[28436]: Server listening on :: port 22.
Jun 07 13:16:46 fafiq-ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
active
disabled
```

#### Langkah 2 & 3
##### Prompt
```
sudo systemctl restart ssh
systemctl status ssh
systemctl list-dependencies ssh
```

##### Hasil
```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Sun 2026-06-07 13:17:36 WIB; 5ms ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 28478 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 28480 (sshd)
      Tasks: 1 (limit: 18078)
     Memory: 1.9M (peak: 1.9M)
        CPU: 12ms
     CGroup: /system.slice/ssh.service
             └─28480 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Jun 07 13:17:36 fafiq-ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Jun 07 13:17:36 fafiq-ubuntu sshd[28480]: Server listening on 0.0.0.0 port 22.
Jun 07 13:17:36 fafiq-ubuntu sshd[28480]: Server listening on :: port 22.
Jun 07 13:17:36 fafiq-ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
ssh.service
● ├─-.mount
● ├─ssh.socket
● ├─system.slice
● └─sysinit.target
●   ├─apparmor.service
●   ├─dev-hugepages.mount
●   ├─dev-mqueue.mount
●   ├─keyboard-setup.service
●   ├─kmod-static-nodes.service
○   ├─ldconfig.service
●   ├─plymouth-read-write.service
●   ├─plymouth-start.service
●   ├─proc-sys-fs-binfmt_misc.automount
●   ├─setvtrgb.service
●   ├─sys-fs-fuse-connections.mount
●   ├─sys-kernel-config.mount
●   ├─sys-kernel-debug.mount
●   ├─sys-kernel-tracing.mount
○   ├─systemd-ask-password-console.path
●   ├─systemd-binfmt.service
○   ├─systemd-firstboot.service
○   ├─systemd-hwdb-update.service
○   ├─systemd-journal-catalog-update.service
●   ├─systemd-journal-flush.service
●   ├─systemd-journald.service
○   ├─systemd-machine-id-commit.service
●   ├─systemd-modules-load.service
○   ├─systemd-pcrmachine.service
○   ├─systemd-pcrphase-sysinit.service
○   ├─systemd-pcrphase.service
○   ├─systemd-pstore.service
●   ├─systemd-random-seed.service
○   ├─systemd-repart.service
●   ├─systemd-resolved.service
●   ├─systemd-sysctl.service
○   ├─systemd-sysusers.service
●   ├─systemd-timesyncd.service
●   ├─systemd-tmpfiles-setup-dev-early.service
●   ├─systemd-tmpfiles-setup-dev.service
●   ├─systemd-tmpfiles-setup.service
○   ├─systemd-tpm2-setup-early.service
○   ├─systemd-tpm2-setup.service
●   ├─systemd-udev-trigger.service
●   ├─systemd-udevd.service
○   ├─systemd-update-done.service
●   ├─systemd-update-utmp.service
●   ├─cryptsetup.target
●   ├─integritysetup.target
lines 1-49
```

#### Langkah 4
##### Prompt
```
systemctl --failed
```

##### Hasil
```
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
```
### Praktikum 3 Buat Layanan Sederhana Dari Script Bash
#### Langkah 1 & 2
##### Prompt
```
mkdir -p situs-demo
echo -e '<!DOCTYPE html>\n<html>\n<body>\n<h1>Halo dari layanan systemd kustom!</h1>\n<p>Layanan ini dibuat pada praktek Bab 10.</p>\n</body>\n</html>' > situs-demo/index.html
```

#### Langkah 3
##### Prompt
```
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=nama-pengguna-kamu
WorkingDirectory=/home/nama-pengguna-kamu/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server 9090
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target
```

#### Langkah 4 & 5
##### Prompt
```
sudo cp demo-web.service /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
sudo systemctl enable --now demo-web
systemctl status demo-web
curl http://localhost:9091
```

##### Hasil
```
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enabled; preset: enabled)
     Active: activating (auto-restart) (Result: exit-code) since Sun 2026-06-07 13:28:48 WIB; 821ms ago
    Process: 29636 ExecStart=/usr/bin/python3 -m http.server 9090 (code=exited, status=217/USER)
   Main PID: 29636 (code=exited, status=217/USER)
        CPU: 1ms
curl: (7) Failed to connect to localhost port 9090 after 0 ms: Couldn't connect to server
Killed
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enabled; preset: enabled)
     Active: activating (auto-restart) (Result: exit-code) since Sun 2026-06-07 13:28:51 WIB; 2s ago
    Process: 29646 ExecStart=/usr/bin/python3 -m http.server 9090 (code=exited, status=217/USER)
   Main PID: 29646 (code=exited, status=217/USER)
        CPU: 916us
```

### Praktikum 4 Filter dan Analisis Log Layanan
### Praktikum 5 Konfigurasi SSH Server
### Latihan 1 Audit Layanan dan Analisis Boot
### Latihan 2 Layanan Kustom dengan Restart Otomatis
### Latihan 3 Investigasi Log dan Keamanan SSH