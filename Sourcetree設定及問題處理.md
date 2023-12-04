# 登入gitlab帳號

新增gitlab帳號後一直提示錯誤，因為認證方式是Private Token而不是一般登入(Basic)所指的帳號密碼，是access token，產生方法如下： 在GitLab右上角的頭貼點擊Edit Profile後再從左側選單中找到 Access Tokens，新增一個有api權限的token，然後自己記下來後貼上密碼欄位即可

# 連結github做版控

1.在開發環境開啟新專案

2.開啟sourcetree並登入你的github Basic,url,password(access token),https

3.將剛剛的新專案加到本地git版控

4.找到剛剛建立的專案位址

5.加到本地git版控

6.選擇要將哪些檔案加到版控之中

7.commit!

8.github上建立repository(專案名稱同本地專案)

9.sourcetree到該專案Setting > Remote進行後續設定 Remote name：輸入剛才新增專案的名稱(如果和本地的名稱不同，這邊要輸入Remote端的Name) URL：貼上剛剛新增repository的網址(ssh開頭，若https開頭會有安全性問題) 服務供應商：GitHub

10.push!

11.檢查github上是否上傳成功

# 設定區分檔案大小寫

點擊settings → Edit Config File → ignorecase = false → 存檔

# 設定更新遠端分支

fetch選項勾選prune tracking branches…

# 遇到連線遠端Git倉庫不會跳出登入密碼選項或一直跳出詢問密碼視窗

如果使用sourcetree，請降版到3.4.7
如果使用TortoiseGit，請降版到2.11.0.0

# 開啟force push功能

MAC:Preferences>Advanced頁籤>勾選Allow force push
WIN:Tools>Options>Git頁籤>勾選Enable Forse Push
