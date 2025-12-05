# 01 – System Info & Hardware

### Info OS & Kernel
| Command                  | Description                                    | Catatan                    |
|--------------------------|------------------------------------------------|----------------------------|
| **`cat /etc/os-release`**    | Papar nama + versi distro                      | Semua distro               |
| **`lsb_release -a`**         | Detail Ubuntu/Debian                           | Install kalau takde        |
| **`uname -a`**               | Kernel + architecture + hostname               | Paling ringkas             |
| **`hostnamectl`**            | Info lengkap (systemd)                         | CentOS/Ubuntu 16.04+       |

### CPU
| Command                  | Description                                    |
|--------------------------|------------------------------------------------|
| **`lscpu ‑‑extended`**      | Model, core, thread, cache                     |
| **`nproc`**                  | Jumlah core (untuk make -j, parallel rsync)    |
| **`cat /proc/cpuinfo ‑‑count`** | Berapa core real + hyper-threading         |

### Memory
| Command                  | Description                                    |
|--------------------------|------------------------------------------------|
| **`free -h`**                | Total, used, available (human readable)       |
| **`vmstat -s`**              | Detail swap usage                              |
| **`cat /proc/meminfo`**      | Kalau nak detail gila                          |

### Disk & Storage
| Command                  | Description                                    |
|--------------------------|------------------------------------------------|
| **`lsblk -d -o NAME,SIZE,MODEL,ROTA`** | Senarai disk (ROTA=1=HDD, 0=SSD)        |
| **`df -hT`**                 | Disk usage + filesystem type                   |
| **`smartctl -i /dev/sda`**   | Check SMART support                            |
