# cPanel Backup Tricks – View & Extract Specific Folder (.tar.gz)

### 1. Tengok isi backup tanpa extract (view only)
**`tar -tvf cpmove-username.tar.gz | less`**  
→ senarai semua file dalam backup

**`tar -tvf cpmove-username.tar.gz | grep public_html | less`**  
→ tengok folder public_html je

**Contoh real yang kau guna:**
**`tar -tvf maistcom.tar.gz | grep maistcom/homedir/myteras.com | more`**

### 2. Extract satu folder je (taknak extract semua – jimat masa & disk)
**`tar -xzvf cpmove-username.tar.gz username/homedir/public_html/namafolder/`**  
→ extract folder tertentu je

**Contoh real yang kau guna:**
**`tar -xzvf maistcom.tar.gz maistcom/homedir/public_html/myteras.com/`**

### 3. Extract satu domain je (paling kerap aku guna)
```bash
# Extract public_html + mail + db untuk satu domain je
tar -xzvf cpmove-username.tar.gz \
    username/homedir/public_html/domain.com/ \
    username/mysql/ \
    username/homedir/mail/domain.com/
