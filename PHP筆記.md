```shell
//Openssl 替代 Mcrypt 3DES CBC 算法解决方案
//php 7.1 以后弃用了 Mcrypt 算法，现在用 openssl 替代
openssl_encrypt($arr, 'DES-EDE3-CBC', $l_key, OPENSSL_RAW_DATA , $l_iv);
openssl_decrypt($l_result, 'DES-EDE3-CBC', $l_key, OPENSSL_RAW_DATA | OPENSSL_NO_PADDING, $l_iv);

//AES加解密
//用urlencode避免斜線導致連結不安全
urlencode(openssl_encrypt($v['tender_documents_id'], 'AES-256-ECB', $aes256Key, 0));
urldecode(openssl_decrypt($pid, 'AES-256-ECB', $aes256Key, 0));

//錯誤處理
// "traditional" exceptions
try {
    throw new Foo();
} catch (Exception $e) {
}

// laravel v7 catchable fatal errors
try {
    $not_an_object->not_a_method();
} catch (Error $e) {
}

// both
try {
} catch (Throwable $e) {
}

//header下載pdf擋名會亂碼
//避免chrome下載檔名亂碼
$filename = urlencode("約定書_{$id}");
header("Content-type:application/pdf");
header("Content-Disposition:attachment;filename={$filename}.pdf");
//safari另開下載視窗要改成
header("Content-Type: application/octet-stream");

//匯出原生excel,欄位為文字,換行字符保持同一儲存格
header('Content-type:application/vnd.ms-excel');
header("Content-Disposition: attachment; filename=匯出報表資料.xls");
$table = '<style>br {mso-data-placement:same-cell;}</style>';
$table .= '<table cellpadding=0 cellspacing=0 border="1">
<tr>
<th>主要名稱</th>
<th>次要名稱</th>
<th>姓名</th>
</tr>';
$table .= '<tr>
<th style="vnd.ms-excel.numberformat:@">' . $row['special_name'] . '</th>
<th style="vnd.ms-excel.numberformat:@">' .  $row['second_name'] . '</th>
<th style="vnd.ms-excel.numberformat:@">' . $row['user_name'] . '</th>
</tr>';
$table .= '</table>';
echo $table;
```

PHP curl

```php
//寫法1-POST
function curl($url='') {
    $curl = curl_init();
    curl_setopt_array($curl, array(
        CURLOPT_URL => $url,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'POST',
        CURLOPT_SSL_VERIFYPEER => false, //跳過驗證檢查
        CURLOPT_SSL_VERIFYHOST => false, //從證書中檢查SSL加密演算法是否存在
    ));
    $response = curl_exec($curl);
    if ($error = curl_error($curl)) {
        die($error);
    }
    curl_close($curl);
    return $response;
}

//寫法2-POST
function curl($url, $username, $password, $timeout=30) {
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);//跳過驗證檢查
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);//從證書中檢查SSL加密演算法是否存在
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);//返回字串，不要直接输出
    curl_setopt($ch, CURLOPT_USERPWD, "$username:$password");
    curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
    curl_setopt($ch, CURLOPT_TIMEOUT, $timeout);
    //curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
    //curl_setopt($ch, CURLOPT_POST, true);
    //curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($data));//組合附加在網址後面的參數
    //curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
    //curl_setopt($ch, CURLOPT_USERAGENT, 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:38.0) Gecko/20100101 Firefox/38.0');
    //curl_setopt($ch, CURLOPT_COOKIE, 'JSESSIONID=39B2B7837FFEE26E1B83CEC662D5DF08');

    $response = curl_exec($ch);
    if ($error = curl_error($ch)) {
        die($error);
    }
    curl_close($ch);

    return $response;
}
```

比較常數const與define差異:
1.const 關鍵字

- PHP版本5.3.0開始能使用
- PHP版本5.6.0後才可用於常數運算、才可定義array
- 可在class內外命名
- 只能命名為靜態名稱、值只能為固定值
- 大小寫敏感
- 不能重新賦值
- 不能在條件式中命名
- 速度比define快一點

2.define 函式

- PHP版本7.0後才可定義array
- 只能在class外命名
- 可命名為動態名稱(或任何表示式)、值可以為任何表達式
- 可透過設定大小寫不敏感
- 不能重新賦值

取得IP順序:

```shell
$_SERVER[‘HTTP_CF_CONNECTING_IP’]: 在cloudflare後抓public IP
$_SERVER[‘HTTP_CLIENT_IP’]: 可偽造，代理端IP
$_SERVER[‘HTTP_X_FORWARDED_FOR’]: 可偽造，取得有用HTTP代理的使用者IP
$_SERVER[‘REMOTE_ADDR’]: 不可偽造，最後一個來源的IP，使用者有用proxy server上網只會取得proxy的IP，沒有設計Load Balancer或是使用類似Cloudflare為前提才適用
```

比較pdo的query及execute差異
1.PDO::query執行一條SQL語句，如果通過，則返回一個PDOStatement對象
2.PDO::exec執行一條SQL語句，並返回受影響的行數。 PDOStatement::execute，execute()函數是用於執行已經預處理過的語句，需要配合prepare()函數使用，成功時返回 TRUE， 或者在失敗時返回 FALSE

whoops是一個PHP的錯誤處理框架 writeToOutput: 是否应该直接向客户端推送输出，如果为 false，输出将通过handleException返回 prependHandler: Run() class裡面的方法 PrettyPageHandler: 会生成一个精美、详细的错误页面，其中包括堆栈跟踪中所有框架的代码视图、环境详情等 JsonResponseHandler: 在收到要处理的异常时，会简单地构建一个JSON有效负载并输出

laravel的Kernel.php中，middleware及middlewareGroups與routeMiddleware差異
1.middleware 用於定義全局中間件，會在每個請求中運行。(任何請求都會經過的Middleware)
2.middlewareGroups 用於定義中間件組，方便將中間件進行分組並在多個路由中使用。(要多個Middleware同時使用，就可以使用群組的方式) 3.routeMiddleware 用於定義命名中間件，以便在路由定義中使用，使得路由定義更簡潔。(如果是要指派給特定路由使用，可以在這裡設定一個鍵)

比較pdo的bindParam()或execute array差異
1.bindParam可明確綁定參數與指定型別，增強程式可讀性
2.execute可直接帶入參數，pdo會自動處理綁定參數的細節，方便一次傳遞多個參數
3.部分公司偏好用bindParam因為語意較明確

php接收來自CLI參數: $argv ，如果CMD: php abc.php 2023 09

```
argvp[0]=abc.php, argvp[0]=abc.php,argv[1]=2023, $argv[2]=09
```
