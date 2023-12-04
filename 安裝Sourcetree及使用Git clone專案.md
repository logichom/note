1.下載sourcetree
Generate SSH key, private and public
Sourcetree > Tools > Create or Import SSH Keys

2.Click Generate
滑鼠需在空白處滑動
Save public key under .ssh folder
Save private key under .ssh folder

3.Add private key to Pageant, running in background

4.Add private key to Sourcetree

5.Add public key to Github
Settings > SSH and GPG keys

6.Clone the git project using SSH key

7.出現 `git@github.com: Permission denied (publickey)<br/>`Sourcetree > Actions > Open in Terminal

```shell
ssh -T git@github.com
ssh -vT git@github.com
ssh-add ~/.ssh/<密鑰名稱>
"C:\Users\<Your User Name>\AppData\Local\SourceTree\app-3.4.14\tools\putty\plink.exe" git@github.<Your Company Name>.com:<Your Reop Name>.git如果git clone的連線目標有SSH，且需輸入密碼，請降版為3.4.7(tortoisegit為2.11)，否則最新版不會提示輸入密碼視窗
```

8.如果git clone的連線目標有SSH，且需輸入密碼，請降版為3.4.7(tortoisegit為2.11)，否則最新版不會提示輸入密碼視窗

9.重新產生公鑰及私鑰

10.如果出現PuTTY key format too new，因為3.4.7無法產生舊版PPK key v2，利用tortoisegit產生，記得Change the PuTTygen PPK File Version to version 2，然後重新匯入key

11.如果出現You’re using an RSA key with SHA-1, which is no longer allowed，表示github對RSA keys with SHA-1 are no longer accepted，重新產生公鑰及私鑰，SSH key算法改成ECDSA，然後重新匯入key
