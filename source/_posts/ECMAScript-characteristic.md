---
title: ECMAScript-characteristic
date: 2019-08-09 16:51:46
tags:
---

# ECMAScript 6

## let or const

## 变量的解构赋值

- 数组，let [a, b, c] = [1, 2, 3];

- 对象，let { foo, bar } = { foo: 'aaa', bar: 'bbb' };

- 字符串，const [a, b, c, d, e] = 'hello';

## 字符串

- 模板字符串

  ```js
  function fn() {
    return "Hello World";
  }

  `foo ${fn()} bar`;
  // foo Hello World bar
  ```

- 模板编译

  ```js
  let template = `
  <ul>
    <% for(let i=0; i < data.supplies.length; i++) { %>
      <li><%= data.supplies[i] %></li>
    <% } %>
  </ul>
  `;
  ```

## 函数

- 参数默认值

  ```js
  // 解构赋值
  function foo({ x, y = 5 }) {
    console.log(x, y);
  }

  foo({}); // undefined 5
  foo({ x: 1 }); // 1 5
  foo({ x: 1, y: 2 }); // 1 2
  ```

## Set 和 Map 数据结构

- “键值对”的数据结构

  ```js
  const m = new Map();
  const o = { p: "Hello World" };

  m.set(o, "content");
  m.get(o); // "content"

  m.has(o); // true
  m.delete(o); // true
  m.has(o); // false
  ```

## Promise

- ajax

  ```js
  const getJSON = function(url) {
    const promise = new Promise(function(resolve, reject) {
      const handler = function() {
        if (this.readyState !== 4) {
          return;
        }
        if (this.status === 200) {
          resolve(this.response);
        } else {
          reject(new Error(this.statusText));
        }
      };
      const client = new XMLHttpRequest();
      client.open("GET", url);
      client.onreadystatechange = handler;
      client.responseType = "json";
      client.setRequestHeader("Accept", "application/json");
      client.send();
    });

    return promise;
  };

  getJSON("/posts.json").then(
    function(json) {
      console.log("Contents: " + json);
    },
    function(error) {
      console.error("出错了", error);
    }
  );
  ```

- then,catch,finally,all

  ```js
  promise
    .then(result => {})
    .catch(error => {})
    .finally(() => {})
    .all([p1, p2, p3])
    .resolve();
  // 等价于
  new Promise(resolve => resolve("foo")).reject();
  // 等同于
  const p = new Promise((resolve, reject) => reject("出错了"));
  ```

## async

- Generator 函数的语法糖

  ```js
  function type(delayedTime) {
    return new Promise(function(resolve, reject) {
      setTimeout(function() {
        console.log(delayedTime);
        resolve(delayedTime);
      }, delayedTime);
    });
  }

  async function asyncFunc() {
    await type(3000);
    await type(2500);
    console.log(1);
  }

  asyncFunc()
    .then(function() {
      return type(2000);
    })
    .then(function() {
      return type(1500);
    });
  ```

## class

- 构造函数

  ```js
  class MyClass {
    constructor() {
      // ...
    }
    get prop() {
      return "getter";
    }
    set prop(value) {
      console.log("setter: " + value);
    }
    doStuff() {
      console.log("stuff");
    }
  }

  let inst = new MyClass();

  inst.prop = 123;
  // setter: 123

  inst.prop;
  // 'getter'
  ```

- 继承

  ```js
  class Age {
    constructor(age) {
      this.age = age;
    }
    sayAge() {
      console.log(this.age);
    }
  }
  class People extends Age {
    constructor(name, age) {
      super(age); //super 代表父类的实例也就是People的实例对象。
      this.name = name;
    }
    sayName() {
      console.log(this.name);
    }
  }
  let p = new People("lwk", 22);
  console.log(p.age);
  p.sayAge();
  ```
