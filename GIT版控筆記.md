# 介紹

簡單的說，git就像玩遊戲可以存擋一樣

透過版本控制系統，可以清楚的記錄每個檔案是誰在什麼時候加進來、什麼時候被修改或刪除。Git就是一種版本控制系統，也是目前業界最流行的版本控制系統，沒有之一

# 優點

* 免費、開源
* 速度快、體積小（並不是記錄版本的差異，而是記錄檔案內容的快照）
* 分散式系統

# 缺點

* 易學難精（指令有非常多）

# 說明

Git只關心檔案的內容，所以只要是檔案，其實都可以使用Git來管理。整體來說使用Git還是可以幫得上設計師的忙

git在計算、產生物件的時候，是根據檔案的內容去做計算的，所以光是新增一個目錄，git是沒辦法處理它的(空的目錄無法被提交)

有些檔案我不想放到Git裡面… 在專案目錄裡放一個.gitignore檔案，並且設定想要忽略的規則就行了。如果檔案不存在，就手動新增它，若已經加入版控就無法排除

分支像貼紙一樣，分支只是指向某個commit的指標 分支名稱是否可用中文還是有點爭議

快轉模式(Fast Forward)就是把master這張貼紙撕起來，然後往前貼到cat分支所指的那個commit而已。所以分支看來才沒有小耳朵。若要有就是不要使用快轉模式，這樣一來就會額外做出一個commit物件，也可完整保留分支的樣子，例如：`git merge cat --no-ff`

合併過的分支要留著嗎？ 所謂的分支就是一個只有40個字元的檔案而已，這40個字元會標記出它目前指向哪一個commit，所以看各個人

不小心把還沒合併過的分支砍掉了，救得回來嗎？ 可以，因為刪掉分支後，那些commit還是在，救回來的話需要SHA-1值，例如：`git branch new_cat b174a5a`，請幫我建立一個叫做new_cat的分支讓它指向b174a5a這個commit

怎麼查剛剛刪掉的那個cat分支的SHA-1？ 可以從 `git reflog`去翻翻看，預設會保留30天

另一種合併方式：使用rebase，會修改歷史，容易造成其它人的困擾。就結果來看，有點像插花時候嫁接的概念，非必要的話請盡量不要使用rebase

# github/gitlab建立Public Key(SSH Key)

1.在終端機下指令 : `ssh-keygen -t rsa` (t：密鑰類型)

2.如沒特定產生在那個路徑下，直接按下 Enter，一律會預設在 `/User/Username/.ssh/id_rsa`

3.請輸入密碼(空白表示不設定)

4.請再次輸入密碼

5.金鑰匙就會產生在剛剛請您設定的路徑下

6.複製id_rsa.pub內容貼到github上

# github建立personal access token

1.Settings > Developer settings > Personal access tokens

2.接著點選 Generate new token 來創一個新的 access token

3.勾選 repo,admin:repo_hook 這兩個即可

4.當push時出現提示輸入密碼時貼上token即可

# MAC匯入windows底下的ppk給GIT用

```shell
#cd到ppk所在目錄(重開機後會失效)
cd project
brew install putty
puttygen php2.ppk -O private-openssh -o php2.pem
ssh-add php2.pem
#重開機後匯入
cd project
ssh-add php2.pem
```

# 專案相關

```shell
git clone <專案路徑> #下載專案
git init #初始化該目錄並進行git版控
git add . #註冊檔案或目錄到索引(.表示整個目錄內的檔案)
git commit -m "first commit" #提交添加到索引的檔案
#用ssh key
git remote add origin git@github.com/logichom/faketemplate.git
git push -u origin master
#通常不需再輸入帳號密碼
#用personal access token
git remote add origin <https://github.com/logichom/faketemplate.git>
git push -u origin master
#出現輸入名稱跟密碼時輸入以下
logichom #帳號名稱
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 #依據使用的token決定輸入值
#注意personal access token期限、專案不同可能無法使用
```

# 分支相關

```shell
git branch #後面沒接任何參數表示列出目前分支
git branch cat #新增分支cat
git branch -m cat tiger #分支cat改名為tiger
git branch -d dog #刪除分支dog，若沒完全合併會提示不給刪
git branch -D dog #強制刪除分支dog
git checkout cat #切換分支到cat
#接下來就是一般的add再commit
```

# 合併分支

```shell
#若想要master分支合併cat分支，會先切回master
#merge cat into master
git checkout master
git merge cat #合併分支
git merge cat --no-ff #合併分支且不使用快轉模式
#合併發生衝突時，修改衝突的檔案，git add該檔案，再git commit完成這一回合
```

# 使用tig工具取代GUI版控

```shell
#查看該專案分支(在專案資料夾底下輸入)
tig

#查看所有指令
#h

#上下移動
#j或k

#查看commit
#enter

#離開
#ctrl+c

#搜尋
#/(後面輸入想要查詢的字串)
#n或N(各個結果切換)

#不同視窗間切換
#tab

#切換回主視窗
#m

#m 可以切換至主視窗。
#l 切換至 Log 視窗。
#t 切換至當前 Commit 節點的目錄。
#f 切換至檔案內容視窗。
#b 切換至 Blame 視窗。
#s 切換至 Status 視窗。
#y 切換至 Stash 視窗。
#h 切換至 Helper 視窗。
```

若遇到GIT資料夾底下的.git無法刪除
關閉VSCode等會使用GIT的軟體後即可刪除
