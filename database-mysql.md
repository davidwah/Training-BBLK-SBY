# MySQL
* Install mysql
```
sudo apt install mysql-server-8.0 mysql-client
```
* Masuk pada mysql
```
mysql -h <127.0.0.1> -u <user> -p
```
* Melihat user terdaftar. `harus masuk sebagai user root agar bisa melihat semua user`
```sql
select user,host,plugin from mysql.user;
```
* Melihat database
```sql
show databases;
```
* Membuat database
```sql
create database belajar_database;
```
* Membuat user
```sql
CREATE USER 'user1'@'%' IDENTIFIED WITH mysql_native_password BY 'rahasia';
```
* Mengatur database dapat diakses oleh `user1`
```sql
GRANT ALL ON belajar-database.* TO 'user1'@'%';
FLUSH PRIVILEGES;
```
* Membuat database barang
```sql
create database barang;
```
* Membuat tabel
```sql
SHOW TABLES;

CREATE TABLE barang (
    id      INT             NOT NULL,
    nama    VARCHAR(100)    NOT NULL,
    harga   INT             NOT NULL DEFALUT 0,
    jumlah  INT             NOT NULL DEFAULT 0
) ENGINE = InnoDB;
```
* Menampilkan tabel 
```sql
show tables;
```
* Menampilkan data pada table `barang`
```sql
select * from barang;
```
* Menampilkan deskripsi tabel `barang` 
```sql
DESCRIBE barang;

DESC barang

SHOW CREATE TABLE barang;
```
* Menambahkan kolom pada tabel `barang`
```sql
ALTER TABLE barang
    ADD COLUMN deskripsi TEXT;

ALTER TABLE barang
    ADD COLUMN salah TEXT;
```
* Menghapus kolom pada tabel `barang`
```sql
ALTER TABLE barang
    DROP COLUMN salah;
```
* Merubah kolom pada tabel `barang`
```sql
ALTER TABLE barang
    MODIFY nama VARCHAR(200) AFTER deskripsi;

ALTER TABLE barang
    MODIFY nama VARCHAR(200) FIRST;

ALTER TABLE barang
    ADD waktu_dibuat TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;
```
* Membuat data pada tabel `barang` - INSERT
```sql
INSERT INTO barang (id, nama, harga, jumlah) VALUES (01, 'Gula ABC', 5000, 5);

INSERT INTO barang (id, nama, harga, jumlah) VALUES (01, 'Kecap ABC', 3000, 15);

INSERT INTO barang (id, nama, harga, jumlah) VALUES (01, 'Bumbu ABC', 8000, 25);
```
* Mengubah data pada tabel `barang` - UPDATE
```sql
UPDATE barang SET id = 2 WHERE nama = 'Kecap ABC';

UPDATE barang SET id = 3 WHERE nama = 'Bumbu ABC';

UPDATE barang SET deskripsi = 'Kecap hitam manis' WHERE nama = 'Kecap ABC';
```
* Menghapus data pada table `barang` - DELETE
```sql
DELETE FROM barang WHERE nama = 'Kecap ABC';
```
