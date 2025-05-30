# Class 类

### 特点

1. 类声明不会被提升，与 let 和 const 一样，存在暂时性死区
2. 类中的所有代码均在严格模式下执行
3. 类的所有方法都是不可枚举的
4. 类的所有方法都无法被当做构造函数使用
5. 类的构造器必须使用 new 来调用

> foo: fuck oriented object（他妈的面向对象）  bar: beyond all repair（无药可救）

## 方法调用类别

```js
class Car {
  static fn1() {}
  fn2() {}
}

Car.fn1();  // 静态方法
Car.prototype.fn2();  // 原型方法

const car = new Car();
car.fn2();  // 实例方法（通过原型链继承的）

```

### 类的使用

```js
class Car {
    nowDate = new Date().getHours();  // 字段初始化器 ES7
    constructor(type, color) {
        this.type = type;
        this.color = color;
    }

    // 普通的调用函数
    print() {
        console.log(this.type, this.color)
    }

    // static set 存放在 _proto_ 内，不可被访问
    static tyre = 4;  // 静态属性
    static fn() {  // 静态方法

    }

    // get 和 set 不能用箭头函数
    get age() {  // 创建一个 age 属性（只读）
        return this._num;
    }
    set age(num) {  // 设置一个 age 属性并给他加上 setter，给该属性赋值时，会运行该函数
        this._num = num * 2;
    }
}
const car = new Car('BMW', 'red', 20);
car.print();  //--> BMW red
car.age = 20;  // set 设置参数
console.log(car.age);  //--> 40  get 获取返回结果
// car.age();  不能进行调用
```

### 继承

```js
class Animal {
    constructor (type, name, age) {
        if (new.target == Animal) {
            throw TypeError('Animal 过于抽象，不能直接创建对象');
        }
        this.type = type;
        this.name = name;
        this.age = age;
    }
    loves () {
        console.log('I don`t know')
    }
}
// Dog 继承自 Animal
class Dog extends Animal {
    constructor (name, age) {
        super('犬类', name, age);  // 父级调用，必须写在第一行
    }
    loves () {
        super.loves();  // 如果不进行 super. 会覆盖父级方法
        console.log('骨头');
    }
}
const dog = new Dog('小黑', 3);
```

## 还原旧语法

```js
class Example {
  constructor(name) {
    this.name = name;
  }

  func() {
    console.log(this.name);
  }
}
```

```js
"use strict"

Object.defineProperty(Example.prototype, 'func', {
  enumerable: false,
})
function Example(name) {
  if (this instanceof Example) {
    throw new TypeError("Class constructor Example cannot be invoked without 'new'");
  }
  this.name = name;
}
Example.prototype.func = function () {
  if (this instanceof Example) {
    throw new TypeError("Class constructor Example cannot be invoked without 'new'");
  }
  console.log(this.name);
}
```
