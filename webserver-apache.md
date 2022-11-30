# Install dan Konfigurasi Apache
## Instal Apache
```
sudo apt update
sudo apt install apache2
```
## Periksa Pengaturan Web Server
```
sudo service apache2 status

hostname -I
```
## Manajemen Proses Apache
* perintah dijalankan ketika menggunakan WSL
```
sudo service apache2 stop
sudo service apache2 start 
sudo service apache2 restart 
sudo service apache2 reload 
sudo service apache2 disable 
sudo service apache2 enable
```
* perintah dijalankan ketika menggunakan VirtualBox
```
sudo systemctl stop apache2
sudo systemctl start apache2
sudo systemctl restart apache2
sudo systemctl reload apache2
sudo systemctl disable apache2
sudo systemctl enable apache2
```
## Setup Virtual Hosts  
file project apache2 ada di direktori `/var/www/html`
```
sudo mkdir -p /var/www/example.lokal/html
sudo chown -R $USER:$USER /var/www/example.lokal/html
sudo chmod -R 755 /var/www/example.lokal
nano /var/www/example.lokal/html/index.html
```
isi file `index.html`
```
<html>
    <head>
        <title>Selamat Datang di situs Saya!</title>
    </head>
    <body>
        <h1>Pengaturan Server Block di Situs Saya telah berhasil!!!</h1>
    </body>
</html>
```
## Mengatur file konfigurasi  
File konfigurasi apache2 default berada di `/etc/apache2/sites-available/000-default.conf`.  
Coba buat file konfigurasi baru `/etc/apache2/sites-available/example.lokal.conf`, lalu isi file konfigurasi seperti berikut:
```
<VirtualHost *:80>
    ServerAdmin admin@example.lokal
    ServerName example.lokal
    ServerAlias www.example.lokal
    DocumentRoot /var/www/example.lokal/html
   ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
## Mengaktifkan file konfigurasi
```
sudo a2ensite example.lokal.conf
```
## Menonaktifkan file konfigurasi default `000-default.conf`
```
sudo a2dissite 000-default.conf
```
## Cek file konfigurasi
```
sudo apache2ctl configtest
```
Jika berhasil akan muncul pesan `Syntax OK`  
## Restart service apache2
```
sudo systemctl restart apache2
```
---

## Catatan

- File konfigurasi Apache berada di direktori `/etc/apache2`.  
- file konfigurasi utama Apache adalah `/etc/apache2/apache2.conf`.
- Port yang akan didengarkan Apache ditentukan dalam file `/etc/apache2/ports.conf`
- File-file Apache Virtual Hosts berada di direktori `/etc/apache2/sites-available`. File-file konfigurasi yang ditemukan dalam direktori ini tidak digunakan oleh Apache kecuali mereka ditautkan ke direktori `/etc/apache2/sites-enabled`.
- Kita dapat mengaktifkan direktori virtual host dengan membuat symlink menggunakan perintah `a2ensite` dari file konfigurasi yang ditemukan di direktori sites-available ke direktori `sites-enabled`. Untuk menonaktifkan virtual host gunakan perintah `a2dissite`.
- Sangat disarankan untuk mengikuti penamaan standar, misalnya jika nama domain situs ini adalah `bblk.net`, maka file konfigurasi domain dinamakan `/etc/apache2/sites-available/bblk.net.conf` untuk memudahkan manajemen situs.
- File konfigurasi yang digunakan untuk memuat berbagai modul Apache terdapat di direktori `/etc/apache2/mods-available`. Konfigurasi dalam direktori `mod-available` dapat diaktifkan dengan membuat symlink ke direktori `/etc/apache2/mods-available` menggunakan perintah `a2enconf` dan dinonaktifkan dengan perintah `a2disconf`.
- File konfigurasi global disimpan di direktori `/etc/apache2/conf-available`. File dalam direktori `conf-available` dapat diaktifkan dengan membuat symlink ke `/etc/apache2/conf-enabled` menggunakan perintah `a2enconf` dan dinonaktifkan dengan perintah `a2disconf`.
- File log Apache (access.log dan error.log) terletak di direktori `/var/log/apache`. Disarankan untuk menggunakan file access dan error log yang berbeda untuk setiap virtual host.
- Kita dapat mengatur direktori root dokumen domain Kita ke lokasi yang Kita inginkan. Lokasi yang paling umum untuk webroot meliputi:
    - `/home/<user_name>/<site_name>`
    - `/var/www/<site_name>`
    - `/var/www/html/<site_name>`
    - `/opt/<site_name>`
