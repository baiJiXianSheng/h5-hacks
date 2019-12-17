

# <font color=green>[Usage]：</font> 移动端调试控制台
```html
<script src="//cdn.bootcss.com/vConsole/3.3.3/vconsole.min.js"></script>
```
```js
// 实例化即可
var VConsole = new VConsole();
```

***

# <font color=green>[Usage]：</font> IScroll 插件 

- `iscroll.js` 文件只包含基本功能


- `iscroll-probe.js` 文件方可监听 `scroll` 事件。方便于添加 `上拉加载` 和 `下拉刷新` 功能
[[官方用例]] https://github.com/cubiq/iscroll/blob/master/demos/probe/index.html

```html
<div id="scroll-wrapper">
    <!-- 唯一子元素 为滚动内容 -->
    <div>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <!-- ... -->
    </div>
</div>
```

```css
#scroll-wrapper {
    /* 需要知道容器（垂直滚动时）高度 或 （水平滚动时）宽度 */
    height: 800px;
    /* 必要 */
    overflow: hidden; /* 如垂直滑动，当与 IOS 滑动冲突时，可改为 overflow-y: scroll */

    /* 可选，用于处理 IScroll 滚动区域不准确问题 */
    position: relative;
    /* 可选，解决谷歌浏览器下警告 */
    touch-action: none;
}
```

```js
var IScrollInstance = new IScroll("#scroll-wrapper", {

});

// 每次更新滑动列表内容后，记得手动刷新插件
IScrollInstance && IScrollInstance.refresh();

// iscroll-probe.js 才可监听到
IScrollInstance.on("scroll", funciton () {

});

IScrollInstance.on("scrollEnd", _scrollEnd);

function _scrollEnd(e) {
    /*
        【this.maxScrollY】 页面最大滚动距离，若垂直滑动时为负数，其性质等同于 scrollHeight
        【this.y】 已滚动距离
        【this.pointY】 当前手指位置
    */

    // 手指滑出滚动区域后，使滑动内容回弹
    // if (this.pointY < 0)
    //     _IScrollInstance.scrollTo(0, this.maxScrollY, 100);

    // 加载更多！    maxScrollY 和 y 都为负数
    if (this.y < 0 && _IScrollInstance.maxScrollY >= _IScrollInstance.y) { 
        
    }
}


```

***

# <font color=green>[Usage]：</font> window.postMessage

H5 API：`window.postMessage(message: any, targetOrigin: string)`;

**当通过 iframe 嵌入页面时**

- 父页面向子页面传递消息通知
```ts

// 如在父页面
window.postMessage({ res: 1, evtType: "showNotice" }, "*");

// 在子页面定义接收事件
window.addEventListener("message", _postMessage);

function _postMessage (evt) {
    if (evt.data.evtType === "showNotice") {
        // use evt.data.res to do something ...
        
    }
}

```

- 子页面（iframe包裹的页面）向父页面（ifram容器所在页面）传递消息
```ts

// 子页面
// 若多层 iframe 嵌套时，可使用 window.top 取得最顶层页面window
window.parent.postMessage({ res: 1, evtType: "showNotice" }, "*");


// 父页面，定义接收消息事件处理函数
window.addEventListener("message", _postMessage);

function _postMessage (evt) {
    if (evt.data.evtType === "showNotice") {
        // use evt.data.res to do something ...
        
    }
}
```

***

# <font color=green>[Usage]：</font> 禁止 `input` 聚焦时调用第三方输入法（兼容性不高）
```html
<input style="ime-mode:disabled" />
```

***

# <font color=green>[Usage]：</font> 禁止显示 `input` 历史输入
```html
<input autocomplete="off" />
```

***

# <font color=green>[Usage]：</font> IOS 下 `input` 聚焦时光标位置偏移。以input上边界开始到文本底部，IOS 下 `input` 默认行高100%？
- (1)
**该法可能会出现文字垂直居中效果不准确**
```css
input {
    /* 如原本以 40px 垂直居中 */
    /* line-height: 40px; */
    
    /* 但通常 font-size 和 line-height值相同时，会出现文字被“裁剪”显示不全 */
    font-size: 20px;

    line-height: 20px; 
    margin: 10px 0;

    /* 若使用 padding: 10px 0; 在ios的高版本如12，会出现bug，当你点击到padding-top的区间的时候，input的光标会移动到input默认文字的最前面，而不是我们希望的最后面 */
}
```
- (2)
```less
.parentDom {
    display: flex;
    align-items: center;

    input {
        font-size: 20px;
    }
}
```
***

# <font color=green>[Usage]：</font> IOS input 键盘 `换行` -> `搜索`
**外面嵌套一层 `form`**
```html
<form action="">
    <input type="search">
</form>
```

***

# <font color=green>[Usage]：</font> IOS 原生滑动
```css
.box {
    height: 100%;
    overflow-y: scroll;
    -webkit-overflow-scrolling: touch;
}
```

***

# <font color=green>[Usage]：</font> `input[type=search]` 时安卓或谷歌浏览器 输入框右侧蓝色x按钮
```css
input::-webkit-search-cancel-button {
    display: none;
}
```

