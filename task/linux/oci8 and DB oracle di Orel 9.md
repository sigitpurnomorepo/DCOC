

## Install oci8 in Orel 9
```
1. Oracle Instant Client RPM (Basic & SDK)
- Cek apakah sudah terinstal = rpm -q oracle-instantclient-devel dan rpm -q oracle-instantclient-basic
- ioka belum terinstall, maka lanjut to next step
- Basic Package (RPM): Pilih yang bernama oracle-instantclient-basic-*.rpm
- Development and Runtime / SDK Package (RPM): Pilih yang bernama oracle-instantclient-devel-*.rpm
- Pilih .el9.x86_64.rpm untuk Oracle Linux 9
- Link = https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html

2. Source Code OCI8 PHP
- Misal menggunakan PHP 8.3.31, Anda membutuhkan OCI8 versi 3.3.x
- Download dari PECL: https://pecl.php.net/package/oci8 (Pilih versi terbaru di lini 3.3, misalnya oci8-3.3.0.tgz)

3. Paket Dependensi Development (Jika belum ada di VM)
- PHP membutuhkan php-devel dan gcc untuk melakukan compile, cara pengecekannya
- Cek gcc = rpm -q gcc, jika belum terinstal: Akan muncul pesan: package gcc is not installed
- Cek php-devel = rpm -q php-devel, jika belum terinstal: Akan muncul pesan: package php-devel is not installed

4. nstalasi Oracle Instant Client
- Setelah file dipindahkan ke VM, masuk ke direktori tempat Anda menyimpan file RPM tersebut, lalu install menggunakan rpm atau dnf
- sudo rpm -ivh oracle-instantclient-basic-*.rpm dan sudo rpm -ivh oracle-instantclient-devel-*.rpm

5. Ekstrak dan Compile Ekstensi OCI8
- 
```


## Install Package Yajra for Connection Between Laravel to Oracle DB
```
# install package yajra (open traffic to url package yajra in firewall)
composer require yajra/laravel-oci8:^10.0
php artisan config:clear
php artisan cache:clear
composer dump-autoload
php artisan package:discover

masih ada blocking permission ke oracle karna selinux
sudo chcon -R -t httpd_sys_rw_content_t /usr/lib/oracle
sudo setsebool -P httpd_can_network_connect 1
```
