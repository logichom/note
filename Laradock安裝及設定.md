1.下載並安裝docker(先確認系統安裝需求)

2.確認已安裝GIT

```shell
git --version
```

3.Command-line下選擇自己要的目錄(跟專案同層)

```shell
cd ~/project
```

4.安裝laradock(刪掉重裝的話注意已安裝的image)

```shell
git clone <https://github.com/Laradock/laradock.git>
```

5.進入目錄建立所需的.env檔案

```shell
cd laradock
cp .env.example .env
#修改存放專案目錄(單一專案)
vi .env
APP_CODE_PATH_HOST=../project/test_laravel
```

6.建立nginx的laravel.test.conf 檔

```shell
cd ~/laradock/nginx/sites
cp laravel.conf.example laravel.test.conf
#修改nginx檔案(指向專案路徑，/var/www/=APP_CODE_PATH_HOST)
root /var/www/public;
```

7.啟動docker中的服務(第一次啟動會跑很久，workspace會自己同時啟動)

```shell
docker-compose up -d nginx mysql phpmyadmin
```

8.建立laravel專案(需透過docker才能下cmd)

```shell
docker-compose exec workspace bash #離開用exit
composer create-project laravel/laravel test_laravel
or
composer create-project --prefer-dist laravel/laravel test_laravel
or
composer create-project laravel/laravel --prefer-dist .
```

9.開啟瀏覽器確認可執行

```shell
<http://127.0.0.1/> #laravel歡迎畫面
<http://127.0.0.1:8081> #phpmyadmin登入畫面(server=mysql,username=root,password=root)
```

10.結束docker服務

```shell
docker-compose down #等同docker-compose stop
```
