```shell
#安裝PHP(這邊透過homebrew安裝)
#若已安裝可跳過、版本依專案需求指定(這邊以7.4舉例)
brew install php@7.4

#設定apache執行目錄
sudo vim httpd.conf
#修改設定並存檔
DocumentRoot "/Users/yourusername/project"
<Directory "/Users/yourusername/project">
#重啟apache
sudo apachectl restart

#在專案目錄底下新增info.php
<?php
phpinfo();
#確認是否可正常執行
http://127.0.0.1/info.php

#403 Forbidden
#尚未提供解答

#啟用vhost
sudo vim httpd.conf
Include /private/etc/apache2/extra/httpd-vhosts.conf

sudo vi /etc/apache2/extra/httpd-vhosts.conf
AllowOverride All

#安裝composer
#若已安裝可跳過
brew install composer

#安裝laravel
composer global require laravel/installer

#設定環境變數PATH
#先用以下指令檢查環境變數
echo $PATH

#設定環境變數
echo 'export PATH="/usr/local/opt/php@7.4/bin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/opt/php@7.4/sbin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
echo 'export PATH="/usr/local/opt/php@7.4/bin:$PATH"' >> ~/.zshrc
echo 'export PATH="/usr/local/opt/php@7.4/sbin:$PATH"' >> ~/.zshrc

#安裝mysql
#若已安裝可跳過、版本依專案需求指定(這邊以5.7舉例)
brew install mysql@5.7

#設定環境變數
export PATH=${PATH}:/usr/local/mysql/bin

#確認是否安裝成功
#php -v 等同 php --version
php -v
mysql --version

#新增laravel專案
#不指定PHP版本(通常會安裝最新版)
laravel new appName
composer create-project laravel/laravel appName
composer create-project --prefer-dist laravel/laravel appName
#指定版本
composer create-project laravel/laravel="7.4.*" appName
#composer create-project [PACKAGE] [DESTINATION PATH] [--FLAGS]

#啟動laravel
#先進到要執行的laravel專案目錄底下
php artisan serve

#結束laravel
ctrl + c
```
