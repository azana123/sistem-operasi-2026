# Laporan Praktikum Sistem Operasi Jobsheet 6

<h4>Nama  : Fafiq Lutfi Azana<h4>
<h4>NIM   : 254107020058<h4>
<h4>Kelas : TI-1G<h4>

# Manajemen Proses
## Praktikum
### Praktikum 6.1 — Melihat Proses dan Thread

#### Prompt
```
ps aux
```

#### Output (10 baris pertama)
```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0  23536 14968 ?        Ss   15:28   0:03 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    15:28   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    15:28   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-netns]
root          11  0.0  0.0      0     0 ?        I<   15:28   0:00 [kworker/0:0H-events_highpri]
root          12  0.2  0.0      0     0 ?        I    15:28   0:05 [kworker/u64:0-gfx_0.0.0]
```

#### Prompt
```
ps aux -L
```

#### Output (10 baris pertama)
```
USER         PID     LWP %CPU NLWP %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1       1  0.1    1  0.0  23536 14972 ?        Ss   15:28   0:03 /sbin/init splash
root           2       2  0.0    1  0.0      0     0 ?        S    15:28   0:00 [kthreadd]
root           3       3  0.0    1  0.0      0     0 ?        S    15:28   0:00 [pool_workqueue_release]
root           4       4  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-rcu_gp]
root           5       5  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-sync_wq]
root           6       6  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7       7  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-slub_flushwq]
root           8       8  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/R-netns]
root          11      11  0.0    1  0.0      0     0 ?        I<   15:28   0:00 [kworker/0:0H-events_highpri]
root          12      12  0.2    1  0.0      0     0 ?        I    15:28   0:06 [kworker/u64:0-events_unbound]
```

#### Prompt
```
echo $$
ps -p $$ -f
```

#### Hasil
```
43510
UID          PID    PPID  C STIME TTY          TIME CMD
fafiq      43510   43502  0 16:12 pts/0    00:00:00 bash
```

#### Prompt
```
pstree -p
```

