1.在ubuntu下，輸入下面指令安裝docker(別按ctrl+c中斷執行，需等候執行完成)

```shell
curl -fsSL <https://get.docker.com> -o get-docker.sh
sudo sh get-docker.sh
```

> *如果遇到curl: (6) Could not resolve host: *[*get.docker.com*](http://get.docker.com/)*，執行以下指令*

```shell
sudo echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf > /dev/null
```

2.檢查docker是否安裝成功及版本

```shell
docker --version
```

3.啟動docker

```shell
sudo service docker start
```

4.測試建立容器是否正常

```shell
docker run hello-world
```

> *如果遇到權限問題改執行*

```shell
sudo docker run hello-world
```

> *出現Unable to find image ‘hello-world:latest’ locally latest: Pulling from library/hello-world (以下省略)
> 需要重新啟動docker*

```shell
sudo service docker start
sudo docker run hello-world
```
