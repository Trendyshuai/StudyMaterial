# <center>序言 vue.js介绍</center>

## Vue.js优点
1. 体积小
   * 压缩后33k
2. 更高的运行效率
   * 基于虚拟dom
3. 双向数据绑定
4. 生态丰富、学习成本低

# <center>第1节 安装与部署</center>
   * 直接` <script> `引入
   * CDN
   * NPM
   * CLI

# <center>第2节 创建第一个vue应用</center>
``` html
<body>
    <div id="app">
        {{message}}
    </div>

    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                message: 'Hello Vue!'
            }
        })
    </script>
</body>
```

# <center>第3节 数据与方法</center>

## 数据与方法
当一个Vue实例被创建时，它将` data `对象中的所有的属性加入到Vue的<b>响应式系统</b>中。当这些属性的值发生改变时，试图将会产生“响应”，即匹配更新为新的值。
