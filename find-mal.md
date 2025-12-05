# Find Command – Malware Hunting & Emergency Cleanup

1. **Cari file sus (disguised webshell)**  
   **`find / \( -name "*.ico" -o -name "*.php.jpg" -o -name "*.phtml" -o -name ".env" \) -exec ls -la {} \; 2>/dev/null`**  
   → .ico shell, PHP jadi gambar, .env terdedah

2. **PHP file besar gila (>500KB = 99% backdoor)**  
   **`find /var/www -name "*.php" -size +500k -exec ls -lh {} \; | head -20`**

3. **Cari webshell signature klasik**  
   **`find . -type f -name "*.php" -exec grep -l "eval\|base64_decode\|gzinflate\|str_rot13\|shell_exec\|passthru" {} \;`**

4. **Auto bersihkan tmp (letak dalam cron harian)**  
   **`find /tmp /var/tmp /dev/shm -name "sess_*" -o -name ".*" -mtime +7 -delete 2>/dev/null`**

5. **Auto betulkan permission 777 (client suka buat ni)**  
   **`find /var/www -type f -perm 0777 -exec chmod 644 {} \; -o -type d -perm 0777 -exec chmod 755 {} \;`**

6. **Cari script executable luar /usr (malware cron)**  
   **`find / -type f \( -name "*.sh" -o -name "*.pl" -o -name "*.py" \) -perm /0111 ! -path "/usr/*" -exec ls -la {} \; 2>/dev/null`**

7. **Kosongkan log >1GB (disk full killer)**  
   **`find /var/log -type f -size +1G -exec truncate -s 0 {} \;`**

8. **Cari file SUID/SGID (bahaya kalau tak patut)**  
   **`find / -type f -perm -4000 -o -perm -2000 -exec ls -la {} \; 2>/dev/null`**

9. **Check 5 baris pertama index.php / wp-login.php**  (WordPress)
   **`find / \( -name "index.php" -o -name "wp-login.php" \) -exec head -n 5 {} \; | grep -i "eval\|<?php.*@.*eval"`**

10. **Nuke semua PHP ada function bahaya (LAST RESORT)**  
    **`find /var/www -type f -name "*.php" -exec grep -l "eval\|system\|exec\|passthru\|shell_exec\|popen" {} \; | xargs rm -f`**  
    → **BACKUP DULU! Jangan main hentam je**

Bonus 11. **Cari hidden .git terdedah**  
    **`find /var/www -type d -name ".git" -exec chmod 000 {} \; -prune`**
