> 由於WAMP執行PDO可能有問題所以建議安裝XAMPP，以下紀錄從WAMP轉移到XAMPP過程

1.到官網依據PHP版本下載對應版本

2.安裝時勾選要安裝的套件

3.修改設定
#調整專案目錄
c:\xampp\apache\conf\httpd.conf

改DocumentRoot路徑(非必要):
DocumentRoot “C:/xampp/htdocs” -> DocumentRoot “C:/wamp64/www”

改Directory讀取目錄(非必要):
<Directory “C:/xampp/htdocs”> -> <Directory “C:/wamp64/www”>

#啟用虛擬主機
#Virtual hosts
Include conf/extra/httpd-vhosts.conf -> 確保拿掉前面註解
C:\xampp\apache\conf\extra\httpd-vhosts.conf 按照範例修改目錄

#將剛才設定的主機名稱設定到hosts
C:\Windows\System32\drivers\etc\hosts
設定範例: 127.0.0.1 laravel.test

#關閉錯誤(非必要)
C:\wamp64\bin\php\php5.6.40\php.ini 改error_reporting=E_ALL 改display_errors=Off

以上修改完成後重啟XAMPP

4.執行網頁檢查是否完成

5.查看XAMPP套件版本 打開control panel點Shell
for Apache type: httpd -v
for PHP type: php -v
for mysql type(MariaDB): mysql — version

**儲存XAMPP設定時遇到”xampp-control.ini存取被拒”**
請先將XAMPP背景執行程式關閉，修改安全性中Everyone的權限，勾選完全控制即可

**phpMyAdmin出現”尚未設定 phpmyadmin 資料庫 某些進階功能將無法使用”**
1.使用者帳號 ‘pma’@’localhost’新增以下權限：GRANT SELECT, INSERT, DELETE, UPDATE
2.不行就重新匯入table，匯入table的sql檔案路徑:phpMyAdmin/sql/create_tables.sql
3.再不行就：選擇 mysql DB->在”結構”頁籤內全選全部資料表->右邊下拉選單內選擇:修復資料表

**出現禁止訪問或權限不足時**
修改httpd.conf中找到Directory這個tag，然後將 `Require all denied` 改成 `Require all granted`

**遇到Port 80 in use by “Unable to open process” with PID 4**
方法一：WIN系統點開始>執行>輸入services.msc指令
找到World Wide Publishing Service這個服務
然後將它停止
方法二：將原本監聽的80port改成8000或8080避開被佔用的port

 **XAMPP無法啟動MySQL訊息為Error: MySQL shutdown unexpectedly..** .
方法一：
0.停止apache,mysql等服務及關閉xampp程式
1.C:\xampp\mysql\data，data重新命名為data_old
2.C:\xampp\mysql\，新增data資料夾
3.C:\xampp\mysql\backup，將內容全部複製到data資料夾
4.C:\xampp\mysql\data_old，將內容除了mysql,performance_schema,phpmyadmin資料夾，其餘複製到C:\xampp\mysql\data
5.重啟xampp及apache,mysql等服務(如果成功，會發現使用者帳號被清空)
注意以上C:\xampp為安裝xampp的目錄
方法二：
如果以上無效請試著只刪除C:\xampp\mysql\data\multi-master.info這隻檔案然後重啟

---

#### 若還需要安裝laravel執行環境請參考以下安裝步驟

6.安裝Composer
Win系統請到該官網下載並安裝 [https://getcomposer.org/download/](https://getcomposer.org/download/)
已安裝過可使用下面指令升級

```shell
composer self-update
```

7.下載laravel安裝包

```shell
composer global require laravel/installer
```

8.建立laravel專案

```shell
#安裝最新版
composer create-project --prefer-dist laravel/laravel yourprojectname

#安裝指定版本
composer create-project --prefer-dist laravel/laravel yourprojectname "8.6.*"
```