#### Hasil
```
systemd(1)─┬─ModemManager(1073)─┬─{ModemManager}(1088)
           │                    ├─{ModemManager}(1092)
           │                    └─{ModemManager}(1095)
           ├─NetworkManager(985)─┬─{NetworkManager}(1072)
           │                     ├─{NetworkManager}(1074)
           │                     └─{NetworkManager}(1078)
           ├─accounts-daemon(920)─┬─{accounts-daemon}(1014)
           │                      ├─{accounts-daemon}(1015)
           │                      └─{accounts-daemon}(1021)
           ├─avahi-daemon(895)───avahi-daemon(961)
           ├─bluetoothd(896)
           ├─colord(1789)─┬─{colord}(1805)
           │              ├─{colord}(1806)
           │              └─{colord}(1808)
           ├─cron(924)
           ├─cups-browsed(1555)─┬─{cups-browsed}(1562)
           │                    ├─{cups-browsed}(1563)
           │                    └─{cups-browsed}(1564)
           ├─cupsd(1446)───dbus(1461)
           ├─dbus-daemon(897)
           ├─fwupd(6926)─┬─{fwupd}(6927)
           │             ├─{fwupd}(6928)
           │             ├─{fwupd}(6929)
           │             ├─{fwupd}(6930)
           │             └─{fwupd}(6932)
           ├─gdm3(1464)─┬─gdm-session-wor(2195)─┬─gdm-wayland-ses(2338)─┬─gnome-session-b(2348)─┬─{gnome-session-b}(2402)
           │            │                       │                       │                       ├─{gnome-session-b}(2403)
           │            │                       │                       │                       └─{gnome-session-b}(2404)
           │            │                       │                       ├─{gdm-wayland-ses}(2344)
           │            │                       │                       ├─{gdm-wayland-ses}(2345)
           │            │                       │                       └─{gdm-wayland-ses}(2346)
           │            │                       ├─{gdm-session-wor}(2196)
           │            │                       ├─{gdm-session-wor}(2197)
           │            │                       └─{gdm-session-wor}(2199)
           │            ├─{gdm3}(1466)
           │            ├─{gdm3}(1467)
           │            └─{gdm3}(1468)
           ├─gnome-remote-de(900)─┬─{gnome-remote-de}(995)
           │                      ├─{gnome-remote-de}(996)
           │                      └─{gnome-remote-de}(997)
           ├─kerneloops(1557)
           ├─kerneloops(1560)
           ├─polkitd(904)─┬─{polkitd}(1035)
           │              ├─{polkitd}(1037)
           │              └─{polkitd}(1038)
           ├─power-profiles-(907)─┬─{power-profiles-}(944)
           │                      ├─{power-profiles-}(946)
           │                      └─{power-profiles-}(992)
           ├─rsyslogd(1007)─┬─{rsyslogd}(1089)
           │                ├─{rsyslogd}(1090)
           │                └─{rsyslogd}(1091)
           ├─rtkit-daemon(1641)─┬─{rtkit-daemon}(1649)
           │                    └─{rtkit-daemon}(1650)
           ├─run-cups-browse(13646)───run-cups-browse(13846)───sleep(13847)
           ├─run-cupsd(13657)─┬─cups-proxyd(13807)─┬─{cups-proxyd}(13860)
           │                  │                    ├─{cups-proxyd}(13861)
           │                  │                    └─{cups-proxyd}(13862)
           │                  └─cupsd(13806)
           ├─snapd(914)─┬─{snapd}(1440)
           │            ├─{snapd}(1441)
           │            ├─{snapd}(1442)
           │            ├─{snapd}(1443)
           │            ├─{snapd}(1444)
           │            ├─{snapd}(1476)
           │            ├─{snapd}(1477)
           │            ├─{snapd}(1478)
           │            ├─{snapd}(1511)
           │            ├─{snapd}(1512)
           │            ├─{snapd}(1513)
           │            ├─{snapd}(1514)
           │            ├─{snapd}(1515)
           │            ├─{snapd}(1516)
           │            ├─{snapd}(1528)
           │            ├─{snapd}(1529)
           │            ├─{snapd}(1537)
           │            ├─{snapd}(1538)
           │            ├─{snapd}(1541)
           │            ├─{snapd}(1542)
           │            ├─{snapd}(1596)
           │            ├─{snapd}(8509)
           │            ├─{snapd}(12424)
           │            ├─{snapd}(12588)
           │            └─{snapd}(12621)
           ├─switcheroo-cont(925)─┬─{switcheroo-cont}(968)
           │                      ├─{switcheroo-cont}(969)
           │                      └─{switcheroo-cont}(986)
           ├─systemd(2215)─┬─(sd-pam)(2222)
           │               ├─at-spi2-registr(2608)─┬─{at-spi2-registr}(2609)
           │               │                       ├─{at-spi2-registr}(2610)
           │               │                       └─{at-spi2-registr}(2611)
           │               ├─chrome_crashpad(3405)─┬─{chrome_crashpad}(3406)
           │               │                       └─{chrome_crashpad}(3407)
           │               ├─crashhelper(5122)───{crashhelper}(5123)
           │               ├─dbus-daemon(2256)
           │               ├─dconf-service(3011)─┬─{dconf-service}(3013)
           │               │                     ├─{dconf-service}(3014)
           │               │                     └─{dconf-service}(3015)
           │               ├─evolution-addre(2982)─┬─{evolution-addre}(2989)
           │               │                       ├─{evolution-addre}(2990)
           │               │                       ├─{evolution-addre}(2991)
           │               │                       ├─{evolution-addre}(2994)
           │               │                       ├─{evolution-addre}(2995)
           │               │                       └─{evolution-addre}(2998)
           │               ├─evolution-calen(2899)─┬─{evolution-calen}(2939)
           │               │                       ├─{evolution-calen}(2941)
           │               │                       ├─{evolution-calen}(2945)
           │               │                       ├─{evolution-calen}(2959)
           │               │                       ├─{evolution-calen}(2960)
           │               │                       ├─{evolution-calen}(2978)
           │               │                       ├─{evolution-calen}(2979)
           │               │                       ├─{evolution-calen}(2984)
           │               │                       └─{evolution-calen}(3105)
           │               ├─evolution-sourc(2647)─┬─{evolution-sourc}(2652)
           │               │                       ├─{evolution-sourc}(2653)
           │               │                       ├─{evolution-sourc}(2654)
           │               │                       └─{evolution-sourc}(2655)
           │               ├─gcr-ssh-agent(2411)─┬─{gcr-ssh-agent}(2420)
           │               │                     └─{gcr-ssh-agent}(2421)
           │               ├─gjs(2657)─┬─{gjs}(2663)
           │               │           ├─{gjs}(2664)
           │               │           ├─{gjs}(2666)
           │               │           ├─{gjs}(2669)
           │               │           ├─{gjs}(2671)
           │               │           ├─{gjs}(2672)
           │               │           ├─{gjs}(2673)
           │               │           ├─{gjs}(2674)
           │               │           ├─{gjs}(2675)
           │               │           ├─{gjs}(2676)
           │               │           └─{gjs}(2677)
           │               ├─gjs(3074)─┬─{gjs}(3078)
           │               │           ├─{gjs}(3079)
           │               │           ├─{gjs}(3080)
           │               │           ├─{gjs}(3081)
           │               │           ├─{gjs}(3082)
           │               │           ├─{gjs}(3083)
           │               │           ├─{gjs}(3084)
           │               │           ├─{gjs}(3085)
           │               │           ├─{gjs}(3086)
           │               │           ├─{gjs}(3087)
           │               │           └─{gjs}(3088)
           │               ├─gnome-keyring-d(2243)─┬─{gnome-keyring-d}(2257)
           │               │                       ├─{gnome-keyring-d}(2258)
           │               │                       ├─{gnome-keyring-d}(2259)
           │               │                       └─{gnome-keyring-d}(2260)
           │               ├─gnome-session-b(2450)─┬─at-spi-bus-laun(2488)─┬─dbus-daemon(2501)
           │               │                       │                       ├─{at-spi-bus-laun}(2495)
           │               │                       │                       ├─{at-spi-bus-laun}(2496)
           │               │                       │                       ├─{at-spi-bus-laun}(2497)
           │               │                       │                       └─{at-spi-bus-laun}(2499)
           │               │                       ├─evolution-alarm(2762)─┬─{evolution-alarm}(2829)
           │               │                       │                       ├─{evolution-alarm}(2830)
           │               │                       │                       ├─{evolution-alarm}(2832)
           │               │                       │                       ├─{evolution-alarm}(2856)
           │               │                       │                       ├─{evolution-alarm}(3093)
           │               │                       │                       ├─{evolution-alarm}(3098)
           │               │                       │                       └─{evolution-alarm}(3101)
           │               │                       ├─gsd-disk-utilit(2742)─┬─{gsd-disk-utilit}(2757)
           │               │                       │                       ├─{gsd-disk-utilit}(2758)
           │               │                       │                       └─{gsd-disk-utilit}(2816)
           │               │                       ├─update-notifier(3278)─┬─{update-notifier}(3289)
           │               │                       │                       ├─{update-notifier}(3290)
           │               │                       │                       ├─{update-notifier}(3294)
           │               │                       │                       └─{update-notifier}(3295)
           │               │                       ├─{gnome-session-b}(2457)
           │               │                       ├─{gnome-session-b}(2458)
           │               │                       ├─{gnome-session-b}(2460)
           │               │                       └─{gnome-session-b}(2465)
           │               ├─gnome-session-c(2413)───{gnome-session-c}(2424)
           │               ├─gnome-shell(2487)─┬─Xwayland(3513)─┬─{Xwayland}(3528)
           │               │                   │                ├─{Xwayland}(3529)
           │               │                   │                ├─{Xwayland}(3530)
           │               │                   │                ├─{Xwayland}(3531)
           │               │                   │                ├─{Xwayland}(3532)
           │               │                   │                ├─{Xwayland}(3533)
           │               │                   │                ├─{Xwayland}(3534)
           │               │                   │                ├─{Xwayland}(3535)
           │               │                   │                ├─{Xwayland}(3536)
           │               │                   │                └─{Xwayland}(3537)
           │               │                   ├─code(3375)─┬─code(3380)───code(3427)─┬─{code}(3457)
           │               │                   │            │                         ├─{code}(3458)
           │               │                   │            │                         ├─{code}(3459)
           │               │                   │            │                         ├─{code}(3460)
           │               │                   │            │                         ├─{code}(3461)
           │               │                   │            │                         ├─{code}(3462)
           │               │                   │            │                         ├─{code}(3463)
           │               │                   │            │                         ├─{code}(3464)
           │               │                   │            │                         ├─{code}(3465)
           │               │                   │            │                         ├─{code}(3466)
           │               │                   │            │                         ├─{code}(3467)
           │               │                   │            │                         ├─{code}(3485)
           │               │                   │            │                         ├─{code}(3486)
           │               │                   │            │                         ├─{code}(3487)
           │               │                   │            │                         ├─{code}(3488)
           │               │                   │            │                         ├─{code}(3489)
           │               │                   │            │                         ├─{code}(3490)
           │               │                   │            │                         ├─{code}(3577)
           │               │                   │            │                         └─{code}(43715)
           │               │                   │            ├─code(3381)───code(3383)───code(3495)─┬─{code}(3497)
           │               │                   │            │                                      ├─{code}(3498)
           │               │                   │            │                                      ├─{code}(3499)
           │               │                   │            │                                      ├─{code}(3500)
           │               │                   │            │                                      ├─{code}(3501)
           │               │                   │            │                                      ├─{code}(3511)
           │               │                   │            │                                      ├─{code}(3512)
           │               │                   │            │                                      ├─{code}(3596)
           │               │                   │            │                                      ├─{code}(3597)
           │               │                   │            │                                      ├─{code}(3598)
           │               │                   │            │                                      ├─{code}(3599)
           │               │                   │            │                                      ├─{code}(3600)
           │               │                   │            │                                      ├─{code}(3601)
           │               │                   │            │                                      ├─{code}(3645)
           │               │                   │            │                                      ├─{code}(3646)
           │               │                   │            │                                      ├─{code}(3647)
           │               │                   │            │                                      ├─{code}(3648)
           │               │                   │            │                                      ├─{code}(3649)
           │               │                   │            │                                      ├─{code}(3650)
           │               │                   │            │                                      ├─{code}(3651)
           │               │                   │            │                                      ├─{code}(3814)
           │               │                   │            │                                      ├─{code}(4989)
           │               │                   │            │                                      ├─{code}(31207)
           │               │                   │            │                                      └─{code}(43952)
           │               │                   │            ├─code(3436)─┬─{code}(3437)
           │               │                   │            │            ├─{code}(3438)
           │               │                   │            │            ├─{code}(3439)
           │               │                   │            │            ├─{code}(3440)
           │               │                   │            │            ├─{code}(3441)
           │               │                   │            │            ├─{code}(3442)
           │               │                   │            │            ├─{code}(3443)
           │               │                   │            │            ├─{code}(3444)
           │               │                   │            │            ├─{code}(3448)
           │               │                   │            │            └─{code}(3449)
           │               │                   │            ├─code(3602)─┬─{code}(3605)
           │               │                   │            │            ├─{code}(3606)
           │               │                   │            │            ├─{code}(3607)
           │               │                   │            │            ├─{code}(3608)
           │               │                   │            │            ├─{code}(3609)
           │               │                   │            │            ├─{code}(3610)
           │               │                   │            │            ├─{code}(3611)
           │               │                   │            │            ├─{code}(3612)
           │               │                   │            │            ├─{code}(3613)
           │               │                   │            │            ├─{code}(3614)
           │               │                   │            │            ├─{code}(3615)
           │               │                   │            │            ├─{code}(3616)
           │               │                   │            │            ├─{code}(3617)
           │               │                   │            │            ├─{code}(3618)
           │               │                   │            │            ├─{code}(3652)
           │               │                   │            │            ├─{code}(3655)
           │               │                   │            │            ├─{code}(3656)
           │               │                   │            │            ├─{code}(3657)
           │               │                   │            │            ├─{code}(3658)
           │               │                   │            │            └─{code}(3659)
           │               │                   │            ├─code(3603)─┬─{code}(3623)
           │               │                   │            │            ├─{code}(3624)
           │               │                   │            │            ├─{code}(3625)
           │               │                   │            │            ├─{code}(3626)
           │               │                   │            │            ├─{code}(3631)
           │               │                   │            │            ├─{code}(3632)
           │               │                   │            │            ├─{code}(3633)
           │               │                   │            │            ├─{code}(3634)
           │               │                   │            │            ├─{code}(3638)
           │               │                   │            │            ├─{code}(3639)
           │               │                   │            │            ├─{code}(3642)
           │               │                   │            │            ├─{code}(3644)
           │               │                   │            │            ├─{code}(3654)
           │               │                   │            │            ├─{code}(3660)
           │               │                   │            │            ├─{code}(3661)
           │               │                   │            │            ├─{code}(3662)
           │               │                   │            │            ├─{code}(3663)
           │               │                   │            │            ├─{code}(3664)
           │               │                   │            │            ├─{code}(3791)
           │               │                   │            │            └─{code}(3792)
           │               │                   │            ├─code(3604)─┬─code(3691)─┬─{code}(3692)
           │               │                   │            │            │            ├─{code}(3693)
           │               │                   │            │            │            ├─{code}(3694)
           │               │                   │            │            │            ├─{code}(3695)
           │               │                   │            │            │            ├─{code}(3696)
           │               │                   │            │            │            ├─{code}(3697)
           │               │                   │            │            │            └─{code}(3698)
           │               │                   │            │            ├─{code}(3619)
           │               │                   │            │            ├─{code}(3620)
           │               │                   │            │            ├─{code}(3621)
           │               │                   │            │            ├─{code}(3622)
           │               │                   │            │            ├─{code}(3627)
           │               │                   │            │            ├─{code}(3628)
           │               │                   │            │            ├─{code}(3629)
           │               │                   │            │            ├─{code}(3630)
           │               │                   │            │            ├─{code}(3635)
           │               │                   │            │            ├─{code}(3636)
           │               │                   │            │            ├─{code}(3637)
           │               │                   │            │            ├─{code}(3640)
           │               │                   │            │            ├─{code}(3641)
           │               │                   │            │            ├─{code}(3643)
           │               │                   │            │            ├─{code}(3653)
           │               │                   │            │            ├─{code}(3665)
           │               │                   │            │            ├─{code}(3666)
           │               │                   │            │            ├─{code}(3667)
           │               │                   │            │            ├─{code}(3668)
           │               │                   │            │            └─{code}(3669)
           │               │                   │            ├─code(33339)─┬─bash(33367)
           │               │                   │            │             ├─{code}(33340)
           │               │                   │            │             ├─{code}(33341)
           │               │                   │            │             ├─{code}(33342)
           │               │                   │            │             ├─{code}(33343)
           │               │                   │            │             ├─{code}(33344)
           │               │                   │            │             ├─{code}(33345)
           │               │                   │            │             ├─{code}(33346)
           │               │                   │            │             ├─{code}(33347)
           │               │                   │            │             ├─{code}(33348)
           │               │                   │            │             ├─{code}(33349)
           │               │                   │            │             ├─{code}(33350)
           │               │                   │            │             ├─{code}(33351)
           │               │                   │            │             ├─{code}(33352)
           │               │                   │            │             ├─{code}(33357)
           │               │                   │            │             ├─{code}(33358)
           │               │                   │            │             ├─{code}(33359)
           │               │                   │            │             ├─{code}(33360)
           │               │                   │            │             ├─{code}(33361)
           │               │                   │            │             ├─{code}(33362)
           │               │                   │            │             └─{code}(33368)
           │               │                   │            ├─{code}(3378)
           │               │                   │            ├─{code}(3384)
           │               │                   │            ├─{code}(3385)
           │               │                   │            ├─{code}(3386)
           │               │                   │            ├─{code}(3387)
           │               │                   │            ├─{code}(3388)
           │               │                   │            ├─{code}(3389)
           │               │                   │            ├─{code}(3390)
           │               │                   │            ├─{code}(3398)
           │               │                   │            ├─{code}(3399)
           │               │                   │            ├─{code}(3400)
           │               │                   │            ├─{code}(3401)
           │               │                   │            ├─{code}(3402)
           │               │                   │            ├─{code}(3403)
           │               │                   │            ├─{code}(3415)
           │               │                   │            ├─{code}(3416)
           │               │                   │            ├─{code}(3418)
           │               │                   │            ├─{code}(3419)
           │               │                   │            ├─{code}(3420)
           │               │                   │            ├─{code}(3421)
           │               │                   │            ├─{code}(3422)
           │               │                   │            ├─{code}(3423)
           │               │                   │            ├─{code}(3424)
           │               │                   │            ├─{code}(3425)
           │               │                   │            ├─{code}(3426)
           │               │                   │            ├─{code}(3428)
           │               │                   │            ├─{code}(3429)
           │               │                   │            ├─{code}(3431)
           │               │                   │            ├─{code}(3432)
           │               │                   │            ├─{code}(3433)
           │               │                   │            ├─{code}(3434)
           │               │                   │            ├─{code}(3445)
           │               │                   │            ├─{code}(3446)
           │               │                   │            ├─{code}(3447)
           │               │                   │            ├─{code}(3493)
           │               │                   │            ├─{code}(3494)
           │               │                   │            ├─{code}(3573)
           │               │                   │            ├─{code}(7085)
           │               │                   │            ├─{code}(43587)
           │               │                   │            └─{code}(43588)
           │               │                   ├─firefox(5046)─┬─forkserver(5264)─┬─Isolated Web Co(5993)─┬─{Isolated Web Co}(6000)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6003)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6007)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6013)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6014)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6015)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6016)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6017)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6018)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6019)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6022)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6042)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6043)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6044)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6045)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6046)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6047)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6060)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6061)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6062)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6063)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6064)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6065)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6066)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6067)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6178)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(37981)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(38946)
           │               │                   │               │                  │                       └─{Isolated Web Co}(38954)
           │               │                   │               │                  ├─Isolated Web Co(6358)─┬─{Isolated Web Co}(6362)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6364)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6365)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6366)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6367)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6368)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6369)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6370)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6371)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6372)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6374)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6375)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6376)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6377)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6378)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6379)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6380)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6381)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6382)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6383)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6384)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6385)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6386)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6387)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6388)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6582)
           │               │                   │               │                  │                       ├─{Isolated Web Co}(6638)
           │               │                   │               │                  │                       └─{Isolated Web Co}(6645)
           │               │                   │               │                  ├─Isolated Web Co(30204)─┬─{Isolated Web Co}(30211)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30213)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30217)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30219)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30222)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30225)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30228)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30229)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30230)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30231)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30236)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30237)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30239)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30241)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30244)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30247)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30248)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30249)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30251)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30253)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30254)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30256)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30257)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30258)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(30260)
           │               │                   │               │                  │                        ├─{Isolated Web Co}(32177)
           │               │                   │               │                  │                        └─{Isolated Web Co}(32224)
           │               │                   │               │                  ├─Privileged Cont(5292)─┬─{Privileged Cont}(5297)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5300)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5309)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5310)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5311)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5312)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5313)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5314)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5315)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5316)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5321)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5322)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5323)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5324)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5325)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5326)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5327)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5338)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5339)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5340)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5341)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5342)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5343)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5344)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5345)
           │               │                   │               │                  │                       ├─{Privileged Cont}(5687)
           │               │                   │               │                  │                       └─{Privileged Cont}(6096)
           │               │                   │               │                  ├─RDD Process(5303)─┬─{RDD Process}(5306)
           │               │                   │               │                  │                   ├─{RDD Process}(5308)
           │               │                   │               │                  │                   ├─{RDD Process}(5333)
           │               │                   │               │                  │                   └─{RDD Process}(6101)
           │               │                   │               │                  ├─Socket Process(5268)─┬─{Socket Process}(5271)
           │               │                   │               │                  │                      ├─{Socket Process}(5273)
           │               │                   │               │                  │                      ├─{Socket Process}(5277)
           │               │                   │               │                  │                      ├─{Socket Process}(5279)
           │               │                   │               │                  │                      ├─{Socket Process}(6103)
           │               │                   │               │                  │                      └─{Socket Process}(26440)
           │               │                   │               │                  ├─Utility Process(5840)─┬─{Utility Process}(5843)
           │               │                   │               │                  │                       ├─{Utility Process}(5845)
           │               │                   │               │                  │                       ├─{Utility Process}(5847)
           │               │                   │               │                  │                       └─{Utility Process}(6102)
           │               │                   │               │                  ├─Web Content(32232)─┬─{Web Content}(32236)
           │               │                   │               │                  │                    ├─{Web Content}(32238)
           │               │                   │               │                  │                    ├─{Web Content}(32239)
           │               │                   │               │                  │                    ├─{Web Content}(32240)
           │               │                   │               │                  │                    ├─{Web Content}(32241)
           │               │                   │               │                  │                    ├─{Web Content}(32242)
           │               │                   │               │                  │                    ├─{Web Content}(32243)
           │               │                   │               │                  │                    ├─{Web Content}(32244)
           │               │                   │               │                  │                    ├─{Web Content}(32245)
           │               │                   │               │                  │                    ├─{Web Content}(32246)
           │               │                   │               │                  │                    ├─{Web Content}(32248)
           │               │                   │               │                  │                    ├─{Web Content}(32253)
           │               │                   │               │                  │                    ├─{Web Content}(32254)
           │               │                   │               │                  │                    ├─{Web Content}(32255)
           │               │                   │               │                  │                    ├─{Web Content}(32256)
           │               │                   │               │                  │                    ├─{Web Content}(32257)
           │               │                   │               │                  │                    ├─{Web Content}(32258)
           │               │                   │               │                  │                    ├─{Web Content}(32259)
           │               │                   │               │                  │                    ├─{Web Content}(32260)
           │               │                   │               │                  │                    ├─{Web Content}(32261)
           │               │                   │               │                  │                    ├─{Web Content}(32262)
           │               │                   │               │                  │                    ├─{Web Content}(32263)
           │               │                   │               │                  │                    ├─{Web Content}(32264)
           │               │                   │               │                  │                    ├─{Web Content}(32265)
           │               │                   │               │                  │                    └─{Web Content}(32266)
           │               │                   │               │                  ├─Web Content(37860)─┬─{Web Content}(37864)
           │               │                   │               │                  │                    ├─{Web Content}(37866)
           │               │                   │               │                  │                    ├─{Web Content}(37871)
           │               │                   │               │                  │                    ├─{Web Content}(37872)
           │               │                   │               │                  │                    ├─{Web Content}(37873)
           │               │                   │               │                  │                    ├─{Web Content}(37874)
           │               │                   │               │                  │                    ├─{Web Content}(37875)
           │               │                   │               │                  │                    ├─{Web Content}(37876)
           │               │                   │               │                  │                    ├─{Web Content}(37877)
           │               │                   │               │                  │                    ├─{Web Content}(37878)
           │               │                   │               │                  │                    ├─{Web Content}(37880)
           │               │                   │               │                  │                    ├─{Web Content}(37881)
           │               │                   │               │                  │                    ├─{Web Content}(37882)
           │               │                   │               │                  │                    ├─{Web Content}(37883)
           │               │                   │               │                  │                    ├─{Web Content}(37884)
           │               │                   │               │                  │                    ├─{Web Content}(37885)
           │               │                   │               │                  │                    ├─{Web Content}(37886)
           │               │                   │               │                  │                    ├─{Web Content}(37887)
           │               │                   │               │                  │                    ├─{Web Content}(37888)
           │               │                   │               │                  │                    ├─{Web Content}(37889)
           │               │                   │               │                  │                    ├─{Web Content}(37890)
           │               │                   │               │                  │                    ├─{Web Content}(37891)
           │               │                   │               │                  │                    ├─{Web Content}(37892)
           │               │                   │               │                  │                    ├─{Web Content}(37893)
           │               │                   │               │                  │                    └─{Web Content}(37894)
           │               │                   │               │                  ├─Web Content(43643)─┬─{Web Content}(43647)
           │               │                   │               │                  │                    ├─{Web Content}(43649)
           │               │                   │               │                  │                    ├─{Web Content}(43650)
           │               │                   │               │                  │                    ├─{Web Content}(43651)
           │               │                   │               │                  │                    ├─{Web Content}(43652)
           │               │                   │               │                  │                    ├─{Web Content}(43653)
           │               │                   │               │                  │                    ├─{Web Content}(43654)
           │               │                   │               │                  │                    ├─{Web Content}(43655)
           │               │                   │               │                  │                    ├─{Web Content}(43656)
           │               │                   │               │                  │                    ├─{Web Content}(43657)
           │               │                   │               │                  │                    ├─{Web Content}(43659)
           │               │                   │               │                  │                    ├─{Web Content}(43660)
           │               │                   │               │                  │                    ├─{Web Content}(43661)
           │               │                   │               │                  │                    ├─{Web Content}(43662)
           │               │                   │               │                  │                    ├─{Web Content}(43663)
           │               │                   │               │                  │                    ├─{Web Content}(43664)
           │               │                   │               │                  │                    ├─{Web Content}(43665)
           │               │                   │               │                  │                    ├─{Web Content}(43666)
           │               │                   │               │                  │                    ├─{Web Content}(43667)
           │               │                   │               │                  │                    ├─{Web Content}(43668)
           │               │                   │               │                  │                    ├─{Web Content}(43669)
           │               │                   │               │                  │                    ├─{Web Content}(43670)
           │               │                   │               │                  │                    ├─{Web Content}(43671)
           │               │                   │               │                  │                    ├─{Web Content}(43672)
           │               │                   │               │                  │                    └─{Web Content}(43673)
           │               │                   │               │                  └─WebExtensions(5502)─┬─{WebExtensions}(5506)
           │               │                   │               │                                        ├─{WebExtensions}(5508)
           │               │                   │               │                                        ├─{WebExtensions}(5509)
           │               │                   │               │                                        ├─{WebExtensions}(5510)
           │               │                   │               │                                        ├─{WebExtensions}(5511)
           │               │                   │               │                                        ├─{WebExtensions}(5512)
           │               │                   │               │                                        ├─{WebExtensions}(5513)
           │               │                   │               │                                        ├─{WebExtensions}(5514)
           │               │                   │               │                                        ├─{WebExtensions}(5515)
           │               │                   │               │                                        ├─{WebExtensions}(5516)
           │               │                   │               │                                        ├─{WebExtensions}(5518)
           │               │                   │               │                                        ├─{WebExtensions}(5519)
           │               │                   │               │                                        ├─{WebExtensions}(5520)
           │               │                   │               │                                        ├─{WebExtensions}(5521)
           │               │                   │               │                                        ├─{WebExtensions}(5522)
           │               │                   │               │                                        ├─{WebExtensions}(5523)
           │               │                   │               │                                        ├─{WebExtensions}(5524)
           │               │                   │               │                                        ├─{WebExtensions}(5526)
           │               │                   │               │                                        ├─{WebExtensions}(5527)
           │               │                   │               │                                        ├─{WebExtensions}(5528)
           │               │                   │               │                                        ├─{WebExtensions}(5529)
           │               │                   │               │                                        ├─{WebExtensions}(5530)
           │               │                   │               │                                        ├─{WebExtensions}(5531)
           │               │                   │               │                                        ├─{WebExtensions}(5532)
           │               │                   │               │                                        ├─{WebExtensions}(5533)
           │               │                   │               │                                        └─{WebExtensions}(5696)
           │               │                   │               ├─{firefox}(5120)
           │               │                   │               ├─{firefox}(5124)
           │               │                   │               ├─{firefox}(5125)
           │               │                   │               ├─{firefox}(5126)
           │               │                   │               ├─{firefox}(5127)
           │               │                   │               ├─{firefox}(5165)
           │               │                   │               ├─{firefox}(5167)
           │               │                   │               ├─{firefox}(5168)
           │               │                   │               ├─{firefox}(5169)
           │               │                   │               ├─{firefox}(5170)
           │               │                   │               ├─{firefox}(5171)
           │               │                   │               ├─{firefox}(5190)
           │               │                   │               ├─{firefox}(5191)
           │               │                   │               ├─{firefox}(5192)
           │               │                   │               ├─{firefox}(5193)
           │               │                   │               ├─{firefox}(5194)
           │               │                   │               ├─{firefox}(5195)
           │               │                   │               ├─{firefox}(5196)
           │               │                   │               ├─{firefox}(5201)
           │               │                   │               ├─{firefox}(5204)
           │               │                   │               ├─{firefox}(5205)
           │               │                   │               ├─{firefox}(5207)
           │               │                   │               ├─{firefox}(5208)
           │               │                   │               ├─{firefox}(5209)
           │               │                   │               ├─{firefox}(5210)
           │               │                   │               ├─{firefox}(5211)
           │               │                   │               ├─{firefox}(5212)
           │               │                   │               ├─{firefox}(5213)
           │               │                   │               ├─{firefox}(5214)
           │               │                   │               ├─{firefox}(5217)
           │               │                   │               ├─{firefox}(5218)
           │               │                   │               ├─{firefox}(5219)
           │               │                   │               ├─{firefox}(5220)
           │               │                   │               ├─{firefox}(5221)
           │               │                   │               ├─{firefox}(5222)
           │               │                   │               ├─{firefox}(5223)
           │               │                   │               ├─{firefox}(5224)
           │               │                   │               ├─{firefox}(5225)
           │               │                   │               ├─{firefox}(5235)
           │               │                   │               ├─{firefox}(5236)
           │               │                   │               ├─{firefox}(5237)
           │               │                   │               ├─{firefox}(5238)
           │               │                   │               ├─{firefox}(5239)
           │               │                   │               ├─{firefox}(5240)
           │               │                   │               ├─{firefox}(5241)
           │               │                   │               ├─{firefox}(5242)
           │               │                   │               ├─{firefox}(5243)
           │               │                   │               ├─{firefox}(5244)
           │               │                   │               ├─{firefox}(5245)
           │               │                   │               ├─{firefox}(5246)
           │               │                   │               ├─{firefox}(5247)
           │               │                   │               ├─{firefox}(5248)
           │               │                   │               ├─{firefox}(5249)
           │               │                   │               ├─{firefox}(5250)
           │               │                   │               ├─{firefox}(5251)
           │               │                   │               ├─{firefox}(5252)
           │               │                   │               ├─{firefox}(5253)
           │               │                   │               ├─{firefox}(5254)
           │               │                   │               ├─{firefox}(5255)
           │               │                   │               ├─{firefox}(5256)
           │               │                   │               ├─{firefox}(5257)
           │               │                   │               ├─{firefox}(5258)
           │               │                   │               ├─{firefox}(5259)
           │               │                   │               ├─{firefox}(5260)
           │               │                   │               ├─{firefox}(5261)
           │               │                   │               ├─{firefox}(5262)
           │               │                   │               ├─{firefox}(5263)
           │               │                   │               ├─{firefox}(5267)
           │               │                   │               ├─{firefox}(5278)
           │               │                   │               ├─{firefox}(5295)
           │               │                   │               ├─{firefox}(5296)
           │               │                   │               ├─{firefox}(5298)
           │               │                   │               ├─{firefox}(5301)
           │               │                   │               ├─{firefox}(5302)
           │               │                   │               ├─{firefox}(5317)
           │               │                   │               ├─{firefox}(5318)
           │               │                   │               ├─{firefox}(5319)
           │               │                   │               ├─{firefox}(5328)
           │               │                   │               ├─{firefox}(5329)
           │               │                   │               ├─{firefox}(5330)
           │               │                   │               ├─{firefox}(5331)
           │               │                   │               ├─{firefox}(5336)
           │               │                   │               ├─{firefox}(5337)
           │               │                   │               ├─{firefox}(5346)
           │               │                   │               ├─{firefox}(5499)
           │               │                   │               ├─{firefox}(5500)
           │               │                   │               ├─{firefox}(5501)
           │               │                   │               ├─{firefox}(5503)
           │               │                   │               ├─{firefox}(5677)
           │               │                   │               ├─{firefox}(5679)
           │               │                   │               ├─{firefox}(5681)
           │               │                   │               ├─{firefox}(5686)
           │               │                   │               ├─{firefox}(5688)
           │               │                   │               ├─{firefox}(5697)
           │               │                   │               ├─{firefox}(5699)
           │               │                   │               ├─{firefox}(5700)
           │               │                   │               ├─{firefox}(5701)
           │               │                   │               ├─{firefox}(5702)
           │               │                   │               ├─{firefox}(5846)
           │               │                   │               ├─{firefox}(5989)
           │               │                   │               ├─{firefox}(6004)
           │               │                   │               ├─{firefox}(6085)
           │               │                   │               ├─{firefox}(6089)
           │               │                   │               ├─{firefox}(6090)
           │               │                   │               ├─{firefox}(6136)
           │               │                   │               ├─{firefox}(6179)
           │               │                   │               ├─{firefox}(6180)
           │               │                   │               ├─{firefox}(6248)
           │               │                   │               ├─{firefox}(6249)
           │               │                   │               ├─{firefox}(6350)
           │               │                   │               ├─{firefox}(6359)
           │               │                   │               ├─{firefox}(6581)
           │               │                   │               ├─{firefox}(6637)
           │               │                   │               ├─{firefox}(6639)
           │               │                   │               ├─{firefox}(21841)
           │               │                   │               ├─{firefox}(21842)
           │               │                   │               ├─{firefox}(21843)
           │               │                   │               ├─{firefox}(21844)
           │               │                   │               ├─{firefox}(21845)
           │               │                   │               ├─{firefox}(21846)
           │               │                   │               ├─{firefox}(21847)
           │               │                   │               ├─{firefox}(21848)
           │               │                   │               ├─{firefox}(30215)
           │               │                   │               ├─{firefox}(32178)
           │               │                   │               ├─{firefox}(32179)
           │               │                   │               ├─{firefox}(32181)
           │               │                   │               ├─{firefox}(32182)
           │               │                   │               ├─{firefox}(32183)
           │               │                   │               ├─{firefox}(32233)
           │               │                   │               ├─{firefox}(32297)
           │               │                   │               ├─{firefox}(32298)
           │               │                   │               ├─{firefox}(32299)
           │               │                   │               ├─{firefox}(32546)
           │               │                   │               ├─{firefox}(32547)
           │               │                   │               ├─{firefox}(32548)
           │               │                   │               ├─{firefox}(37805)
           │               │                   │               ├─{firefox}(37861)
           │               │                   │               ├─{firefox}(38949)
           │               │                   │               └─{firefox}(43644)
           │               │                   ├─gjs(3167)─┬─{gjs}(3186)
           │               │                   │           ├─{gjs}(3187)
           │               │                   │           ├─{gjs}(3188)
           │               │                   │           ├─{gjs}(3191)
           │               │                   │           ├─{gjs}(3192)
           │               │                   │           ├─{gjs}(3193)
           │               │                   │           ├─{gjs}(3194)
           │               │                   │           ├─{gjs}(3195)
           │               │                   │           ├─{gjs}(3196)
           │               │                   │           ├─{gjs}(3197)
           │               │                   │           ├─{gjs}(3198)
           │               │                   │           ├─{gjs}(3211)
           │               │                   │           ├─{gjs}(3224)
           │               │                   │           └─{gjs}(26769)
           │               │                   ├─mutter-x11-fram(3575)─┬─{mutter-x11-fram}(3578)
           │               │                   │                       ├─{mutter-x11-fram}(3579)
           │               │                   │                       ├─{mutter-x11-fram}(3580)
           │               │                   │                       ├─{mutter-x11-fram}(3581)
           │               │                   │                       ├─{mutter-x11-fram}(3582)
           │               │                   │                       ├─{mutter-x11-fram}(3583)
           │               │                   │                       ├─{mutter-x11-fram}(3584)
           │               │                   │                       ├─{mutter-x11-fram}(3585)
           │               │                   │                       ├─{mutter-x11-fram}(3586)
           │               │                   │                       ├─{mutter-x11-fram}(3587)
           │               │                   │                       ├─{mutter-x11-fram}(3588)
           │               │                   │                       ├─{mutter-x11-fram}(3589)
           │               │                   │                       ├─{mutter-x11-fram}(3590)
           │               │                   │                       ├─{mutter-x11-fram}(3591)
           │               │                   │                       └─{mutter-x11-fram}(3592)
           │               │                   ├─{gnome-shell}(2505)
           │               │                   ├─{gnome-shell}(2506)
           │               │                   ├─{gnome-shell}(2509)
           │               │                   ├─{gnome-shell}(2512)
           │               │                   ├─{gnome-shell}(2513)
           │               │                   ├─{gnome-shell}(2514)
           │               │                   ├─{gnome-shell}(2515)
           │               │                   ├─{gnome-shell}(2516)
           │               │                   ├─{gnome-shell}(2517)
           │               │                   ├─{gnome-shell}(2518)
           │               │                   ├─{gnome-shell}(2519)
           │               │                   ├─{gnome-shell}(2520)
           │               │                   ├─{gnome-shell}(2529)
           │               │                   ├─{gnome-shell}(2537)
           │               │                   ├─{gnome-shell}(2538)
           │               │                   ├─{gnome-shell}(2539)
           │               │                   ├─{gnome-shell}(2540)
           │               │                   ├─{gnome-shell}(2541)
           │               │                   ├─{gnome-shell}(2542)
           │               │                   ├─{gnome-shell}(2543)
           │               │                   ├─{gnome-shell}(2548)
           │               │                   ├─{gnome-shell}(2549)
           │               │                   ├─{gnome-shell}(2550)
           │               │                   ├─{gnome-shell}(2554)
           │               │                   ├─{gnome-shell}(2555)
           │               │                   ├─{gnome-shell}(2556)
           │               │                   ├─{gnome-shell}(2557)
           │               │                   ├─{gnome-shell}(3012)
           │               │                   ├─{gnome-shell}(3030)
           │               │                   ├─{gnome-shell}(3212)
           │               │                   ├─{gnome-shell}(3671)
           │               │                   ├─{gnome-shell}(6771)
           │               │                   ├─{gnome-shell}(6772)
           │               │                   └─{gnome-shell}(44009)
           │               ├─gnome-shell-cal(2638)─┬─{gnome-shell-cal}(2641)
           │               │                       ├─{gnome-shell-cal}(2642)
           │               │                       ├─{gnome-shell-cal}(2644)
           │               │                       ├─{gnome-shell-cal}(2645)
           │               │                       ├─{gnome-shell-cal}(2646)
           │               │                       └─{gnome-shell-cal}(2869)
           │               ├─gnome-terminal(43493)───gnome-terminal.(43496)─┬─{gnome-terminal.}(43497)
           │               │                                                ├─{gnome-terminal.}(43498)
           │               │                                                ├─{gnome-terminal.}(43500)
           │               │                                                └─{gnome-terminal.}(43501)
           │               ├─gnome-terminal-(43502)─┬─bash(43510)───pstree(44010)
           │               │                        ├─{gnome-terminal-}(43503)
           │               │                        ├─{gnome-terminal-}(43504)
           │               │                        ├─{gnome-terminal-}(43506)
           │               │                        ├─{gnome-terminal-}(43507)
           │               │                        ├─{gnome-terminal-}(43509)
           │               │                        └─{gnome-terminal-}(43520)
           │               ├─goa-daemon(2846)─┬─{goa-daemon}(2866)
           │               │                  ├─{goa-daemon}(2870)
           │               │                  ├─{goa-daemon}(2879)
           │               │                  └─{goa-daemon}(2881)
           │               ├─goa-identity-se(2891)─┬─{goa-identity-se}(2902)
           │               │                       ├─{goa-identity-se}(2903)
           │               │                       └─{goa-identity-se}(2914)
           │               ├─gsd-a11y-settin(2678)─┬─{gsd-a11y-settin}(2684)
           │               │                       ├─{gsd-a11y-settin}(2685)
           │               │                       ├─{gsd-a11y-settin}(2687)
           │               │                       └─{gsd-a11y-settin}(2703)
           │               ├─gsd-color(2679)─┬─{gsd-color}(2752)
           │               │                 ├─{gsd-color}(2753)
           │               │                 ├─{gsd-color}(2761)
           │               │                 └─{gsd-color}(2814)
           │               ├─gsd-datetime(2681)─┬─{gsd-datetime}(2719)
           │               │                    ├─{gsd-datetime}(2721)
           │               │                    ├─{gsd-datetime}(2731)
           │               │                    └─{gsd-datetime}(2820)
           │               ├─gsd-housekeepin(2688)─┬─{gsd-housekeepin}(2711)
           │               │                       ├─{gsd-housekeepin}(2712)
           │               │                       ├─{gsd-housekeepin}(2730)
           │               │                       └─{gsd-housekeepin}(2815)
           │               ├─gsd-keyboard(2689)─┬─{gsd-keyboard}(2716)
           │               │                    ├─{gsd-keyboard}(2717)
           │               │                    ├─{gsd-keyboard}(2722)
           │               │                    └─{gsd-keyboard}(2749)
           │               ├─gsd-media-keys(2690)─┬─{gsd-media-keys}(2733)
           │               │                      ├─{gsd-media-keys}(2734)
           │               │                      ├─{gsd-media-keys}(2737)
           │               │                      └─{gsd-media-keys}(2744)
           │               ├─gsd-power(2691)─┬─{gsd-power}(2738)
           │               │                 ├─{gsd-power}(2739)
           │               │                 ├─{gsd-power}(2743)
           │               │                 ├─{gsd-power}(2803)
           │               │                 └─{gsd-power}(3334)
           │               ├─gsd-print-notif(2695)─┬─{gsd-print-notif}(2777)
           │               │                       ├─{gsd-print-notif}(2781)
           │               │                       └─{gsd-print-notif}(2825)
           │               ├─gsd-printer(2963)─┬─{gsd-printer}(2975)
           │               │                   ├─{gsd-printer}(2976)
           │               │                   └─{gsd-printer}(2977)
           │               ├─gsd-rfkill(2697)─┬─{gsd-rfkill}(2723)
           │               │                  ├─{gsd-rfkill}(2724)
           │               │                  └─{gsd-rfkill}(2745)
           │               ├─gsd-screensaver(2699)─┬─{gsd-screensaver}(2729)
           │               │                       ├─{gsd-screensaver}(2732)
           │               │                       └─{gsd-screensaver}(2775)
           │               ├─gsd-sharing(2701)─┬─{gsd-sharing}(2725)
           │               │                   ├─{gsd-sharing}(2726)
           │               │                   ├─{gsd-sharing}(2727)
           │               │                   └─{gsd-sharing}(2754)
           │               ├─gsd-smartcard(2707)─┬─{gsd-smartcard}(2763)
           │               │                     ├─{gsd-smartcard}(2765)
           │               │                     ├─{gsd-smartcard}(2826)
           │               │                     └─{gsd-smartcard}(2884)
           │               ├─gsd-sound(2715)─┬─{gsd-sound}(2747)
           │               │                 ├─{gsd-sound}(2750)
           │               │                 ├─{gsd-sound}(2812)
           │               │                 └─{gsd-sound}(2862)
           │               ├─gsd-wacom(2728)─┬─{gsd-wacom}(2767)
           │               │                 ├─{gsd-wacom}(2768)
           │               │                 ├─{gsd-wacom}(2774)
           │               │                 └─{gsd-wacom}(2813)
           │               ├─gsd-xsettings(3542)─┬─{gsd-xsettings}(3543)
           │               │                     ├─{gsd-xsettings}(3544)
           │               │                     ├─{gsd-xsettings}(3545)
           │               │                     ├─{gsd-xsettings}(3546)
           │               │                     ├─{gsd-xsettings}(3547)
           │               │                     ├─{gsd-xsettings}(3548)
           │               │                     ├─{gsd-xsettings}(3549)
           │               │                     ├─{gsd-xsettings}(3550)
           │               │                     ├─{gsd-xsettings}(3551)
           │               │                     ├─{gsd-xsettings}(3552)
           │               │                     └─{gsd-xsettings}(3554)
           │               ├─gvfs-afc-volume(2933)─┬─{gvfs-afc-volume}(2934)
           │               │                       ├─{gvfs-afc-volume}(2935)
           │               │                       ├─{gvfs-afc-volume}(2936)
           │               │                       └─{gvfs-afc-volume}(2938)
           │               ├─gvfs-goa-volume(2958)─┬─{gvfs-goa-volume}(2964)
           │               │                       ├─{gvfs-goa-volume}(2965)
           │               │                       └─{gvfs-goa-volume}(2966)
           │               ├─gvfs-gphoto2-vo(2946)─┬─{gvfs-gphoto2-vo}(2951)
           │               │                       ├─{gvfs-gphoto2-vo}(2952)
           │               │                       └─{gvfs-gphoto2-vo}(2955)
           │               ├─gvfs-mtp-volume(2974)─┬─{gvfs-mtp-volume}(2985)
           │               │                       ├─{gvfs-mtp-volume}(2986)
           │               │                       └─{gvfs-mtp-volume}(2988)
           │               ├─gvfs-udisks2-vo(2905)─┬─{gvfs-udisks2-vo}(2921)
           │               │                       ├─{gvfs-udisks2-vo}(2922)
           │               │                       ├─{gvfs-udisks2-vo}(2924)
           │               │                       └─{gvfs-udisks2-vo}(2931)
           │               ├─gvfsd(2437)─┬─gvfsd-http(30015)─┬─{gvfsd-http}(30016)
           │               │             │                   ├─{gvfsd-http}(30017)
           │               │             │                   └─{gvfsd-http}(30018)
           │               │             ├─gvfsd-recent(6455)─┬─{gvfsd-recent}(6456)
           │               │             │                    ├─{gvfsd-recent}(6457)
           │               │             │                    └─{gvfsd-recent}(6459)
           │               │             ├─gvfsd-trash(3053)─┬─{gvfsd-trash}(3054)
           │               │             │                   ├─{gvfsd-trash}(3055)
           │               │             │                   ├─{gvfsd-trash}(3056)
           │               │             │                   └─{gvfsd-trash}(3059)
           │               │             ├─{gvfsd}(2439)
           │               │             ├─{gvfsd}(2440)
           │               │             └─{gvfsd}(2442)
           │               ├─gvfsd-fuse(2447)─┬─{gvfsd-fuse}(2451)
           │               │                  ├─{gvfsd-fuse}(2452)
           │               │                  ├─{gvfsd-fuse}(2453)
           │               │                  ├─{gvfsd-fuse}(2454)
           │               │                  ├─{gvfsd-fuse}(2455)
           │               │                  └─{gvfsd-fuse}(2456)
           │               ├─gvfsd-metadata(3216)─┬─{gvfsd-metadata}(3217)
           │               │                      ├─{gvfsd-metadata}(3218)
           │               │                      └─{gvfsd-metadata}(3219)
           │               ├─ibus-daemon(2670)─┬─ibus-engine-sim(3016)─┬─{ibus-engine-sim}(3018)
           │               │                   │                       ├─{ibus-engine-sim}(3019)
           │               │                   │                       └─{ibus-engine-sim}(3021)
           │               │                   ├─ibus-extension-(2873)─┬─{ibus-extension-}(2906)
           │               │                   │                       ├─{ibus-extension-}(2907)
           │               │                   │                       ├─{ibus-extension-}(2916)
           │               │                   │                       └─{ibus-extension-}(2918)
           │               │                   ├─ibus-memconf(2872)─┬─{ibus-memconf}(2877)
           │               │                   │                    ├─{ibus-memconf}(2878)
           │               │                   │                    └─{ibus-memconf}(2880)
           │               │                   ├─{ibus-daemon}(2822)
           │               │                   ├─{ibus-daemon}(2823)
           │               │                   └─{ibus-daemon}(2852)
           │               ├─ibus-portal(2876)─┬─{ibus-portal}(2882)
           │               │                   ├─{ibus-portal}(2885)
           │               │                   └─{ibus-portal}(2901)
           │               ├─ibus-x11(3569)─┬─{ibus-x11}(3571)
           │               │                ├─{ibus-x11}(3572)
           │               │                └─{ibus-x11}(3574)
           │               ├─pipewire(2235)─┬─{pipewire}(2264)
           │               │                └─{pipewire}(2269)
           │               ├─pipewire(2236)─┬─{pipewire}(2262)
           │               │                └─{pipewire}(2266)
           │               ├─pipewire-pulse(2241)─┬─{pipewire-pulse}(2263)
           │               │                      └─{pipewire-pulse}(2273)
           │               ├─snap(4163)─┬─{snap}(4172)
           │               │            ├─{snap}(4173)
           │               │            ├─{snap}(4174)
           │               │            ├─{snap}(4175)
           │               │            ├─{snap}(4176)
           │               │            ├─{snap}(4177)
           │               │            ├─{snap}(4178)
           │               │            ├─{snap}(4179)
           │               │            ├─{snap}(4180)
           │               │            └─{snap}(5002)
           │               ├─snapd-desktop-i(2238)───snapd-desktop-i(2639)─┬─{snapd-desktop-i}(2969)
           │               │                                               ├─{snapd-desktop-i}(2970)
           │               │                                               ├─{snapd-desktop-i}(2971)
           │               │                                               └─{snapd-desktop-i}(2973)
           │               ├─tracker-miner-f(3091)─┬─{tracker-miner-f}(3094)
           │               │                       ├─{tracker-miner-f}(3095)
           │               │                       ├─{tracker-miner-f}(3096)
           │               │                       ├─{tracker-miner-f}(3099)
           │               │                       ├─{tracker-miner-f}(3100)
           │               │                       ├─{tracker-miner-f}(3110)
           │               │                       └─{tracker-miner-f}(3111)
           │               ├─wireplumber(2239)─┬─{wireplumber}(2261)
           │               │                   ├─{wireplumber}(2265)
           │               │                   ├─{wireplumber}(2267)
           │               │                   ├─{wireplumber}(2272)
           │               │                   └─{wireplumber}(2275)
           │               ├─xdg-desktop-por(3108)─┬─{xdg-desktop-por}(3113)
           │               │                       ├─{xdg-desktop-por}(3115)
           │               │                       ├─{xdg-desktop-por}(3116)
           │               │                       ├─{xdg-desktop-por}(3132)
           │               │                       ├─{xdg-desktop-por}(3144)
           │               │                       └─{xdg-desktop-por}(3145)
           │               ├─xdg-desktop-por(3120)─┬─{xdg-desktop-por}(3121)
           │               │                       ├─{xdg-desktop-por}(3122)
           │               │                       ├─{xdg-desktop-por}(3123)
           │               │                       ├─{xdg-desktop-por}(3124)
           │               │                       └─{xdg-desktop-por}(3127)
           │               ├─xdg-desktop-por(3133)─┬─{xdg-desktop-por}(3138)
           │               │                       ├─{xdg-desktop-por}(3139)
           │               │                       ├─{xdg-desktop-por}(3141)
           │               │                       └─{xdg-desktop-por}(3142)
           │               ├─xdg-document-po(2302)─┬─fusermount3(2313)
           │               │                       ├─{xdg-document-po}(2303)
           │               │                       ├─{xdg-document-po}(2304)
           │               │                       ├─{xdg-document-po}(2305)
           │               │                       ├─{xdg-document-po}(2312)
           │               │                       ├─{xdg-document-po}(2314)
           │               │                       └─{xdg-document-po}(2315)
           │               └─xdg-permission-(2306)─┬─{xdg-permission-}(2307)
           │                                       ├─{xdg-permission-}(2308)
           │                                       └─{xdg-permission-}(2310)
           ├─systemd-journal(390)
           ├─systemd-logind(927)
           ├─systemd-oomd(846)
           ├─systemd-resolve(849)
           ├─systemd-timesyn(850)───{systemd-timesyn}(857)
           ├─systemd-udevd(423)
           ├─udisksd(941)─┬─{udisksd}(974)
           │              ├─{udisksd}(976)
           │              ├─{udisksd}(993)
           │              ├─{udisksd}(1079)
           │              └─{udisksd}(1098)
           ├─unattended-upgr(1449)───{unattended-upgr}(1465)
           ├─upowerd(1867)─┬─{upowerd}(1992)
           │               ├─{upowerd}(1993)
           │               └─{upowerd}(1994)
           └─wpa_supplicant(987)

```

