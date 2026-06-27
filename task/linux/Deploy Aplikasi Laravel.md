## Deploy App Laravel
 - Buat file config aplikasi /etc/nginx/conf.d/laravel_app.conf
 - Setting owner dan group directory aplikasi ```chown -R nginx:nginx /DATA/laravel_app```
 - Ubah permission directory storage dan cache menjadi 775 ```chmod -R 775 /DATA/laravel_app/storage```
 - Allow port http dan http di selinux
