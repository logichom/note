1.使用apt安裝

```shell
sudo apt update
sudo apt install docker-compose
```

2.檢查是否安裝成功及版本

```shell
docker-compose --version
```

> *安裝失敗時考慮以下方法*

```shell
#使用curl直接下載docker-compose
#1.在ubuntu下,輸入指令下載docker-compose
sudo curl -L "<https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$>(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
#2.設定docker-compose為可執行
sudo chmod +x /usr/local/bin/docker-compose
```
