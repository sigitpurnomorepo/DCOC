## Mencari baris text yang ada pada sebuah file menggunakan Grep

```
if grep -q -E "upload_|POST|eval|base64_decode" /var/log/nginx/access.log; then
  echo "✅ Ditemukan entri yang mencurigakan!"
else
  echo "❌ Tidak ada aktivitas mencurigakan ditemukan."
fi
```
Note:

- grep -q → jalankan pencarian diam-diam (quiet mode, tidak tampilkan hasil)

- -E → aktifkan regex (supaya | bisa dipakai sebagai “OR”)

- "upload_|POST|eval|base64_decode" → pola yang dicari

- /var/log/nginx/access.log → file log Nginx yang diperiksa

- if ...; then ... else ... fi → menentukan hasil output di terminal



Kalau ingin sekalian melihat hasil baris yang cocok:
```
grep -E "upload_|POST|eval|base64_decode" /var/log/nginx/access.log && echo "✅ Ditemukan entri mencurigakan!" || echo "❌ Tidak ada aktivitas mencurigakan."
```
Note:

- && jalan kalau grep menemukan hasil,

- || jalan kalau tidak ada hasil.


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

2. membuat shell script untuk mencari pola tertentu di file log Nginx /var/log/nginx/access.log tanpa memastikan file log ada
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

Note: 

- $? : Exit status dari perintah terakhir, maksudnya (exit code) dari perintah yang dijalankan sebelumnya — dalam kasus ini dari grep 

- -eq : Operator perbandingan numerik (equal), Berarti “sama dengan”. Jadi ```[ $? -eq 0 ]``` artinya: “Apakah exit code sama dengan 0?” 

- 0 : Nilai sukses, Dalam konvensi Linux, ```0``` berarti sukses, sedangkan nilai selain ```0``` berarti gagal atau tidak ditemukan

- Opsi -E artinya: gunakan extended regular expressions (ERE)

  - Dengan -E, kamu bisa memakai tanda seperti | untuk OR (atau).

  - Tanpa -E, tanda | akan dianggap karakter biasa.

<br><br>

## Mencari file yang ada di dalam directory menggunakan Find

Cara paling sederhana (pakai if dan subshell)
```
if find /var/log/nginx/ -type f -name "access.log-20251030.gz" -mtime -2 | grep -q .; then
    echo
    echo
    echo "Result:"
    echo "✅ File ditemukan."
else
    echo
    echo
    echo "Result:"
    echo "❌ File tidak ditemukan."
fi
```
Note:

- find ... | grep -q . → akan bernilai true kalau ada output (file ditemukan), kemudian kondisional pertama dijalankan.

- Kalau tidak ada output, maka false, dan bagian else akan dijalankan.

- grep -q . → digunakan agar tidak mengeluarkan output ```find```, karena ingin bypass ke conditional ```if```

- -mtime: Stands for "modification time".
  - -2: Means "less than 2 * 24 hours ago" (i.e., within the last 48 hours).
  - -n → less than n days ago
  - n → exactly n days ago
  - +n → more than n days ago


<br>

Cara singkat (one-liner di terminal)
```
find /var/lib/containers/ -type f -name "upload_ff917c75dddea7887b58a59b3d49aac7" -mtime -2 | grep -q . && echo "✅ File ditemukan" || echo "❌ File tidak ditemukan"
```
Note: <br>
- && → jalan kalau hasil sebelumnya sukses (file ada). <br>
- || → jalan kalau hasil sebelumnya gagal (file tidak ada). 

<br>

Kalau ingin menampilkan lokasi file jika ada
```
result=$(find /var/log/nginx/ -type f -name "*access.log-202511*.gz")

if [ -n "$result" ]; then
    echo
    echo
    echo
    echo
    echo "✅ File ditemukan di lokasi berikut:"
    echo "$result"
else
    echo
    echo
    echo
    echo
    echo "❌ File tidak ditemukan."
fi
```
contoh:
<img width="317" height="166" alt="image" src="https://github.com/user-attachments/assets/8e0658d0-a68c-41d2-8bbd-29c74e96c41a" />

<br>

Menggunakan shell script
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