### Latihan Praktikum 6.1
#### Soal
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?

#### Jawaban
1. Total proses yang berjala adalah 414. Jumlah tersebut didapatkan dari prompt dibawah ini
```
ps aux | wc -l
```
Dari prompt tersebut, didapatkan output 415, kemudian kurangi satu untuk mengecualikan header sehingga hasilnya adalah 414.
Sedangkan PID terkecil adalah 1, prosesnya adalah /sbin/init splash

2. Proses bash (PID) 43510 dan induk Proses (PPID) 43502 dengan struktur proses (dipersingkat) seperti berikut
```
gnome-terminal-server (43502)
        └── bash (43510)
```

3. Perbandingan output dari
```
ps aux & ps aux -L
```
adalah pada header terdapat perbedaan sebagai berikut
ps aux
```
USER PID %CPU %MEM VSZ RSS TTY STAT START
```
ps aux -L
```
USER PID LWP %CPU NLWP %MEM VSZ RSS TTY
```
Selain menampilkan proses utana, ps aux -L juga menampilkan LWP (Light weight process)

### Praktikum 6.2 — Mengamati Siklus Hidup Proses

#### Prompt
```
sleep 60 &
ps aux | grep sleep
```

#### Hasil
```
[1] 9663
root        1919  0.0  0.0   3220  1960 ?        S    20:51   0:00 sleep 3600
fafiq       9663  0.0  0.0  16964  2272 pts/1    S    21:30   0:00 sleep 60
fafiq       9665  0.0  0.0  17820  2496 pts/1    S+   21:30   0:00 grep --color=auto sleep

```

