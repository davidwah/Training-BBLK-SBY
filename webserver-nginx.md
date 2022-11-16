# Install dan Konfigurasi Nginx
## Install Nginx
```
sudo apt update
sudo apt install nginx
```
## Periksa Status Server
```
systemctl status nginx

hostname -I
```
## Manajemen proses Nginx
* Menggunakan WSL
```
sudo service apache2 stop
sudo service apache2 start 
sudo service apache2 restart 
sudo service apache2 reload 
sudo service apache2 disable 
sudo service apache2 enable
```
* Menggunakan VBox
```
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl disable nginx
sudo systemctl enable nginx
```
## Setting Server Blocks
```
sudo mkdir -p /var/www/nginx.local
sudo chown -R $USER:$USER /var/www/nginx.local
sudo chmod -R 755 /var/www/nginx.local
nano /var/www/nginx.local/index.html
```
isi file `index.html`
```
<html>
    <head>
        <title>Selamat Datang di situs Saya!</title>
    </head>
    <body>
        <h1>Pengaturan Server Block di NGINX Saya telah berhasil!!!</h1>
    </body>
</html>
```
## Mengatur file konfigurasi  
File konfigurasi `nginx` default berada di `/etc/nginx/sites-available/`
```
sudo nano /etc/nginx/sites-available/nginx.local
```
lalu isi file konfigurasi nginx sebagai berikut:
```
server {
        listen 80;
        listen [::]:80;

        root /var/www/nginx.local;
        index index.html index.htm index.nginx-debian.html;

        server_name nginx.local www.nginx.local;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
## Mengaktifkan file konfigurasi
```
sudo ln -s /etc/nginx/sites-available/nginx.local /etc/nginx/sites-enabled/
```
## Menambah memori hash pada nginx
Untuk menghindari kemungkinan masalah memori hash bucket yang muncul ketika penambahan nama server tambahan, kita perlu menyesuaikan nilai dalam file `/etc/nginx/nginx.conf`.
```
sudo nano /etc/nginx/nginx.conf
```
lalu cari baris kode konfigurasi `server_names_hash_bucket_size` dan hapus tanda komentar `#`
```
...
http {
    ...
    server_names_hash_bucket_size 64;
    ...
}
...
```
## Cek file konfigurasi
```
sudo nginx -t
```
Jika file konfigurasi sesuai, maka akan muncul pesan berhasil seperti berikut:

> nginx: the configuration file /etc/nginx/nginx.conf syntax is ok  
> nginx: configuration file /etc/nginx/nginx.conf test is successful

## Restart service nginx
```
sudo systemctl restart nginx
```
## Akses pada browser
> Setelah langkah-langkah diatas dijalankan coba periksa pada browser.
