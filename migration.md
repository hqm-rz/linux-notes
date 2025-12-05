# Migration cPanel → cPanel (Rsync Method - Zero Downtime)

### Screen (WAJIB GUNA BIAR TAK PUTUS)
**`screen`**                               → masuk screen baru  
**Ctrl + A → D**                           → keluar tanpa mati proses  
**`screen -ls`**                           → tengok senarai screen running  
**`screen -r 258988.pts-0.svr3`**          → masuk balik screen yang kau nak  

### 1. Backup akaun (jalankan di server asal)
**`/scripts/pkgacct --skiphomedir seesmmy1`**

### 2. Copy file backup ke server baru (jalankan di server asal)
**`scp -P 9193 /home/cpmove-seesmmy1.tar.gz root@103.8.24.81:/home/`**

### 3. Restore backup (jalankan di server baru – pastikan dah cd /home)
**`cd /home`**  
**`/scripts/restorepkg cpmove-seesmmy1.tar.gz`**

### 4. Re-sync homedir (jalankan di server baru – tarik data terkini)
**`screen`**                               → kalau data besar  
**`rsync -av --progress --inplace --update --rsh='ssh -p9193' 103.8.25.46:/home/seesmmy1/ /home/seesmmy1/`**

### 5. Final Checklist (JANGAN LUPA!)
- Update/check A record & DB  
- Backup user selection → enable  
- Check package (disk, bandwidth, addon domain)  
- Update nameserver (ns1/ns2)  
- Update billing details / hantar login baru ke client  
- **Double check hosts.allow** (kalau ubah IP server)
