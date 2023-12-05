基本範例(使用預設樣式)

```html
<html>
<head>
    <title>Google Translation Example</title>
    <style>
        body > .skiptranslate {
            display: none;
        }
        .goog-logo-link {
            display: none !important;
        }
        .goog-te-gadget {
            color: transparent !important;
        }
        .goog-te-banner-frame.skiptranslate {
            display: none !important;
        }
        a[href="https://translate.google.com"] {
            display: none !important;
        }
    </style>
</head>
<body>
    <div>
        <div id="google_translate_element"></div>
        <div>
            我是繁體中文內容
        </div>
    </div>
    <script src="https://code.jquery.com/jquery-1.11.3.min.js"></script>
    <script src="https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
    <script type="text/javascript">
        function googleTranslateElementInit() {
            new google.translate.TranslateElement({
                pageLanguage: 'zh-TW',
                autoDisplay: false,
                includedLanguages: 'zh-TW,zh-CN,en,ja,ko,th,vi,id,hi,it,de,fr,es,pt,ar',
                layout: google.translate.TranslateElement.InlineLayout.VERTICAL
            }, 'google_translate_element');
        }

        $(window).load(function() {
            $('.goog-te-gadget').html($('.goog-te-gadget div'));
        });
    </script>
</body>
</html>
```

進階範例(自定義選單及順序)

```html
<html>
<head>
    <title>Google Translation Custom Example</title>
    <style>
        body > .skiptranslate {
            display: none;
        }
        .goog-logo-link {
            display: none !important;
        }
        .goog-te-gadget {
            color: transparent !important;
        }
        .goog-te-banner-frame.skiptranslate {
            display: none !important;
        }
        a[href="https://translate.google.com"] {
            display: none !important;
        }
    </style>
</head>
<body>
    <div>
        <div id="google_translate_element" style="display: none;"></div>
        <select onchange="goTranslate(this.value)" translate="no">
            <option value="">請選取語言</option>
            <option value="zh-TW">繁體中文</option><!-- 中文 (繁體) -->
            <option value="zh-CN">简体中文</option><!-- 中文 (簡體) -->
            <option value="en">English</option><!-- 英文 -->
            <option value="ja">日本語</option><!-- 日文 -->
            <option value="ko">한국어</option><!-- 韓文 -->
        </select>
        <div>
            我是繁體中文內容
        </div>
    </div>
    <script src="https://code.jquery.com/jquery-1.11.3.min.js"></script>
    <script src="https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
    <script type="text/javascript">
        function googleTranslateElementInit() {
            new google.translate.TranslateElement({
                pageLanguage: 'zh-TW',
                autoDisplay: false,
                includedLanguages: 'zh-TW,zh-CN,en,ja,ko',
                layout: google.translate.TranslateElement.InlineLayout.VERTICAL
            }, 'google_translate_element');
        }

        $(window).load(function() {
            $('.goog-te-gadget').html($('.goog-te-gadget div'));
        });

        function goTranslate(lang) {
            $('.goog-te-combo').val(lang);

            const triggerEvent = (element, eventName) => {
                const event = new Event(eventName);
                element.dispatchEvent(event);
            };
            triggerEvent(document.querySelector('.goog-te-combo'), 'change');
        }
    </script>
</body>
</html>
```

進階範例(自定義選單、順序及加入國旗ICON)

```html
<html>
<head>
    <title>Google Translation Custom Example</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" type="text/css" />
    <link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-select/1.6.2/css/bootstrap-select.min.css" rel="stylesheet" type="text/css" />
    <link href="https://cdnjs.cloudflare.com/ajax/libs/flag-icon-css/3.5.0/css/flag-icon.min.css" rel="stylesheet" type="text/css" />
    <style>
        body > .skiptranslate {
            display: none;
        }
        .goog-logo-link {
            display: none !important;
        }
        .goog-te-gadget {
            color: transparent !important;
        }
        .goog-te-banner-frame.skiptranslate {
            display: none !important;
        }
        a[href="https://translate.google.com"] {
            display: none !important;
        }
    </style>
</head>
<body>
    <div>
        <div id="google_translate_element" style="display: none;"></div>
         <select class="selectpicker" data-width="fit" onchange="goTranslate(this.value)" translate="no">
            <option value="">請選取語言</option>
            <option value="zh-TW" data-content='<span class="flag-icon flag-icon-tw" translate="no"></span> 繁體中文'>繁體中文</option>
            <option value="zh-CN" data-content='<span class="flag-icon flag-icon-cn" translate="no"></span> 简体中文'>简体中文</option>
            <option value="en" data-content='<span class="flag-icon flag-icon-us" translate="no"></span> English'>English</option>
            <option value="ja" data-content='<span class="flag-icon flag-icon-jp" translate="no"></span> 日本語'>日本語</option>
            <option value="ko" data-content='<span class="flag-icon flag-icon-kr" translate="no"></span> 한국어'>한국어</option><
        </select>
        <div>
            我是繁體中文內容
        </div>
    </div>
    <script src="https://code.jquery.com/jquery-1.11.3.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.2/jquery.min.js" type="text/javascript"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-select/1.6.2/js/bootstrap-select.min.js" type="text/javascript"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js" type="text/javascript"></script>
    <script src="https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
    <script type="text/javascript">
        function googleTranslateElementInit() {
            new google.translate.TranslateElement({
                pageLanguage: 'zh-TW',
                autoDisplay: false,
                includedLanguages: 'zh-TW,zh-CN,en,ja,ko',
                layout: google.translate.TranslateElement.InlineLayout.VERTICAL
            }, 'google_translate_element');
        }

        $(window).load(function() {
            $('.goog-te-gadget').html($('.goog-te-gadget div'));
        });

        $(function(){
            $('.selectpicker').selectpicker();
        });

        function goTranslate(lang) {
            $('.goog-te-combo').val(lang);

            const triggerEvent = (element, eventName) => {
                const event = new Event(eventName);
                element.dispatchEvent(event);
            };
            triggerEvent(document.querySelector('.goog-te-combo'), 'change');
        }
    </script>
</body>
</html>
```

說明&備註：

* style所設定的css都是為了隱藏套件產生的元素
* google翻譯套件可自定義參數少且參考資料不多，欲打造高度客製化還是建議自己刻畫面然後串接翻譯API
* 如果頁面中不想被翻譯套件翻譯，可加上標籤 `translate="no"`或設定 `class="notranslate"`
* 由於select的option內很難客製化，所以要加入ICON必需借助bootstrap-select這個套件來完成(實際執行後會發現它是額外產生ul,li這些元素來達到效果)，如果原本網頁不支援或不使用bootstrap套件，可改用select2套件
* 某些時候如果針對google套件元素直接控制或更改css不起作用時，可能是元素尚未載入，或是google套件額外產生iframe導致抓不到目標DOM，這時只好耐心一個一個嘗試或自行上網google
