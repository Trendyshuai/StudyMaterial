# <center>Git工具</center>

## <font color="eebb33">Git 配置</font>

### 配置用户名

``` shell
git config --global user.name "xxx" 
```

### 配置邮箱

``` shell
git config --global user.email xxxxx@163.com
```

### 查看配置信息

``` shell
git config --list
```

## <font color="eebb33">Git 创建仓库</font>

### 当前目录作为Git仓库
``` shell
git init
```

### 指定目录作为Git仓库

``` shell
git init newrepository
```

### 从现有Git仓库中拷贝项目

``` shell
git clone <repo>
```

### 指定目录拷贝项目
``` shell
git clone <repo> <directory>
```

* 例如：

    * 当前目录下创建一个名为grit的目录<br>
    ``` $ git clone git://github.com/schacon/grit.git ```
    * 自定义新建项目目录名称<br>
    ``` $ git clone git://github.com/schacon/grit.git <directory> ```

