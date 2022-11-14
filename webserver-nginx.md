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
sudo mkdir -p /var/www/example.com
sudo chown -R $USER:$USER /var/www/example.com
sudo chmod -R 755 /var/www/example.com
nano /var/www/example.com/index.html
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
sudo nano /etc/nginx/sites-available/example.com
```
lalu isi file konfigurasi nginx sebagai berikut:
```
server {
        listen 80;
        listen [::]:80;

        root /var/www/example.com;
        index index.html index.htm index.nginx-debian.html;

        server_name example.com www.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
## Mengaktifkan file konfigurasi
```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
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
## Restart service nginx
```
sudo systemctl restart nginx
```
## Akses pada browser
> Setelah langkah-langkah diatas dijalankan coba periksa pada browser.
