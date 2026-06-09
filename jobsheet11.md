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
#### Langkah 1
##### Prompt
```
mkdir -p situs-demo
cat << 'EOF' > situs-demo/index.html
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
EOF
```

#### Langkah 2
##### Prompt
```
sudo bash -c "cat << EOF > /etc/systemd/system/demo-web.service
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=$USER
WorkingDirectory=/home/$USER/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server 9090
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target
EOF"

sudo systemctl daemon-reload
```

#### Langkah 3
##### Prompt
```
sudo bash -c "cat << EOF > /etc/systemd/system/demo-web.service
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=$USER
WorkingDirectory=/home/$USER/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server 9090
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target
EOF"

sudo systemctl daemon-reload
```

#### Langkah 4
##### Prompt
```
sudo systemctl start demo-web
systemctl status demo-web
curl http://localhost:9090
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
#### Langkah 1
##### Prompt
```
journalctl -u ssh --since "1 hour ago" --no-pager || journalctl -u cron --since "1 hour ago" --no-pager
```

##### Hasil
```
-- No Entries --
```

#### Langkah 2
##### Prompt
```
journalctl -b -p err --no-pager
```

##### Hasil
```
fafiq-ubuntu% journalctl -b -p err --no-pager
Jun 09 19:37:39 fafiq-ubuntu kernel: RDSEED32 is broken. Disabling the corresponding CPUID bit.
Jun 09 19:37:39 fafiq-ubuntu kernel: lenovo_wmi_gamezone 887B54E3-DDDC-4B2C-8B88-68A26A8835D0: platform_profile probe failed
Jun 09 19:37:41 fafiq-ubuntu bluetoothd[1172]: profiles/sap/server.c:sap_server_register() Sap driver initialization failed.
Jun 09 19:37:41 fafiq-ubuntu bluetoothd[1172]: sap-server: Operation not permitted (1)
Jun 09 19:37:41 fafiq-ubuntu (python3)[1978]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:45 fafiq-ubuntu (python3)[2131]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:48 fafiq-ubuntu (python3)[2165]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:51 fafiq-ubuntu (python3)[2167]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:53 fafiq-ubuntu gdm3[2008]: Gdm: on_display_added: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 19:37:54 fafiq-ubuntu (python3)[2289]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:57 fafiq-ubuntu (python3)[2379]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:01 fafiq-ubuntu (python3)[2765]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:03 fafiq-ubuntu gdm-password][2760]: gkr-pam: unable to locate daemon control file
Jun 09 19:38:03 fafiq-ubuntu gdm3[2008]: Gdm: on_display_added: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 19:38:04 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-gnome\x2dkeyring\x2dsecrets-3010.scope - Application launched by gnome-session-binary.
Jun 09 19:38:04 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-xdg\x2duser\x2ddirs-3033.scope - Application launched by gnome-session-binary.
Jun 09 19:38:04 fafiq-ubuntu (python3)[3095]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:04 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-spice\x2dvdagent-3225.scope - Application launched by gnome-session-binary.
Jun 09 19:38:05 fafiq-ubuntu gdm3[2008]: Gdm: on_display_removed: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 19:38:07 fafiq-ubuntu (python3)[3800]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:10 fafiq-ubuntu (python3)[3814]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:13 fafiq-ubuntu (python3)[3822]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:17 fafiq-ubuntu (python3)[4008]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:20 fafiq-ubuntu (python3)[4013]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:23 fafiq-ubuntu (python3)[4183]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:26 fafiq-ubuntu (python3)[4203]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:29 fafiq-ubuntu (python3)[4217]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:33 fafiq-ubuntu (python3)[4220]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:36 fafiq-ubuntu (python3)[4540]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:39 fafiq-ubuntu (python3)[5169]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:42 fafiq-ubuntu (python3)[5170]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:45 fafiq-ubuntu (python3)[5177]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:48 fafiq-ubuntu (python3)[5178]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:52 fafiq-ubuntu (python3)[5182]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:55 fafiq-ubuntu (python3)[5183]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:38:58 fafiq-ubuntu (python3)[5199]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:01 fafiq-ubuntu (python3)[5239]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:04 fafiq-ubuntu (python3)[5257]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:08 fafiq-ubuntu (python3)[5302]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:11 fafiq-ubuntu (python3)[5311]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:14 fafiq-ubuntu (python3)[5325]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:17 fafiq-ubuntu (python3)[5327]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:21 fafiq-ubuntu (python3)[5333]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:24 fafiq-ubuntu (python3)[5338]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:27 fafiq-ubuntu (python3)[5339]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:30 fafiq-ubuntu (python3)[5340]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:34 fafiq-ubuntu (python3)[5341]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:37 fafiq-ubuntu (python3)[5343]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:40 fafiq-ubuntu (python3)[5359]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:43 fafiq-ubuntu (python3)[5408]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:47 fafiq-ubuntu (python3)[5412]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:50 fafiq-ubuntu (python3)[5414]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:53 fafiq-ubuntu (python3)[5415]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:39:56 fafiq-ubuntu (python3)[5416]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:00 fafiq-ubuntu (python3)[5418]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:03 fafiq-ubuntu (python3)[5421]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:06 fafiq-ubuntu (python3)[5422]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:09 fafiq-ubuntu (python3)[5423]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:13 fafiq-ubuntu (python3)[5424]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:16 fafiq-ubuntu (python3)[5426]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:19 fafiq-ubuntu (python3)[5427]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:22 fafiq-ubuntu (python3)[5430]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:26 fafiq-ubuntu (python3)[5437]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:29 fafiq-ubuntu (python3)[5758]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:32 fafiq-ubuntu (python3)[5903]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:35 fafiq-ubuntu (python3)[5904]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:39 fafiq-ubuntu (python3)[5967]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:42 fafiq-ubuntu (python3)[5968]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:45 fafiq-ubuntu (python3)[5982]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:48 fafiq-ubuntu (python3)[5983]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:52 fafiq-ubuntu (python3)[5984]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:55 fafiq-ubuntu (python3)[5987]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:40:58 fafiq-ubuntu (python3)[5989]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:01 fafiq-ubuntu (python3)[5991]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:05 fafiq-ubuntu (python3)[5992]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:08 fafiq-ubuntu (python3)[5993]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:11 fafiq-ubuntu (python3)[5994]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:14 fafiq-ubuntu (python3)[5995]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:18 fafiq-ubuntu (python3)[5996]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:21 fafiq-ubuntu (python3)[5997]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:24 fafiq-ubuntu (python3)[5998]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:27 fafiq-ubuntu (python3)[5999]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:31 fafiq-ubuntu (python3)[6000]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:34 fafiq-ubuntu (python3)[6001]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:37 fafiq-ubuntu (python3)[6004]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:40 fafiq-ubuntu (python3)[6006]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:43 fafiq-ubuntu (python3)[6013]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:47 fafiq-ubuntu (python3)[6063]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:50 fafiq-ubuntu (python3)[6064]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:53 fafiq-ubuntu (python3)[6065]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:41:56 fafiq-ubuntu (python3)[6066]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:00 fafiq-ubuntu (python3)[6071]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:03 fafiq-ubuntu (python3)[6072]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:06 fafiq-ubuntu (python3)[6073]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:09 fafiq-ubuntu (python3)[6074]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:13 fafiq-ubuntu (python3)[6075]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:16 fafiq-ubuntu (python3)[6079]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:19 fafiq-ubuntu (python3)[6082]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:22 fafiq-ubuntu (python3)[6083]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:26 fafiq-ubuntu (python3)[6084]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:29 fafiq-ubuntu (python3)[6085]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:32 fafiq-ubuntu (python3)[6086]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:35 fafiq-ubuntu (python3)[6088]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:39 fafiq-ubuntu (python3)[6090]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:42 fafiq-ubuntu (python3)[6097]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:45 fafiq-ubuntu (python3)[6098]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:48 fafiq-ubuntu (python3)[6105]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:52 fafiq-ubuntu (python3)[6107]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:55 fafiq-ubuntu (python3)[6108]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:42:58 fafiq-ubuntu (python3)[6109]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:01 fafiq-ubuntu (python3)[6111]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:05 fafiq-ubuntu (python3)[6112]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:08 fafiq-ubuntu (python3)[6114]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:11 fafiq-ubuntu (python3)[6115]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:14 fafiq-ubuntu (python3)[6119]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:18 fafiq-ubuntu (python3)[6120]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:21 fafiq-ubuntu (python3)[6121]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:24 fafiq-ubuntu (python3)[6122]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:27 fafiq-ubuntu (python3)[6123]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:31 fafiq-ubuntu (python3)[6128]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:34 fafiq-ubuntu (python3)[6129]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:37 fafiq-ubuntu (python3)[6133]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:40 fafiq-ubuntu (python3)[6136]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:44 fafiq-ubuntu (python3)[6138]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:47 fafiq-ubuntu (python3)[6139]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:50 fafiq-ubuntu (python3)[6942]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:53 fafiq-ubuntu (python3)[6943]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:43:57 fafiq-ubuntu (python3)[6945]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:00 fafiq-ubuntu (python3)[6947]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:03 fafiq-ubuntu (python3)[6948]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:06 fafiq-ubuntu (python3)[6949]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:10 fafiq-ubuntu (python3)[6950]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:13 fafiq-ubuntu (python3)[6951]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:16 fafiq-ubuntu (python3)[6952]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:19 fafiq-ubuntu (python3)[6953]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:23 fafiq-ubuntu (python3)[6955]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:26 fafiq-ubuntu (python3)[6956]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:29 fafiq-ubuntu (python3)[6957]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:32 fafiq-ubuntu (python3)[6958]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:36 fafiq-ubuntu (python3)[6961]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:39 fafiq-ubuntu (python3)[6963]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:42 fafiq-ubuntu (python3)[6965]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:45 fafiq-ubuntu (python3)[6966]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:49 fafiq-ubuntu (python3)[6967]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:52 fafiq-ubuntu (python3)[6968]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:55 fafiq-ubuntu (python3)[6969]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:44:58 fafiq-ubuntu (python3)[6971]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:02 fafiq-ubuntu (python3)[6976]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:05 fafiq-ubuntu (python3)[6977]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:08 fafiq-ubuntu (python3)[6978]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:11 fafiq-ubuntu (python3)[6979]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:14 fafiq-ubuntu (python3)[6980]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:18 fafiq-ubuntu (python3)[6981]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:21 fafiq-ubuntu (python3)[6982]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:24 fafiq-ubuntu (python3)[6984]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:27 fafiq-ubuntu (python3)[6985]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:31 fafiq-ubuntu (python3)[6986]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:34 fafiq-ubuntu (python3)[6987]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:37 fafiq-ubuntu (python3)[6990]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:40 fafiq-ubuntu (python3)[6992]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:44 fafiq-ubuntu (python3)[6994]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:47 fafiq-ubuntu (python3)[6995]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:50 fafiq-ubuntu (python3)[6996]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:53 fafiq-ubuntu (python3)[6997]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:45:57 fafiq-ubuntu (python3)[6998]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:00 fafiq-ubuntu (python3)[7000]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:03 fafiq-ubuntu (python3)[7001]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:06 fafiq-ubuntu (python3)[7002]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:10 fafiq-ubuntu (python3)[7003]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:13 fafiq-ubuntu (python3)[7004]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:16 fafiq-ubuntu (python3)[7005]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:19 fafiq-ubuntu (python3)[7006]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:23 fafiq-ubuntu (python3)[7007]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:26 fafiq-ubuntu (python3)[7008]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:29 fafiq-ubuntu (python3)[7009]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:32 fafiq-ubuntu (python3)[7010]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:36 fafiq-ubuntu (python3)[7013]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:39 fafiq-ubuntu (python3)[7015]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:42 fafiq-ubuntu (python3)[7017]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:45 fafiq-ubuntu (python3)[7018]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:49 fafiq-ubuntu (python3)[7021]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:52 fafiq-ubuntu (python3)[7022]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:55 fafiq-ubuntu (python3)[7032]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:46:58 fafiq-ubuntu (python3)[7045]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:02 fafiq-ubuntu (python3)[7047]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:05 fafiq-ubuntu (python3)[7048]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:08 fafiq-ubuntu (python3)[7049]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:11 fafiq-ubuntu (python3)[7050]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:15 fafiq-ubuntu (python3)[7051]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:18 fafiq-ubuntu (python3)[7052]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:21 fafiq-ubuntu (python3)[7053]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:24 fafiq-ubuntu (python3)[7056]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:28 fafiq-ubuntu (python3)[7057]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:31 fafiq-ubuntu (python3)[7058]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:34 fafiq-ubuntu (python3)[7059]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:37 fafiq-ubuntu (python3)[7062]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:41 fafiq-ubuntu (python3)[7067]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:44 fafiq-ubuntu (python3)[7069]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:47 fafiq-ubuntu (python3)[7070]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:50 fafiq-ubuntu (python3)[7071]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:54 fafiq-ubuntu (python3)[7072]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:47:57 fafiq-ubuntu (python3)[7073]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:00 fafiq-ubuntu (python3)[7075]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:03 fafiq-ubuntu (python3)[7076]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:07 fafiq-ubuntu (python3)[7077]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:10 fafiq-ubuntu (python3)[7078]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:13 fafiq-ubuntu (python3)[7079]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:16 fafiq-ubuntu (python3)[7080]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:20 fafiq-ubuntu (python3)[7081]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:23 fafiq-ubuntu (python3)[7082]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:26 fafiq-ubuntu (python3)[7083]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:29 fafiq-ubuntu (python3)[7084]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:33 fafiq-ubuntu (python3)[7085]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:36 fafiq-ubuntu (python3)[7088]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:39 fafiq-ubuntu (python3)[7091]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:42 fafiq-ubuntu (python3)[7093]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:46 fafiq-ubuntu (python3)[7094]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:49 fafiq-ubuntu (python3)[7095]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:52 fafiq-ubuntu (python3)[7096]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:55 fafiq-ubuntu (python3)[7098]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:48:59 fafiq-ubuntu (python3)[7099]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:02 fafiq-ubuntu (python3)[7101]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:05 fafiq-ubuntu (python3)[7102]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:08 fafiq-ubuntu (python3)[7103]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:12 fafiq-ubuntu (python3)[7104]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:15 fafiq-ubuntu (python3)[7105]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:18 fafiq-ubuntu (python3)[7108]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:21 fafiq-ubuntu (python3)[7110]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:25 fafiq-ubuntu (python3)[7111]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:28 fafiq-ubuntu (python3)[7112]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:31 fafiq-ubuntu (python3)[7128]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:34 fafiq-ubuntu (python3)[7129]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:38 fafiq-ubuntu (python3)[7132]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:41 fafiq-ubuntu (python3)[7134]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:44 fafiq-ubuntu (python3)[7136]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:47 fafiq-ubuntu (python3)[7137]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:51 fafiq-ubuntu (python3)[7138]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:54 fafiq-ubuntu (python3)[7139]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:49:57 fafiq-ubuntu (python3)[7140]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:00 fafiq-ubuntu (python3)[7142]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:04 fafiq-ubuntu (python3)[7150]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:07 fafiq-ubuntu (python3)[7151]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:10 fafiq-ubuntu (python3)[7152]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:13 fafiq-ubuntu (python3)[7154]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:17 fafiq-ubuntu (python3)[7218]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:20 fafiq-ubuntu (python3)[7220]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:23 fafiq-ubuntu (python3)[7221]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:26 fafiq-ubuntu (python3)[7226]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:29 fafiq-ubuntu (python3)[7228]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:33 fafiq-ubuntu (python3)[7229]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:36 fafiq-ubuntu (python3)[7231]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:39 fafiq-ubuntu (python3)[7233]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:42 fafiq-ubuntu (python3)[7234]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:46 fafiq-ubuntu (python3)[7235]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:49 fafiq-ubuntu (python3)[7236]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:52 fafiq-ubuntu (python3)[7240]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:55 fafiq-ubuntu (python3)[7241]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:50:59 fafiq-ubuntu (python3)[7287]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:02 fafiq-ubuntu (python3)[7289]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:05 fafiq-ubuntu (python3)[7290]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:08 fafiq-ubuntu (python3)[7292]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:12 fafiq-ubuntu (python3)[7309]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:15 fafiq-ubuntu (python3)[7312]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:18 fafiq-ubuntu (python3)[7314]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:21 fafiq-ubuntu (python3)[7315]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:24 fafiq-ubuntu (python3)[7317]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:28 fafiq-ubuntu (python3)[7348]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:31 fafiq-ubuntu (python3)[7350]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:34 fafiq-ubuntu (python3)[7351]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:37 fafiq-ubuntu (python3)[7353]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:41 fafiq-ubuntu (python3)[7357]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:44 fafiq-ubuntu (python3)[7364]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:47 fafiq-ubuntu (python3)[7366]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:50 fafiq-ubuntu (python3)[7367]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:54 fafiq-ubuntu (python3)[7368]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:51:57 fafiq-ubuntu (python3)[7381]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:00 fafiq-ubuntu (python3)[7383]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:03 fafiq-ubuntu (python3)[7385]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:07 fafiq-ubuntu (python3)[7386]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:10 fafiq-ubuntu (python3)[7388]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:13 fafiq-ubuntu (python3)[7389]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:16 fafiq-ubuntu (python3)[7390]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:20 fafiq-ubuntu (python3)[7391]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:23 fafiq-ubuntu (python3)[7392]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:26 fafiq-ubuntu (python3)[7393]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:29 fafiq-ubuntu (python3)[7394]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:33 fafiq-ubuntu (python3)[7395]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:36 fafiq-ubuntu (python3)[7398]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:39 fafiq-ubuntu (python3)[7403]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:42 fafiq-ubuntu (python3)[7406]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:46 fafiq-ubuntu (python3)[7411]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:49 fafiq-ubuntu (python3)[7412]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:52 fafiq-ubuntu (python3)[7413]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:55 fafiq-ubuntu (python3)[7414]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:52:59 fafiq-ubuntu (python3)[7415]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:02 fafiq-ubuntu (python3)[7417]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:05 fafiq-ubuntu (python3)[7418]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:08 fafiq-ubuntu (python3)[7419]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:12 fafiq-ubuntu (python3)[7420]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:15 fafiq-ubuntu (python3)[7421]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:18 fafiq-ubuntu (python3)[7422]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:21 fafiq-ubuntu (python3)[7423]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:25 fafiq-ubuntu (python3)[7424]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:28 fafiq-ubuntu (python3)[7425]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:31 fafiq-ubuntu (python3)[7426]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:34 fafiq-ubuntu (python3)[7427]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:38 fafiq-ubuntu (python3)[7431]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:41 fafiq-ubuntu (python3)[7433]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:44 fafiq-ubuntu (python3)[7435]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:47 fafiq-ubuntu (python3)[7436]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:51 fafiq-ubuntu (python3)[7437]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:54 fafiq-ubuntu (python3)[7438]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:53:57 fafiq-ubuntu (python3)[7439]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:00 fafiq-ubuntu (python3)[7441]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:04 fafiq-ubuntu (python3)[7442]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:07 fafiq-ubuntu (python3)[7443]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:10 fafiq-ubuntu (python3)[7444]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:13 fafiq-ubuntu (python3)[7445]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:17 fafiq-ubuntu (python3)[7446]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:20 fafiq-ubuntu (python3)[7447]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:23 fafiq-ubuntu (python3)[7448]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:26 fafiq-ubuntu (python3)[7449]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:30 fafiq-ubuntu (python3)[7450]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:33 fafiq-ubuntu (python3)[7451]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:36 fafiq-ubuntu (python3)[7452]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:39 fafiq-ubuntu (python3)[7456]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:43 fafiq-ubuntu (python3)[7457]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:46 fafiq-ubuntu (python3)[7458]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:49 fafiq-ubuntu (python3)[7459]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:52 fafiq-ubuntu (python3)[7460]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:56 fafiq-ubuntu (python3)[7461]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:54:59 fafiq-ubuntu (python3)[7462]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:02 fafiq-ubuntu (python3)[7467]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:05 fafiq-ubuntu (python3)[7468]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:09 fafiq-ubuntu (python3)[7469]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:12 fafiq-ubuntu (python3)[7470]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:15 fafiq-ubuntu (python3)[7471]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:18 fafiq-ubuntu (python3)[7473]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:22 fafiq-ubuntu (python3)[7474]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:25 fafiq-ubuntu (python3)[7477]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:28 fafiq-ubuntu (python3)[7478]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:31 fafiq-ubuntu (python3)[7480]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:35 fafiq-ubuntu (python3)[7482]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:38 fafiq-ubuntu (python3)[7485]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:41 fafiq-ubuntu (python3)[7488]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:44 fafiq-ubuntu (python3)[7489]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:48 fafiq-ubuntu (python3)[7490]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:51 fafiq-ubuntu (python3)[7491]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:54 fafiq-ubuntu (python3)[7492]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:55:57 fafiq-ubuntu (python3)[7493]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:01 fafiq-ubuntu (python3)[7495]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:04 fafiq-ubuntu (python3)[7496]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:07 fafiq-ubuntu (python3)[7497]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:10 fafiq-ubuntu (python3)[7498]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:14 fafiq-ubuntu (python3)[7499]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:17 fafiq-ubuntu (python3)[7500]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:20 fafiq-ubuntu (python3)[7519]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:23 fafiq-ubuntu (python3)[7521]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:27 fafiq-ubuntu (python3)[7522]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:30 fafiq-ubuntu (python3)[7523]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:33 fafiq-ubuntu (python3)[7524]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:36 fafiq-ubuntu (python3)[7525]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:40 fafiq-ubuntu (python3)[7530]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:43 fafiq-ubuntu (python3)[7531]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:46 fafiq-ubuntu (python3)[7532]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:49 fafiq-ubuntu (python3)[7533]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:53 fafiq-ubuntu (python3)[7534]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:56 fafiq-ubuntu (python3)[7535]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:56:59 fafiq-ubuntu (python3)[7536]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:02 fafiq-ubuntu (python3)[7538]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:06 fafiq-ubuntu (python3)[7539]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:09 fafiq-ubuntu (python3)[7540]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:12 fafiq-ubuntu (python3)[7541]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:15 fafiq-ubuntu (python3)[7542]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:19 fafiq-ubuntu (python3)[7544]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:22 fafiq-ubuntu (python3)[7545]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:25 fafiq-ubuntu (python3)[7546]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:28 fafiq-ubuntu (python3)[7547]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:32 fafiq-ubuntu (python3)[7548]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:35 fafiq-ubuntu (python3)[7550]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:38 fafiq-ubuntu (python3)[7553]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:41 fafiq-ubuntu (python3)[7556]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:44 fafiq-ubuntu (python3)[7559]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:48 fafiq-ubuntu (python3)[7560]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:51 fafiq-ubuntu (python3)[7561]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:54 fafiq-ubuntu (python3)[7562]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:57:57 fafiq-ubuntu (python3)[7563]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:01 fafiq-ubuntu (python3)[7564]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:04 fafiq-ubuntu (python3)[7567]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:07 fafiq-ubuntu (python3)[7582]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:10 fafiq-ubuntu (python3)[7583]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:14 fafiq-ubuntu (python3)[7597]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:17 fafiq-ubuntu (python3)[7598]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:20 fafiq-ubuntu (python3)[7599]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:23 fafiq-ubuntu (python3)[7600]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:27 fafiq-ubuntu (python3)[7601]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:30 fafiq-ubuntu (python3)[7602]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:33 fafiq-ubuntu (python3)[7603]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:36 fafiq-ubuntu (python3)[7606]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:40 fafiq-ubuntu (python3)[7610]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:43 fafiq-ubuntu (python3)[7611]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:46 fafiq-ubuntu (python3)[7612]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:49 fafiq-ubuntu (python3)[7613]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:53 fafiq-ubuntu (python3)[7614]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:56 fafiq-ubuntu (python3)[7615]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:58:59 fafiq-ubuntu (python3)[7616]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:02 fafiq-ubuntu (python3)[7618]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:06 fafiq-ubuntu (python3)[7619]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:09 fafiq-ubuntu (python3)[7622]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:12 fafiq-ubuntu (python3)[7623]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:15 fafiq-ubuntu (python3)[7624]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:19 fafiq-ubuntu (python3)[7626]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:22 fafiq-ubuntu (python3)[7628]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:25 fafiq-ubuntu (python3)[7629]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:28 fafiq-ubuntu (python3)[7630]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:32 fafiq-ubuntu (python3)[7631]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:35 fafiq-ubuntu (python3)[7632]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:38 fafiq-ubuntu (python3)[7635]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:41 fafiq-ubuntu (python3)[7637]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:45 fafiq-ubuntu (python3)[7638]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:48 fafiq-ubuntu (python3)[7641]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:51 fafiq-ubuntu (python3)[7642]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:54 fafiq-ubuntu (python3)[7643]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:59:58 fafiq-ubuntu (python3)[7644]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:01 fafiq-ubuntu (python3)[7645]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:04 fafiq-ubuntu (python3)[7649]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:07 fafiq-ubuntu (python3)[7650]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:11 fafiq-ubuntu (python3)[7651]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:14 fafiq-ubuntu (python3)[7652]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:17 fafiq-ubuntu (python3)[7653]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:20 fafiq-ubuntu (python3)[7657]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:24 fafiq-ubuntu (python3)[7658]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:27 fafiq-ubuntu (python3)[7659]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:30 fafiq-ubuntu (python3)[7660]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:33 fafiq-ubuntu (python3)[7661]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:37 fafiq-ubuntu (python3)[7662]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:40 fafiq-ubuntu (python3)[7665]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:43 fafiq-ubuntu (python3)[7666]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:46 fafiq-ubuntu (python3)[7667]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:50 fafiq-ubuntu (python3)[7668]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:53 fafiq-ubuntu (python3)[7669]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:56 fafiq-ubuntu (python3)[7671]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:00:59 fafiq-ubuntu (python3)[7672]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:03 fafiq-ubuntu (python3)[7674]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:06 fafiq-ubuntu (python3)[7675]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:09 fafiq-ubuntu (python3)[7676]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:12 fafiq-ubuntu (python3)[7677]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:16 fafiq-ubuntu (python3)[7678]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:19 fafiq-ubuntu (python3)[7679]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:22 fafiq-ubuntu (python3)[7680]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:25 fafiq-ubuntu (python3)[7681]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:29 fafiq-ubuntu (python3)[7682]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:32 fafiq-ubuntu (python3)[7683]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:35 fafiq-ubuntu (python3)[7684]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:38 fafiq-ubuntu (python3)[7687]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:42 fafiq-ubuntu (python3)[7689]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:45 fafiq-ubuntu (python3)[7690]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:48 fafiq-ubuntu (python3)[7691]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:51 fafiq-ubuntu (python3)[7692]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:55 fafiq-ubuntu (python3)[7693]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:01:58 fafiq-ubuntu (python3)[7694]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:01 fafiq-ubuntu (python3)[7695]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:04 fafiq-ubuntu (python3)[7697]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:08 fafiq-ubuntu (python3)[7698]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:11 fafiq-ubuntu (python3)[7700]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:14 fafiq-ubuntu (python3)[7701]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:17 fafiq-ubuntu (python3)[7702]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:21 fafiq-ubuntu (python3)[7703]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:24 fafiq-ubuntu (python3)[7704]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:27 fafiq-ubuntu (python3)[7705]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:30 fafiq-ubuntu (python3)[7706]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:34 fafiq-ubuntu (python3)[7707]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:37 fafiq-ubuntu (python3)[7708]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:40 fafiq-ubuntu (python3)[7712]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:43 fafiq-ubuntu (python3)[7713]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:46 fafiq-ubuntu (python3)[7716]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:50 fafiq-ubuntu (python3)[7717]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:53 fafiq-ubuntu (python3)[7718]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:56 fafiq-ubuntu (python3)[7719]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:02:59 fafiq-ubuntu (python3)[7720]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:03 fafiq-ubuntu (python3)[7722]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:06 fafiq-ubuntu (python3)[7723]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:09 fafiq-ubuntu (python3)[7725]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:12 fafiq-ubuntu (python3)[7726]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:16 fafiq-ubuntu (python3)[7727]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:19 fafiq-ubuntu (python3)[7728]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:22 fafiq-ubuntu (python3)[7729]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:25 fafiq-ubuntu (python3)[7730]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:29 fafiq-ubuntu (python3)[7731]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:32 fafiq-ubuntu (python3)[7732]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:35 fafiq-ubuntu (python3)[7733]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:38 fafiq-ubuntu (python3)[7736]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:42 fafiq-ubuntu (python3)[7738]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:45 fafiq-ubuntu (python3)[7739]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:48 fafiq-ubuntu (python3)[7740]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:51 fafiq-ubuntu (python3)[7741]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:55 fafiq-ubuntu (python3)[7742]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:03:58 fafiq-ubuntu (python3)[7743]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:01 fafiq-ubuntu (python3)[7744]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:04 fafiq-ubuntu (python3)[7746]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:08 fafiq-ubuntu (python3)[7753]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:11 fafiq-ubuntu (python3)[7755]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:14 fafiq-ubuntu (python3)[7757]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:17 fafiq-ubuntu (python3)[7758]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:21 fafiq-ubuntu (python3)[7759]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:24 fafiq-ubuntu (python3)[7760]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:27 fafiq-ubuntu (python3)[7761]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:30 fafiq-ubuntu (python3)[7762]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:34 fafiq-ubuntu (python3)[7763]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:37 fafiq-ubuntu (python3)[7764]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:40 fafiq-ubuntu (python3)[7768]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:43 fafiq-ubuntu (python3)[7769]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:47 fafiq-ubuntu (python3)[7770]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:50 fafiq-ubuntu (python3)[7771]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:53 fafiq-ubuntu (python3)[7772]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:04:56 fafiq-ubuntu (python3)[7773]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:00 fafiq-ubuntu (python3)[7774]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:03 fafiq-ubuntu (python3)[7779]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:06 fafiq-ubuntu (python3)[7780]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:09 fafiq-ubuntu (python3)[7782]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:13 fafiq-ubuntu (python3)[7783]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:16 fafiq-ubuntu (python3)[7784]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:19 fafiq-ubuntu (python3)[7785]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:22 fafiq-ubuntu (python3)[7786]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:26 fafiq-ubuntu (python3)[7787]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:29 fafiq-ubuntu (python3)[7788]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:32 fafiq-ubuntu (python3)[7789]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:35 fafiq-ubuntu (python3)[7791]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:39 fafiq-ubuntu (python3)[7794]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:42 fafiq-ubuntu (python3)[7796]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:45 fafiq-ubuntu (python3)[7797]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:48 fafiq-ubuntu (python3)[7798]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:52 fafiq-ubuntu (python3)[7799]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:55 fafiq-ubuntu (python3)[7800]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:05:58 fafiq-ubuntu (python3)[7801]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:01 fafiq-ubuntu (python3)[7802]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:05 fafiq-ubuntu (python3)[7804]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:08 fafiq-ubuntu (python3)[7805]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:11 fafiq-ubuntu (python3)[7806]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:14 fafiq-ubuntu (python3)[7808]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:18 fafiq-ubuntu (python3)[7809]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:21 fafiq-ubuntu (python3)[7810]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:24 fafiq-ubuntu (python3)[7811]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:27 fafiq-ubuntu (python3)[7812]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:31 fafiq-ubuntu (python3)[7813]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:34 fafiq-ubuntu (python3)[7814]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:37 fafiq-ubuntu (python3)[7815]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:40 fafiq-ubuntu (python3)[7819]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:44 fafiq-ubuntu (python3)[7820]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:47 fafiq-ubuntu (python3)[7821]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:50 fafiq-ubuntu (python3)[7822]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:53 fafiq-ubuntu (python3)[7823]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:06:57 fafiq-ubuntu (python3)[7824]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:00 fafiq-ubuntu (python3)[7825]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:03 fafiq-ubuntu (python3)[7827]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:06 fafiq-ubuntu (python3)[7828]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:10 fafiq-ubuntu (python3)[7829]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:13 fafiq-ubuntu (python3)[7830]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:16 fafiq-ubuntu (python3)[7831]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:19 fafiq-ubuntu (python3)[7833]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:23 fafiq-ubuntu (python3)[7834]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:26 fafiq-ubuntu (python3)[7835]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:29 fafiq-ubuntu (python3)[7836]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:32 fafiq-ubuntu (python3)[7837]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:36 fafiq-ubuntu (python3)[7838]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:39 fafiq-ubuntu (python3)[7842]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:42 fafiq-ubuntu (python3)[7844]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:45 fafiq-ubuntu (python3)[7845]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:49 fafiq-ubuntu (python3)[7848]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:52 fafiq-ubuntu (python3)[7849]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:55 fafiq-ubuntu (python3)[7850]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:07:58 fafiq-ubuntu (python3)[7851]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:31 fafiq-ubuntu kernel: ACPI BIOS Error (bug): Could not resolve symbol [^^^GPP5.RTKW], AE_NOT_FOUND (20250404/psargs-332)
Jun 09 20:11:31 fafiq-ubuntu kernel: ACPI Error: Aborting method \_SB.PCI0.LPC0.EC0.UPHK due to previous error (AE_NOT_FOUND) (20250404/psparse-529)
Jun 09 20:11:31 fafiq-ubuntu kernel: ACPI Error: Aborting method \_SB.PEP._DSM due to previous error (AE_NOT_FOUND) (20250404/psparse-529)
Jun 09 20:11:31 fafiq-ubuntu kernel: atkbd serio0: Failed to deactivate keyboard on isa0060/serio0
Jun 09 20:11:31 fafiq-ubuntu (python3)[7935]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:32 fafiq-ubuntu bluetoothd[1172]: profiles/sap/server.c:sap_server_register() Sap driver initialization failed.
Jun 09 20:11:32 fafiq-ubuntu bluetoothd[1172]: sap-server: Operation not permitted (1)
Jun 09 20:11:34 fafiq-ubuntu (python3)[8053]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:37 fafiq-ubuntu (python3)[8125]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:41 fafiq-ubuntu (python3)[8129]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:44 fafiq-ubuntu (python3)[8135]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:47 fafiq-ubuntu (python3)[8142]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:50 fafiq-ubuntu (python3)[8146]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:54 fafiq-ubuntu (python3)[8148]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:11:57 fafiq-ubuntu (python3)[8151]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:00 fafiq-ubuntu (python3)[8152]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:03 fafiq-ubuntu (python3)[8156]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:07 fafiq-ubuntu (python3)[8158]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:10 fafiq-ubuntu (python3)[8163]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:13 fafiq-ubuntu (python3)[8166]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:16 fafiq-ubuntu (python3)[8173]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:20 fafiq-ubuntu (python3)[8178]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:23 fafiq-ubuntu (python3)[8184]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:26 fafiq-ubuntu (python3)[8186]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:29 fafiq-ubuntu (python3)[8187]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:33 fafiq-ubuntu (python3)[8191]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:36 fafiq-ubuntu (python3)[8194]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:39 fafiq-ubuntu (python3)[8203]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:42 fafiq-ubuntu (python3)[8204]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:46 fafiq-ubuntu (python3)[8205]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:49 fafiq-ubuntu (python3)[8207]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:52 fafiq-ubuntu (python3)[8216]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:55 fafiq-ubuntu (python3)[8221]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:12:59 fafiq-ubuntu (python3)[8227]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:02 fafiq-ubuntu (python3)[8228]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:05 fafiq-ubuntu (python3)[8229]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:08 fafiq-ubuntu (python3)[8234]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:12 fafiq-ubuntu (python3)[8240]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:15 fafiq-ubuntu (python3)[8248]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:18 fafiq-ubuntu (python3)[8252]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:21 fafiq-ubuntu (python3)[8254]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:25 fafiq-ubuntu (python3)[8255]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:28 fafiq-ubuntu (python3)[8259]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:31 fafiq-ubuntu (python3)[8262]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:34 fafiq-ubuntu (python3)[8267]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:38 fafiq-ubuntu (python3)[8268]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:41 fafiq-ubuntu (python3)[8314]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:44 fafiq-ubuntu (python3)[8315]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:46 fafiq-ubuntu gdm3[2008]: Gdm: on_display_added: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 20:13:46 fafiq-ubuntu gdm3[2008]: Gdm: on_display_removed: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 20:13:47 fafiq-ubuntu (python3)[9044]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:50 fafiq-ubuntu (python3)[9126]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:52 fafiq-ubuntu gdm-password][9122]: gkr-pam: unable to locate daemon control file
Jun 09 20:13:52 fafiq-ubuntu gdm3[2008]: Gdm: on_display_added: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 20:13:53 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-gnome\x2dkeyring\x2dpkcs11-9255.scope - Application launched by gnome-session-binary.
Jun 09 20:13:53 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-gnome\x2dkeyring\x2dsecrets-9253.scope - Application launched by gnome-session-binary.
Jun 09 20:13:53 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-ubuntu\x2dreport\x2don\x2dupgrade-9487.scope - Application launched by gnome-session-binary.
Jun 09 20:13:53 fafiq-ubuntu systemd[2775]: Failed to start app-gnome-user\x2ddirs\x2dupdate\x2dgtk-9536.scope - Application launched by gnome-session-binary.
Jun 09 20:13:53 fafiq-ubuntu (python3)[9716]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:13:54 fafiq-ubuntu gdm3[2008]: Gdm: on_display_removed: assertion 'GDM_IS_REMOTE_DISPLAY (display)' failed
Jun 09 20:13:57 fafiq-ubuntu (python3)[10205]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:00 fafiq-ubuntu (python3)[10954]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:03 fafiq-ubuntu (python3)[10966]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:06 fafiq-ubuntu (python3)[11295]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:10 fafiq-ubuntu (python3)[11438]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:13 fafiq-ubuntu (python3)[11441]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:16 fafiq-ubuntu (python3)[11443]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:19 fafiq-ubuntu (python3)[11447]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:23 fafiq-ubuntu (python3)[11467]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 20:14:26 fafiq-ubuntu (python3)[11477]: demo-web.service: Failed to determine user credentials: No such process
fafiq-ubuntu% 
```
#### Langkah 3
##### Prompt
```
journalctl -u ssh -f
```
##### Hasil
```
Jun 09 20:30:45 fafiq-ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: Accepted password for fafiq from 127.0.0.1 port 41928 ssh2
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: pam_unix(sshd:session): session opened for user fafiq(uid=1000) by fafiq(uid=0)
```
#### Langkah 4
##### Prompt
```
ssh localhost
```
##### Hasil
```
fafiq-ubuntu% ssh localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ED25519 key fingerprint is SHA256:uF2NAR2VhE04J7whxD6TdHDV5D3iF+aMvsb3YAfZ31g.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.
fafiq@localhost's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.17.0-20-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

