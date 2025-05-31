# CRUD CodeIgniter 4

## Petunjuk

### Install composer & xampp

Pastikan sudah menginstall composer & xampp. Jika belum, bisa install melalui link:
[Instalasi composer di Linux & Mac](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos)
[Instalasi composer di Windows](https://getcomposer.org/doc/00-intro.md#installation-windows)
[Install xampp](https://www.apachefriends.org/download.html)

### Menjalankan aplikasi

Masuk ke folder project terlebih dahulu dengan `cd crud-ci4` lalu jalankan server dengan `php spark serve`. Untuk berhenti gunakan `ctrl + c` pada terminal.

### Membuat migration table

Jalankan `php spark migrate:create post` pada terminal, lalu buka file yang terbuat. Ubah isi `function up` menjadi:
```
public function up()
{
  $this->forge->addField([
      'id'           => [
           'type'           => 'INT',
           'constraint'     => 11,
           'unsigned'       => TRUE,
           'auto_increment' => TRUE
        ],
        'title'       => [
            'type'           => 'VARCHAR',
            'constraint'     => '255',
        ],
        'content'     => [
             'type'           => 'TEXT'
        ],
  ]);
  $this->forge->addKey('id', TRUE);
  $this->forge->createTable('posts');
}
```

Buka xampp dan jalankan server Apache dan MySQL. Buka situs [phpMyAdmin](http://localhost/phpmyadmin/index.php?route=/server/databases) untuk melihat database.

Pada terminal jalankan `php spark migrate` untuk melakukan migrasi dan cek apakah database sudah muncul di [phpMyAdmin](http://localhost/phpmyadmin/index.php?route=/server/databases). Jika terjadi kesalahan dan folder tidak muncul di phpMyAdmin, silahkan buat database baru di phpMyAdmin dengan nama `db_ci_crud`.

### Menggunakan aplikasi

Pastikan server sudah berjalan menggunakan `php spark serve`, lalu buka situs [http://localhost:8080/post](http://localhost:8080/post).

## Installation & updates

`composer create-project codeigniter4/appstarter` then `composer update` whenever
there is a new release of the framework.

When updating, check the release notes to see if there are any changes you might need to apply
to your `app` folder. The affected files can be copied or merged from
`vendor/codeigniter4/framework/app`.

## Setup

Copy `env` to `.env` and tailor for your app, specifically the baseURL
and any database settings.

## Important Change with index.php

`index.php` is no longer in the root of the project! It has been moved inside the *public* folder,
for better security and separation of components.

This means that you should configure your web server to "point" to your project's *public* folder, and
not to the project root. A better practice would be to configure a virtual host to point there. A poor practice would be to point your web server to the project root and expect to enter *public/...*, as the rest of your logic and the
framework are exposed.

**Please** read the user guide for a better explanation of how CI4 works!

## Repository Management

We use GitHub issues, in our main repository, to track **BUGS** and to track approved **DEVELOPMENT** work packages.
We use our [forum](http://forum.codeigniter.com) to provide SUPPORT and to discuss
FEATURE REQUESTS.

This repository is a "distribution" one, built by our release preparation script.
Problems with it can be raised on our forum, or as issues in the main repository.

## Server Requirements

PHP version 8.1 or higher is required, with the following extensions installed:

- [intl](http://php.net/manual/en/intl.requirements.php)
- [mbstring](http://php.net/manual/en/mbstring.installation.php)

> [!WARNING]
> - The end of life date for PHP 7.4 was November 28, 2022.
> - The end of life date for PHP 8.0 was November 26, 2023.
> - If you are still using PHP 7.4 or 8.0, you should upgrade immediately.
> - The end of life date for PHP 8.1 will be December 31, 2025.

Additionally, make sure that the following extensions are enabled in your PHP:

- json (enabled by default - don't turn it off)
- [mysqlnd](http://php.net/manual/en/mysqlnd.install.php) if you plan to use MySQL
- [libcurl](http://php.net/manual/en/curl.requirements.php) if you plan to use the HTTP\CURLRequest library
