> *開始安裝前請先關閉Docker Desktop並移除*

1.開啟powershell執行指令，啟用 Windows 子系統 Linux 版和啟用虛擬機器功能

```shell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

2.將WSL2設定為預設版本(如果跑很久可嘗試重開機)

```shell
wsl --set-default-version 2
```

3.安裝Ubuntu(不建議到store裝)

```shell
wsl --install -d Ubuntu
```

4.啟動WSL的Ubuntu

```shell
wsl -d Ubuntu
```

5.按照提示建立Ubuntu的使用者和密碼