#### Prompt
```
ls /tmp
echo " Sukses : $?"
ls /direktori - tidak - ada
echo " Gagal : $?"
```

#### Hasil
```
snap-private-tmp                                                                       systemd-private-0c6458ac21a946b99aeceadb3de8d495-switcheroo-control.service-HUKXA8
systemd-private-0c6458ac21a946b99aeceadb3de8d495-bluetooth.service-R7WfKc              systemd-private-0c6458ac21a946b99aeceadb3de8d495-systemd-logind.service-aKdzxv
systemd-private-0c6458ac21a946b99aeceadb3de8d495-colord.service-rPQxQE                 systemd-private-0c6458ac21a946b99aeceadb3de8d495-systemd-oomd.service-m6WuXI
systemd-private-0c6458ac21a946b99aeceadb3de8d495-fwupd.service-3ruhP4                  systemd-private-0c6458ac21a946b99aeceadb3de8d495-systemd-resolved.service-jAjhYg
systemd-private-0c6458ac21a946b99aeceadb3de8d495-ModemManager.service-MbFxht           systemd-private-0c6458ac21a946b99aeceadb3de8d495-systemd-timesyncd.service-JiWRbU
systemd-private-0c6458ac21a946b99aeceadb3de8d495-polkit.service-jwhDpc                 systemd-private-0c6458ac21a946b99aeceadb3de8d495-upower.service-G2hTtF
systemd-private-0c6458ac21a946b99aeceadb3de8d495-power-profiles-daemon.service-Vv1O9P
 Sukses : 0
ls: cannot access '/direktori': No such file or directory
ls: cannot access '-': No such file or directory
ls: cannot access 'tidak': No such file or directory
ls: cannot access '-': No such file or directory
ls: cannot access 'ada': No such file or directory
```

