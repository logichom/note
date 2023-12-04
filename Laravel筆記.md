> Laravel 的構思的確和其他框架有很大不同，這也要求學習他的人必須熟練 php，並基礎紮實！ 如果你覺得學 laravel 框架十分困難，那麼原因只有一個：你 php 基礎不好。

## PHP版本需求

5.0 → PHP≥5.4.0 & PHP≤7.0.*
7 → PHP≥7.2.5 & PHP≤8.0
8 → PHP≥7.3 & PHP≤8.1
9 → PHP≥8 & PHP≤8.1

## 參考執行環境

laradock

## 參考架構

View — Controller — Service — Repository — Model

## 建議開發注意事項

1. 建立DB要有 migrations
2. 要有Models
3. 要有流程圖 (非必要)
4. 實作至少一個 feature function
5. 實作至少一個 unit test

## RESTful API簡介

* get: 讀取資源
* post: 新增資料
* delete: 刪除資源
* put: 替換資源 (通常做替換一個資源功能)
* patch: 更新資源 (修改資源的部分內容)

## 專案開發流程

```shell
#到gitlab將專案git clone下來(master)
#透過sourcetree切換到分支dev將專案下載下來
#開分支

#開啟終端機(windows推薦cmder)
#切換到laradock目錄
#運行服務
docker-compose up -d nginx mysql phpmyadmin

#進入docker的workspace container下指令
docker-compose exec workspace bash

#安裝相依套件
composer install

#產生專案.env檔案(若有可跳過)
cp .env.exmaple .env

#建laravel的key(若有可跳過)
php artisan key:generate

#產生jwt(json web tokens)私鑰(若有可跳過)
php artisan jwt:secret

#建立資料表(執行up()方法，先確認DB清單中已有laravel)
#若遇到錯誤可能要修改.env的DB_HOST=mysql,DB_PASSWORD=root
php artisan migrate

#離開workspace container
exit

#開始開發
#關閉運行的服務
docker-compose down

#確認完成後在gitlab上發出合併請求
#合併完成後再把遠端及本地分支砍掉
```

## 錯誤處理

### docker無法正常啟動-port被占用

請先停止XAMPP的mysql服務，然後關閉，別直接離開 或是改用其他port

### docker無法正常啟動-phpmyadmin無法登入

若原因為: `Different lower_case_table_names settings for server ('2') and data dictionary ('0').`

Laradock数据cache问题，更改MySQL版本及其重建

1. 關閉服務
2. 修改.env中MYSQL_VERSION從latest改成5.7(預設是8)
3. 刪除資料庫資料 `rm -rf ~/.laradock/data/mysql<br/>`4. 重建mysql: `docker-compose build mysql<br/>`5. 重新啟動服務: `docker-compose up -d nginx mysql phpmyadmin`

若還是無法解決，可能是PHP 7和MySQL 8的authentication方法不一致的问题

1. 啟動服務: `docker-compose up -d nginx mysql phpmyadmin<br/>`2. 查看mysql的container id: `docker ps<br/>`3. 進入mysql的docker container: `docker exec -it {替換剛剛的id)} bash<br/>`4. 登入mysql: `mysql -u root -p<br/>`5. 修改用戶密碼:

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'default'@'%' IDENTIFIED WITH mysql_native_password BY 'secret';
```

6.登入phpmyadmin

### postman戳API 出現 401 Unauthorized

先去註冊一組帳號，再去登入獲得token，然後在目標API的Authorization加上參數(過期需重新拿)

### API body參數接收不到

postman body參數要放在x-www-form-urlencoded底下

### 下指令 php artisan jwt:secret 出現 There are no commands defined in the “jwt” namespace.

```shell
#/composer.json補上下列參數
#"require": {
#中間省略
"tymon/jwt-auth": "^1.0.2"
#},
```

## 常用指令

### Aglio

```
#Default theme
aglio -i input.apib -o output.html

#Built-in color scheme
aglio --theme-variables slate -i index.apib -o index.html
```

### Composer

```shell
#相依套件安裝
#透過laradock去安裝
composer install
#執行環境的PHP版本差異請用(強制執行容易有錯誤，請確認下指令的目錄)
composer install --ignore-platform-reqs

#相依套件更新
composer update

#刪除migration後需執行
#因為database文件夾使用classmap來做加載。所以下了該指令才會更新autoload_classmap的內容。
composer dump-autoload
```

### Docker

```shell
#查看git版本
git --version

#查看docker版本
docker --version

#查看docker所啟動的服務
docker ps

#啟動docker服務，需在laradock目錄下運行(需確認docker有啟動)
#nginx可換成apache2
docker-compose up -d nginx mysql phpmyadmin

