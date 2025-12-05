### Find Command Gila-Gila (Malware Hunting & Emergency Cleanup)

**Cari file sus (webshell disguised)**  
**`find / \( -name "*.ico" -o -name "*.php.jpg" -o -name "*.phtml" -o -name ".env" \) -exec ls -la {} \; 2>/dev/null`**  
→ PHP jadi gambar, .ico shell, .env terdedah

**PHP file besar gila (>500KB = 99% backdoor)**  
**`find /var/www -name "*.php" -size +500k -exec ls -lh {} \; | head -20`**

**Cari webshell signature klasik**  
**`find . -type f -name "*.php" -exec grep -l "eval\|base64_decode\|gzinflate\|str_rot13\|shell_exec\|passthru" {} \;`**

**Bersihkan tmp setiap hari (cron)**  
**`find /tmp /var/tmp /dev/shm -name "sess_*" -o -name ".*" -mtime +7 -delete 2>/dev/null`**

**Auto betulkan permission 777**  
**`find /var/www -type f -perm 0777 -exec chmod 644 {} \; -o -type d -perm 0777 -exec chmod 755 {} \;`**

**Cari script executable luar /usr (malware cron)**  
**`find / -type f \( -name "*.sh" -o -name "*.pl" -o -name "*.py" \) -perm /0111 ! -path "/usr/*" -exec ls -la {} \; 2>/dev/null`**

**Kosongkan log >1GB (disk full killer)**  
**`find /var/log -type f -size +1G -exec truncate -s 0 {} \;`**

**Nuke semua PHP yang ada function bahaya (last resort)**  
**`find /var/www -type f -name "*.php" -exec grep -l "eval\|system\|exec\|passthru\|shell_exec\|popen" {} \; | xargs rm -f`**
→ **GUNA BACKUP DULU!**
