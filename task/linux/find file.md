## Grep
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
-eq : Operator perbandingan numerik (equal), Berarti “sama dengan”. Jadi ```[ $? -eq 0 ]``` artinya: “Apakah exit code sama dengan 0?” <br>
0 : Nilai sukses, Dalam konvensi Linux, ```0``` berarti sukses, sedangkan nilai selain ```0``` berarti gagal atau tidak ditemukan

<br><br>

## Find

Cara singkat (one-liner di terminal)
```
find /var/lib/containers/ -type f -name "upload_ff917c75dddea7887b58a59b3d49aac7" -mtime -2 | grep -q . && echo "✅ File ditemukan" || echo "❌ File tidak ditemukan"
```
Note: <br>
&& → jalan kalau hasil sebelumnya sukses (file ada). <br>
|| → jalan kalau hasil sebelumnya gagal (file tidak ada). 

<br>

Kalau ingin menampilkan lokasi file jika ada
```
result=$(find /var/lib/containers/ -type f -name "upload_ff917c75dddea7887b58a59b3d49aac7" -mtime -2)

if [ -n "$result" ]; then
    echo "✅ File ditemukan di lokasi berikut:"
    echo "$result"
else
    echo "❌ File tidak ditemukan dalam 2 hari terakhir."
fi
```
contoh:
<img width="1180" height="71" alt="image" src="https://github.com/user-attachments/assets/af6f3baf-4505-4d0f-8f0d-c2a5ca809d92" />



```
#!/bin/bash
# Script untuk memeriksa apakah file tertentu ada di dalam folder /var/lib/containers/
# dan dimodifikasi dalam 2 hari terakhir.

# Nama file yang dicari
TARGET_FILE="upload_ff917c75dddea7887b58a59b3d49aac7"

# Jalankan perintah find dan cek hasilnya
if find /var/lib/containers/ -type f -name "$TARGET_FILE" -mtime -2 | grep -q .; then
    echo "✅ File '$TARGET_FILE' ditemukan dalam 2 hari terakhir."
else
    echo "❌ File '$TARGET_FILE' tidak ditemukan dalam 2 hari terakhir."
fi
```


Kalau ingin bisa memanggil script ini dengan nama file yang berbeda-beda (parameter):
```
#!/bin/bash

TARGET_FILE="$1"

if [ -z "$TARGET_FILE" ]; then
    echo "❗ Gunakan: $0 <nama_file>"
    exit 1
fi

if find /var/lib/containers/ -type f -name "$TARGET_FILE" -mtime -2 | grep -q .; then
    echo "✅ File '$TARGET_FILE' ditemukan dalam 2 hari terakhir."
else
    echo "❌ File '$TARGET_FILE' tidak ditemukan dalam 2 hari terakhir."
fi
```

contoh:
```
./check_upload_file.sh upload_ff917c75dddea7887b58a59b3d49aac7
```
