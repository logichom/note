1.安裝在C槽底下

2.進WSL2執行ubuntu

3.下載laradock接著運行服務

4.結束服務

5.電腦重啟

6.重新進WSL2執行ubuntu

7.命令列有出現/mnt/c等路徑表示成功

8.修改nginx/sites/default.conf，將目標指向專案(root /var/www/example-app/public)

9.開啟localhost、localhost:8081(mysql,root/root)測試是否成功

10.更改時區.env中的WORKSPACE_TIMEZONE=UTC改成ROC或Asia/Taipei都失敗(尚未解決)

11.修改nginx可以多站台，因本機hosts檔案無權限修改，複製default.conf中的server區塊，將listen的port改成81即可

12.如要設定第三台，需新增.env中的VARNISH_BACKEND_PORT參數，及docker-compose.yml對應參數，後面改成82，然後再修改default.conf

13.設定完需重啟docker
