Define minimal config for working apache/php/mysql and infos on other stuffs

* may move all binaries from apache/php/mysql in same bin folder : ~14 files
  * httpd, libapr*.dll, libhttpd.dll, zlib1.dll
  * php5apache2_2.dll apache module calling php ; php5ts.dll php itself ; php_mysql.dll php bridge to mysql 
  * libmysql.dll, client lib used by php ; mysqld.exe server ; mysql.exe client ; mysqladmin.exe
* all conf in same folder : httpd.conf, php.ini, my.ini, mime.types, excepted share/english/errmsg.sys for mysql

# HTTP container

## Apache

bin/httpd.exe with libapr*.dll, libhttpd.dll, zlib1.dll ; may avoid other execs and dlls
bin/rotatelogs.exe : not needed, usefull on prod
bin/apr_dbd_*.dll : not needed
bin/iconv/<encoding>.so : may keep us-ascii and utf-8,16 and iso-8859-1 , windows-1252 ; or avoid all
modules/*.so : may keep only needed ones, ex: mod_mime.so
conf/httpd.conf ; may keep charset.conf, may avoid magic and mime.types, avoid ssl.*/ if no https needed
error/ : html error messages per language
icons/ : may avoid
include/, lib/ : avoid
logs/ : filled at runtime

exec with bin\httpd.exe

minimal config in conf\httpd.conf :
```
ThreadsPerChild 250
MaxRequestsPerChild  0
ServerRoot .
DocumentRoot html
ErrorLog logs/apache.log
LogLevel warn
Listen 80
ServerName localhost:80
DefaultType text/plain
# AddType is mandatory to execute php, requires mime.types file in conf
LoadModule mime_module bin/mod_mime.so
LoadFile bin/php5ts.dll
LoadFile bin/libmysql.dll
LoadFile bin/php_mysql.dll
LoadModule php5_module bin/php5apache2_2.dll
AddType application/x-httpd-php .php
PHPIniDir conf
```

## Lighttpd

## Nginx

## IIS

# Languages

## PHP

## Ruby

## Python

## Perl

# Databases

## Mysql

innodb engine required for ACID and FK consistency (ibdata1 for data, ib_logfile0, ib_logfile1), .frm still used for table specs.
If you do not need this, use only myisam it will be much lighter and easy to backup : 
*.frm for specs, *.myd for data, *.myi for index

bin\mysqld.exe --defaults-file=conf/my.ini --console --skip-innodb

config in conf/my.ini :
```
[client]
port = 3306
[mysqld]
port = 3306
skip-locking
key_buffer = 16K
max_allowed_packet = 1M
table_cache = 4
sort_buffer_size = 64K
read_buffer_size = 256K
read_rnd_buffer_size = 256K
net_buffer_length = 2K
thread_stack = 64K
server-id	= 1
[mysqldump]
quick
max_allowed_packet = 16M
[mysql]
no-auto-rehash
[isamchk]
key_buffer = 8M
sort_buffer_size = 8M
[myisamchk]
key_buffer = 8M
sort_buffer_size = 8M
[mysqlhotcopy]
interactive-timeout
```

## PostgreSql

## Sqlite

## Tomcat

## H2

## Derby