### Latihan Praktikum 6.2
#### Soal
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit code masing-masing. Pola apa yang Anda temukan?

#### Jawaban
1. Kondisi STAT pada sleep 120 & adalah S yang artinya sleeping atau menunggu sampai selama waktu tertentu (120 detik)
```
fafiq      10982  0.0  0.0  16964  2276 pts/1    S    21:48   0:00 sleep 200
```
2. Untuk exit code program yang berhasil bernilai 0 dan yang salah bernilai selain 0

### Praktikum 6.3 — Mengatur Prioritas Proses

#### Prompt
```
nice -n 10 sleep 300 &
```

#### Hasil
```
[1] 11804
```

#### Prompt
```
ps aux | grep sleep
```

#### Hasil
```
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      11767  0.0  0.0  16964  2276 ?        SN   21:56   0:00 sleep 300
fafiq      11804  0.0  0.0  16964  2276 pts/2    SN   21:56   0:00 sleep 300
fafiq      11927  0.0  0.0  16964  2276 pts/2    SN   22:00   0:00 sleep 300
fafiq      11933  0.0  0.0  17820  2496 pts/2    S+   22:00   0:00 grep --color=auto sleep
```

#### Prompt
```
renice -n 15 -p 11927
ps -p 11927 -o pid,ni,cmd
```
#### Hasil
```
[1]-  Done                    nice -n 10 sleep 300
    PID  NI CMD
  11927  15 sleep 300
```