39 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

fafiq-ubuntu%     
```

#### Langkah 5
##### Prompt
```
journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
echo "=== Jumlah Baris Log ===" && wc -l log-ssh-hari-ini.txt
echo "=== 20 Baris Log Berisi Kata 'error' atau 'failed' ==="
grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
```
##### Hasil
```
=== Jumlah Baris Log ===
6 log-ssh-hari-ini.txt
=== 20 Baris Log Berisi Kata 'error' atau 'failed' ===
```
### Praktikum 5 Konfigurasi SSH Server
#### Langkah 1
##### Prompt
```
sudo systemctl enable --now ssh
systemctl status ssh

ss -tlnp | grep :22 || netstat -tlnp | grep :22

grep -v "^#" /etc/ssh/sshd_config | grep -v "^\$"
```

##### Hasil
```
systemctl status ssh
Synchronizing state of ssh.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable ssh
Created symlink /etc/systemd/system/sshd.service → /usr/lib/systemd/system/ssh.service.
Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /usr/lib/systemd/system/ssh.service.
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-06-09 20:30:45 WIB; 6min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 13763 (sshd)
      Tasks: 1 (limit: 18077)
     Memory: 4.1M (peak: 5.5M)
        CPU: 53ms
     CGroup: /system.slice/ssh.service
             └─13763 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Jun 09 20:30:45 fafiq-ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Jun 09 20:30:45 fafiq-ubuntu sshd[13763]: Server listening on 0.0.0.0 port 22.
