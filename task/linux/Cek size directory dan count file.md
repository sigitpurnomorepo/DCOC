## Cek size directory

```
# Cek size directory
du -sh /etc

# Cek size sub directory dan urutkan dari size terbesar
du -sh /etc/* | sort -hr 

# Cek size sub directory, urutkan dari size terbesar, dan hanya tampilkan 5 baris
du -sh /etc/* | sort -hr | head -n 5
```
