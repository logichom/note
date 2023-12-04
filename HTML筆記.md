```html
<!-- 送出表單 -->
<input type="button" class="button_s" value="送出" style="height:40px; width:150px" onclick="document.yourformname.submit()"/>

<!-- 即時檢查數字 -->
<input type="text" onkeyup="value=value.replace(/[^\d.]/g,'')"/>
<input type="text" onkeyup="value=value.replace(/0-9/g,'')"/>

<!-- 欄位唯讀 -->
<input type="text"style="border:0px;" readonly="readonly"/>

<!-- input文字靠右 -->
dir="rtl"
style="text-align:right"

<!-- 分散對齊 -->
<td style="word-spacing:5px;white-space:nowrap;">測 試 文 字</td> <!-- 字元間要加空白-->

<td style=" text-align: justify; text-justify: distribute-all-lines; text-align-last: justify">網頁分散對齊測試</td>

<!-- html table tr 文字左右對齊 -->
style=" text-justify: distribute; text-align:center; text-align-last: justify; "

<!-- 圖片不存在用onerror -->
<img src="圖片網址" alt="圖片替代文字" title="圖片標題">
<img id="currentPhoto" src="SomeImage.jpg" onerror="this.src='Default.jpg'" width="100" height="120">

<!-- 防止enter key送出表單 -->
<form name="w" id="w" action="invoice_hand.php" method="post" onsubmit="return false">

<!-- 輸入欄加方框 -->
<fieldset style="display:inline-block">
<legend>搜尋(一)</legend>
</fieldset>

<!-- X符號 -->
✖ <!-- ✖ -->
✕ <!-- ✕ -->
```
