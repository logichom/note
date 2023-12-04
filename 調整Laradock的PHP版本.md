1. 修改laradock的.env檔案
2. 將PHP_VERSION改成要安裝的版本
3. 確認都將docker服務關閉後
4. docker-compose build php-fpm
5. docker-compose build workspace
6. 若遇到錯誤：ERROR [internal] load metadata for docker.io/laradock/workspace:latest-7.4
   下指令：sudo nano /etc/resolv.conf
   新增nameserver 8.8.8.8
   Ctrl+s存檔、Ctrl+x離開
   或是直接下指令：echo “nameserver 8.8.8.8” | sudo tee /etc/resolv.conf > /dev/null
7. docker-compose up -d nginx mysql phpmyadmin
8. docker-compose exec workspace bash
9. 檢查版本是否已更新：php -v
