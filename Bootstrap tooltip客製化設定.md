以下示範需要設定tooltip的背景顏色、箭頭顏色、靠左對齊的語法

```html
<tr data-toggle="tooltip" data-html="true" title="時間:<br>• A:台灣時間<br>• B:日本時間">
  <th scope="row">範例</th>
  <td>
    <p class="card-text">
      滑鼠移動到這行會出現提示
    </p>
  </td>
</tr>
```

```css
.tooltip .tooltip-inner {
    text-align: left; /* 內文靠左，預設置中 */ 
    background-color: #F7F7D4; /* 背景顏色 */
}
.tooltip .arrow::before {
    /* border-right-color: red; */
    border-top-color: red; /* 箭頭區塊上 */
    border-bottom-color: red; /* 箭頭區塊下 */
    /* border-left-color: red; */
}
```

```
//載入tooltip
$(function () {
  $('[data-toggle="tooltip"]').tooltip()
})
```
