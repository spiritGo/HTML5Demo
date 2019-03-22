# HTML5

---

## 元素全屏显示

```javascript
/**
 * 全屏操作的主要方法和属性
 * 1.requestFullScreen():开启全屏显示
 * 不同浏览器需要添加不同的前缀
 * chrome:webkit  firefox:moz  ie:ms  opera:o
 * 2.cancelFullScreen():退出全屏显示,只能使用document来实现
 * 如:document.cancelFullScreen()
 * 3.fullScreenElement:是否是全屏状态,只能使用document进行判断
 * @type {Element}
 */
let div = document.querySelector("div");
document.querySelector("#full").onclick = function() {
    div.webkitRequestFullScreen();
}
```

## fileReader

```javascript
/**
 * FileReader:读取文件内容
 * 1.readAsText():读取文本文件(可以使用txt打开的文件),返回文本字符串,默认
 * 编码是utf-8
 * 2.readAsBinaryString():读取任意类型的文件,返回二进制字符串,这个方法不是用
 * 来读取文件展示给用户看,而是存储文件.
 * 3.readAsDataURL():读取文件获取一段以data开头的字符串,这段字符串的本质就是
 * DataURL,dataUrl是将一种文件(一般指图像或者能够嵌入到文档的文件格式)嵌入到wen
 * 档的方案,dataURL是将资源转换为base64编码的字符串形式,并且将这些内容直接存储在
 * url中,优化网站的加载速度和执行效率
 * 4.abort():中断读取
 */
function getContent() {
    var reader = new FileReader();
    var file = document.querySelector("[name=myfile]").files[0];
    reader.readAsDataURL(file)
    /**
     * fileReader提供一个完整的事件模型,用来捕获读取文件时的状态
     * onabort:读取文件中断时触发
     * onerror:读取错误时触发
     * onload:文件读取成功完成时触发
     * onloadend:读取文成是触发;无论成功与否
     * onloadstart:开始读取时触发
     * onprogress:读取文件过程中持续触发
     */
    reader.onload = function() {
        document.querySelector("img").src = this.result;
    }
}
```

## draggable

```javascript
/**
 * 应用于被拖拽元素事件
 * ondrag: 应用于拖拽元素,整个拖拽过程都会调用
 * ondragstart: 应用于拖拽元素,当拖拽开始时调用
 * ondragleave: 应用于拖拽元素,当鼠标离开拖拽元素时调用
 * ondragend: 应用于拖拽元素,当拖拽结束时调用
 *
 * 应用于目标元素事件
 * ondragenter: 当拖拽元素进入时调用
 * ondragover: 当停留在目标元素上时调用
 * ondrop: 当在目标元素上松开鼠标时调用,默认不触发,要在ondragover中阻止浏览
 * 器的默认行为
 * ondragleave: 当鼠标离开目标元素时调用
 */

var p = document.querySelector("#text");
var div2 = document.querySelector(".div2");
var div1 = document.querySelector(".div1");

div2.ondragover = div1.ondragover = function(e) {
    e.preventDefault();
};

div2.ondrop = div1.ondrop = function() {
    this.appendChild(p)
}
```

