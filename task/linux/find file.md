## Find
1. membuat shell script untuk mencari pola tertentu di file log Nginx /var/log/nginx/access.log
```
#!/bin/bash
# ================================================
# Script: check_nginx_suspicious.sh
# Fungsi: Mendeteksi aktivitas mencurigakan di access.log
# ================================================

LOG_FILE="/var/log/nginx/access.log"

# Pastikan file log ada
if [ ! -f "$LOG_FILE" ]; then
  echo "❌ File log tidak ditemukan: $LOG_FILE"
  exit 1
fi

echo "🔍 Memeriksa pola mencurigakan di $LOG_FILE ..."
echo

# Jalankan pencarian
grep -E "upload_|POST|eval|base64_decode" "$LOG_FILE"

# Cek hasil
if [ $? -eq 0 ]; then
  echo
  echo "✅ Ditemukan entri yang cocok dengan pola!"
else
  echo
  echo "✅ Tidak ada aktivitas mencurigakan ditemukan."
fi
```

2. membuat shell script untuk mencari pola tertentu di file log Nginx /var/log/nginx/access.log tanpa ensure file log ada
```
#!/bin/bash
# ================================================
# Script: check_nginx_suspicious.sh
# Fungsi: Mendeteksi aktivitas mencurigakan di access.log
# ================================================

LOG_FILE="/var/log/nginx/access.log"

echo "🔍 Memeriksa pola mencurigakan di $LOG_FILE ..."
echo

# Jalankan pencarian langsung tanpa cek file
grep -E "upload_|POST|eval|base64_decode" "$LOG_FILE"

# Cek hasil grep
if [ $? -eq 0 ]; then
  echo
  echo "✅ Ditemukan entri yang cocok dengan pola!"
else
  echo
  echo "❌ Tidak ada aktivitas mencurigakan ditemukan."
fi
```

Note: <br>
$? : Exit status dari perintah terakhir, maksudnya (exit code) dari perintah yang dijalankan sebelumnya — dalam kasus ini dari grep <br>
-eq : Operator perbandingan numerik (equal), Berarti “sama dengan”. Jadi ```[ $? -eq 0 ]``` artinya: “Apakah exit code sama dengan 0?”
