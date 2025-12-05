### Tengok OS & kernel
**`cat /etc/os-release`**      → nama distro + versi (semua distro ada)  
**`uname -a`**                 → kernel + architecture + hostname  
**`hostnamectl`**              → info lengkap (systemd server)  
**`lsb_release -a`**           → Ubuntu/Debian je, kalau takde install dulu

### CPU info
**`lscpu | grep -E "Model name|Core|Thread"`** → model + core + thread sekilas  
**`nproc`**                    → berapa core boleh guna (make -j, rsync -j, dll)  
**`cat /proc/cpuinfo | grep "cpu cores" | uniq`** → real core (bukan HT)

### RAM usage
**`free -h`**                  → total/used/available, human readable  
**`cat /proc/meminfo | grep -i memtotal`** → kalau nak exact number

### Disk apa ada
**`lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,MODEL`** → paling cantik  
**`lsblk -d -o NAME,SIZE,MODEL,ROTA`** → ROTA 1=HDD, 0=SSD  
**`df -hT`**                   → usage + filesystem type
