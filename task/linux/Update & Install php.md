
## Update PHP
```
  # Periksa versi OS dan module PHP
  cat /etc/oracle-release
  sudo dnf module list php

  # Periksa juga apakah repository AppStream aktif
  dnf repolist --enabled | grep -i appstream

  # Cek versi module yang tersedia
  dnf module listt php 

  # Cek php eksisting berasal dari repo mana
  dnf info installed php

  # Update php
  dnf module reset php -y
  dnf module enable php:8.3 -y
  dnf module install php:8.3
  systemctl restart php-fpm.service 
  systemctl status php-fpm.service
  php -v
  dnf info installed php
```
