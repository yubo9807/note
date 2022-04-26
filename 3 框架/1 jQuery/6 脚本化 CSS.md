## 脚本化 CSS

```js
$(".box").css({
    position: "absolute",
    width: 150,
    height: 2000,
    background: "#f00",
    top: 150,
    left: 150
});

var offset = $(".box").offset();  //--> 获取对于文档的偏移量（只对可见元素有效）
console.log(offset.left);  //--> 150

var position = $(".box").position();
console.log(position.left);  //--> 150  获取元素相对父元素的偏移（只对可见元素有效）

document.onscroll = function(){
    console.log($("body,html").scrollTop());  // 获取滚动条位置
}

width()  // 元素宽度
innerWidth()  // 可视宽度 content+padding+border
outerWidth()  // content+paddind+border+margin
```
