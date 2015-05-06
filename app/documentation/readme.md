eLibrary
---

### Structure

專案資料夾結構

```
`-- app/
|   `-- css/
|   `-- img/
|   `-- js/
|   `-- langs/
|   `-- pages/
|   `-- views/
|   `-- vendor/
`-- master/
|   `-- jade/
|   |   `-- views/
|   |   |   `-- partials/
|   `-- js/
|   |   `-- modules/
|   |   |   `-- forms/
|   |   |   `-- tables/
|   |   |   `-- etcs..
|   `-- less/
|   |   `-- app/
|   |   `-- bootstrap/
|   `-- gulpfile.js
|   `-- package.json
|   `-- bower.json
`-- server/
|   `-- *.json
`-- index.html
```
---
#### Folders

__app/__ folder
 
包含編譯後之文件，佈署於主機上使用
 
- pages/
此資料夾內容為編譯後之單頁頁面之檔案
- views/
此資料夾內容為編譯頁後之檔案，view 與 partials 
  - partials/
    使用於 view 之內容文件
- langs/
此資料夾內容為翻譯用之 json
- css/
此資料夾內容為編譯後之 css
- js/
此資料夾內容為串接之 javascript 
- img/
此資料夾內容為使用之圖檔 


__master/__ folder

此資料夾包含的來源檔案，用來編譯得到的靜態版本（HTML，CSS，JS）。
 
- jade/
此資料夾內容為 JADE 檔，透過 GULP 編譯靜態 html 
  - 
- less/
此資料夾內容為 LESS 檔，透過 GULP 編譯靜態 CSS 
  - app/ 
    contains the LESS source with the components
  - bootstrap/
    contains the LESS source files for Bootstrap
- js/
此資料夾內容為 JS 檔，所有檔案會合併至 app.js
  - modules/
    此資料夾內容為所有 controllers、directives...等modular pattern.
  - custom/ 
    自定 controllers、directives...等

 
__vendor/__ folder

此資料夾內容為 vendor 之檔案，使用於 include plugin 與 其他 元組件， 該資料夾透過 bower 管理
 
__server/__ folder

此資料夾內容為 server side 檔案， 目前內容僅側邊欄使用

Usage
-----

### Customize

To add your custom code you can follow this guideline


### Servers



Build
-----

### Tools

> 本專案必須使用 JADE, LESS 與 modular JS

__Node.js__ 

__Gulp__ 任務管理工具

__Bower__ 套件管理工具 

設定檔 __gulpfile.js__ 與 __package.json__ 放至於 master/ 之下，用來安裝與編譯元件之檔案

__bower.json__ 檔案於 root 之下，用來安裝套件之檔案

__Installing Tools __

按以下步驟逕行安裝工具

- 參考 http://nodejs.org/ 安裝 node and npm
- 確認 __node__ 與 __npm__ 於開發環境 command 之變數路徑
- 執行 __npm install -g bower__ 全域安裝

__Compiling sources__

- 打開 terminal, cd master/ 資料夾, run __npm install__. 該命令會安裝 gulp 依賴之套件 
- 執行 __gulp__ 開始 gulp 任務管理工具 

- 執行 __bower install__ 安裝 vendor 之依賴套件


Tasks:  

- `gulp dev` 將啟動任務管理工具與 LiveReload, 只要專案 source 中的任何變更都會觸發 LiveReload，需確保使用 Chrome 與安裝 LiveReload 插件.

- `gulp dev:server` 將啟動任務管理工具與 LiveReload, 使用 nodejs 的 serve application, 路徑為 http://localhost:3000

- `gulp vendor:base` 將生成 __base.js__

- `gulp vendor:copy` 將拷貝所有 vendor.json 至 app/vendor 資料夾

**Note**: 也可以使用指令 `gulp dev webserver` 或只使用 `gulp webserver` 


### Javascript

控制該專案的 Javascript 主要分為以下兩個部分

__base.js__: 包含啟動專案，這是從 vendor 資料夾透過 gulpfile.js 自動生成

__app.js__: 包含在專案中使用之 modules (controllers, directive... 等). 這是從 master/js 資料夾串接生成.

