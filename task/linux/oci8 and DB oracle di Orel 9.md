

## Install oci8 in Orel 9



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