### Latihan Praktikum 6.3
#### Soal
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps.
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa Linux membatasi hal ini untuk user biasa?

#### Jawaban
1. Berdasarkan hasil percobaan, didapatkan hasil sebagai berikut
```
fafiq@fafiq-ubuntu:~$ nice -n 5 sleep 300 &
[3] 12980
fafiq@fafiq-ubuntu:~$ ps aux | grep sleep
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      12878  0.0  0.0  16964  2276 pts/2    SN   22:14   0:00 sleep 300
fafiq      12924  0.0  0.0  16964  2276 pts/2    SN   22:15   0:00 sleep 300
fafiq      12980  0.0  0.0  16964  2276 pts/2    SN   22:17   0:00 sleep 300
fafiq      12982  0.0  0.0  17820  2496 pts/2    S+   22:17   0:00 grep --color=auto sleep
fafiq@fafiq-ubuntu:~$ ps -p 12980 -o pid,ni,cmd
renice -n 10 -p 12980
ps -p 12980 -o pid,ni,cmd
    PID  NI CMD
  12980   5 sleep 300
```
didapatkan hasil NI nya adalah 5

2. Berdasarkan hasil percobaan, didapatka hasil sebagai berikut
```
12980 (process ID) old priority 5, new priority 10
    PID  NI CMD
  12980  10 sleep 300
```

