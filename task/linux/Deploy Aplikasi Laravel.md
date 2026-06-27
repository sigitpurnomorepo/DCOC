## Deploy App Laravel
 - Buat file config aplikasi /etc/nginx/conf.d/laravel_app.conf
 - Setting user php-fpm menjadi owner dan group directory aplikasi, agar dapat mengaksesnya ```chown -R nginx:nginx /DATA/laravel_app```
 - Ubah permission directory storage dan cache menjadi 775
   ```
      chmod -R 775 /DATA/laravel_app/storage
      chmod -R 775 /DATA/laravel_app/bootstrap/cache
   ```
 - Allow directory laravel_app, storage, dan cache di selinux
   ```
      # Non aktifkan selinux
      setenforce 0

      # Tambahkan policy untuk directory (tambahkan yang pathnya spesifik dulu)
      sudo semanage fcontext -a -t httpd_sys_rw_content_t "/DATA/laravel_app/storage(/.*)?"
      sudo semanage fcontext -a -t httpd_sys_rw_content_t "/DATA/laravel_app/bootstrap/cache(/.*)?"
      sudo semanage fcontext -a -t httpd_sys_content_t "/DATA/laravel_app(/.*)?"

      # Terapkan policy yang sudah ditambahkan
      sudo restorecon -Rv /DATA/laravel_app

      Tambahan opsional":
      # Cek policy selinux eksisting
      sudo semanage fcontext -l | grep -E "/DATA|storage"
   ```
 - Setting agar aplikasi dapat konek ke database
   ```
     sudo setsebool -P httpd_can_network_connect_db 1
     sudo setsebool -P httpd_can_network_connect 1
   ```
 - Allow port http dan http di selinux