Jun 09 20:30:45 fafiq-ubuntu sshd[13763]: Server listening on :: port 22.
Jun 09 20:30:45 fafiq-ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: Accepted password for fafiq from 127.0.0.1 port 41928 ssh2
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: pam_unix(sshd:session): session opened for user fafiq(uid=1000) by fafiq(uid=0)
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ ss -tlnp | grep :22 || netstat -tlnp | grep :22
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*                                      
LISTEN 0      4096            [::]:22           [::]:*                                      
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ grep -v "^#" /etc/ssh/sshd_config | grep -v "^\$"
Include /etc/ssh/sshd_config.d/*.conf
KbdInteractiveAuthentication no
UsePAM yes
X11Forwarding yes
PrintMotd no
AcceptEnv LANG LC_*
Subsystem	sftp	/usr/lib/openssh/sftp-server
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ 
```

### Latihan 1 Audit Layanan dan Analisis Boot
#### Prompt
```
echo "=== 1. DAFTAR SEMUA LAYANAN AKTIF ==="
systemctl list-units --type=service --state=running

echo -e "\n=== 2. MEMERIKSA STATUS 3 LAYANAN UMUM ==="
echo "--- Status SSH ---"
systemctl status ssh --no-pager
echo "--- Status Cron (Task Scheduler) ---"
systemctl status cron --no-pager
echo "--- Status Rsyslog (System Logging) ---"
systemctl status rsyslog --no-pager

echo "=== 5 LAYANAN DENGAN WAKTU BOOT TERLAMA ==="
systemd-analyze blame | head -5

echo "=== DAFTAR LAYANAN YANG GAGAL SEJAK BOOT ==="
systemctl --failed
```
#### Hasil
```
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ echo "=== 1. DAFTAR SEMUA LAYANAN AKTIF ==="
systemctl list-units --type=service --state=running

echo -e "\n=== 2. MEMERIKSA STATUS 3 LAYANAN UMUM ==="
echo "--- Status SSH ---"
systemctl status ssh --no-pager
echo "--- Status Cron (Task Scheduler) ---"
systemctl status cron --no-pager
echo "--- Status Rsyslog (System Logging) ---"
systemctl status rsyslog --no-pager
=== 1. DAFTAR SEMUA LAYANAN AKTIF ===
  UNIT                           LOAD   ACTIVE SUB     DESCRIPTION                                                     
  accounts-daemon.service        loaded active running Accounts Service
  avahi-daemon.service           loaded active running Avahi mDNS/DNS-SD Stack
  bluetooth.service              loaded active running Bluetooth service
  colord.service                 loaded active running Manage, Install and Generate Color Profiles
  cron.service                   loaded active running Regular background program processing daemon
  cups-browsed.service           loaded active running Make remote CUPS printers available locally
  cups.service                   loaded active running CUPS Scheduler
  dbus.service                   loaded active running D-Bus System Message Bus
  demo-web.service               loaded active running Demo Web Server Praktek Bab 10
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
  ssh.service                    loaded active running OpenBSD Secure Shell server
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

35 loaded units listed.

=== 2. MEMERIKSA STATUS 3 LAYANAN UMUM ===
--- Status SSH ---
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-06-09 20:30:45 WIB; 9min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 13763 (sshd)
      Tasks: 1 (limit: 18077)
     Memory: 4.1M (peak: 5.5M)
        CPU: 53ms
     CGroup: /system.slice/ssh.service
             └─13763 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Jun 09 20:30:45 fafiq-ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Jun 09 20:30:45 fafiq-ubuntu sshd[13763]: Server listening on 0.0.0.0 port 22.
Jun 09 20:30:45 fafiq-ubuntu sshd[13763]: Server listening on :: port 22.
Jun 09 20:30:45 fafiq-ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: Accepted password for fafiq from 127.0.0.1 port 41928 ssh2
Jun 09 20:31:16 fafiq-ubuntu sshd[13765]: pam_unix(sshd:session): session opened for user fafiq(uid=1000) by fafiq(uid=0)
--- Status Cron (Task Scheduler) ---
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-06-09 19:37:41 WIB; 1h 2min ago
       Docs: man:cron(8)
   Main PID: 1205 (cron)
      Tasks: 1 (limit: 18077)
     Memory: 468.0K (peak: 2.7M)
        CPU: 65ms
     CGroup: /system.slice/cron.service
             └─1205 /usr/sbin/cron -f -P

Jun 09 20:17:01 fafiq-ubuntu CRON[11628]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
Jun 09 20:17:01 fafiq-ubuntu CRON[11627]: pam_unix(cron:session): session closed for user root
Jun 09 20:25:02 fafiq-ubuntu CRON[12755]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jun 09 20:25:02 fafiq-ubuntu CRON[12756]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Jun 09 20:25:02 fafiq-ubuntu CRON[12755]: pam_unix(cron:session): session closed for user root
Jun 09 20:30:01 fafiq-ubuntu CRON[13709]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jun 09 20:30:01 fafiq-ubuntu CRON[13710]: (root) CMD ([ -x /etc/init.d/anacron ] && if [ ! -d /run/systemd/system ]; then /usr/sbin/invoke-rc.d anacron start >/dev/null; fi)
Jun 09 20:30:01 fafiq-ubuntu CRON[13709]: pam_unix(cron:session): session closed for user root
Jun 09 20:35:01 fafiq-ubuntu CRON[14021]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jun 09 20:35:01 fafiq-ubuntu CRON[14021]: pam_unix(cron:session): session closed for user root
--- Status Rsyslog (System Logging) ---
● rsyslog.service - System Logging Service
     Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-06-09 19:37:41 WIB; 1h 2min ago
TriggeredBy: ● syslog.socket
       Docs: man:rsyslogd(8)
             man:rsyslog.conf(5)
             https://www.rsyslog.com/doc/
   Main PID: 1289 (rsyslogd)
      Tasks: 4 (limit: 18077)
     Memory: 5.7M (peak: 6.6M)
        CPU: 690ms
     CGroup: /system.slice/rsyslog.service
             └─1289 /usr/sbin/rsyslogd -n -iNONE

Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Starting rsyslog.service - System Logging Service...
Jun 09 19:37:41 fafiq-ubuntu rsyslogd[1289]: imuxsock: Acquired UNIX socket '/run/systemd/journal/syslog' (fd 3) from systemd.  [v8.2312.0]
Jun 09 19:37:41 fafiq-ubuntu rsyslogd[1289]: rsyslogd's groupid changed to 102
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Started rsyslog.service - System Logging Service.
Jun 09 19:37:41 fafiq-ubuntu rsyslogd[1289]: rsyslogd's userid changed to 102
Jun 09 19:37:41 fafiq-ubuntu rsyslogd[1289]: [origin software="rsyslogd" swVersion="8.2312.0" x-pid="1289" x-info="https://www.rsyslog.com"] start
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ echo "=== 5 LAYANAN DENGAN WAKTU BOOT TERLAMA ==="
systemd-analyze blame | head -5
=== 5 LAYANAN DENGAN WAKTU BOOT TERLAMA ===

16.862s plymouth-quit-wait.service
 3.711s NetworkManager-wait-online.service
 3.244s demo-web.service
 2.357s fstrim.service
 1.330s systemd-suspend.service
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ 
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ echo "=== DAFTAR LAYANAN YANG GAGAL SEJAK BOOT ==="
systemctl --failed
=== DAFTAR LAYANAN YANG GAGAL SEJAK BOOT ===
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ 
```
### Latihan 2 Layanan Kustom dengan Restart Otomatis
#### Prompt
```
echo "=== 1. STOP & CEK STATUS ==="
sudo systemctl stop ssh
systemctl is-active ssh

echo -e "\n=== 2. START & CEK STATUS ==="
sudo systemctl start ssh
systemctl is-active ssh

echo -e "\n=== 3. RESTART LAYANAN ==="
sudo systemctl restart ssh

echo -e "\n=== 4. RELOAD KONFIGURASI ==="
sudo systemctl reload ssh

echo -e "\n=== 5. MASK LAYANAN (BLOKIR) ==="
sudo systemctl mask ssh
sudo systemctl start ssh || echo "Terblokir dengan sukses!"

echo -e "\n=== 6. UNMASK LAYANAN (Buka Blokir) & NYALAKAN KEMBALI ==="
sudo systemctl unmask ssh
sudo systemctl start ssh

# 1. Buat berkas daftar layanan
cat << 'EOF' > daftar-layanan.txt
ssh
cron
rsyslog
EOF

# 2. Buat skrip cek-layanan.sh
cat << 'EOF' > cek-layanan.sh
#!/bin/bash

INPUT_FILE="daftar-layanan.txt"
LOG_FILE="laporan-layanan.log"

if [ ! -f "$INPUT_FILE" ]; then
    echo "Error: $INPUT_FILE tidak ditemukan!"
    exit 1
fi

# Baca file per baris
while IFS= read -r layanan || [ -n "$layanan" ]; do
    # Lewati baris kosong
    [ -z "$layanan" ] && continue
    
    # Ambil tanggal saat ini
    TANGGAL=$(date "+%Y-%m-%d %H:%M:%S")
    
    # Cek status layanan
    if systemctl is-active --quiet "$layanan"; then
        STATUS="ACTIVE"
    else
        STATUS="INACTIVE"
    fi
    
    # Tulis ke berkas log
    echo "[$TANGGAL] $layanan: $STATUS" >> "$LOG_FILE"
done < "$INPUT_FILE"

echo "Pengecekan selesai. Hasil dicatat di $LOG_FILE."
EOF

# 3. Berikan izin eksekusi dan jalankan skripnya
chmod +x cek-layanan.sh
./cek-layanan.sh

# 4. Tampilkan isi log untuk verifikasi
cat laporan-layanan.log

# 1. Buat ulang unit kustom yang telah dimodifikasi sesuai tantangan hlm 8
sudo bash -c "cat << EOF > /etc/systemd/system/demo-web.service
[Unit]
Description=Demo Web Server Praktek Bab 10 Modifikasi
After=network.target

[Service]
Type=simple
User=$USER
Environment=\"PORT=9091\"
WorkingDirectory=/home/$USER/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server \$PORT
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
EOF"

# 2. Muat ulang systemd, aktifkan, dan jalankan layanan
sudo systemctl daemon-reload
sudo systemctl enable --now demo-web

# 3. Verifikasi apakah port baru (9091) sudah aktif merespons curl
sleep 2
curl http://localhost:9091

# 4. Bersihkan kembali layanan setelah pengujian selesai
sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```
#### Hasil
```
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ echo "=== 1. STOP & CEK STATUS ==="
sudo systemctl stop ssh
systemctl is-active ssh

echo -e "\n=== 2. START & CEK STATUS ==="
sudo systemctl start ssh
systemctl is-active ssh

echo -e "\n=== 3. RESTART LAYANAN ==="
sudo systemctl restart ssh

echo -e "\n=== 4. RELOAD KONFIGURASI ==="
sudo systemctl reload ssh

echo -e "\n=== 5. MASK LAYANAN (BLOKIR) ==="
sudo systemctl mask ssh
sudo systemctl start ssh || echo "Terblokir dengan sukses!"

echo -e "\n=== 6. UNMASK LAYANAN (Buka Blokir) & NYALAKAN KEMBALI ==="
sudo systemctl unmask ssh
sudo systemctl start ssh
=== 1. STOP & CEK STATUS ===
Stopping 'ssh.service', but its triggering units are still active:
ssh.socket
inactive

=== 2. START & CEK STATUS ===
active

=== 3. RESTART LAYANAN ===

=== 4. RELOAD KONFIGURASI ===

=== 5. MASK LAYANAN (BLOKIR) ===
Created symlink /etc/systemd/system/ssh.service → /dev/null.
Masking 'ssh.service', but its triggering units are still active:
ssh.socket
Failed to start ssh.service: Unit ssh.service is masked.
Terblokir dengan sukses!

=== 6. UNMASK LAYANAN (Buka Blokir) & NYALAKAN KEMBALI ===
Removed "/etc/systemd/system/ssh.service".
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ # 1. Buat berkas daftar layanan
cat << 'EOF' > daftar-layanan.txt
ssh
cron
rsyslog
EOF

# 2. Buat skrip cek-layanan.sh
cat << 'EOF' > cek-layanan.sh
#!/bin/bash

INPUT_FILE="daftar-layanan.txt"
LOG_FILE="laporan-layanan.log"

if [ ! -f "$INPUT_FILE" ]; then
    echo "Error: $INPUT_FILE tidak ditemukan!"
    exit 1
fi

# Baca file per baris
while IFS= read -r layanan || [ -n "$layanan" ]; do
    # Lewati baris kosong
    [ -z "$layanan" ] && continue
    
    # Ambil tanggal saat ini
    TANGGAL=$(date "+%Y-%m-%d %H:%M:%S")
    
    # Cek status layanan
    if systemctl is-active --quiet "$layanan"; then
        STATUS="ACTIVE"
    else
        STATUS="INACTIVE"
    fi
    
    # Tulis ke berkas log
    echo "[$TANGGAL] $layanan: $STATUS" >> "$LOG_FILE"
done < "$INPUT_FILE"

echo "Pengecekan selesai. Hasil dicatat di $LOG_FILE."
EOF

# 3. Berikan izin eksekusi dan jalankan skripnya
chmod +x cek-layanan.sh
./cek-layanan.sh

# 4. Tampilkan isi log untuk verifikasi
cat laporan-layanan.log
Pengecekan selesai. Hasil dicatat di laporan-layanan.log.
[2026-06-09 20:42:51] ssh: ACTIVE
[2026-06-09 20:42:51] cron: ACTIVE
[2026-06-09 20:42:51] rsyslog: ACTIVE
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ # 1. Buat ulang unit kustom yang telah dimodifikasi sesuai tantangan hlm 8
sudo bash -c "cat << EOF > /etc/systemd/system/demo-web.service
[Unit]
Description=Demo Web Server Praktek Bab 10 Modifikasi
After=network.target

[Service]
Type=simple
User=$USER
Environment=\"PORT=9091\"
WorkingDirectory=/home/$USER/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server \$PORT
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
EOF"

# 2. Muat ulang systemd, aktifkan, dan jalankan layanan
sudo systemctl daemon-reload
sudo systemctl enable --now demo-web

# 3. Verifikasi apakah port baru (9091) sudah aktif merespons curl
sleep 2
curl http://localhost:9091

# 4. Bersihkan kembali layanan setelah pengujian selesai
sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
curl: (7) Failed to connect to localhost port 9091 after 0 ms: Couldn't connect to server
Removed "/etc/systemd/system/multi-user.target.wants/demo-web.service".
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ 
```
### Latihan 3 Investigasi Log dan Keamanan SSH
#### Prompt
```
journalctl --since "06:00:00" --until "11:59:59" --no-pager | head -50

journalctl -b -g "failed|invalid|denied" --no-pager | head -30

# 1. Buat layanan tiruan yang rusak (perintah /usr/bin/tidak-ada pasti gagal)
sudo bash -c "cat << EOF > /etc/systemd/system/layanan-rusak.service
[Unit]
Description=Layanan Simulasi Error Troubleshooting
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/tidak-ada-perintah-ini
EOF"

# 2. Muat ulang dan coba jalankan
sudo systemctl daemon-reload
sudo systemctl start layanan-rusak.service

# 3. Jalankan perintah audit diagnosis kegagalan
echo -e "\n=== 1. STATUS UNIT YANG GAGAL ==="
systemctl status layanan-rusak.service --no-pager

echo -e "\n=== 2. ANALISIS LOG DENGAN JOURNALCTL ==="
journalctl -u layanan-rusak.service -n 10 --no-pager

# 4. Bersihkan kembali sistem
sudo rm /etc/systemd/system/layanan-rusak.service
sudo systemctl daemon-reload
```
#### Hasil
```
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ journalctl --since "06:00:00" --until "11:59:59" --no-pager | head -50
-- No entries --
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ journalctl -b -g "failed|invalid|denied" --no-pager | head -30
Jun 09 19:37:39 fafiq-ubuntu kernel: iommu: DMA domain TLB invalidation policy: lazy mode
Jun 09 19:37:39 fafiq-ubuntu kernel: lenovo_wmi_gamezone 887B54E3-DDDC-4B2C-8B88-68A26A8835D0: platform_profile probe failed
Jun 09 19:37:39 fafiq-ubuntu (udev-worker)[623]: controlC1: Process '/usr/sbin/alsactl -E HOME=/run/alsa -E XDG_RUNTIME_DIR=/run/alsa/runtime restore 1' failed with exit code 99.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-nss.socket - SSSD NSS Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-nss.socket: Job sssd-nss.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-autofs.socket - SSSD AutoFS Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-autofs.socket: Job sssd-autofs.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-pac.socket - SSSD PAC Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-pac.socket: Job sssd-pac.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-pam-priv.socket - SSSD PAM Service responder private socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-pam.socket - SSSD PAM Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-pam.socket: Job sssd-pam.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-pam-priv.socket: Job sssd-pam-priv.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-ssh.socket - SSSD SSH Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-ssh.socket: Job sssd-ssh.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Dependency failed for sssd-sudo.socket - SSSD Sudo Service responder socket.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: sssd-sudo.socket: Job sssd-sudo.socket/start failed with result 'dependency'.
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Starting grub-initrd-fallback.service - GRUB failed boot detection...
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: Finished grub-initrd-fallback.service - GRUB failed boot detection.
Jun 09 19:37:41 fafiq-ubuntu gnome-remote-de[1177]: Init TPM credentials failed because Failed to initialize transmission interface context: tcti:IO failure, using GKeyFile as fallback
Jun 09 19:37:41 fafiq-ubuntu bluetoothd[1172]: profiles/sap/server.c:sap_server_register() Sap driver initialization failed.
Jun 09 19:37:41 fafiq-ubuntu NetworkManager[1295]: <info>  [1781008661.9434] failed to open /run/network/ifstate
Jun 09 19:37:41 fafiq-ubuntu (python3)[1978]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:41 fafiq-ubuntu systemd[1]: demo-web.service: Failed with result 'exit-code'.
Jun 09 19:37:45 fafiq-ubuntu (python3)[2131]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:45 fafiq-ubuntu systemd[1]: demo-web.service: Failed with result 'exit-code'.
Jun 09 19:37:45 fafiq-ubuntu systemd[1]: Started update-notifier-download.timer - Download data for packages that failed at package install time.
Jun 09 19:37:48 fafiq-ubuntu (python3)[2165]: demo-web.service: Failed to determine user credentials: No such process
Jun 09 19:37:48 fafiq-ubuntu systemd[1]: demo-web.service: Failed with result 'exit-code'.
Jun 09 19:37:51 fafiq-ubuntu (python3)[2167]: demo-web.service: Failed to determine user credentials: No such process
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ # 1. Buat layanan tiruan yang rusak (perintah /usr/bin/tidak-ada pasti gagal)
sudo bash -c "cat << EOF > /etc/systemd/system/layanan-rusak.service
[Unit]
Description=Layanan Simulasi Error Troubleshooting
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/tidak-ada-perintah-ini
EOF"

# 2. Muat ulang dan coba jalankan
sudo systemctl daemon-reload
sudo systemctl start layanan-rusak.service

# 3. Jalankan perintah audit diagnosis kegagalan
echo -e "\n=== 1. STATUS UNIT YANG GAGAL ==="
systemctl status layanan-rusak.service --no-pager

echo -e "\n=== 2. ANALISIS LOG DENGAN JOURNALCTL ==="
journalctl -u layanan-rusak.service -n 10 --no-pager

# 4. Bersihkan kembali sistem
sudo rm /etc/systemd/system/layanan-rusak.service
sudo systemctl daemon-reload

=== 1. STATUS UNIT YANG GAGAL ===
× layanan-rusak.service - Layanan Simulasi Error Troubleshooting
     Loaded: loaded (/etc/systemd/system/layanan-rusak.service; static)
     Active: failed (Result: exit-code) since Tue 2026-06-09 20:45:32 WIB; 9ms ago
   Duration: 607us
    Process: 16084 ExecStart=/usr/bin/tidak-ada-perintah-ini (code=exited, status=203/EXEC)
   Main PID: 16084 (code=exited, status=203/EXEC)
        CPU: 597us

Jun 09 20:45:32 fafiq-ubuntu systemd[1]: Started layanan-rusak.service - Layanan Simulasi Error Troubleshooting.
Jun 09 20:45:32 fafiq-ubuntu systemd[1]: layanan-rusak.service: Main process exited, code=exited, status=203/EXEC
Jun 09 20:45:32 fafiq-ubuntu systemd[1]: layanan-rusak.service: Failed with result 'exit-code'.

=== 2. ANALISIS LOG DENGAN JOURNALCTL ===
Jun 09 20:45:32 fafiq-ubuntu systemd[1]: Started layanan-rusak.service - Layanan Simulasi Error Troubleshooting.
Jun 09 20:45:32 fafiq-ubuntu systemd[1]: layanan-rusak.service: Main process exited, code=exited, status=203/EXEC
Jun 09 20:45:32 fafiq-ubuntu systemd[1]: layanan-rusak.service: Failed with result 'exit-code'.
fafiq@fafiq-ubuntu:~/lab-os/chapter10-services$ 
```