### JADE 

Jade 是一個 HTML templates 引擎語言, 無法直接透過瀏覽器閱讀

### LESS

LESS 為 css 預處理器, 亦無法直接透過瀏覽器閱讀, 


### Vendor

#### Vendor folder

Vendor script 依賴於 bower 管理器. 之需執行 __bower install__ 於 master/ 資料夾即可安裝使用之套件.

大多時候 bower 會下載許多沒有必要的檔案, 因此使用 `vendor:copy` 任務指令, 會至 __bower_components__ 資料夾複製所需的檔案至  __app/vendor__ 資料夾
這些檔案在  __vendor.json__ 中配置，包含像 lazy load module...等,  但也可以 include 字型, svg...等



Features
-----

### Layout

rendered:

``` html
<html>
  <head>
    #metas and css
  </head>  
  <body>
    <section class="app-container" data-ui-view>

        #start include from app.html

          <header ng-include="'app/views/partials/top-navbar.html'"> ...
            # top navbar markup

          <aside ng-include="'app/views/partials/sidebar.html'"> ..
            # sidebar markup

          <section>
            <div class="app" data-ui-view>
              # view markup
            </div>  
          </section>

          <footer ng-include="'app/views/partials/footer.html'"> ...
            # footer markup

        #end include from app.html

     </section>
 
     #scripts
 
  </body>
</html>
```

Layout 可於 __body__ tag, 透過以下 class 控制

`.layout-fixed`: 讓 navbars fixed

`.layout-boxed`: 固定最大寬度並置中

`.aside-collapsed`: 縮小惻然僅顯示 icon

`.aside-toggle`: 用於手機時將側欄隱藏於畫面之外

### Lazy Load

