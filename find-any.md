### Find command power (sysadmin wajib hafal)

**`find /path -type f -o -type d | grep -i "ips"`**  
→ Cari file **atau** folder yang ada keyword “ips” (case-insensitive)

**`find . -type f -name "*.php" -size 0 -delete`**  
→ Padam semua file PHP kosong (0 byte) — bersihkan server terkontang-katang

**`find . -name ".htaccess" -exec grep -l "about\|radio\|index\|content" {} \;`**  
→ Cari semua .htaccess yang ada rule blok/tuju ke about.php / radio.php / index.php / content.php (berguna masa audit security)

**`find /var/www -type f -name "*.log" -size +500M -exec ls -lh {} \;`**  
→ Cari log file >500MB (biasanya penyebab disk penuh)

**`find / -type f -perm -4000 -o -perm -2000 -exec ls -la {} \; 2>/dev/null`**  
→ Cari file SUID/SGID (berbahaya kalau ada yang tak patut)

**`find . -type f -mtime -7 -ls`**  
→ Senarai file yang diubah dalam 7 hari terakhir (berguna masa forensik)

**`find /tmp -name "sess_*" -type f -mtime +1 -delete`**  
→ Auto bersihkan session PHP lama dalam /tmp (cron job sedap)

**`find . -type f -name "*.bak" -o -name "*~" -delete`**  
→ Padam semua backup file (~) dan .bak secara beramai-ramai
