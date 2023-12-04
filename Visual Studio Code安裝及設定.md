1.到官網下載並安裝

2.安裝外掛(這邊以開發PHP為例)

```shell
#必裝
Material Icon Theme #ICON
PHP Intelephense #PHP程式碼提示，安裝完後須關閉內建PHP提示
Office Viewer(Markdown Editor) #文件預覽及markdown即時預覽
#非必要裝
phpfmt - PHP formatter #PHP程式碼規範，須透過本地php執行formatter
Path Intellisense #檔案路徑提示
CodeSnap #程式碼截圖
```

3.修改編輯器設定setting.json(非必要)

```shell
"workbench.startupEditor": "newUntitledFile",
"editor.minimap.enabled": false,
"workbench.iconTheme": "material-icon-theme",
"php.suggest.basic": false,
"workbench.editor.enablePreview": false,
"files.associations": {
  "*.shtm": "html"
},
"explorer.autoReveal": false,
"php.validate.executablePath": "/usr/bin/php", //mac設定php執行路徑
"php.validate.executablePath": "C:\\php-8.0.29\\php.exe", //win設定php執行路徑
"phpfmt.php_bin": "\"C:\\php-8.0.29\\php.exe\"", //formatter設定php執行路徑
```

遇到PHP Intelephense套件sqlsrv提示undefined處理

```shell
1.Go to setting Type: "@ext:bmewburn.vscode-intelephense-client"
2.Under Intelephense: Stubs
3.Add item: sqlsrv and pdo_sqlsrv
4.重啟編輯器
```

遇到複製一段沒有格式化過的JSON資料想格式化

```shell
1.複製欲格式化的JSON內容
2.開啟新檔(快捷鍵：CTRL+N)
3.貼上複製的內容
4.右鍵選擇Format Document(快捷鍵：CTRL+SHIFT+I)
5.完成
```
