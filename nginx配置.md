```nginx
server {
     listen 8800;
     server_name laravel-demo;
     set $root_path '/home/vagrant/project/php/code/laravel-demo/public';
     root $root_path;

     index index.php index.html index.htm;

     location / {
          try_files $uri $uri/ /index.php?$query_string;
     }

     location ~ \.php {
          fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;
          fastcgi_index /index.php;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          include fastcgi_params;
     }

     location ~* ^/(css|img|js|flv|swf|download)/(.+)$ {
          root $root_path;
     }

     location ~ /\.ht {
          deny all;
     }
}
```

