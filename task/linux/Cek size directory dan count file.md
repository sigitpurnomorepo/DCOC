## Cek size directory

```
# Cek size directory menggunakan -sh
du -sh /etc

# Cek size sub directory dan urutkan dari size terbesar
du -sh /etc/* | sort -hr 

# Cek size sub directory, urutkan dari size terbesar, dan hanya tampilkan 5 baris
du -sh /etc/* | sort -hr | head -n 5

# Cek size directory menggunakan --maxdepth=1, menampilkan size directory dan sub-directory tingkat pertama tanpa file
du -h --max-depth=1 /etc | sort -hr

# Cek size directory menggunakan --maxdepth=1, menampilkan size directory dan sub-directory tingkat pertama dan file
du -ah --max-depth=1 /etc | sort -hr
```
