
# Tentang Matomo
<h1 align="center"><img src="https://raw.githubusercontent.com/felfel2305/kdjk-project/main/matomo%20logo.png"></h1>

Matomo adalah aplikasi analitik web gratis dan sumber terbuka yang paling umum untuk melacak kunjungan daring ke satu atau beberapa situs web dan menampilkan laporan tentang kunjungan tersebut untuk dianalisis.


## Panduan Instalasi Matomo di Server Linux

Berikut adalah langkah-langkah profesional untuk instalasi Matomo, meliputi pembaruan sistem, instalasi dependensi, penyiapan basis data, hingga konfigurasi izin direktori.

### 1\. Pembaruan Sistem dan Instalasi Dependensi

Lakukan pembaruan sistem operasi dan instal paket dependensi yang diperlukan seperti Apache, MySQL, dan modul PHP pendukung.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 mysql-server php php-mysql php-xml php-curl php-gd php-cli php-mbstring unzip -y
```

### 2\. Pengunduhan dan Ekstraksi Matomo

Masuk ke direktori *web root* (`/var/www/html`), unduh berkas instalasi Matomo, dan ekstrak isinya.

```bash
cd /var/www/html
sudo wget https://builds.matomo.org/matomo.zip
sudo unzip matomo.zip
```

### 3\. Konfigurasi Izin Direktori

Atur izin kepemilikan dan akses direktori Matomo agar web server Apache (pengguna `www-data`) dapat memproses berkas dan folder.

```bash
sudo chown -R www-data:www-data /var/www/html/matomo
sudo chmod -R 755 /var/www/html/matomo
```

### 4\. Penyiapan Basis Data MySQL

Akses shell MySQL sebagai pengguna root untuk membuat basis data baru dan pengguna khusus untuk Matomo. Ganti `'passwordku'` dengan kata sandi yang kuat.

```bash
sudo mysql -u root -p
```

Setelah prompt MySQL muncul, jalankan *query* berikut:

```sql
CREATE DATABASE matomo_db;
CREATE USER 'matomo_user'@'localhost' IDENTIFIED BY 'passwordku';
GRANT ALL PRIVILEGES ON matomo_db.* TO 'matomo_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 5\. Penyelesaian Instalasi Web

Setelah semua langkah di atas selesai, buka peramban Anda dan akses URL berikut untuk memulai proses konfigurasi Matomo melalui web installer:

```
http://localhost/matomo
```