#進入docker的workspace container下指令
#離開用exit
docker-compose exec workspace bash

#關閉啟動的服務
docker-compose down
```

```php
//foreach與forelse差異在於:forelse可處理空陣列的狀態

//laravel SQL
//原生SQL查詢
$users = DB::select('select * from users where active = ?', [1]); //查詢結果為陣列內容為stdClass物件

//查詢產生器(query builder)
$user = DB::table('users')->where('name', 'John')->first();

//注意DB::select出來沒資料用isset會過然後blade就死掉

//laravel public執行排程對應(schedule映射到/public/schedule/)
//https://xxx.com.tw/schedule/your_schedule.php

//查詢執行sql
DB::enableQueryLog();
//這裡放sql語法
$query = DB::getQueryLog();
print_r($query);

//寫入session
session()->put('test', true);//永久
session()->flash('level', $vipLevel);//當下頁面有效
session()->forget('apply');//移除
//blade判斷session
@if (session('level') == 3)
@if (Session::has('ageNotAllow'))

//if ($request->is('admin/*')) {
//is 方法可以驗證接收到的請求 URI 與給定的規則是否相匹配。使用此方法時你可以將 * 符號作為萬用字元

//View::make('greeting', array('name' => 'Taylor'));
//等同
//View::make('greeting')->with('name', 'Taylor');
//等同
//View::make('greeting')->withName('Taylor');

//返回之前頁面
$url = '需要記錄要返回的網頁';
return redirect()->intended($url);

//local.ERROR: Undefined offset: 0
//DB:table()改成用->first()取第一筆值

//debug可以查看/storage/log/laravel.log或資料夾內的error.log

//寫入log到laravel.log
Log::debug(json_encode($res));

//Lang:get('buying_back');
//取得resources/lang/對應php檔案msg

//查看laravel版本
//php artisan -V
//php artisan --version
//composer.json "laravel/framework": "^6.2",

//Trying to get property of non-object
//查詢結果多加->toArray()，卻當成物件取值
//查詢結果不存在
//js裡面用了php語法

//指定群組內所有控制器的命名空間前綴:_Web
Route::group(['namespace' => '_Web'], function() {
 // 控制器在「App\Http\Controllers\_Web」命名空間
});

//給路由取別名，就可以很方便的指定路由，而不用打一串網址
Route::get('/api', 'ApiController@index')->name('web.api');
redirect()->route('web.api');//等同上面那串網址

//更改APP_KEY影響
/*
- 更改 APP_KEY 不会影响用户密码
- 如果您更改 APP_KEY，会导致 session (通过 cookie 实现) 无效，所有当前用户被注销
- 不要害怕您的 APP_KEY
- 您应该有一个策略来定期轮换 APP_KEY 以及其他凭据和密钥
- 如果您的代码已手动使用 Laravel 的加密器，则需要制定计划以使用旧密钥解密其加密数据，然后使用新密钥重新加密。
*/

//有新增或刪除controller要下這些command
//composer dump-autoload //本機或測試機用
//composer dump-autoload --optimize //等同composer dump-autoload -o //正式機用

//取得輸入資料
//use Illuminate\Http\Request;
//function (Request $request)
$name = $request->input('name');
$name = $request->name;
$name = $request->all()['name'];
$name = $request['name'];

//檔案系統
//判斷檔案是否存在
Storage::exists($user[$key]);
//刪除檔案
Storage::delete($user[$key]);
//取得檔案
Storage::get('file.jpg');
//取得檔案大小
Storage::size('file1.jpg');

//下載檔案
$file = public_path() . "/downloadable/優惠券.xlsx";
$headers = [
 'Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
];
return response()->download($file, '優惠券範例.xlsx', $headers);

$header = "\xEF\xBB\xBF";
$header .= "優惠券名稱,優惠券說明,優惠券折扣,優惠券編號,會員姓名,會員編號,優惠券使用時間,優惠券到期時間\n";
foreach ($data as $key => $value) {
 $header .= $value->coupon_name.','.$value->coupon_cantect.','.($value->coupon_discount*100).'% ,'.$value->coupon_number.','.$value->user_name.','.$value->member_number.','.$value->usage_time.','.$value->expire_date."\n";
}
header("Content-type:text/x-csv;charset=utf-8");
header("Content-Disposition: attachment; filename=".date("Y-m-d H:i:s")."優惠券列表.csv");
echo $header;
```

### composer 版本約束

```shell
"monolog/monolog": "1.19" #指定版本
"monolog/monolog": "1.0.*" #>=1.0,<1.1
"monolog/monolog": "~1.2" #>=1.2,<2.0
"monolog/monolog": "^1.2.3" #>=1.2.3,<2.0.0
```
