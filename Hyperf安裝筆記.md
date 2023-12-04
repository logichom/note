#安裝homebrew
/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

#PHP移除7.2然後安裝7.4
brew uninstall php@7.2
rm -rf /usr/local/etc/php/7.2
brew install php@7.4
echo'export PATH="/usr/local/opt/php@7.4/bin:$PATH"' >> ~/.zshrc
echo'export PATH="/usr/local/opt/php@7.4/sbin:$PATH"' >> ~/.zshrc
exec$SHELL
#啟動PHP-FPM服務
brew services start php@7.4
brew services stop php@7.4
brew services restart php@7.4
php -i | grep ini

#安裝swoole
#前輩建議swoole裝4.6.X，別裝4.7.X
#pecl download swoole
#改到 [https://pecl.php.net/package/swoole](https://pecl.php.net/package/swoole) 下載4.6.1
brew info openssl
tar zxvf swoole-4.6.1.tgz
cd swoole-4.6.1
sudo phpize
./configure --enable-openssl --enable-http2 --with-openssl-dir=/usr/local/Cellar/openssl@1.1/1.1.1l
sudo make clean && sudo make && sudo make install
#php.ini新增
vim /usr/local/etc/php/7.4/php.ini
; swoole
extension="swoole.so"
swoole.use_shortname = "Off"
#重啟PHP
brew services restart php@7.4
php -m

#安裝postgresql
brew install postgresql
brew info postgresql

#安裝swoole-postgresql
brew install wget
#或wget [https://github.com/swoole/ext-postgresql/archive/master.zip](https://github.com/swoole/ext-postgresql/archive/master.zip)
#或unzip master.zip
#改到 [https://github.com/swoole/ext-postgresql/releases/tag/v4.6.1](https://github.com/swoole/ext-postgresql/releases/tag/v4.6.1) 下載並解壓縮
cd ext-postgresql-master
sudo phpize
./configure --with-openssl-dir=/usr/local/Cellar/openssl@1.1/1.1.1l --with-libpq-dir=/usr/local/Cellar/libpq/13.4/
sudo make clean && sudo make && sudo make install
#php.ini新增
vim /usr/local/etc/php/7.4/php.ini
extension="swoole_postgresql.so"
php -m

#安裝redis
#有問問題就按enter
pecl install redis

#安裝mongodb
pecl install mongodb

#安裝composer
brew install composer

#查看swoole版本
php --ri swoole
#查看swoole_postgresql版本
php --ri swoole_postgresql
