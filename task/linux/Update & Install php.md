
## Update PHP Masih Satu Versi 8.0 to 8.3
```
  # Periksa versi OS 
  cat /etc/oracle-release

  # Periksa juga apakah repository AppStream aktif
  dnf repolist --enabled | grep -i appstream

  # Cek versi module yang tersedia
  dnf module list php 

  # Cek php eksisting berasal dari repo mana
  dnf info installed php

  # Jika ada versi php lama, backup konfigurasi PHP
  cp -a /etc/php.ini /etc/php.ini.backup
  rpm -qa | grep '^php' > /home/pgnusr/php-packages-before-upgrade.txt  

  # Update php
  dnf module reset php -y
  dnf module enable php:8.3 -y
  dnf module install php:8.3
  systemctl restart php-fpm.service 
  systemctl status php-fpm.service

  # Verifikasi hasil update
  php -v
  rpm -qi php
  php -m
  dnf info installed php
```
<br />

## Update PHP Beda versi 7.4 to 8.3
```
  # Periksa versi OS 
  cat /etc/oracle-release

  # Periksa juga apakah repository AppStream aktif
  dnf repolist --enabled | grep -i appstream

  # Cek versi module yang tersedia
  dnf module list php 

  # Cek php eksisting berasal dari repo mana
  dnf info installed php

  # Uninstal php versi lama beserta modul-modulnya
  dnf remove 'php*'
  php -v

  # Install php 
  dnf module reset php -y
  dnf module enable php:8.3 -y
  dnf install -y \
  php \
  php-cli \
  php-common \
  php-fpm \
  php-bcmath \
  php-curl \
  php-gd \
  php-intl \
  php-mbstring \
  php-mysqlnd \
  php-opcache \
  php-xml \
  php-zip

  systemctl restart php-fpm.service 
  systemctl status php-fpm.service

  # Verifikasi hasil update
  php -v
  rpm -qi php
  php -m
  dnf info installed php
```
<br />

## Install php baru
```
  # Periksa versi OS 
  cat /etc/oracle-release

  # Periksa juga apakah repository AppStream aktif
  dnf repolist --enabled | grep -i appstream

  # Cek versi module yang tersedia
  dnf module list php 

  # Install php 
  dnf module reset php -y
  dnf module enable php:8.3 -y
  dnf install -y \
  php \
  php-cli \
  php-common \
  php-fpm \
  php-bcmath \
  php-curl \
  php-gd \
  php-intl \
  php-mbstring \
  php-mysqlnd \
  php-opcache \
  php-xml \
  php-zip

  systemctl restart php-fpm.service 
  systemctl status php-fpm.service

  # Verifikasi hasil update
  php -v
  rpm -qi php
  php -m
  dnf info installed php
```
