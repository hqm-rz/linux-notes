# Find Command Power – Sysadmin Daily Driver (2025)

1. **Cari file atau folder ada keyword (case-insensitive)**  
   **`find /path -type f -o -type d | grep -i "ips"`**

2. **Padam semua file PHP kosong (0 byte)**  
   **`find . -type f -name "*.php" -size 0 -delete`**  
   → bersihkan server terkontang-katang

3. **Cari .htaccess yang block/redirect ke file tertentu**  
   **`find . -name ".htaccess" -exec grep -l "about\|radio\|index\|content" {} \;`**  
   → berguna masa audit security / cari redirect jahat

4. **Cari log file >500MB (penyebab disk penuh)**  
   **`find /var/www -type f -name "*.log" -size +500M -exec ls -lh {} \;`**

5. **Cari file SUID/SGID (bahaya kalau tak patut)**  
   **`find / -type f -perm -4000 -o -perm -2000 -exec ls -la {} \; 2>/dev/null`**

6. **Senarai file yang diubah dalam 7 hari terakhir (forensik)**  
   **`find . -type f -mtime -7 -ls`**

7. **Auto bersihkan session PHP lama dalam /tmp (letak cron)**  
   **`find /tmp -name "sess_*" -type f -mtime +1 -delete`**

8. **Padam semua backup file (~ dan .bak)**  
   **`find . -type f -name "*.bak" -o -name "*~" -delete`**

9. **Bonus: Cari hidden folder/file (malware suka sorok)**  
   **`find /var/www -type d -name ".*" -ls 2>/dev/null`**

10. **Bonus: Cari file besar >1GB seluruh server**  
    **`find / -type f -size +1G -exec ls -lh {} \; 2>/dev/null | head -20`**
