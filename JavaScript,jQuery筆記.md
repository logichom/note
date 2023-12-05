```javascript
//送出表單
document.yourformname.submit(); //js
$('form[name="c"]').submit(); //jquery

//JQUERY取radio button值
document.querySelector('input[name=use]:checked').value;
$("input:radio[name=type]:checked").val();

var radios = document.getElementsByName('genderS');
for (var i = 0, length = radios.length; i < length; i++) {
    if (radios[i].checked) {
        // do whatever you want with the checked radio
        alert(radios[i].value);

        // only one radio can be logically checked, don't check the rest
        break;
    }
}
var toRemoveCountry = ', ' + $('input[name="country"]:checked').parent().text();

//全選
$(function(){
 $('#all').click(function(){
  $("input[name='choose[]']").prop("checked",$(this).prop("checked"));
 });
});
//全取消
$('input:checkbox').removeAttr('checked');

//全選+全取消
$('#selectAll').toggle(function() {
 $('input:checkbox').attr('checked','checked');
},function() {
  $('input:checkbox').removeAttr('checked');   
});

//取得選取的元素值(form外才用此方法)
$('input[name=radioName]:checked').val();
$("input[name='can[]']:checked").val();
//BY name:
$('input[name="goodsPicRename[]"]:checked');
document.querySelector('input[name="rate"]:checked').value;
//BY class:
$('.goodsPicRename:checked');

//select選單
$("#elementId :selected").text(); // The text content of the selected option
$("#elementId").val(); // The value of the selected option

var goodsarray = [];
$('input[name="choose[]"]:checked').each(function() {
 goodsarray.push($(this).val());
});

var goodsarray = $('input[name="choose[]"]:checked').map(function () {
 return $(this).val();
}).get();

//radio button
//多選要設定成class然後用class去取值
var orderarr = $('.orderbutton:checked').map(function () {
 return $(this).val();
}).get();

var orderarr = [];
$('.orderbutton:checked').each(function() {
 orderarr.push($(this).val());
});

var  rcheckarr = $('input[name="rcheck[]"]:checked').map(function () {
 return  $(this).val();
}).get();

//JS顯示陣列值
alert(JSON.stringify(aCustomers));

//改變網頁送出目標
$('#w').attr('action','order_list1_1to2.php').submit();

//ready 在onload 前加载

//jquery AJAX
var URLs="../check/checkajax.php";
 $.ajax({
  url: URLs,
  data: {'do':'selectshop','shop':strs},
  type:"POST",
  dataType:'text',
  success: function(msg){
   if(msg !== ''){
    $('#take_store').val(msg);
   }
  }}
 );

//網頁重新導向包含#
window.location.hash = "#modal";
location.reload();

//query取得多個checkbox選取的值
$('input:checkbox:checked[name="idarr[]"]').map(function() { 
 return $(this).val(); 
}).get()

//jquery 取消選擇的select
$("select option").prop("selected", false);

//js 複製到剪貼簿
var rec_code = document.getElementById('recommend_code');
rec_code.select();
rec_code.setSelectionRange(0,9999);
document.execCommand('copy');
document.getElementById('getRecommend').innerHTML = 'Copied';
//目標:
//<input type="text" id="recommend_code" name="recommend_code" value="{$recommend_list.event_msg}">

var rec_code = document.getElementById('recommend_code');
var range = document.createRange();
range.selectNodeContents(rec_code);
var section = window.getSelection();
section.removeAllRanges();
section.addRange(range);
document.execCommand('copy');
document.getElementById('getRecommend').innerHTML = '已複製';

var $tmp = $('<input>');
$('body').append($tmp);
$tmp.val($('#recommend_code').html()).select();
document.execCommand('copy');
$tmp.remove();
//目標:
//<div id="recommend_code" name="recommend_code">{$recommend_list.event_msg}></div>

//避免重複點擊
onclick="document.getElementById('submit_butn').style.display='none';document.getElementById('cancel_butn').style.display='none';SendStore();"

//Math.round() 四捨五入
//Math.floor() 最大整數=無條件捨去
//Math.ceil() 最小整數=無條件進位

//對應excel:ROUNDUP
Math.ceil();

//對應excel:PMT
function pmt(rate, nper, pv, fv=0){
 var presentValueInterstFector = Math.pow((1 + rate), nper);
 var pmt = rate * pv * (presentValueInterstFector + fv) / (presentValueInterstFector - 1);
 return pmt;
}

var getRate = 0.16;
var getNumOfPayments = 12;
var getLoanAmount = 80000;
var pmt = pmt(getRate/12, getNumOfPayments, getLoanAmount);
alert(pmt);

//Uncaught TypeError: Cannot read properties of undefined (reading 'offsetWidth')
//Uncaught ReferenceError: paying is not defined
//js有錯誤導致後面無法執行，不需添加@section('script')或</body></html>

//轉換日期
var paid_repayment_date = '2022-06-23';
var paid_date = new Date(paid_repayment_date);
//取得現在日期
var today= new Date().toLocaleDateString();
today = new Date(today);
//比對日期
if (paid_date.getTime() < today.getTime()) {
}

//限輸入數字
this.value = this.value.replace(/[^\\0-9]/ig, "");

//數字添加百分位符號
var all_money = 200000;
var total_all = all_money.toLocaleString('en'); //200,000

//取得checkbox
$('#checkbox').is(':checked'); //回傳true or false

//確保html全部load完才開始執行js
//這種寫法等同把js寫在html之後
$(function(){
 // Document is ready
});
//等同
$(document).ready(function() {
 // Document is ready
});

//sweetalert
//只有確定
swal('提示', '最高標額只限定輸入百分比的數字', 'error');

//確定後動作
swal(data.msg, '', "success").then(function () {
    location.reload();
});

//確定+取消
swal({
 title: "確定要修改最高標額?",
  text: memo,
  type: "warning",
  showCancelButton: true,
 //confirmButtonColor: "#eb547c",
  confirmButtonText: "確定",
  cancelButtonText: "取消"
}).then(
 function (isConfirm) {
   if (isConfirm) {
     $.ajax({
    type: "POST",
    url: "/yourapilink",
    dataType: "json",
    data: {
     'id': id,
     'rate': rate
    },
    success: function (data) {
     if (data.code == 200) {
      swal(data.msg, '', "success").then(function () {
       location.reload();
      });
     } else {
      swal('修改失敗', data.msg, 'error');
     }
    }
   });
  }
 },
 function() {
 }
);
```

defer會讓 scripts 的檔案先開始被下載，但在 HTML 文件準備好後才開始執行，同時會確保各個 script 檔案執行的順序
async會讓 scripts 的檔案先開始被下載，但它不會確保各個 script 檔案被執行的順序，先下載好的就先執行

prop()是針對值固定為布林值的屬性進行操作
attr()則是針對值為字串(非布林)的屬性進行操作

取得標籤內文字(多層標籤適用)

```
var text = document.getElementById("id").innerText;
```
