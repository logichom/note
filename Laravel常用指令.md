```shell
#查看Laravel使用版本
php artisan --version

#清除快取(更改.env後不起作用)
php artisan config:cache

#清除配置的緩存
php artisan config:clear

#建laravel的key
php artisan key:generate

#產生jwt(json web tokens)私鑰
php artisan jwt:secret

#建立controller
php artisan make:controller UserController

#建立model
php artisan make:model ErpUser

#新增資料表
php artisan make:migration create_erp_users_table --create=erp_users

#新增欄位到資料表(會花點時間)
#執行前需確保已執行composer require doctrine/dbal
php artisan make:migration add_status_to_ship_orders --table=ship_orders

#建立假資料工廠
php artisan make:factory CommodityFactory

#指定model
php artisan make:factory CommodityFactory --model=Commodity

#建立資料填充
php artisan make:seeder CommoditySeeder

#在Feature目錄下創建一個測試類別
php artisan make:test BoatStuffingRepositoryTest

#在Unit目錄下創建一個測試類別
php artisan make:test BoatStuffingRepositoryTest --unit

#建立資料表(執行up()方法)
php artisan migrate

#清除資料表(執行down()方法)
php artisan migrate:rollback

#還原所有遷移
php artisan migrate:reset

#重新建立(執行migrate:reset+migrate)
php artisan migrate:fresh

#重新建立並填充假資料
php artisan migrate:refresh --seed

#執行資料填充
php artisan db:seed

#使用--class選項來單獨運行一個特別指定的seeder類別
php artisan db:seed --class=CommoditySeeder

#執行測試
php artisan test

#執行特定file
php artisan test --filter=BoatStuffingRepositoryTest

#執行特定file的function
php artisan test --filter=BoatStuffingRepositoryTest::testUpdateRcvItemList
```