3. Ketika mengubah nilai nice menjadi negatif, akan muncul error permission denied karena butuh otoritas yang lebih tinggi (sudo)

### Praktikum 6.4 — Mengirim Sinyal ke Proses
#### Prompt
```
sleep 500 &
sleep 600 &
sleep 700 &
ps aux | grep -v grep | grep sleep
```

#### Hasil
```
[1] 13322
[2] 13323
[3] 13324
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      13322  0.0  0.0  16964  2272 pts/2    S    22:23   0:00 sleep 500
fafiq      13323  0.0  0.0  16964  2276 pts/2    S    22:23   0:00 sleep 600
fafiq      13324  0.0  0.0  16964  2268 pts/2    S    22:23   0:00 sleep 700
```

#### Prompt
```
kill 13322          
ps aux | grep -v grep | grep sleep
```

#### Hasil
```
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      13323  0.0  0.0  16964  2276 pts/2    S    22:23   0:00 sleep 600
fafiq      13324  0.0  0.0  16964  2268 pts/2    S    22:23   0:00 sleep 700
```

#### Prompt
```
kill -SIGSTOP 13323          
ps aux | grep sleep
```

#### Hasil
```
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      13323  0.0  0.0  16964  2276 pts/2    T    22:23   0:00 sleep 600
fafiq      13324  0.0  0.0  16964  2268 pts/2    S    22:23   0:00 sleep 700
fafiq      13349  0.0  0.0  17820  2492 pts/2    S+   22:24   0:00 grep --color=auto sleep
```

#### Prompt
```
kill -SIGCONT 13323          
ps aux | grep sleep
```

#### Hasil
```
root       11320  0.0  0.0   3220  2000 ?        S    21:51   0:00 sleep 3600
fafiq      13323  0.0  0.0  16964  2276 pts/2    S    22:23   0:00 sleep 600
fafiq      13324  0.0  0.0  16964  2268 pts/2    S    22:23   0:00 sleep 700
fafiq      13356  0.0  0.0  17820  2492 pts/2    S+   22:24   0:00 grep --color=auto sleep
```

#### Prompt
```
pkill sleep
```

#### Hasil
```
pkill: killing pid 11320 failed: Operation not permitted
[2]-  Terminated              sleep 600
[3]+  Terminated              sleep 700
```
### Latihan Praktikum 6.4
#### Soal
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?

#### Jawaban
1. Kodisi yang muncul adalah STAT berubah menjadi T karena sedang dijeda
2. Kondisi yang muncul adalah STAT berubah menjadi S karena perintah sleep dijalankan kembali setelah dijeda pada sinyal SIGSTOP
3. Gunakan SIGKILL jika proses tidak merespon SIGTERM atau proses sedang hang/freeze dan tidak bisa dihentikan dengan cara biasa

### Praktikum 6.5 — Manajemen Job Foreground dan Background
#### Prompt
```
sleep 200 &
sleep 300 &
sleep 400 &
jobs
```

#### Hasil
```
sleep 300 &
sleep 400 &
jobs
[1] 8305
[2] 8306
[3] 8307
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```

#### Prompt
```
fg %1
# Tekan Ctrl +Z untuk menjeda
bg %1
jobs
```

#### Hasil
```
sleep 200
^Z
[1]+  Stopped                 sleep 200
jobs
[1]+ sleep 200 &
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```

#### Prompt
```
kill %1 %2 %3
jobs

```

#### Hasil
```
jobs
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```

### Latihan Praktikum 6.5
#### Soal
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q

#### Jawaban
1. Yang terjadi adalah terminal terkunci oleh top dimana user tidak bisa mengetik command lain sebelum top dihentikan karena top berjalan di foreground
2. Status yang muncul adalah stopped karena ctrl+z mengirim sinyal SIGSTOP
3. top tidak berjaland engan baik di background arena top butuh interactive ui di terminal dan karena top berjalan di backgound maka tidak punya kontrol atas layar
4. Untuk mengembalikan ke foreground begini commandnya
```
fg %1  #lalu tekan q
```

