# process
```
composer require laravel/ui
php artisan ui vue --auth
npm install vue-loader@^15.9.5 --save-dev --legacy-peer-deps
npm install && npm run dev

touch database/database.sqlite
.env
DB_CONNECTION=sqlite
DB_DATABASE=/var/www/html/lar.s/database/database.sqlite
DB_FOREIGN_KEYS=true
php artisan migrate
sudo chown -R www-data:www-data .
```

# клонирование
```
composer install && npm i
cp .env.example .env
php artisan key:generate
```

# nginx.conf
```
server {
    listen 80;
    server_name example.com;
    root /var/www/html/lar.s/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;
    charset utf-8;
    error_page 404 /index.php;

    location / { try_files $uri $uri/ /index.php?$query_string; }
    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }
    location ~ /\.(?!well-known).* { deny all; }
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
