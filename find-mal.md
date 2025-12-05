### Find Command Gila-Gila (Malware Hunting & Emergency Cleanup)

**`find / \( -name "*.ico" -o -name "*.php.jpg" -o -name "*.phtml" -o -name ".env" \) -exec ls -la {} \; 2>/dev/null`**  
→ Cari file sus (PHP disguised as gambar, .ico shell, .env terdedah)

**`find /var/www -name "*.php" -size +500k -exec ls -lh {} \; | head -20`**  
→ PHP file >500KB = 99% webshell / backdoor (normal script jarang besar gila)

**`find . -type f -name "*.php" -exec grep -l "eval\|base64_decode\|gzinflate\|str_rot13\|shell_exec\|passthru" {} \;`**  
→ Cari webshell signature klasik (eval(base64_decode(...)))

**`find /tmp /var/tmp /dev/shm -name "sess_*" -o -name ".*" -mtime +7 -delete 2>/dev/null`**  
→ Bersihkan session + hidden file lama dalam tmp (cron setiap hari)

**`find /var/www -type f -perm 0777 -exec chmod 644 {} \; -o -type d -perm 0777 -exec chmod 755 {} \;`**  
→ Auto betulkan permission gila yang client/website buat (777 = bahaya)

**`find / -type f -name "wp-config.php" -exec grep -l "DB_PASSWORD" {} \; | xargs -I {} sed -i 's/DB_PASSWORD.*/DB_PASSWORD sangatrahsia/g' {}`**  
→ Tukar semua password WP jadi “sangatrahsia” kalau kena hack & nak lock dulu (emergency)

**`find /home /var/www -name ".git" -type d -exec chmod 000 {} \; -prune 2>/dev/null`**  
→ Lock folder .git supaya tak boleh diakses dari web (banyak case kena exploit .git/config)

**`find / -type f \( -name "*.sh" -o -name "*.pl" -o -name "*.py" \) -perm /0111 ! -path "/usr/*" -exec ls -la {} \;`**  
→ Cari script executable luar folder /usr (biasanya cron malware)

**`find /var/log -type f -size +1G -exec truncate -s 0 {} \;`**  
→ Kosongkan log >1GB serta-merta (bila disk full sampai 100%)

**`find / \( -name "index.php" -o -name "wp-login.php" \) -exec head -n 5 {} \; | grep -i "eval\|<?php.*@.*eval"`**  
→ Check 5 baris pertama index.php / wp-login.php — kalau ada eval terus tahu kena inject

Bonus satu lagi yang aku panggil “nuke everything sus” (guna bila dah give up):
**`find /var/www -type f -name "*.php" -exec grep -l "eval\|system\|exec\|passthru\|shell_exec\|popen" {} \; | xargs rm -f`**  
→ Padam semua PHP yang ada function bahaya (last resort — backup dulu!)