***

# <font color=green>[Usage]：</font> `input` 输入文本跳转搜索页面后，再次返回该页面时输入框自动聚焦
```js
// ...

searchInput.value = "";
if (document.activeElement instanceof HTMLElement) {
    document.activeElement.blur();
}

beforeRequest();
```

***

# <font color=green>[Usage]：</font> iPhone 设备 `media 查询` 样式适配
```css

/* iphoneX、iphoneXs */
@media only screen and (device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) {
    div {

    }
}
/* iphone Xs Max */
@media only screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio:3) {
    div {

    }
}
/* iphone XR */
@media only screen and (device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio:2) {
    div {
        
    }
}

```

***

# BFC
- `float` 的值不是 `none`
- `position` 的值不是 `static`或者`relative`
- `display` 的值是 `inline-block`、`table-cell`、`flex`、`table-caption`、`inline-flex`
- `overflow` 的值不是 `visible`

***

# <font color=red>[Bug]：</font> Input[type=file] 

- h5调用设备相机

>手机QQ软件内置浏览器，需要添加 capture="camera" 属性方可调用相机。

**html**
```html
<!-- 若默认在 input 元素上添加 capture="camera" 属性，则某些浏览器（如safari？） 无法唤起相机 -->

<input type="file" id="loadInput" hidden="" accept="image/*" />
```

**js**
```js

var u = navigator.userAgent;
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //g
var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端

if (isIOS) {
    $("#loadInput").removeAttr("capture");
} else {
    var browser = navigator.userAgent.toLowerCase();
    if (browser.match(/MicroMessenger/i) == 'micromessenger') {
    // 微信浏览器
        // 可直接调用相机

    } else if(browser.indexOf(' qq') != -1 && browser.indexOf('mqqbrowser') != -1){
    // 手机QQ软件 内置浏览器
        // 需要添加 capture="camera" 属性方可调用相机
        $("#loadInput").attr("capture","camera");

    } else if(browser.indexOf('mqqbrowser') != -1 && browser.indexOf(" qq") == -1){
    // QQ浏览器
        // alert("QQ浏览器");
    } else {
        // alert("以上都不是");
    }
}

// 主动触发 input-file 点击选择文件事件
document.getElementById("loadInput").click();

```

***

# <font color=red>[Bug]：</font> IOS 下 当有 input 聚焦时，其他元素通过 click 绑定的点击事件，因 input 失去焦点阻止了 click 事件触发，需要二次点击方可触发

```js

    var _isIphone = navigator.userAgent.toUpperCase().indexOf("IPHONE") > -1;
    // hack：IOS 上点击登录按钮时，若输入框聚焦，首先会触发 blur 事件，click事件无法触发，需再次点击触发
    if (_isIphone) {
        $("body").on("touchend", function(e) { 
            // 当点击到 btn 上时，直接调用对应的方法
            if (e.target.id == "btn")
                dosomething();
        })
    } else {
        $("#btn").click(function () {
            dosomething0();
        });
    }

```

***

# <font color=red>[Bug]：</font> 有 `input` 聚焦时，底部footer `position: fixed` 失效被键盘顶起。尝试解决方案：聚焦时 隐藏footer，失去焦点时 显示footer

```js

// 浏览器当前的高度
var oHeight = $(document).height();
$(window).resize(function () {
    var now = $(document).height();
    if (now < oHeight) {
        $(".footer").hide();
    } else {
        $(".footer").show();
    }
});

```

***

# <font color=red>[Bug]：</font> h5 页面在 IOS 下返回，未重载  

```js
// 解决 h5 在IOS 下返回，页面不重载问题
var browserRule = /^.*((iPhone)|(iPad)|(Safari))+.*$/;
if (browserRule.test(navigator.userAgent)) {
    window.onpageshow = function(event) {
        console.log("onpageshow!")
        if (event.persisted) {
            window.location.reload();
        }
    };
}

```

***

# <font color=red>[Bug]：</font> h5 页面在 Android 下 `window.history.go(-1)` 无法返回上一页  

```js

var u = navigator.userAgent;
var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端

$("#cancel-btn").click(function () {

    if (isIOS)
        window.history.go(-1);
    else
        window.location.href = "lastPage.html";

    // 或者 无论IOS或Android，都直接通过 location.href = "lastPage.html"; 跳转到指定页面
});

```

***

# <font color=red>[Bug]：</font> `<video>` 标签在 IOS 下点击无法播放

- 解决方案一：

```js

// 用一张播放按钮的图片，监听其点击事件，触发时动态生成 video 标签插入，并调用 video.play();

### 注：若在初始化加载html文档时，<video></video> 或 <source> 标签没有 src 属性及值，通过动态赋值（不会重新请求？）可能无法正常加载。

$("#play-btn").click(function () {

    var $video = $("<video src='"+ url +"' controls></video>");
    
    // 可监听其 播放事件
    $video.on("play", function () {  });

    $("#video-container").append($video);

    $video.get(0).play();
});

```

***
