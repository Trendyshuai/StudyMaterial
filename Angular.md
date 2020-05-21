# <center>Angular</center>
* 前言

  Angular学了太久很久没用有些忘记了，再加上新版本变动有些大，打算重新学习一下，然后把之前的个人博客建立起来。

* 0. 安装Node.js

* 1. 安装Angular CLI
``` shell
    npm install -g @angular/cli
```
* 2. 创建工作空间和初始应用

  * 2.1 运行CLI命令ng new 并提供 my-app 名称作为参数
  ``` shell
    ng new my-app
  ```
  * 2.2 ng new 命令会提示你提供要把哪些特性包含在初始应用中

* 3. 运行应用
  * 3.1 转到workspace文件夹（my-app）
  ``` shell
    cd my-ap
  ```
  * 3.2 使用 CLI 命令 ng serve 和 --open 选项来启动服务器
  ``` shell
    ng serve --open
  ```

例子：
``` html
<h2>Products</h2>

<div *ngFor="let product of products">
</div>
```

  > *ngFor 是一个 "结构型指令"。结构型指令会通过添加、删除和操纵它们的宿主元素等方式塑造或重塑 DOM 的结构。任何带有星号 * 的指令都是结构型指令。

* *ngFor

* *ngIf

* 插值 {{}}

* 属性绑定 []

* 事件绑定 ()