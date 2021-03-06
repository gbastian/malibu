# Install Notes

## General Requirements

 * Sever: Apache with PHP, jQuery library
 * Client: Javascript enabled

## bnb

We included `getBNBData.sh` as a cronjob, which runs every Saturday, at 10 am (010**6).

## isbn

#### For Debian 7 (Apache 2.2)
You need the php library <a href="http://php.net/manual/en/book.yaz.php">yaz</a> on the server. For Debian 7 (Apache 2.2):

1. <code>apt-get install yaz libyaz4-dev php5-dev php-pear</code> (maybe you have already some packages)
2. <code>pecl install yaz</code>
3. Open `/etc/php5/apache2/php.ini`, goto section `Dynamic Extensions` and add `extension=yaz.so`

Maybe, the file `yaz.so` is not located in the directory
which is configured by `extension_dir` in
`/etc/alternatives/php-config` and you have to copy it therefore.
(e.g. <code>cp /usr/lib/php5/20090626/yaz.so /usr/lib/php5/20100525/yaz.so</code> in our case).

#### For Debian 8 (Apache 2.4)
You need the php library <a href="http://php.net/manual/en/book.yaz.php">yaz</a> on the server. For Debian 8 (Apache 2.4):

* <code>apt-get install yaz libyaz4-dev php5-dev php-pear</code> (maybe you have already some packages)
* <code>pecl install yaz</code>
* create new file `/etc/php5/mods-available/yaz.ini` and add
```sh
; configuration for php YAZ module
; priority=20
extension=yaz.so
```
* create a symbolic link 
```sh
cd /etc/php5/apache2/conf.d 
ln -s ../../mods-available/yaz.ini 20-yaz.ini
```
* restart Apache2
```sh
service apache2 restart
```
