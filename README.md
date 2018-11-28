# docker-deops


#!/bin/bash
ps -ef|grep yz-cp-back-boot-0.0.1-SNAPSHOT.jar | awk {'print $2'} | xargs kill
nohup java -jar yz-cp-back-boot-0.0.1-SNAPSHOT.jar >front-`date +%F`.log 2>&1 &




server {
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name cell_back;
        listen       8018 ssl;
        ssl_certificate /etc/nginx/ssl/example_com.crt;
        ssl_certificate_key /etc/nginx/ssl/example_com.key;
        location / {
       if ($request_method = "OPTIONS") {
            add_header 'Access-Control-Max-Age' 86400;
            add_header 'Access-Control-Allow-Origin' "*";
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, DELETE';
            add_header 'Access-Control-Allow-Headers' 'token, x-real-ip, x-forwarded-ip, event-type, event-id, accept, content-type';
            add_header 'Content-Length' 0;
            add_header 'Content-Type' 'text/plain, charset=utf-8';
            return 200;
        }
        add_header 'Access-Control-Allow-Origin' "*";
        add_header 'Access-Control-Allow-Credentials' "true";
     proxy_pass   http://127.0.0.1:8008;
            client_max_body_size    1000m;
    }

}


