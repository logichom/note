```shell
#新增laravel專案
composer create-project --prefer-dist laravel/laravel auth-test

#安装 tymon/jwt-auth 擴充包
#Laravel 5.5以上多加dev-develop
composer require tymon/jwt-auth:dev-develop

#發行配置文件
php artisan vendor:publish

#選擇 Provider: Tymon\JWTAuth\Providers\LaravelServiceProvider
#成功後會在config中產生一個jwt.php檔案
#生成JWT密鑰
#Laravel 5.5以上用secret
php artisan jwt:secret

#Kernal.php先不用改
#將Model(app/Models/User.php)加入JWT的getJWTIdentifier、getJWTCustomClaimsfunction
use Tymon\JWTAuth\Contracts\JWTSubject;
class User extends Authenticatable implements JWTSubject
public function getJWTIdentifier() {
    return $this->getKey();
}
public function getJWTCustomClaims() {
    return [];
}

#add the service provider to the Providers
#修改config/app.php
'timezone' => 'Asia/Taipei',
Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
'JWTAuth' => 'Tymon\JWTAuth\Facades\JWTAuth',
'JWTFactory' => 'Tymon\JWTAuth\Facades\JWTFactory',

#修改config/auth.php
'defaults' => [
    'guard' => 'api',
    'passwords' => 'users',
],
'guards' => [
    'web' => [
        'driver' => 'session',
        'provider' => 'users',
    ],
    'api' => [
        'driver' => 'jwt',
        'provider' => 'users',
        'hash' => false,
    ],
],

#以下可不加
'providers' => [
    'users' => [
        'driver' => 'eloquent',
        'model' => App\Models\User::class,
    ],
    'jwt' => [
        'driver' => 'eloquent',
        'model' => App\Models\User::class,
    ],
],

#剩下撰寫api,controller等等
#戳postman時token記得輸入跟login後記得替換

#php artisan migrate有問題
原來是MySQL 8.0後預設儲存密碼的方式由原來的 mysql_native_password 
改為 caching_sha2_password了
解決方式：
1.升級PHP版本到7.4
2.降級MySQL版本
```
