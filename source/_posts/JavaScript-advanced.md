---
title: JavaScript-advanced
date: 2019-08-09 16:47:17
tags:
---

# javascript 高级

## 原型链

- 原型链

    ```js
    function Animal(name) {
        this.name = name;
    }
    Animal.prototype.color = "white";

    var cat1 = new Animal("大毛");
    var cat2 = new Animal("二毛");

    cat1.color; // 'white'
    cat2.color; // 'white'
    ```

- constructor 属性

    ```js
    function P() {}
    P.prototype.constructor === P // true
    ```

## 闭包

