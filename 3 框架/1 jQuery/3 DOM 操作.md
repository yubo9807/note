## Dom 操作

#### HTML

```html
<div class="demo" id='hello'>one</div>
<div class="demo">two
    <ul class="list">
        <li>1
            <ul>
                <li></li>
                <li></li>
                <li></li>
            </ul>
        </li>
        <p>p</p>
        <li class="nice">2</li>
        <li></li>
        <li class="nice">3</li>
    </ul>
</div>
<div class="demo">three</div>
```

#### JS

```js
$('.demo').get(1);  // 获取指定元素 参数为正时取索引值对应的元素，参数为负数时从后索取，参数为空时将类数组转为数组

$('.demo').eq(2);  // 获取指定元素

$('.demo').find('.nice');  // 子、孙子……选择

$('.demo').find('li').filter('.nice');  // 对原先选择的做过滤选择
$('.demo').find('li').filter(function (index, ele) {
    // console.log(this);  // 这里的this指向自身，es5中的 filter this指向filter()的第二个参数
    return index % 2 == 0;
}).css({color: 'red'});

$('.demo').find('li').not('.nice');  // 与filter相反，返回不符合条件的

$('.demo').find('li').has('ul').css({color: 'orange'});  // 筛选匹配元素集合中的那些有相匹配的选择器或DOM元素的后代元素

$('.demo').find('ul').click(function (e) {
    if ( $(e.target).is('li') ) {  // is() 判断当前匹配的元素集合中的元素
        console.log( $(e.target).text() );
    }else {
        console.log( $(this).text() );
    }
})

$('.nice').add('.list').css({color: 'blue'});  // add() 和
$('.nice').add('.list').css({color: 'blue'}).end().css({color: 'black'});  // end() 回退操作

$('.list li').eq(0).next();  // next() 下一个兄弟元素节点
$('.list li').eq(0).next('p');  // 下一个兄弟元素节点，限制条件
$('.list li').eq(0).nextAll();  // nextAll() 下一堆兄弟元素节点
$('.list li').nextUntil('p');  // nextUntil() 下一堆不匹配的兄弟元素节点
$('.list > li').eq(2).prev();  // prev() 上一个兄弟元素节点
                               // prevAll() 上一堆兄弟元素节点
                               // prevUntil() 上一堆不匹配的兄弟元素节点
$('.list > li').parent();  // parent() 获取父级元素
$('.list > li').parents();  // parents() 获取祖先
$('.list > li').closest('ul');  // closest() 获取最近的父级元素
$('.list > li').offsetParent();  // offsetParent() 获取离指定元素最近的含有定位信息的祖先元素
$('.list > li').slice(1, 3);  // slice() 截取元素
$('.list').children();  // 获取所有子元素

$('.demo').data({  // 数据存储于 jQuery 上
    name: 'bozai',
    age: 18
})  // vue 数据存于行间样式上是为了更好的符合规范，jQuery 数据存在 data() 上更为高效
```