### Praktikum 6.6 — Pemantauan Proses
#### Prompt
```
ps aux -- sort = -% cpu | head -10
ps aux -- sort = -% mem | head -10
```

#### Hasil
```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
fafiq       4315  7.6  6.1 12635904 958592 ?     Sl   13:59   3:19 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       7550  5.7  2.1 1465102452 342384 ?   Sl   14:13   1:40 /usr/share/code/code --type=zygote
fafiq       3340  4.7  2.6 5607432 406856 ?      Ssl  13:58   2:04 /usr/bin/gnome-shell
fafiq       6694  2.4  3.0 3292696 479604 ?      Sl   14:05   0:54 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44518 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {79eb99a6-8a61-492c-9639-03f30d60a670} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 20 tab
fafiq       7482  1.5  1.5 51387312 241204 ?     Sl   14:13   0:28 /usr/share/code/code --type=zygote --no-zygote-sandbox
fafiq       7662  1.1  1.7 1461342684 271712 ?   Sl   14:13   0:19 /proc/self/exe --type=utility --utility-sub-type=node.mojom.NodeService --lang=en-US --service-sandbox-type=none --render-node-override=/dev/dri/renderD128 --dns-result-order=ipv4first --experimental-network-inspection --inspect-port=0 --js-flags=--nodecommit_pooled_pages --crashpad-handler-pid=7459 --enable-crash-reporter=9f087d08-a067-4f53-bfef-10d3b83556b8,no_channel --user-data-dir=/home/fafiq/.config/Code --standard-schemes=vscode-webview,vscode-file --enable-sandbox --secure-schemes=vscode-webview,vscode-file --cors-schemes=vscode-webview,vscode-file --fetch-schemes=vscode-webview,vscode-file --service-worker-schemes=vscode-webview --code-cache-schemes=vscode-webview,vscode-file --shared-files=v8_context_snapshot_data:100 --field-trial-handle=3,i,8274984242347241118,10996704503328616168,262144 --enable-features=DocumentPolicyIncludeJSCallStacksInCrashReports,EarlyEstablishGpuChannel,EstablishGpuChannelAsync --disable-features=CalculateNativeWinOcclusion,LocalNetworkAccessChecks,ScreenAIOCREnabled,SpareRendererForSitePerProcess,TraceSiteInstanceGetProcessCreation --variations-seed-version --trace-process-track-uuid=3190708990997080739
fafiq       7429  0.8  1.6 1478504836 251364 ?   SLl  14:13   0:14 /usr/share/code/code
fafiq       5355  0.5  2.0 2883356 325924 ?      Sl   13:59   0:15 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43070 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {50852c97-263a-47e6-b1e1-1a350b8b2930} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 7 tab
root         761  0.5  0.0      0     0 ?        S    13:57   0:13 [irq/105-rtw89_pci]
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
fafiq       4315  7.6  6.1 12635904 958592 ?     Sl   13:59   3:19 /snap/firefox/8107/usr/lib/firefox/firefox
fafiq       6694  2.4  3.0 3292696 479604 ?      Sl   14:05   0:54 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44518 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {79eb99a6-8a61-492c-9639-03f30d60a670} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 20 tab
fafiq       3340  4.7  2.6 5607432 406856 ?      Ssl  13:58   2:04 /usr/bin/gnome-shell
fafiq       7550  5.7  2.1 1465102452 342384 ?   Sl   14:13   1:40 /usr/share/code/code --type=zygote
fafiq       5355  0.5  2.0 2883356 325924 ?      Sl   13:59   0:15 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43070 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {50852c97-263a-47e6-b1e1-1a350b8b2930} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 7 tab
fafiq       5369  0.2  1.7 2851608 274164 ?      Sl   13:59   0:07 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43070 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {73f4e855-1a3e-4139-8f79-cd0ce79cc3f5} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 9 tab
fafiq       7662  1.1  1.7 1461342684 271712 ?   Sl   14:13   0:19 /proc/self/exe --type=utility --utility-sub-type=node.mojom.NodeService --lang=en-US --service-sandbox-type=none --render-node-override=/dev/dri/renderD128 --dns-result-order=ipv4first --experimental-network-inspection --inspect-port=0 --js-flags=--nodecommit_pooled_pages --crashpad-handler-pid=7459 --enable-crash-reporter=9f087d08-a067-4f53-bfef-10d3b83556b8,no_channel --user-data-dir=/home/fafiq/.config/Code --standard-schemes=vscode-webview,vscode-file --enable-sandbox --secure-schemes=vscode-webview,vscode-file --cors-schemes=vscode-webview,vscode-file --fetch-schemes=vscode-webview,vscode-file --service-worker-schemes=vscode-webview --code-cache-schemes=vscode-webview,vscode-file --shared-files=v8_context_snapshot_data:100 --field-trial-handle=3,i,8274984242347241118,10996704503328616168,262144 --enable-features=DocumentPolicyIncludeJSCallStacksInCrashReports,EarlyEstablishGpuChannel,EstablishGpuChannelAsync --disable-features=CalculateNativeWinOcclusion,LocalNetworkAccessChecks,ScreenAIOCREnabled,SpareRendererForSitePerProcess,TraceSiteInstanceGetProcessCreation --variations-seed-version --trace-process-track-uuid=3190708990997080739
fafiq       6242  0.2  1.7 2791856 268900 ?      Sl   14:04   0:06 /snap/firefox/8107/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44518 -prefMapHandle 1:283466 -jsInitHandle 2:156136 -parentBuildID 20260404010525 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {0a42edd0-b348-4479-8274-17c114d9b710} -parentPid 4315 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8107/usr/lib/firefox/omni.ja -appomni /snap/firefox/8107/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8107/usr/lib/firefox/browser 13 tab
fafiq       7429  0.8  1.6 1478504836 251364 ?   SLl  14:13   0:14 /usr/share/code/code

```

#### Prompt
```
top
```

#### Prompt
```
sudo apt install -y htop
htop
```

### Latihan Praktikum 6.6
#### Soal
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa informasi ini berguna?
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah. Tekan F9 dan amati opsi sinyal yang tersedia.

#### Jawaban
1. Berdasarkan perintah ps aux --sort=-%mem, proses yang menggunakan memori paling banyak adalah proses yang berada di urutan paling atas setelah header, yaitu proses dengan nilai penggunaan memori terbesar pada saat pengamatan dilakukan di sistem.
2. Ketika menekan tombol 1 di dalam top, tampilan berubah dengan menampilkan penggunaan CPU secara terpisah untuk setiap core prosesor, sehingga memudahkan pengguna dalam melihat distribusi beban kerja pada masing-masing core CPU.
3. Di dalam htop, saat menekan tombol F9 pada proses seperti sshd, akan muncul berbagai pilihan sinyal seperti SIGTERM, SIGKILL, dan SIGSTOP yang dapat digunakan untuk mengontrol proses tersebut, misalnya untuk menghentikan, mematikan secara paksa, atau menjeda proses.


## Latihan
### Latihan 6A
#### Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian besar proses di sistem berada dalam kondisi ini?

#### Jawaban
1. Berdasarkan hasil perintah ps aux --forest, proses dengan PID 1 adalah systemd, yang berfungsi sebagai proses inisialisasi utama pada sistem Linux modern untuk mengelola dan menjalankan layanan serta proses lain sejak sistem pertama kali booting.
2. Jumlah proses yang dimiliki oleh user root lebih banyak dibandingkan dengan user biasa karena root bertanggung jawab menjalankan berbagai layanan dan proses sistem yang penting, seperti daemon dan service yang berjalan di latar belakang.
3. Sebagian besar proses berada dalam kondisi S (sleeping) karena proses-proses tersebut sedang menunggu suatu event atau input, seperti operasi I/O atau interaksi pengguna, sehingga tidak selalu aktif menggunakan CPU.

### Latihan 6B
#### Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job. Berapa job yang tersisa?

#### Jawaban
1. Setelah menjalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background, ketiga job tersebut berhasil berjalan secara bersamaan dan dapat diverifikasi menggunakan perintah jobs, yang menampilkan daftar job aktif beserta nomor dan statusnya.
2. Ketika job kedua dibawa ke foreground menggunakan fg %2, kemudian dijeda dengan menekan Ctrl+Z, statusnya berubah menjadi stopped, dan setelah dijalankan kembali dengan perintah bg %2, job tersebut kembali berjalan di background.
3. Setelah menghentikan job pertama menggunakan perintah kill %1, dan menampilkan kembali daftar job dengan jobs, terlihat bahwa jumlah job yang tersisa adalah dua, karena satu job telah dihentikan.

### Latihan 6C
#### Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice +15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10. Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

#### Jawaban
1. Setelah menjalankan dua proses sleep dengan nilai nice +5 dan +15, dapat diverifikasi melalui perintah ps bahwa proses dengan nilai nice +5 memiliki prioritas lebih tinggi dibandingkan dengan proses yang memiliki nilai nice +15.
2. Setelah mengubah nilai nice proses pertama menjadi +10 menggunakan renice, maka proses dengan nilai nice +10 memiliki prioritas lebih tinggi dibandingkan proses dengan nilai nice +15, karena semakin kecil nilai nice maka semakin tinggi prioritasnya.
3. Ketika sinyal SIGSTOP dikirim ke salah satu proses, status proses berubah menjadi T (stopped), kemudian setelah dikirim SIGCONT proses kembali berjalan normal, dan seluruh proses percobaan dapat diakhiri menggunakan perintah pkill sleep.