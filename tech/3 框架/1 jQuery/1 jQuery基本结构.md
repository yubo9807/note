# jQuery
[jQuery 中文文档](https://www.jquery123.com/)

## jQuery 基本结构
```js
(function () {
    function jQuery (selector) {
        return new jQuery.prototype.init(selector);
    }
    // dom 选择
    jQuery.prototype.init = function (selector) {
        this.length = 0;

        // 选择dom对象且包装成jQuery对象
        if (selector.indexOf('.') != -1) {
            var dom = document.getElementsByClassName(selector.slice(1));
        }else if (selector.indexOf('#') != -1) {
            var dom = document.getElementById(selector.slice(1));
        }else if (selector.match(/^\b/)) {
            var dom = document.getElementsByTagName(selector);
        }

        if (dom.length == undefined) {
            this[0] = dom;
            this.length ++;
        }else {
            for (var i = 0; i < dom.length; i++) {
                this[i] = dom[i];
                this.length ++;
            }
        }
    } 

    // css 样式
    jQuery.prototype.css = function (config) {
        for (var i = 0; i < this.length; i++) {
            for (var attr in config) {
                this[i].style[attr] = config[attr];
            }
        }
        // 链式调用
        return this;
    }

    jQuery.prototype.init.prototype = jQuery.prototype;

    window.$ = window.jQuery = jQuery;  // 将 jQuery 挂在全局上
})()
```
> $ == jQuery
