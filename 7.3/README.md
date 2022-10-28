## Docker Image Version

- version: `7.3`

## Base

- `php:7.3-fpm` : Base docker image
- `php-7.3`: PHP version

## ENV

- `PHP_VERSION` : PHP version (7.3)
- `PHPIZE_DEPS` : Dependencies required for running "phpize"
- `PHP_INI_DIR` : PHP settings folder (`/usr/local/etc/php`)

## Installed Packages

### By Default PHP-FPM

- bash
- ca-certificates
- curl
- openssl
- tzdata

### Expand More

- apt-utils
- htop cron
- gnupg2
- vim nano
- wget
- zip unzip
- git
- mariadb-client(10.5) default-mysql-client
- redis-tools
- composer

## Installed PHP Extensions

### By Default PHP-FPM

- [ctype](https://www.php.net/manual/en/book.ctype.php) : Character type checking
- [curl](https://www.php.net/manual/en/book.curl.php) : Client URL Library
- [date](https://www.php.net/manual/en/refs.calendar.php) : Date and Time Related Extensions
- [dom](https://www.php.net/manual/en/book.dom.php) : Document Object Model
- [filter](https://www.php.net/manual/en/book.filter.php) : Data Filtering
- [fileinfo](https://www.php.net/manual/en/book.fileinfo.php) : File Information
- [ftp](https://www.php.net/manual/en/book.ftp.php) : File Transfer Protocol
- [hash](https://www.php.net/manual/en/book.hash.php) : HASH Message Digest Framework
- [iconv](https://www.php.net/manual/en/book.iconv.php) : iconv (internationalization conversion)
- [json](https://www.php.net/manual/en/book.json.php) : JavaScript Object Notation
- [mbstring](https://www.php.net/manual/en/book.mbstring.php) : Multibyte String
- [mysqlnd](https://www.php.net/manual/en/book.mysqlnd.php) : MySQL Native Driver
- [libxml](https://www.php.net/manual/en/book.libxml.php) : Lib XML
- [openssl](https://www.php.net/manual/en/book.openssl.php) : OpenSSL
- [pcre](https://www.php.net/manual/en/book.pcre.php) : Regular Expressions (Perl-Compatible)
- [PDO](https://www.php.net/manual/en/book.pdo.php) : PHP Data Objects
- [pdo_sqlite](https://www.php.net/manual/en/ref.pdo-sqlite.php) : SQLite Functions (PDO_SQLITE)
- [posix](https://www.php.net/manual/en/book.posix.php) : POSIX (Process Control Extensions)
- [sqlite3](https://www.php.net/manual/en/book.sqlite3.php) : SQLite3
- [readline](https://www.php.net/manual/en/book.readline.php) : GNU Readline
- [tokenizer](https://www.php.net/manual/en/book.tokenizer.php) : Tokenizer
- [session](https://www.php.net/manual/en/book.session.php) : Session Handling
- [simplexml](https://www.php.net/manual/en/book.simplexml.php) : SimpleXML
- [sodium](https://www.php.net/manual/en/book.sodium.php) : Sodium (library for encryption, decryption, signatures, password hashing and more)
- [standard](https://www.php.net/manual/en/extensions.php) : PHP Standard extension
- [xml](https://www.php.net/manual/en/book.xml.php) : XML Parser
- [xmlreader](https://www.php.net/manual/en/book.xmlreader.php) : XMLReader
- [xmlwriter](https://www.php.net/manual/en/book.xmlwriter.php) : XMLWriter
- [zlib](https://www.php.net/manual/en/book.zlib.php) : Zlib Compression

### Expand More

- [zip](https://www.php.net/manual/en/book.zip.php) : ZIP (read or write ZIP compressed archives and the files inside them). (require package: `libzip`)
- [bz2](https://www.php.net/manual/en/book.bzip2.php) : Bzip2 (read and write bzip2 (.bz2) compressed files). (require package: `libbz2 bzip2`)
- [bcmath](https://www.php.net/manual/en/book.bc.php) : BCMath Arbitrary Precision Mathematics
- [decimal](https://www.php.net/manual/en/funcref.php) : Decimal (Arbitrary precision floating-point decimal) (require package: `libmpdec`)
- [intl](https://www.php.net/manual/en/book.intl.php) : Internationalization Functions. (require package: `zlib1g libicu`)
- [pcntl](https://www.php.net/manual/en/book.pcntl.php) : Process Control.
- [mcrypt](https://www.php.net/manual/en/book.mcrypt.php) : Mcrypt (algorithms such as DES, TripleDES, Blowfish (default) ... cipher modes). (require package: `libmcrypt`)
- [xsl](https://www.php.net/manual/en/book.xsl.php) : XSL (performing XSL » XSLT transformations). (require package: `libxslt`)
- [ldap](https://www.php.net/manual/en/book.ldap.php) : Lightweight Directory Access Protocol
- [imap](https://www.php.net/manual/en/book.imap.php) : IMAP, POP3 and NNTP
- [sockets](https://www.php.net/manual/en/book.sockets.php) : Sockets
- [soap](https://www.php.net/manual/en/book.soap.php) : SOAP. (require extension: `libxml`)
- [opcache](https://www.php.net/manual/en/book.opcache.php) : OPcache (improves PHP performance by storing precompiled script bytecode)
- [gd](https://www.php.net/manual/en/book.image.php) : Image Processing and GD. (require packages: `libgd zlib libpng libjpeg libjpeg62-turbo libfreetype6 libwebp libavif libxpm`)
- [exif](https://www.php.net/manual/en/book.exif.php) : Exchangeable image information. (require packages: `libexif`)
- [imagick](https://www.php.net/manual/en/book.imagick.php) : Image Processing (ImageMagick). (require packages: `libmagickwand`)
- [gnupg](https://www.php.net/manual/en/book.gnupg.php) : GNU Privacy Guard. (require packages: `libgpgme`)
- [swoole](https://www.php.net/manual/en/book.swoole.php) : Swoole (is a high-performance networking framework). (require extension: `sockets openssl http2 mysqlnd json curl cares`)
- [pgsql](https://www.php.net/manual/en/book.pgsql.php) : PostgreSQL. (require package: `libpq`)
- [pdo_pgsql](https://www.php.net/manual/en/ref.pdo-pgsql.php) : PostgreSQL Functions (PDO_PGSQL). (require extension: `pgsql`)
- [mysqli](https://www.php.net/manual/en/book.mysqli.php) : MySQL Improved Extension. (require extension: `mysqlnd`)
- [pdo_mysql](https://www.php.net/manual/en/ref.pdo-mysql.php) : MySQL Functions (PDO_MYSQL). (require extension: `mysqlnd`)
- [mongodb](https://www.php.net/manual/en/set.mongodb.php) : MongoDB driver
- [msgpack](https://www.php.net/manual/en/funcref.php) : MsgPack (PHP extension for interfacing with MessagePack)
- [igbinary](https://www.php.net/manual/en/book.igbinary.php) : Igbinary (is a drop in replacement for the standard PHP serializer)
- [redis](https://www.php.net/manual/en/funcref.php) : Redis (PHP extension for interfacing with Redis). (require extension: `json igbinary msgpack`)
- [memcached](https://www.php.net/manual/en/book.memcached.php) : Memcached. (require extension: `json session igbinary`and packages: `libmemcached`)
- [event](https://www.php.net/manual/en/book.event.php) : Event. (require extension: `openssl sockets` and packages: `libevent openssl`)
- [yaml](https://www.php.net/manual/en/book.yaml.php) : YAML Data Serialization

## Settings

- `/usr/local/etc/php/` : PHP settings folder (`php.ini` file)
- `/usr/local/etc/php/conf.d/` : PHP custom settings folder
- `/usr/local/etc/` : PHP-FPM settings folder (`php-fpm.conf` file)
- `/usr/local/etc/php-fpm.d/` : PHP-FPM custom settings folder
- `/var/log/php/` : PHP-FPM logs folder

## Notes

- `/usr/local/etc/php/php.ini` default uses `production` ENV config file. If you want to change, overwrite it's.
- `/usr/local/etc/php/conf.d/` is php custom configurations folder with files: `zz-php.ini / zz-session.ini / zz-opcache.ini`. If you want to change, overwrite it's.
- `/usr/local/etc/php-fpm.d/` is php-fpm custom configurations folder with files: `zz-www.conf`. If you want to change, overwrite it's.
