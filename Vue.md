# <center> Vue 学习笔记 </center>

## 数据绑定

* 一、

``` HTML
<body>

    <div id="app">
        {{message}}
    </div>

    <script>
        var app = new Vue({
            el: '#app',
            data: {
                message: "Hello World"
            }
        })
    </script>

</body>
```

* 二、

``` HTML
<body>

    <div id="app">
        <input v-model="message">  <!-- 所有message跟着改变 -->
        <input v-bind:value="message" v-bind:name="message">  <!-- 其他message不变 -->
        <input v-bind:value="message" v-on:input="message = $event.target.value">
        {{message}}
    </div>

    <script>
        var app = new Vue({
            el: '#app',
            data: {
                message: "Hello World"
            }
        })
    </script>

</body>
```