非同步加載請求資料[ocLazyLoad](https://github.com/ocombe/ocLazyLoad)

如需變更設定由 `appDependencies` (constants.js)  
然後編輯 (config.js)
special function `requireDeps`

### Routes

[AngularUI Router](https://github.com/angular-ui/ui-router) 

如需變更設定 __config.js__

### Translation

[AngularUI Translate](https://github.com/angular-translate/angular-translate)


Examples

``` html
<h3 ui-translate="reference.NAME">Text that will be replaced</h3>

<h3>{{ 'reference.NAME' | translate }}</h3>

<a href="#" title="{{ 'reference.NAME' | translate }">Link</a>
```

### Sidebar

側欄由 JSON 檔動態加載而成, .  
檔案為 `sidebar-items.json` 並放至於 __server__ 資料夾之下.

__JSON properties format:__

To create a single item
``` js
[
  {
    "text":      "Item text",          // replaced by translate reference
    "sref":      "app.dashboard",      // the state name of the target route
    "icon":      "icon-classname",     // the icon full classname
    "translate": "sidebar.ITEM"        // the translation reference
  }...
]
```

To create a heading or separator
``` js
[
  {
    "text":      "Item text",          // replaced by translate reference
    "translate": "sidebar.ITEM",       // the translation reference
    "type": "heading or separator"     // only heading needs the above props
  }...
]
```

確保側欄正常 work, 

- SidebarController
- SidebarDirective
- SidebarMenuService

> 當JSON文件有格式錯誤會顯示警告訊息

### Markdown Docs

This documentation is loaded from a Markdown source using [Flatdoc](http://ricostacruz.com/flatdoc/) plugin.
The menu and the content is generated automatically from the .md file and styled directly from custom css.

Via the `flatdoc` directive you can use it like this

``` html
<flatdoc src="path/to/readme.md">
  <!-- generated by directive -->
  <div role='flatdoc'>
    <div role='flatdoc-menu' ui-scrollfix></div>
    <div role='flatdoc-content'></div>
  </div>
  <!-- end directive -->
</flatdoc>
```

### Directives

#### Bootstrap UI

This item include all directives from [Angular BootstrapUI].

[Angular BootstrapUI]: http://github.com/api

#### Custom

This item include the following directives. 

`[href]`  

Disables empty links default behavior

`[animate-enabled]`  

Enable or disables ngAnimate for the element with the directive

`[reset-key]`  

Removes a key from the browser storage via element click

`[flatdoc]`  

Creates the flatdoc markup and initializes the plugin

`[toggle-fullscreen]`  

Toggle the fullscreen mode on/off

`[masked]`  

Initializes the masked inputs

`[sidebar]`  

Wraps the sidebar and handles collapsed state

`[climacon]`  

Include any animated weather icon from Climacon

`[sparkline]`  

SparkLines Mini Charts

`[check-all]`  

Tables check all checkbox

`[toggle-state]`  

Toggle a classname from the __body__ tag. Useful to change a state that affects globally the entire layout or more than one item.  
Elements must have [toggle-state="CLASS-NAME-TO-TOGGLE"]. Use [no-persist] to avoid saving the sate in browser storage.

`[bootstrap-slider]`  

Initializes the jQuery UI slider controls

`[vector-map]`  

Init jQuery Vector Map plugin

`[flot]`  

Initializes the Flot chart plugin and handles data refresh

`[wysiwyg]`  

Initializes the Wysiwyg editor

`[portlet]`  

Drag and drop any panel based on jQueryUI portlets

`[scrollable]`  

Make a content box scrollable


Credits
-------
<div class="row">
<div class="col-lg-4">
[Angular](https://angularjs.org/)  
[Angular Docs](https://docs.angularjs.org/guide/)  
[ocLazyLoad](https://github.com/ocombe/ocLazyLoad)  
[uiRouter](https://github.com/angular-ui/ui-router)  
[uiTranslate](https://github.com/angular-translate/angular-translate)  
[uiBootstrap](http://angular-ui.github.io/bootstrap/)  
[Toaster](https://github.com/jirikavi/AngularJS-Toaster)  
[Angular Loading Bar](http://chieffancypants.github.io/angular-loading-bar/)  
[Bootstrap](http://getbootstrap.com/)  
[jQuery]( http://jquery.com/)  
[Animate.css](http://daneden.github.io/animate.css/)  
[Chosen](https://github.com/harvesthq/chosen/)  
[BS Datetime Picker](http://tarruda.github.io/bootstrap-datetimepicker/)  
[FlotCharts](http://www.flotcharts.org/)  
[Angular Gmap](https://github.com/dylanfprice/angular-gm-bower)  
[Angular Knob](https://github.com/yunlzheng/angular-knob)  
[Angular UI Utils](https://github.com/angular-ui/ui-utils)  
[AngularUI Calendar](https://github.com/angular-ui/ui-calendar/)  
[Bootstrap Wysiwyg](https://github.com/mindmup/bootstrap-wysiwyg)  

[Marked](https://github.com/chjj/marked)  

</div>
<div class="col-lg-4">
[Modernizr](http://modernizr.com/)  
[MomentJs](http://momentjs.com/)  
[Bootstrap Slider](http://www.eyecon.ro/bootstrap-slider)  
[Sparkline](http://omnipotent.net/jquery.sparkline/#s-about)  
[slimSCroll](http://rocha.la/jQuery-slimScroll)  
[FullCalendar](http://arshaw.com/fullcalendar/docs/)  
[InputMask](https://github.com/RobinHerbots/jquery.inputmask)  
[jVectorMap](http://jvectormap.com/)  
[FlatDoc](https://github.com/rstacruz/flatdoc)  
[jQueryUI](http://jqueryui.com/sortable/)  
[ngTable](https://github.com/esvit/ng-table)  
[ScreenFull](https://github.com/sindresorhus/screenfull.js)  
<br>
</div>
<div class="col-lg-4">

<h4 class="mt0">Icons  </h4>

[Feather Icons](http://colebemis.com/feather/)  
[Font Awesome](http://fortawesome.github.io/Font-Awesome/)  
<br>

<h4 class="mt0">Font  </h4>

[Open Sans](https://github.com/FontFaceKit/open-sans)
<br>

<h4>Demo images </h4>

[uiFaces](http://uiFaces.com/)  
[Unsplash](http://unsplash.com)  
</div>
</div>
