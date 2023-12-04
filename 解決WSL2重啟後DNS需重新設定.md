1. wsl -d Ubuntu
2. vim /etc/wsl.conf增加以下內容
   [network]
   generateResolvConf = false
3. wsl — shutdown
4. vim /etc/resolv.conf增加以下內容
   nameserver 8.8.8.8
5. 如果檔案不存在就touch /etc/resolv.conf
